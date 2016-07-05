# iOS 환경의 브라우저에서 ```position:fixed``` 속성의 div 를 배경으로 지정 시 발생되는 Issue

## Input 태그에 포커스 되는 경우 div(fixed) 가 hidden 처리 되는 현상
Input 에 포커스 되는 경우 배경이미지를 주었던 div 가 숨겨지고, ```<body>``` 의 ```background-color``` 가 보이는 현상이 발생된다. 가상키보드가 올라오면서 포커스가 되는데, 이때 문제의 div는 가상키보드 아래 영역으로 밀려져버리게 된다. (top:0 을 주더라도..)

이때는 포커스가 될 때 ```position:fixed``` 를 ```position:absolute``` 로 변경하고, ```transform:translate3d(0,'+$(window).scrollTop()+',0)``` 를 주어 absolute 형태에서 현재 브라우저의 scrollTop 로 강제로 반영되게 하는 방법밖에 없다.


### 예제 코드 (with jQuery)
1. Focus In
```JavaScript
if (UserAgent.match(/iPhone|iPod|iPad/)) {
	disableScrolling(); // System Scroll Event Disable
	$('.bg').css({
		'position': 'absolute',
		'transform': 'translate3d(0, ' + ($(window).scrollTop()) + 'px, 0)'
	});
	setTimeout(function() {
		$('.bg').css({
			'transform': 'translate3d(0, ' + $(window).scrollTop() + 'px, 0)',
			'height': mui.common.getWindowHeight() + (mui.common.getWindowHeight() * 0.5)
		});
	}, 200); // The `200` that input focus and show virtual keyboards is timing.
}
```

2. Focus Out
```JavaScript
if (UserAgent.match(/iPhone|iPod|iPad/)) {
	enableScrolling();  // System Scroll Event Enable
	$('.bg').removeAttr('style').height(mui.common.getWindowHeight());
}
```