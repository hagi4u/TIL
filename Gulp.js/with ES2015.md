# gulp.js with ES2015

##1. Install Gulp
```
npm install gulp & npm install gulp -g
```

##2. Install Babel(Transpiler) & Configuration Babel
```
npm install babel-core babel-preset-es2015 --save-dev
touch .babelrc
```

아래 내용을 .babelrc 에 작성

```JSON
{
    "presets": ["es2015"]
}
```

### Polyfill (ES3 지원 브라우저)
```
npm install babel-polyfill babel-plugin-transform-es3-member-expression-literals babel-plugin-transform-es3-property-literals --save-dev
```

.babelrc 파일 수정
```JSON
{
    "presets": ["es2015"],
    "plugins": [
        "transform-es3-property-literals",
        "transform-es3-member-expression-literals"
    ]
}
```
> IE8에서는 ES5이 100% 지원되지 않기때문에 특정 메소드 (indexOf 등등)은 별도의 Polyfill로 관리.
> 이곳을 참고! [es5-shim](https://github.com/es-shims/es5-shim)


##3. Configuration Gulp
```
touch gulp.babel.js
```

아래 내용을 gulp.babel.js 에 작성

```JavaScript
'use strict';

import gulp from 'gulp';

gulp.task('default', () => {
    console.log('hello world!');
});
```
