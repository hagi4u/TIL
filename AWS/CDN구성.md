# AWS CDN (Content Delivery) 구성

## AWS 에서 사용 해야 할 도구

1. S3 Storage
2. Route 53
3. CloudFront
4. ACM (AWS Certificate Manager)

## 전체 플로우

1. S3 Storage 버킷 생성
2. S3 Storage 를 CloudFront에 연결
3. Route 53에 도메인 추가 후 레코드 추가
4. ACM에서 인증서 추가 후 도메인 명 입력 (추가 네임으로 \*.domain.com 입력하는게 좋음)
5. 4에서 검증이 끝나면 CloudFront 에서 SSL 과 관련된 정보(Custom SSL)에 검증된 SSL 추가
6. In Progress 가 끝나게 되면 사용


## 방법

작성 예정..