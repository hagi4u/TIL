# Internet Explorer 에서 <main> Element 사용

```<main>``` Element 는 CSS에서 main 속성에 ```display:block;``` 를 주지 않으면 block 형태로 표시되지 않는다.

```HTML
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Main Element?</title>
  <style>
    html,
    body,
    main{
      height:100%;
      padding:0;
      margin:0;
    }
    main{
      /*display:block;*/ 
      background-color:#E0E0E0;
    }
  </style>
</head>
<body>
    <main>
      
    </main>
</body>
</html>
```

|IE Version|지원여부|
|---|---|
|9|X|
|10|X|
|11|X|
|Edge|O|

위의 코드에서 ```display:block``` 를 주면 IE11 이하 브라우저(IE9까지)는 <main> 태그에 ```height:100%``` 가 적용된다.