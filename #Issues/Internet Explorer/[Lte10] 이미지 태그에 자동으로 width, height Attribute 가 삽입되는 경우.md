#이미지 태그에 자동으로 width, height Attribute 가 삽입되는 경우 

HTML 코드 상에서 width, height 를 지정하지 않고, CSS 에서도 지정하지 않은 경우, 이미지의 크기를 계산 해 온 뒤 브라우저가 알아서 값을 넣는 현상.

----

## 해결방법

1. HTML 코드에서 width, height 값을 넣어 준다. (선택사항)
2. CSS 코드에서 ```max-width``` 속성만 지정하는 경우, 반드시 ```height``` 속성을 ```auto```로 지정 해야 한다.