#JavaScript Event Handling (without jQuery)
자바스크립트에서 이벤트를 다루는 방법

## HTML Attribute
```HTML
<div onclick='foo()'> </div>
```

- 초창기 이벤트 핸들러 방식
- 전통적인 방법으로 현재까지도 급(?)한사람들은 사용하는 방법
- 비동기 스크립트 로딩방식인경우 실행되지 않아 자주 사용되진 않음

## onload
```HTML
<a id="foo" href="#">run foo();</a>
```
```JavaScript
var elem = document.getElementById('foo');
elem.onclick = function(){
	foo();
};
```

- 하위호환성 보증
- 타 스크립트와의 충돌방지를 위하여 잘 사용되진 않음
- 같은 DOM에 대해 onclick 를 중복하여 쓸 수 없음 (가장 마지막에 선언된 것으로 실행)

## addEventListener / attachEvent 를 이용한 등록
```HTML
<a id="foo" href="#">run foo()</a>
```
```JavaScript
var elem = document.getElementById('foo');
elem.addEventListener('click', function(){
	foo();
})
```

- IE8 이하 및 오페라 미지원
    > 여기서는 attachEvent 를 사용하여 미지원 브라우저에 대해 대체 가능

- 라이브러리 및 확장 플러그인 개발에 용이
- 같은 DOM에 대해 click 이벤트를 다중으로 걸어주면, 걸어 준 횟수만큼 해당 함수 실행
- 이벤트를 capture 방식으로 처리하기 용이, 즉 이벤트 동작 방식을 조정하여 불필요한 이벤트에 대해 핸들링이 가능
- 따라서 eventListener 가 발생하는 시기를 조절할 수 있음
- HTML뿐만 아니라 SGML, XML에도 사용가능 (DOM 단위로 설정 가능)
- 주로 자주 사용됨 



## addEventListener for Cross-browsing
```JavaScript
function addEvt(elem, evtName, callback, isCapture){
	if ( window.addEventListener ){
    	elem.addEventListener(evtName, callback, isCapture);
    } else if ( window.attachEvent ){
    	elem.attachEvent('on'+evtName, callback);
    } else { // 사용하지 않는것을 권장
    	elem['on'+eventName] = callback;
    }
}

var elem = document.elementById('foo');

addEvent(elem, 'click', function(e){
	foo();
}, false)
```
즉시호출함수로 Encapsulation 으로 변환하여 사용 가능하다.

참고사이트 : [Unikys](http://unikys.tistory.com/312)