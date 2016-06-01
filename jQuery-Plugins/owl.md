# owl.carousel 기록노트

## owl.carousel 에서 특정 슬라이더드인 경우 좌/우 드래깅을 막고 싶을 때
###HTML
```HTML
<div class="owl-carousel">
	<div> </div>
    <div> </div>
    <div class="js-disable-touch"> </div> <!-- 이녀석은 내가 막을테다! -->
    <div> </div>
</div>
```

### jQuery
```JavaScript
$(".js-disable-touch").on("touchstart mousedown", function(e) {
    // Prevent carousel swipe
    e.stopPropagation();
})
```
> Touch / Mousemove 에 대한 이벤트 해제

[참고URL](http://stackoverflow.com/questions/22909399/disable-dragging-in-specific-element-item-in-owl-carousel-jquery)