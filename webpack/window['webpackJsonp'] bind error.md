## 상황1. webpack3 를 사용하는 개발 환경(Nuxt.js)에서 webpack4 을 사용하여 번들 된 Script 파일을 로딩 하는 경우

이 문제는 webpack 으로 번들 된 코드가 청크 로딩을 할 적에 window.webpackJsonp 를 사용하게 되는데,


webpack3 에서는 첫번째 번들파일 (entry 파일)은 webpackJsonp 라는 전역함수를 등록하고 다른 청크를 로드할 때 이 함수를 호출 하게된다. webpack3 에서 청크 로딩에 대한 문제는 런타임(entry)에 로드 되어야 하는 파일이 다른 청크보다 먼저 로딩이 되어야 한다. (따라서 script 태그의 async 속성을 실행할 수 없음)

webpack4 는 새로운 방식으로 청크 로딩으로 배열 푸시를 통해 청크 로딩을 하게된다. 푸시 된 배열에 있는 모든 대기열을 처리하기 때문에 런타임에서의 등록된 전역 함수를 요구하지 않기 때문에 비동기 로딩이 가능하다.


```
*.js:906 Uncaught TypeError: Cannot read property 'bind' of undefined
```

위와 같은 오류가 발생하고, 코드의 내용은 아래와 같은 경우.

```
/******/ 	var jsonpArray = window["webpackJsonp"] = window["webpackJsonp"] || [];
/******/ 	var oldJsonpFunction = jsonpArray.push.bind(jsonpArray);
```

