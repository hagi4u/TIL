# 글로벌 대응 시 프론트엔드 고려 해야 할 사항

## 시간 
서버시간의 GMT 에 따라 DB에 기록되는 시간에 대해 각 나라별 시간차에 대한 이슈를 명확히 대응해야 함

> 마버리/스타.ai 에 댓글이나 피드쪽을 보게되면 GMT 반영이 잘 안되어서 (n시간전 이 아니라 n시간후 형태로 나오게 되는데 서버기준에서 이 타임존을 클라이언트에서 잘 세팅)

### 호텔 예약에서의 이슈
한국시간은 12/28일 토요일인데, 샌프란시스코 시간은 12/27 금요일인 경우
GMT 기준의 클라이언트 사이드 시간에 대해 UI 작인 verification 이 필요함

## 언어
- 현지에서 지내다보니 언어에 대한 기준은 위치가 아닌 클라이언트의 언어를 기준으로 해야 하는것으로 판단
- 하지만 언어에 대한 변화를 요청하는 UI 는 alternative 하게 제공 되어야 함 

## TTFB, DNS Lookup 의 필요성
- 각 리소스 및 API 엔드포인트들에 대해 TTFB, DNS Lookup 는 해외에서 (특히 느린 환경) 이 부분이 시간이 가장 오래 걸림 
- 따라서 preconnect, preload 와 같은 메타태그를 


## Asset Chunks
- 자바스크립트의 번들 용량을 최대 100kb - 150kb 로 맞추고, 모두 청크를 만들어서 리퀘스트를 늘려야 함
- HTTP/2 의 경우는 한번 리퀘스트 시 제한된 갯수가 없음
- 미국의 경우 브라우저 환경은 국내와 다르게 HTTP/2 환경이 자주 사용되는 환경이기 때문 (국내만 유일하게 좀 있는 수준)


## API Response timing
- 현재 우리회사의 백엔드 개발 방식은 리전별로 CF+Lambda+APIGateway 형태로 EdgeLambda 를 통해 HTTP Request 의 값을 토대로 어느쪽의 리전이 더 가까운지 판단하여 그리로 보내는 방식
- 하지만 CloudFront만 써서 Origin Connection 에 대한 지연이 없으면 굳이 비용 두배로 나가지 않게 써도 무방할 것 같음