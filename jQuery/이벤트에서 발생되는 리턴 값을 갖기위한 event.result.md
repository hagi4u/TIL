# 이벤트에서 발생되는 리턴 값을 갖기 위한 event.result
자세히보기 >> [jQuery API Document](https://api.jquery.com/event.result/)

## Example
Input maxlength 구현(IE8이상 지원)과 API 개념으로 현재 input 의 length 값을 실시간으로 표현

### API Level
```JavaScript
 /**
 * maxlength 지원 (IE8 ~)
 */
$(document).on('input keyup', 'input[maxlength], textarea[maxlength]', function(e) {
  // maxlength attribute does not in IE prior to IE10
  // http://stackoverflow.com/q/4717168/740639
  var $this = $(this);
  var maxlength = $this.attr('maxlength');
  if (!!maxlength) {
    var text = $this.val();

    if (text.length > maxlength) {
      // truncate excess text (in the case of a paste)
      $this.val(text.substring(0, maxlength));
      e.preventDefault();
    }

    return text.length;
  }
});
```

### Using in JavaScript with jQuery (included API Level)
```HTML
	<p class="input-length-state"> 
    	<b> 00 </b> / 100
	</p>
```


```JavaScript
$(document).on('keyup', 'input[maxlength], textarea[maxlength]', function(e) {
    var length = e.result; // API Level 에서 return 되는 값을 리턴
    var maxLength = $(this).attr('maxlength');

    $('.input-length-state).find('b').text(length);
});
```

e.result 는 API Level 의 동일한(keyup) 이벤트 핸들러에서 return 되는 text.length 값을 받아온다.
