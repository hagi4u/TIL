#module 테이블의 apiurl 필드의 특정 패턴의 값을 찾아서 변경하는 예제

UPDATE {table}
SET {field} = REPLACE({field}, '{source}', '{target}')
WHERE {field} LIKE ('{pattern source value}%');


##example
```
UPDATE modules
SET apiurl = REPLACE(apiurl, 'https://celeb.api.mycelebs.com/', 'https://f1r7tet08j.execute-api.ap-northeast-1.amazonaws.com/prod/')
WHERE url LIKE ('https://celeb.api.mycelebs.com/%');
```