# ```<A>```를 이용한 이미지 맵

반응형 웹 페이지를 제작할 때에는 이미지의 일부 요소에 대해 링크를 걸기위해 ```<map>```을 이용한 이미지맵을 사용하기보다는 %단위로 이루어 진 ```<a>``` 태그로 링크를 거는게 훨씬 수월하다. 이때, 위치값을 지정 해 줄때 absolute 포지션과 top,right,bottom,left 및 width/height 속성을 적절히 사용하게 되는데, IE10 이하에서 관련 이슈가 생겨 정리한다.

## 예제 : 이미지가 있는 ```<div>``` 에서 ```<a>```태그
아래의 구조로 된 HTML 문서가 있다고 가정하자.

### Markup
```html
<div class="wrap">
	<img src="http://img14.deviantart.net/09c8/i/2012/170/2/c/freebie_monday_background_01___blue_by_cthulhu1976-d541usk.jpg" alt=""/>
    <a href="http://google.com" class="isMap-blank"></a>
    <a href="http://google.com" class="isMap-color"></a>
    <a href="http://google.com" class="isMap-image"></a>
    
    <span class="lbl-blank">↑ </span>
    <span class="lbl-color">↑</span>
    <span class="lbl-image">↑</span>
</div>
```

### CSS
```CSS
a {
  display: block;
}

span {
  position: absolute;
  top: 80px;
  color: white;
}

.wrap {
  position: relative;
  width: 500px;
  height: 500px;
  overflow: hidden;
}

.isMap-blank {
  position: absolute;
  top: 10px;
  left: 10px;
  width: 50px;
  height: 50px;
}
.isMap-color {
  position: absolute;
  top: 10px;
  left: 70px;
  width: 50px;
  height: 50px;
  background-color: white;
}
.isMap-image {
  position: absolute;
  top: 10px;
  left: 130px;
  width: 50px;
  height: 50px;
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVQIHWP4zwAAAgEBAMVfG14AAAAASUVORK5CYII=);
}

.lbl-blank {
  left: 30px;
}
.lbl-color {
  left: 90px;
}
.lbl-image {
  left: 150px;
}

```

위와같은 형태의 문서에서, ```.isMap-blank``` 의 ```<a>``` 태그는 IE10 이하에서 정상적인 Anchor 로서의 작동이 되지 않는다. 처음에는 IE가 z-index 에 대한 이슈가 있는지 체크하였지만 그것도 아니였다. 

진짜 이유는 IE10 이하에서는 DOM 렌더 시 아무리 ```display:block, width/height``` 등등을 잡아놓더라도 ```position:absolute``` 속성일 때에는 지정되었던 그 영역에 무언가의 내용이 들어 가 있어야 실제로 동작하는 영역으로 잡기 때문이다.

```.isMap-color``` 의 경우는 배경 색상으로 해당 영역에 대한 내용이 표시되었기 때문에 정상적으로 가능 하지만 배경색상이 반영되어 실제로 적용하기엔 힘들다.

```.isMap-image``` 는 가로/세로 1 크기의 투명 png 파일을 base64 코드로 변환하여 이것을 ```background-image``` 처리하여 실제로 적용할 수 있게 된다.


이 사실을 원래 알고 있었기 때문에 근 4년간 아래와 같은 마크업으로 ```<a>``` 태그를 이용하여 이미지맵 작업을 하였다.

```HTML
 <a href="http://google.com">
 	<img src="./images/spacer.png" class="spacer">
 </a>
```

이번에 해당 이슈를 다시 한번 체크하여 정리하였고, 실제로 섰던 방법보다 더 좋은 방법(```.isMap-image``` 클래스처럼 사용)이 위 내용에 기술되어 있어 한번 정리하였다. (background-image 를 base64로 변환하여 HTTP Request 최소, markup 1단계 축소)