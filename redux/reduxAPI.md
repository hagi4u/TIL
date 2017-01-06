# Redux for ES2015 (using React)

## 동작 원리

### Flux Pattern
> 한 방향으로 흐르게 하는게 핵심 (Flux Pattern)

```
action -> dispetch -> store -> view
               |                 |
               |                 |
               -----<=action------
```

## 작업 순서
1. action 작성
2. reducer 작성
3. component 작성
4. dispetcher 작성
5. store 생성
6. 렌더링

### action 작성
```{components}/action.js``` 파일 생성 후 action을 작성한다.

```JavaScript
export const GET_MODULE = 'GET_MODULE';

export function getModule(idx) {
    return{
        type: GET_MODULE,
        idx: action.idx
    }   
}
```

여기서 return 의 ```type``` 는 무조건 가장 상단에 위치 해야하며 나머지는 순서 상관없이 작성, Dispatcher 에서의 Argument 는 ```action.{variable}``` 로 받는다.

### reducer 작성

#### Require Methods
* combineReducers
> 여러개의 Reducer들을 하나로 합칠 때 사용되는 redux method

```JavaScript
import { getModules } from './action';
import {combineReducers} from 'redux';

const initialState = {
    value: 0
};

const modules = (state = initialState, action){
    switch (action.type) {
        case GET_MODULES:
            return Object.assign({}, state, {
                value: state.value;
            });
        break;
        default:
            return state;
    }
};

export default combineReducers({
    modules
});
```


### component , dispetcher

#### Connect API
```
connect([mapStateToProps], [mapDispetcherToProps], [mergeProps], [Options])()
```
React Component 를 Redux Store 에 연결시켜줌

- mapStateToProps: Store의 state들을 Component의 Props 에 매핑
- mapDispetcherToProps: Component의 특정 함수형 props 를 실행시켰을 때 action을 dispetch 하도록 설정


### store 생성