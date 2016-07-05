# iOS Scroll Cut-off 현상
> Cut-off: 아래로 스크롤 시 아래 내용이 바로 나오는게 아니라, 일정 시간 후 다시 rendering 되는 현상으로, z-index 상으로 아래에 다른 영역이 잡혀있으면 그 내용이 일시적으로 보이다가 실제로 보일 내용이 다시 보여지는 현상

- ```position:fixed``` 로 지정 된 ```<div>```에 ```position:relative``` 를 override 한 상황
	> ```position:fixed``` 를 지정하지 말고 ```position:absolute``` 로 지정하자.
	> 전체화면(레이어)에 대한 CSS Styling 시 영역 전체를 position:fixed 주지말고 absolute 를 주어 기준점에 대한 위치값만 잡은 후, 자식 영역에 대해 relative 를 자식 영역의 높이값에 맞는 스크롤을 할 수 있게 하면된다.