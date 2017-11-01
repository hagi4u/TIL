# App WebView Issue (Android/iOS)

## WebView 는 Custome Header 을 유지하지 않는다.

안드로이드와 아이폰의 모든 디바이스에서 webView 를 호출 할 때 Http Request Header 에 Custom Property 를 붙이는 경우가 생기는데, 이때는 처음 호출 된 웹 페이지의 리퀘스트에만 Request Header 이 붙여지고, 다른 페이지로 이동 하는 경우 이 Reqeust Header 가 유지 되지 않는다.

이때는 보통 서버사이드 (혹은 인증을 유지하는 곳과 관련된 곳)에서 쿠키, 파일, DB, Redis 등등으로 리퀘스트 헤더를 유지 해 주면 된다.