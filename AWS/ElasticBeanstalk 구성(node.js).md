# AWS Elasticbeanstalk 구성


## AWS 콘솔에서 환경 및 어플리케이션 생성

## aws-cli 를 통해 initialize

## .ebignore 에서 eb 에 배포되지 않아야 할 파일 설정

## .elasticbeanstalk/config.yml 에서 환경값 설정

## .ebextensions/{filename}.config 에서 추가옵션 설정

### Node.js
```yaml
option_settings:
  aws:elasticbeanstalk:container:nodejs:
    NodeCommand: "npm start"
```
와 같이 인스턴스 떴을 때 코맨드를 실행하는 것과 같은 설정을 해야 한다.


## 추가

### 20180511 기준
Node.js 플랫폼의 nginx 포트 기본 설정이 8081 로 되어있어 .ebextensions 에서 ngnix 의 고급 설정을 진행 하던지, Express.js (외 웹 서버 프로그램) 에서 서버 포트를 8081로 변환 해야 함.


### 20180528
express.js 에서 별도의 라우트가 존재하지 않고, 클라이언트 사이드에서 라우팅을 전담할 때, 
아래와 같은 코드를 꼭 추가 해야 elasticbeanstalk 에서 route 로 인식함

모든 라우트에 대해 클라이언트 사이드 라우팅이 반영 된 스크립트를 불러오는 html 로 sendFile 처리.

#### AS-IS
```
app.use('/', express.static(path.resolve(__dirname, '../build')));
```


#### TO-BE
```
app.use('/', express.static(path.resolve(__dirname, '../build')));
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname + '/../build/index.html'));
});
```