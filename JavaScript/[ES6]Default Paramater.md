# 함수 파라미터 중 기본 파라미터 할당에 대한 내용

## Variable
- 일반적인 내용대로 진행

## Object
동일한 Object 형태로 하고, Paramater 내 key 에 대해서 default value 를 지정

```
function f({a} = {a: 1}){
  ...
}
```

## Array
동일한 Array 형태로 하고, Paramater 내 index안에 value를 동일한 index로 지정
```
function f([1,2] = ['a', 'b']){
  ...
}
```