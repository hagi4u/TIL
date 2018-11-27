# Lambda, API Gateway 그리고 Cloudfront 구성에서의 Issues

## MIME Issue
인터넷에 전달되는 파일 포맷, 그리고 컨텐츠를 위한 부분 식별자 역할을 함, 

### 예시 코드

```
const serverless = require('serverless-http');
...

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
  'text/xml',
]
...
module.exports.lambdaFunc = serverless(app, {binary: binaryMimeTypes});
```


위와 같은 MIMEType 으로 `serverless-http` 를 실행 시키는 경우에는 일반적인 웹 사이트의 파일 포멧과 컨텐츠를 모두 가져올 수 있지만 아래와 같은 형태의 파일은 불러오지만 인식할 수 없는 현상이 생김
```
*.woff, *.ttf
```
보편적으로 웹 폰트에 많이 사용되며 (fontawesome...) 아이콘이 들어가야 할 자리에 ㅁ 가 생겨 아이콘이 깨지는 현상 발생 (일반적인 글꼴 데이터가 저장 된 웹 폰트라면 브라우저에서 해당되는 웹 폰트로 렌더링이 되지 않을 것)

여기서는 `binaryMimeTypes` 배열에 아래와 같은 내용을 추가 해야 함
```
'application/font-woff',
'application/x-font-ttf'
```

- 위 내용은 크롬 디버깅 툴 Network 탭에서 `ttf, woff` 파일을 받아올 때 기록되는 content-type 를 카피 한 것
- 이 외 나머지 파일들도 위와 같은 메커니즘으로 진행을 하면 됨
