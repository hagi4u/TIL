# HEX 코드를 RGBA 코드로 컴파일되게 해보자

`rgba(<HEX_CODE>, <ALPHA>)` 형태로 추가하면 된다.

## EX
border-color 에 `#D9D9D9` 와 0.3의 alpha 값을 활용 시

### SCSS
```CSS
.some{
  border-color: 1px solid rgba(#D9D9D9, 0.3)
}
```

### CSS
```CSS
.some{
  border: 1px solid rgba(217, 217, 217, 0.5);
}
```