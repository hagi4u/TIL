# @keyup.enter 에서 이벤트 리스터 실행 시 함수가 2번 호출되는 현상

인풋박스에서 텍스트 입력을 하면서 한글의 경우 받침이 있기 때문에 글자가 온전히 입력되어 있지 않은 상태 (받침 혹은 자음을 쓰기 위해 기다리게끔 커서가 포커싱 되어있을때)에 엔터키를 치게되면 2번 호출되는 현상이 있음

```HTML
<input
  type="search"
  placeholder="검색해보세요"
  @input="handleSearchChange"
  @keyup.enter="handleEnterPress($event)"
/>
```

와 같이 엔터키를 입력했을 시 반응이 보이게 하는 코드가 있는데, @keyup.enter 에 대한 이벤트 리스너 실행 시 두번 호출되는 현상이 있음 (아이ㅇ 에서 ㅠ를 입력한 후 커서가 `유` 에 있을 때)

```JavaScript
handleEnterPress() {
  console.log('handleEnterPress');
},
```

이렇게 코드를 실행하면 `handleEnterPress` 가 콘솔로 2번 뜨게 된다.

이때는 아래와 같이 바꿔주면 된다 
1. `@keyup.enter` -> `@keydown.enter`
```HTML
<input
  type="search"
  placeholder="검색해보세요"
  @input="handleSearchChange"
  @keydown.enter="handleEnterPress($event)"
/>
```

2. `ev.isComposing` 체크
```JavaScript
handleEnterPress(ev) {
  if(ev.isComposing){
    return false;
  }
  console.log('handleEnterPress');
},
```

keydown 은 컴포징(isComposing)상태값을 확인 할 수 있고 `유` 라는 단어를 입력했을 때 자음이나 받침을 기다리지 않는 인풋의 상태가 되는것을 판단 해 준다.