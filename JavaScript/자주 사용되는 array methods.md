# 자주 사용되는 JavaScript Array Methods

## Array.prototype.indexOf()
배열에서 특정값이 존재하는지 여부를 판단

-1 이면 존재하지 않으며 그 이외의 숫자는 해당하는 인덱스를 리턴

```JavaScript
var arr = ['apple', 'banana', 'cidar', 'coke'];
var isExistInArr = (arr.indexOf('pineapple') !== -1); // true
var getIndexNo = (arr.indexOf('coke'));	// 3
```

#### IE8 Polyfill
IE9 이하 브라우저에서는 ES5 를 지원하지 않아 IE8 브라우저에서는 별도의 Polyfill 이 필요하다
```JavaScript
/**
 * Array.indexOf()
 * @function  indexOf
 * @param  {String} String 검사 할 문자
 * @param  {Int} Start 시작 순서 
 * @return {Int} 문자열 길이
 */
if (!Array.indexOf) {
  Array.prototype.indexOf = function (obj, start) {
    for (var i = (start || 0); i < this.length; i++) {
      if (this[i] == obj) {
        return i;
      }
    }
  };
}
```

## Array.prototype.filter()
JSON으로 구성된 배열에 대해 JSON의 Key 값 조건을 이용하여 해당하는 영역의 JSON Data 를 리턴한다.

값이 존재하지 않는 경우는 빈 배열을 리턴, Array.length 를 통하여 값이 존재하는지 안하는지 여부 확인 가능(0 이상은 존재 0은 미 존재)

```JavaScript
	
var jsonFilter = [{
  'name': 'apple',
  'price': 1000
}, {
  'name': 'cidar',
  'price': 1000
}, {
  'name': 'banana',
  'price': 3020
}, {
  'name': 'coke',
  'price': 5000
}];

// price 가 1000에 해당하는 것에 대한 JSON Data 들을 리턴한다 (배열 형식)
var getItem = jsonFilter.filter(function(item) {
  return item.price === 1000;
});
  
for (var i = 0; i < getItem.length; i++) {
  document.write('1000 price item is ' + getItem[i].name + '<br>');
}
// 결과값
// 1000 price item is apple
//1000 price item is cidar
```

#### IE8 Polyfill
마찬가지로 Array.prototype.filter 는 ES5의 문법이기 때문에 IE9이하에서는 지원하지 않으며, 그에 대응하는 Polyfill은 아래와 같다.

```
if (!Array.prototype.filter) {
  Array.prototype.filter = function(fun/*, thisArg*/) {
    'use strict';

    if (this === void 0 || this === null) {
      throw new TypeError();
    }

    var t = Object(this);
    var len = t.length >>> 0;
    if (typeof fun !== 'function') {
      throw new TypeError();
    }

    var res = [];
    var thisArg = arguments.length >= 2 ? arguments[1] : void 0;
    for (var i = 0; i < len; i++) {
      if (i in t) {
        var val = t[i];

        // NOTE: Technically this should Object.defineProperty at
        //       the next index, as push can be affected by
        //       properties on Object.prototype and Array.prototype.
        //       But that method's new, and collisions should be
        //       rare, so use the more-compatible alternative.
        if (fun.call(thisArg, val, i, t)) {
          res.push(val);
        }
      }
    }

    return res;
  };
}
```

```JavaScript
```
