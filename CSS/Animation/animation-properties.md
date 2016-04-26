# CSS3 Animation Properties
CSS3의 애니메이션에 대한 정리를 하는 공간입니다.

이 공간은 수시로 업데이트 되며, commit log 를 통해 어떤 내용이 업데이트 되어있는 지 알수 있습니다.

## animation-fill-mode
`애니메이션의 시작/종료에 대한 처리를 어떻게 해야 할 것인가?` 와 관련 된 속성

|Property|Description|
|---|---|
|none **(default)**|애니메이션 시작 전 까지 원래 위치에 고정, 애니메이션이 끝나면 첫 위치로 되돌아감|
|forwards|애니메이션 시작 전 까지 원래 위치에서 대기, 애니메이션이 끝나는 위치에서 멈춤|
|backwards|페이지 로딩 시 애니메이션 시작 위치로 이동, 애니메이션이 끝나면 원래 위치로 돌아감|
|both|페이지 로딩 시 애니메이션 시작위치로 이동 후 재생하고 애니메이션이 끝나는 위치에서 멈춤 (forwards, backwards 적용)|

## animation-direction
`애니메이션의 방향에 대한 제어`속성

|Property|Description|
|---|---|
|normal (default)|시작점에서 시작, 끝점에서 끝나면 다시 시작점에서 시작|
|reverse|끝점에서 시작, 시작점에서 끝나면 다시 끝점에서 시작|
|alternate|시작점에서 시작, 끝점에서 끝나면, 끝점에서 다시 시작|
|alternate-reverse|끝점에서 시작, 시작점에서 끝나면 시작점에서 다시 시작|

## animation-iteration-count
`애니메이션의 반복횟수`설정