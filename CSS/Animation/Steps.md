#Animation steps()

## animation-timing-function
애니메이션 키프레임의 동작에 대한 중간 상태를 어떤 간격으로 실행 할 지 지정하는 속성


### keyword values
- ease
- ease-in
- ease-out
- ease-in-out
- linear
- step-start
- step-end

### functional values
- cubic-bezier
- `steps`
- frames

### multiple animations
```CSS
animation-timing-function: ease, step-start, cubic-bezier(...)
```

### global values
- inherit
- initial
- unset

## steps() 
steps 는 animation keyframes 에서 from, to 의 duration 동안 몇 번의 steps 으로 실행 할 것이냐에 대한 function value 