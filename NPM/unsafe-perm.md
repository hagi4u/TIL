# unsafe-perm

- 타입: Boolean
- 기본값 : false

## 설명
NPM 설치 시 해당 시스템의 UID/GID 권한의 억제 유무를 설정하는 옵션

## 사용법
.npmrc 파일을 만들고,

```env
unsafe-perm=true
```

저장

## 언제 주로 사용하는가?

AWS ElasticBeanstalk 와 같은 컨테이너 서비스에서 root 권한을 이용하여 NPM 설치하지 못할 때 필요.


출처: https://docs.npmjs.com/misc/config#unsafe-perm