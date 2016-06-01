# Internet Explorer 에서 JSONP 호출 시 success 가 아닌 error로 가는 경우

```
$.ajax({
    type:"GET", 
    url: url,
    cache: false,
    datatype: "jsonp",
    data: param,
    success: function(rtn) {},
    error: function(e){}
});
```

위 형태의 코드라면 
```datatype: "jsonp"``` 를 ```dataType: "jsonp"``` 로 바꾸어 줘야 한다.

[참고URL](http://wp.ahcheng.com/2014/03/23/facebook-access-token-request-does-not-work-in-ie-8/)