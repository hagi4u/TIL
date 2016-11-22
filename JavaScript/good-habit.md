# A good habit of using JavaScript
아래 항목은 좋은 코드를 만들기 위한 노력 중 내가 가진 습관이 아닌것에 대한것만 기록 한 것!

> 핵심은 일관성을 지키는 것에 있는것! 



## 유효범위 내 변수 선언시 이쁘게 보기
### Bad
```JavaScript
	var foo = '';
    var bar = '';
```

### Good
```JavaScript
	var foo = '',
      bar = '';
```

## 따옴표는 큰따옴표나 작은따옴표 중 하나를 선택하여 주로 사용하자
난 주로 작은 따옴표를 사용하지

## parseInt 말고 이렇게 쓰자
```JavaScript
	var num = 2.5
    
    parseInt( num, 10 ) // 이거와
    
    //아래 것들은 같다.
    ~~num
    num >> 0
    num >>> 0 // 얘는 음수에서는 다른 결과값이 나온다.
    
```

## 배열체크 조건문 꿀팁
```JavaScript
	// [배열, 스트링, 불린]에 무언가가 들어 가 있는지 확인하려면
	// 이렇게 말고
	if( array.length > 0 )... 
    
    // 이렇게 쓰자
    if( array.length )
    
    // 반대로 배열이 비어있는지 확인하려면
    // 이렇게 말고
    if( array.length === 0 )
    
    // 이렇게 쓰자
    if( !array.length )
```

## 변수 판정할 때 꿀팁
```JavaScript
	// 이렇게 말고
	if( foo === null || foo === undefined )
    
    // 이렇게 하자! (강제 형변환되는 == 를 사용)
    if( foo == null )
```