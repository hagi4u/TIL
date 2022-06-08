# Border inner width
보통 box-model 에 의해 border 속성은 width 만큼 영역을 차지하게 되는데, 특정된 width/height 내에서 border를 포함해야 하는 경우가 생기게 되는데 이때는 `box-shadow` 속성과 `inset` 을 같이 활용하면 된다.

```CSS
box-shadow:0 0 0 <WIDTH>px rgba(0,0,0,.5) inset;
```

## EX
```CSS
.selector{
  display:block;
  width:30px;
  height:30px;  
  box-shadow:0 0 0 1px rgba(0,0,0,.5) inset;
}
```