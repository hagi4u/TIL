# DOM요소에 [aria-hidden="true"] 추가 시 필요 한 사항

`[aria-hidden="true"]` 는 스크린리더 혹은 다른 보조기술로 활용되는 프로그램에서 해당 엘리먼트와 모든 하위 엘리먼트를 인식안되게 만들어주는 역할

`<iframe>` 태그와 같이 포커스 가능한 요소가 하위 엘리먼트에 있다면 부모 엘리먼트의 `[aria-hidden="true"]` 가 있다 하더라도 인식은 안되지만 키보드를 통해서는 포커스가 가능하기 때문에 통일성 없는 (가려지게는 했지만 키보드로 접근은 된다?) 구현방식이됨

[Focusable Elements-Browser Compatibility Table](https://allyjs.io/data-tables/focusable.html)

[in progress.]
