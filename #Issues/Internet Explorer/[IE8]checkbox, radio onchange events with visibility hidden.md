# input[type="checkbox"], [type="radio"]에서 onChange Event 가 먹히지 않는 경우

##상황
Custom Checkbox 에서는 input[type="checkbox"]를 사용해야 하지만 숨겨야 하는 경우가 생긴다. (Radio Button 도 동일)

여기에서 checkbox 를 숨길 때 visibility:hidden 속성을 반영하게 되면 IE8 에서는 change 이벤트가 먹히지 않는다. (jQuery on method 기준)

>IE9 이상 브라우저부터는 정상인식

### jQuery 기준의 change event
```JavaScript
    $('input[type="checkbox"]').on('change', function(e) {
      var $_self = $(this);
      if (!$_self.hasClass('is-custom')) // didn't use customize checkboxes
        return true;

      var $_selfLabel = getLabel($(this), e);
      var isChecked = $_self.is(':checked');

      if (isChecked) {
        $_selfLabel.addClass('is-checked');
      } else {
        $_selfLabel.removeClass('is-checked');
      }
    });
```


### change 이벤트가 먹히지 않는 checkbox 숨김 속성
```CSS
	input[type="checkbox"]{
    	position: absolute;
        overflow: hidden;
        height: 1px;
        width: 1px;
        margin: -1px;
        visibility:hidden
    }
```

### 개선된 checkbox 숨김 속성
```CSS
	input[type="checkbox"]{    
    	position: absolute;
        overflow: hidden;
        clip: rect(0 0 0 0);
        height: 1px;
        width: 1px;
        margin: -1px;
        padding: 0;
        border: 0;
    }
```