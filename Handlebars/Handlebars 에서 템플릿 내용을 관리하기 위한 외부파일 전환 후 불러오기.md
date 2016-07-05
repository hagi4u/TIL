# Handlebars 에서 템플릿 내용을 관리하기 위한 외부파일 전환 후 불러오기
동일한 마크업에 같은 내용이 들어간 템플릿 내용을 각각의 파일에 작성하게 되면 관리 이슈가 생기기 마련

이를위해 Handlebars 형식에 맞는 템플릿 파일을 생성하여 동일한 마크업에 대한 템플릿 내용을 더 용이하게 한다.

## 어떤방법으로 해야할까?
1. ```templates/*.hbs``` 형태의 파일을 생성
2. Ajax GET Method 를 이용하여 hbs 파일을 로드
3. 실제 랜더되어야 할 마크업 내용을 변수로 저장
4. 저장된 변수를 Handlebars.compile(~~) 
5. 컴파일 된 template 에 대해 innerHTML 코드로 대입

## 예제 (회사 홈페이지)
### templates/viewer-header.hbs
```HTML
{{!
	viewer-header.hbs
	WORK 상세페이지의 상단 영역
}}

  <nav class="viewer-lnb">
    <a class="viewer-btn-close"  href="#work-list">
      <i class="uri-work btn-close"></i>
    </a>
    <a class="viewer-btn-next"  href="#{{next}}">
      <i class="uri-work btn-next"></i>
    </a>
    <a class="viewer-btn-prev"  href="#{{prev}}">
      <i class="uri-work btn-prev"></i>
    </a>
  </nav>
  <header class="viewer-header">
    <h1 class="viewer-title">
      {{title}}
      <small>
        {{subtitle}}
      </small>
    </h1>
    {{#if genre}}
    <dl class="viewer-meta">
      <dt>Genre</dt>
      <dd>{{genre}}</dd>
      <dt>Client</dt>
      <dd>{{client}}</dd>
      <dt>Data</dt>
      <dd>{{pdate}}</dd>
    </dl>
    {{/if}}
    <p class="viewer-content">
      {{text}}
    </p>
  </header>
```

### viewer.js
```JavaScript
// Handlebars External Template Load
// JSON 형태로 저장하게 하여 template 변수에 대한 영역을 확장가능 하게 함.
var tmpl = {
	viewerHeader: ''
};

// GET Method 로 hbs 파일을 불러 온 후, Callback 받은 다음에 랜더되어야 할 source 를 변수로 저장
var setTemplate = function() {
	$.get('templates/viewer-header.hbs', function(source) {
		tmpl.viewerHeader = source;
	});
};

// 어느정도 싱크를 맞춰주어야 하기때문에 setTemplate 함수에서 Callback 을 받게 되면 아래 함수를 실행시키는 로직을 짜서 반영
var setViewerHeader = function(data) {
    var template = Handlebars.compile(tmpl.viewerHeader);
    $('#target').empty().append(template(data));
};
```

```setTemplate()``` 에서 Ajax 싱크를 맞추지 못하면 ```setViewerHeader()``` 에서 컴파일 자체가 되지 않는 상황이 발생하기 때문에 이에 대한 싱크는 적당하게 맞춰야 한다.