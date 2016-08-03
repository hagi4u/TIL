# Sass Control Directives 정리
Sass 에서 흔히 사용하는 control directives 정리
> Sass control directives 는  mixin 과 function에 의해 의사(구문)결정에 대한 정형화 된 흐름과 로직을 제공

일부 directives 에 대해서는 사용할 때 마다 정리하는걸로 진행!
(최종 업데이트일자: 160803)

## @if / @else
조건문! 기본적인 연산은 boolean 연산으로 여느 프로그래밍 언어와 동일한 로직을 갖춘다.
### 예제
```Sass
$boolean: true !default;

@if $boolean{
    // do stuff true case
} @else {
    // do stuff false case
}

$condition: 123;

@if $condition == 123{
    // do stuff true case
} @else {
    // do stuff false case
}    	
```

## @else if
조건문에서 다른 조건에 대한 수식을 추가하는 경우
```Sass

$condition: 123;

@if $condition == 123{
    // do stuff 1234 case
} @else if $condition == 456{
    // do stuff 456 case
} @else {
    // do stuff false case
}
```


### Appendix Bitwise Operations
조건문에서는 여러조건에 대해 부합하기위해 bitwise 연산이 필요하다. 현재는 and or 문 추가되었으며 이후 사용에 대해서는 더 추가 하는것으로..

|연산자|내용|
|---|---|
|and|A조건과 B조건이 항상 일치해야한다.|
|or|A조건과 B조건 중 하나만 일치하면된다.|

## @for
기본적인 반복문

```Sass
$length: 10;

@for $i from 1 through $length; {
&.thumb-npc#{$i} {
  @if $i==3 or $i==8 {
    width: rem(133px);
    height: rem(164px);
  }
  @else {
    width: rem(112px);
    height: rem(164px);
  }
}
```