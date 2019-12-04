# nuxt@2 부터 global.document 할당방법


## 문제 정의
서버사이드에서 브라우저에서 쿠키값을 받아와 처리 할 때에는 아래와 같은 형태로 진행하게 된다.

[코드1-1 Node.js 에서 HTTP Request 에 대한 핸들러]
```JavaScript
function(req, res, next){
  if(req.headers.cookie !== undefined){
    global.document = {}
    global.document = req.headers.cookie;
  }
}
```

인터넷에서 나와있는 글에는 (다른 사람들이 블로깅 한 내용) nuxt 에서 위 코드를 대입 할 때에는 `nuxtServerInit` 함수에서 아래와 같은 코드 예제들로 설명한다

[코드 1-2]
```JavaScript
...
async nuxtServerInit(context, { req }) {
  if(req.headers.cookie !== undefined){
    global.document = {}
    global.document = req.headers.cookie;
  } 
}
...
```

위 예시에서 나온 코드는 nuxt@1.x 버전에서는 정상 작동하지만 nuxt@2.x 이상에서는 전혀 작동되지 않는것으로 확인했다. (`global.document` 를 `nuxtServerInit`에서 콘솔로 출력하면 정상 출력 되지만 서버사이드에서 사용하는 NPM 패키지에서는 undefined 로 뜨게 됨)

쿠키를 핸들링 하는 `js-cookie` 모듈에서 `get` 메소드를 실행하게 되는데 소스코드를 보게되면 아래와 같은 형태로 이루어 져 있다.

[코드 1-3]
```JavaScript
...
function get (key, json) {
  if (typeof document === 'undefined') {
    return;
  }
  ...

}
...
```

아쉽게도 위 `document` 를 [코드 1-2] 형태로 작성 할 경우 `undefined` 가 출되고, 이는 곳 `nuxtServerInit` 에서 작성한 [코드 1-2] 이 정상적으로 `global` 변수에 정의되지 않는 문제로 확인했다.


## 해결

`nuxt@2` 부터는 서버사이드 기준으로 미들웨어를 작성할 수 있는 `serverMiddleware` 개념이 추가 되었다.  (아마도 서버/클라이언트에 대한 도메인을 분리하기 위함인듯)


여기서 힌트를 얻어 `nuxt.config.js` 에 아래 코드를 추가 했고,

[코드 2-1]
```JavaScript
...
serverMiddleware: ['~/serverMiddleware/cookie.js'],
...
```


`~/serverMiddleware/cookie.js` 의 아래 코드를 추가 했다.

[코드 2-2]
```JavaScript
export default function(req, res, next) {
  if (req.headers.cookie !== undefined) {
    global.document = {}
    global.document.cookie = req.headers.cookie
  }
  next()
}
```

serverMiddleware 를 추가 후 [코드1-3] 에서 `document` 를 `console.log` 로 출력하니 정상적으로 `global.document` 가 `undefined` 가 아닌 `req.headers.cookie` 내용이 노출 되었음을 확인 했다.