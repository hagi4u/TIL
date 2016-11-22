# Laravel elixir
기본적인 개념은 gulp 스크립트를 이용하여 웹서버 인스턴스를 만든 후 실행

여기서 핵심은 gulp.js 를 얼마나 잘 커스터마이징 하느냐.

## Running artisan
gulp 에서 proxy를 위해 årtisan 실행 시 옵션을 줘야함
```
php artisan serve --host=0
```
```--host=0``` 은 http://0.0.0.0:8000 실행으로 되게 하는옵션, 즉 외부에서도 접속 가능하게 하는것

이렇게 해야만 browsersync 라고 하는 패키지가 프록시를 할 수 있게 된다.


## npm package Install
package.json(compose.json)에 저장된 NPM 패키지 설치 진행
```
npm install gulp-cli --save -g
npm install
```

## Development
```
npm run dev
```


## Build
Javascript, CSS 최적화를 위해서 아래와 같은 명령어 사용
```
npm run prod
```
