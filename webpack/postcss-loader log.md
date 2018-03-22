#postcss-loader log

##Autoprefix plugin with vue.js

### ㅇ issue
vue.js 에서 발생된 현상 (현재까지)

develop 환경에서는 autoprefixer 가 아래 postcss.config.js 처럼 설정 된 경우
```
module.exports = {
  plugins: [
    require('autoprefixer')({browsers: ['last 2 versions','>= 5%','ie >= 9']})
  ]
};
```
번들링이 수시로 이뤄질 때 마다 css의 autoprefixer 이 반영된다.

하지만 이게 build 로 된 경우는 -webkit- 까지만 나오고 autoprefixer 설정은 반영이 안된다.


### ㅇ solve
***package.json*** 파일에 'browserlist' 키를 추가 해 주어 아래와 같이 설정한다.
```
...
  "browserslist": [
    "last 2 versions",
    "> 2%",
    "ie >= 9"
  ],
...
```

***webpack.config.js*** 에서 vue-loader 영역에 아래와 같은 코드를 추가 한다.
```
...
	postcss: [require('autoprefixer')],
...
```

이렇게 되면 postcss-loader 가 webpack 자체에 설정이 없더라도 ***postcss.config.js*** 에서 package.json 파일의 browserslist 값을 인식하여 해당 내용에 맞게 vue-loader에서 로딩되는 postcss-loader 의 autoprefixer 가 개발/빌드 환경에서 모두 정상 작동한다.

는 빌드환경에서 반영 안됨 ..ㅡㅡ