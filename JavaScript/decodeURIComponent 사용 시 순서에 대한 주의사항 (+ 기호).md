#decodeURIComponent 사용 시 순서에 대한 주의사항 (+ 기호)

## 문제
JSON으로 Encoded URIComponent 의 데이터를 받을 시 띄어쓰기가 `+`로 표기가 되어있는데, `+`를 공백문자로 치환을 해야한다.

## As-is
여기서 처음에는 아래와 같은 코드를 사용했다.
```JavaScript
	data.title = decodeURIComponent(data.title).replace(/\+/g, ' ');
```

이렇게 해버리니 띄어쓰기용 `+`가 공백문자로 치환이 되었지만, 특수문자로 쓰여진 `+`로 공백문자로 치환되는 문제가 발생!

## To-be
아래와 같은 코드를 통해 문제를 해결할 수 있었다.
```JavaScript
	data.title = decodeURIComponent(data.title.replace(/\+/g, ' '));
```

즉, Raw 데이터를 받은 상태에서 `+` 문자를 공백문자로 선 치환 시킨 값을 Decode 해주면 되는것이였다.