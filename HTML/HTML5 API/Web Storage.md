# WebStorage (IE8 <= )
- 큰 데이터를 저장 가능
- 서버로는 전송이 되지 않음 (수동으로 가능)
- 도메인별로 영역이 다르게 지정
- 서브도메인 조차도 다르게 지정
- 서브도메인 간 데이터 접근 할 수 없음
- JavaScript 객체를 저장


## Local Storage
 - 데이터 유효기간이 없음
 - 단, 사용자가 브라우저 설정에서 삭제 가능

## Session Storage
 - 데이터 유효기간이 브라우저의 세션
 - 임시 저장소료 주로 이용
 - 여러창을 켜도 같은 도메인이면 같은 영역을 사용하는 것

## Methods (localStorage./ sessionStorage.*)
|메소드|내용|
|:---|:---|
|length|스토리지의 저장 된 데이터 갯수 반환|
|key(idx)|지정된 인덱스의 키를 반환, 없으면 Null 반환|
|getItem(key)|키에 대응하는 값을 반환|
|setItem(key, data)|키와 데이터를 매칭시켜 스토리지에 저장|
|removeItem(key)|키에 대응하는 값을 삭제|
|clear()|모든 데이터를 스토리지에서 삭제|



