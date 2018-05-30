# ESLint 에서 missing radis parameter warning 뜨는 경우

parseInt 는 단순히 1개의 파라미터 ```parseInt(NoStringValue)``` 로만 사용하는 게 아니라,

2개의 파라미터 ```parseInt(NoStringValue, Radix)``` 즉, 진수를 넣으면 해결 된다.

2번째 파라미터 값을 넣지 않으면 0x로 시작되는 문자열은 16진수(0xNoStringValue)로 간주한다.

