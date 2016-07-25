#JavaScript Keyboard Events

## keypress
> Fire when user presses a key on the keyboard

키보드를 눌렀을 때 실행 됨

----
#### keydown 이벤트와의 차이점
- 키보드를 누르는 동안 실행 됨 (손에서 땔때까지 실행)
- Ctrl / Shift / Alt / 방향키 키 입력 시 ***미 작동***
	- 어느부분까지 안되는지는 디테일하게 체크 필요!

## keyup
> Fire when user releases a key on the keyboard

키보드에서 손을 때어냈을 때 실행 되는 이벤트

## keydown
> Fire when user presses a key on the keyboard

키보드를 눌렀을 때 실행 됨

----
#### keypress 이벤트와의 차이점
- 키보드를 누를 시 한번만 실행 됨
- Ctrl / Shift / Alt 키 입력 시 ***작동***


## Issue: Firefox doesn't work that event.keyCode
파이어폭스는 이벤트 처리 구조가 달라 event.keycode 가 먹히지 않는다. (IE는 먹히는데..) 이리하여 아래와 같은 코드를 쓰길 권장한다.
```JavaScript
	var keyCode = (event.keyCode ? event.keyCode : event.which);
```
매개변수로 받아오는 event.keycode 가 존재하지 않으면 keyCode 를 event.which 로 대응해준다. 

jQuery 에서는 이벤트 리스너에서 이벤트를 매개변수로 받아와서 별도의 처리가 필요 없다.


## Appendix: ASCII Code table
[TechFunda](http://techfunda.com/howto/940/keycode-list) 참고