# Javascript Cookie (Like Code-snippet)

## setCookie
``` JavaScript
  function setCookie(name, val, day){
    var cookies = name+'='+escape(val)+'; path=/';
    var expire = new Date();
    expire.setDate(expire.getDate() + day);    
    
    if( day != null ) 
      cookies += ';expires='+expire.toGMTString()+';';

    document.cookie = cookies;
  }
```

## getCookie
```javascript
  function getCookie(name){
    var _name = name + '=',
        cookieData = document.cookie,
        start = cookieData.indexOf(_name),
        val = '';

    if( start != -1 ){
      start+=_name.length;
      var end = cookieData.indexOf(';', start);
      
      if(end == -1) end = cookieData.length;
      
      val = cookieData.substring(start, end);  
    }
    return unescape(val);
  }
```

## Usage
```
	setCookie('name', 'value', 7); // 1주일동안 유지되는 name 쿠키 (값은 value)
    setCookie('name', 'value', -1); // 쿠키 삭제
    
    getCookie('name');	// 쿠키 값 보기
```