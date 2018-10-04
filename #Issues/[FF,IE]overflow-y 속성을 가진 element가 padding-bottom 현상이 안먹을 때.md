아래와 같이 텍스트 박스에 최대 높이값이 지정되어있고 스크롤 축 Y 부분을 자동으로 오버플로우에서 생성된다고 했을 떄,


크롬은 정상적으로 padding-bottom 을 제외하고 높이 지정이 되지만, 파이어폭스 및 인터넷 익스플로러에서는 되지않음

(스크린샷은 코코와 TVSummary 컴포넌트 첨부하기)
```
>div > p{
  position:relative;
  margin:0;
  max-height: 68px;
  padding-bottom:20px;
  overflow-x:visible;
  overflow-y:scroll;
}
```


위 상태에서 해당되는 박스에 가상선택자를 통해 padding-bottom 만큼의 height 를 추가 해 주면 상태 해결
```
&:after{
  content: '';
  display:block;
  width:100%;
  height:20px;
}
```