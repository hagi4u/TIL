# 개요
json object 에서 value 영역에 고유하게 쓰일 quote 가 정상적으로 파싱이 되지 않고, Unicode 형태로 출력되는 경우가 있다.


보통 클라이언트 코드 (EJS Template engine)에서는 서버에서 받은 변수를 출력 할 적에 `<%= variable >` 를 사용하는 편이긴 하지만, escape 문자 처리를 하기에 해당 문제가 발생 한다. 

이 때 `<%- variable>` 로 작성하여 escape 처리를 하지 않게 한다.
> ejs.co 에서는 `Outputs the unescaped value into the template` 로 설명 하고 있음

## 서버 측 리턴 코드
```
  {
    message: encodeURIComponent(JSON.stringify(response.data))
  }
```

## 클라이언트 측 리턴 코드 (EJS)
```
  var messages = <%-JSON.stringify(messages)%>;
```