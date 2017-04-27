# 이벤트 리스너에 2개 이상의 매개변수가 있고, jQuery 의 trigger 메소드에 2개 이상의 매개변수 전달하는 경우

### Event Listener
```JavaScript
this.$wrapper.find(classProps.buttons).on('click', (e, defaultValue = 50, isDispatch = true) => {
  registerFinderButtonHandler(e);

  const $self = $(e.currentTarget);
  this.setFilterCountToHeader();

  if( $self.hasClass('is-active') ){
    $self.trigger('pushFilter', defaultValue);  
  }else {
    $self.trigger('popFilter');
  }

  if( isDispatch ){
    this.dispatchAPI();
  }

  this.toggleSearchButton();
});
```

### Trigger to use multiple arguments
```JavaScript
  $(`[data-filter-key=${filter.filter_key}]`).trigger('click', [28, false]);
```

.trigger() 메소드에서 매개변수로 사용 될 데이터를 배열로 전달한다.