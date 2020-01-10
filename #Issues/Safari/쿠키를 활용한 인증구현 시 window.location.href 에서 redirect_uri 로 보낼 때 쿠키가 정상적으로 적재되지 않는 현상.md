
## 사용 환경
- nuxt.js
- aws-amplify
- amazon-cognito-identify-js

## as-is
```JavaScript
...
mounted(){
  window.location.href = getRedirectURL();
}
...
```

위 코드로 하게되면 크롬/파이어폭스/오페라 브라우저는 정상적으로 쿠키 적재가 되지 않아 아래와 방법으로 디버깅 시도를 해봄


### window.location.href 주석 제거 

주석 제거를 하지 않으니 당연히 redirect 가 되지 않았고, 사파리 개발자 도구의 저장공간에서 쿠키 영역을 보니, 정상적으로 쿠키 데이터들이 적재 되어 있는것을 확인 함


## to-be
```JavaScript
...
mounted(){
  setTimeout(() => {
    window.location.href = getRedirectURL();
  }, 500)
}
...
```

단순히 타이밍의 문제인걸로 우선은 판단되어 setTimeout 를 이용하여 쿠키를 적재 할 시간(?) 을 주었음
