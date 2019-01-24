# 넉스트 (이하 Node.js) 서버 프로그램을 AWS 람다에 배포하여 사용하는 방법.

## 0. 사전 설정

아래 소개 될 serverless 프로그램은 aws 에서 제공하는 cli 를 사용하고, aws cli 를 쓰기 위해서는 적당한 권한이 있는 `aws_access_key_id` 와 `aws_secret_access_key`를 필요로 합니다.

따라서 AWS IAM 에서 적당한 권한이(보통 Administrator, 혹은 serverless.com 에서 권장하는 권한) 부여 된 key, secret 키 값을 발급 받아 아래와 같은 동작을 진행합니다.


### aws credentials 파일 생성
```
$ vi ~/.aws/credentials
```

아래와 같은 내용 추가
```
[default]
aws_access_key_id = YOUR_KEY
aws_secret_access_key = YOUR_SECRET
```

## 1. NPM Package Install
아래 노드 모듈 설치

```
$ yarn add serverless serverless-http
$ yarn add -D serverless-apigw-binary serverless-plugin-warmup
```

## 2. serverless.yml 수정

./serverless.yml
```YAML
service: BDSPackageFrontEndScaffolding # NOTE: update this with your service name

provider:
  name: aws
  runtime: nodejs8.10
  iamRoleStatements:
    - Effect: 'Allow'
      Action:
        - 'lambda:InvokeFunction'
      Resource: "*"
  stage: dev
  region: ap-northeast-2

functions:
  nuxt:
    handler: handler.nuxt
    environment: 
      NODE_ENV: production
    events:
      - http: ANY {proxy+}

plugins:
  - serverless-apigw-binary
  - serverless-plugin-warmup
 
custom:
  apigwBinary:
    types:
      - '*/*'
```

## 3. handler.js 수정
`serverless.yml`에서 functions 에 정의 된 handler 을 기반으로 아래와 같이 handler.js 를 생성합니다. 

굳이 `handler.js` 가 아닌 다른 경로에서 작업 하셔도 되며 스크립트의 경로를 `serverless.yml` 의 handler 값에서 적당히 파일 경로를 넣은 후 export 되는 모듈 이름을 작성하면 됩니다.

아래 예시파일은 nuxt.js 를 사용 했을 때의 예시입니다.

./handler.js
```JavaScript
'use strict';
const { Nuxt } = require('nuxt');
const path = require('path');

const serverless = require('serverless-http');
const express = require('express');
const nuxtConfig = require('./nuxt.config');

const app = express();
app.use('/_nuxt', express.static(path.join(__dirname, './.nuxt/dist/client')))

const binaryMimeTypes = [
  'application/javascript',
  'application/json',
  'application/octet-stream',
  'application/xml',
  'font/eot',
  'font/opentype',
  'font/otf',
  'image/jpeg',
  'image/png',
  'image/svg+xml',
  'text/comma-separated-values',
  'text/css',
  'text/html',
  'text/javascript',
  'text/plain',
  'text/text',
  'text/xml'
]

const config = { dev: false, ...nuxtConfig };
const nuxt = new Nuxt(config);

app.use(nuxt.render);

const handler = serverless(app, {binary: binaryMimeTypes})
module.exports.server = async function (ev, ctx, cb) {
  if (ev.source === 'serverless-plugin-warmup') {
    console.log('람다를 따땃하게!')
    return cb(null, '람다를 따땃하게!')
  }

  return await handler(ev, ctx)
}

```

## 4. 서버 프로그램 수정

./server/index.js

서버 프로그램(express 혹은 nuxt로 구성 된)의 변수를 export 하여 위 handler.js 에서 serverless 함수에 반영해야 합니다.

그러므로 서버 프로그램에 대한 설정 및 라우트들을 개발하여 export 시킵니다. (별도의 트렌스파일러가 없으면 구문은 ES5 문법으로 해야합니다)

```JavaScript
...
app...
...

module.exports = app;
```

## 5. NPM Script 설정

package.json

일반적인 문서들에서는 serverless 모두 전역(-g)설치를 하라는 내용이 있습니다.

하지만 현재 프로젝트 폴더를 기준으로 serverless 프로그램을 실행 해 주는것을 저는 개인적으로 권장합니다. (내 컴퓨터는 소중하니까요)

```
...
  "scripts": {
    ...
    "serverless:dev": "NODE_ENV=production ./node_modules/serverless/bin/serverless deploy",
    ...
  }
...
```