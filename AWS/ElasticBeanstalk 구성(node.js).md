# AWS Elasticbeanstalk 구성


## AWS 콘솔에서 어플리케이션 및 환경  생성
한글버전이니 한글 읽고 어플리케이션, 환경을 생성하자

## aws-cli 설치
https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/eb-cli3-install-osx.html 에서 설치 방법 참고
https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/nodejs-getstarted.html NodeJS 

## aws cli config 설치
https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-chap-getting-started.html

이 설정을 참조 후 AWS KeyID, AccessKey 를 IAM에서 발급받은 (EB 접근에 권한이 있는) 키를 설정

`~/.aws/credentials` 파일
```
[default]
aws_access_key_id = 
aws_secret_access_key = 
```

혹은
```
aws configure
```
명령을 통해 access, secretkey 를 넣는다.

## aws-cli 를 통해 initialize
```
  $ eb init
```
를 하게되면 어플리케이션을 선택하는 프롬포트가 뜬다. 선택하거나 (없으면)새로만들던가 하면 됨 

## .ebignore 에서 eb 에 배포되지 않아야 할 파일 설정
1. .ebignore파일이 존재하면 .gitignore을 사용하지 않고 .ebignore 로 설정 됨
2. .ebignore파일이 존재하지 않으면 .gitignore파일로 설정 됨 


```
# dependencies
node_modules

# logs
npm-debug.log

# Nuxt build 
# nuxt.js 빌드 파일은 git에선 ignore 되어야하고, EB 에서는 ignore 되면 안됨 그래서 제거함

# AWS
.elasticbeanstalk

# Elastic Beanstalk Files
.elasticbeanstalk/*
!.elasticbeanstalk/*.cfg.yml
!.elasticbeanstalk/*.global.yml
```

## .elasticbeanstalk/config.yml 에서 환경값 설정
권장 사항

1. branch-defaults 에서 develop 브런치는 개발환경에 배포하게 하고, master 브런치는 실서버 환경에 배포하게 한다.
  > develop 브런치에서 QA가 모두 버그없이 끝나게되면 EB 콘솔에서 개발환경이 바라보고 있는 배포 파일을 실서버 환경이 바라보게 배포하면 실서버 배포는 끝 


2. 아래 global 영역은 기존 제공해주는 데로 사용 함
```yaml
branch-defaults:
  master:
    environment: ExcitingLotte-env
  develop:
    environment: ExcitingLotte-dev-env
global:
  application_name: Exciting Lotte
  default_ec2_keyname: null
  default_platform: arn:aws:elasticbeanstalk:ap-northeast-2::platform/Node.js running
    on 64bit Amazon Linux/4.5.1
  default_region: ap-northeast-2
  include_git_submodules: true
  instance_profile: null
  platform_name: null
  platform_version: null
  profile: null
  sc: git
  workspace_type: Application
```


## Appendix

### .ebextensions/{filename}.config 에서 추가옵션 설정
이 사항은 필수사항은 아니고 디테일하게 환경 설정을 해야하는 경우에만 사용 함 (앵간해서 사용할 일은 없음)
#### Node.js
```yaml
option_settings:
  aws:elasticbeanstalk:container:nodejs:
    NodeCommand: "npm start"
```
와 같이 인스턴스 떴을 때 코맨드를 실행하는 것과 같은 설정을 해야 한다.

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