# CommonsChunkPlugin 으로 output의 라이브러리를 만드는 경우 

아래와 같은 vendor entry 에서 vendor 을 CommonsChunkPlugin을 이용하는 경우
```JavaScript
...
  entry: {
    ...commonConfig.entry,
    connect: [ // 요놈.
      'jquery',
      'vue',
      'ion-rangeslider',
      'slick-carousel',
      'owl.carousel',
      path.resolve(__dirname, dir.resources + '/js/package/index.js')
      'axios',
    ],
    [config.name]: path.resolve(
      __dirname,
      dir.resources + '/js/package/' + config.name + '/index.js'
    )
  }
...
  output: {
    filename: config.name + '/[name].js',
    library: 'mylib',
    chunkFilename: config.name + '/js/[name].js'
  }
...
  new webpack.optimize.CommonsChunkPlugin({
    name: 'connect'
  }),
```

Array type 의 connect entry 에 들어 가 있는 각각의 모듈들이 export 로 다 되어 있는 상태라면 배열 내 가장 마지막에 있는 스크립트 파일을 기준으로 ```output.library``` 의 값이 전역변수로 지정 된다.

위 경우 ```axios``` 가 connect 의 Array value의 가장 마지막에 차지하기 때문에 번들 후 브라우저에서 window.mylib 를 콘솔에서 입력 해 보면, axios 파일에 담긴 exports 된 내용들이 출력 됨 (함수, 변수 등등)