# Vue.js Server-side rendering Hydration

## 하이드레이션이란?
Client-side (Browser)에서 Vue Component 를 적당한 DOM에 마운트하여 렌더링한다. 


Server-side 렌더링에서는 Serve-side에서 렌더링 된 DOM요소를 다시 생성하지 않고, 정적으로 표시된 마크업 (Server-side rendered markup string)을 하이드레이션 (연결)하여 JavaScript 내용을 상호작용하게 하는 기능이다.




이를 구분하게 하는것은 마운트 될 DOM에 ```data-server-rendered="true"``` 속성 인데 Client-side 에서 렌더링 시 해당 data attribute 를 불러와서 하이드레이션 하게 된다.


### 주의사항
- 브라우저가 자체적으로 자동생성 해 주는 태그들을 Vue Component 단에서도 꼭 작성 해야 함
- a(inline-level)같은 태그안에 p(block-level)같은 태그 사용을 자제
- 마운트 될 DOM과 Vue component 의 ```<template>``` 태그 아래 root level 태그 명이 같아야 함

주의사항의 핵심은 Server-side에서 render된 string 의 DOM 구조와 Client-side 에서의 하이드레이션 해야 할 DOM구조가 일치해야 한다는 점이다. (심지어 태그까지도)

[참고사이트](https://github.com/vuejs/vue-ssr-docs/blob/master/ko/hydration.md)

