# `<Fragment>` 컴포넌트 만들기 

## Fragment는 무엇인가?

React의 JSX 문법, Vue의 `<Template>` 코드에서는 최 상위 레벨에서 2개 이상의 자식 노드를 추가할 수 없다. 하지만 경우에 따라서 (예를 들면 특정 조건에 따른 렌더링을 위한), 그리고 DOM 의 depth 를 줄이기 위해서 불가피하게 최 상위 레벨에서 2개 이상의 자식노드를 추가 해야 하는 경우가 생기게 되는데 이때 사용하는게 React 에서 나온 컨셉의 `<Fragment>` 컴포넌트이다.


## Vue.js ..?

Vue.js 는 기본적으로 리액트의 `<Fragment>` 컴포넌트를 제공하지 않고, 사실 잘 쓸일이 없다. 하지만 작업을 하다보니 여러모로 필요한 상황에 처했고 두가지 정도 케이스를 작성하려 한다.

주의할 사항은 Vue.js 의 `<Fragment>` 컴포넌트는 React와는 다르게 무조건 최 상위 레벨에서 n개의 노드 중 1개의 노드만 렌더링 할 수 있도록 `v-if` 디렉티브를 통해 작성 되어야 한다

<br/>

### Case1. nuxt.js 에서 조건부 앵커 태그를 사용하려 할 때

일반적으로 nuxt.js 를 사용하면 `<nuxt-link>`를 통해서 client-side 렌더링으로 페이지 전환을 하고는 있지만, 웹뷰 작업을 하게되면 상황이 달라진다.

nuxt.js 에서 웹뷰를 통해 client-side 렌더링을 하게되면 Request 헤더값이 보장되지 않아서 (특히 인증과 관련된 내용이 존재하는 경우) 부득이하게 `<nuxt-link>` 태그를 쓰지 않고 `<a>` 태그를 사용해서 렌더링을 해야한다.

하지만 웹뷰가 아닌 웹브라우저에서는 `<nuxt-link>`를 사용해야 하는데, 그렇다고 웹뷰와 웹브라우저 페이지를 각각 2개 만들수도 없는것,

따라서 해당되는 경우에는 아래와 같은 샘플 코드로 `<Hybrid-Link>` 컴포넌트를 만든다.

```JavaScript
<Template>
  <Fragment>
    <a :href="href" :target="taget" :rel="rel" v-if="isWebView" /><slot/></a>
    <nuxt-link :to="href" v-else><slot/></nuxt-link>
  </Fragment>
</Teamplte>

<script>...</script>
<style>...</style>
```


### Case2. 횡 스크롤러 컴포넌트 제작 시

횡 스크롤이 기능한 컴포넌트를 만들때는 보편적으로 (모바일에선) 아래와 같은 CSS 를 기준으로 작성해서 쓰게 된다. (굳이 라이브러리를 쓰지 않더라도)

```CSS
.parent {
  white-space:nowrap;
  overflow-x:auto;
  overflow-y:hidden;
  -webkit-overflow-scrolling: touch;
}
.child{
  display:inline-block;
}
/* 스크롤바를 보이게 하지 않는 속성 */
::-webkit-scrollbar {
  display:none;
}
```

흔한 케이스는 아니지만 이런 경우가 종종 발생할 때가 있다. iOS 일부(12)버전에서는 위 CSS 반영 시 스크롤바가 뜨는 영역이 있고 안뜨는 영역이 발생한다. (안드로이드는 잘 먹힘)

+@로 PC에서는 (특히 윈도우) 스크롤바가 지저분 해 보이기에 자바스크립트의 라이브러리 도움을 받아야 한다.

그럼 특정 운영체제는 라이브러리로 횡 스크롤러 컴포넌트를 구현, 그것이 아니라면 Pure CSS를 통해 구현해야 하는 전제가 생기는데, 나는 아래와 같은 코드 구현


```JavaScript
<template>
  <Fragment>
    <div
      v-if="withSwiper"
      v-swiper:horizontalScroller="swiperOption"
      class="horizontal-scroller swiper-container"
    >
      <div class="swiper-wrapper">
        <slot />
      </div>
    </div>
    <div
      v-else
      ref="horizontalScroller"
      v-touch:start="touchStart"
      v-touch:moving="moving"
      v-touch:end="touchEnd"
      class="horizontal-scroller without-swiper"
    >
      <div class="swiper-wrapper">
        <slot/>
      </div>
    </div>
  </Fragment>
</template>

<script>...</script>
<style>...</style>
```

`this.withSwiper` 의 상태값을 통해 적당하게 스와이퍼를 작동하는 코드만 넣으면 끝이 나고 (기본값은 `ture`), 안드로이드 운영체제 인 경우에는 CSS만으로 작성된 코드로 실행하게 함.

```JavaScript
...
  mounted(){
    if (/(android|Android)/.test(window.navigator.userAgent)) {
      this.withSwiper = false;
    }
  }
...
```



## 어떻게 구현하나?

Vue.js 에는 `Functional Component` 라는것이 존재한다. 구현 프로토타입은 생각보다 간단하다.

```JavaScript
export default {
  functional: true,
  render(h, ctx) {
    return ctx.children;
  },
};
```

매개변수 h(createElement) 를 받아서 실행하는 것이 아니라, context로 받아온 children을 바로 노출 시켜주면 되는것, 이렇게 간단하게 코드를 구현할 수 있다.


## 정리?
컴포넌트를 잘 설계하고 활용을 효율적으로 하게되면 이렇게 까지 해야하나.. 하는일은 없을수도 있지만, 문제해결을 위해 필요할 땐 써야하니 잘 활용 하도록 하자.