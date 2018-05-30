# git commit 후 unstage 로 특정 파일 보내기
상황.

도메인에 상관없이 여라가지 파일을 수정하고 특정 도메인별로 커밋 로그를 남기고 싶은데, 실수로 ```git add .```명령을 사용 한 경우.


## 1. git commit --amend
최근 커밋에 대한 정보를 확인 하는 명령어, 여기서 unstage 로 보낼 파일을 선정할 수 있다.

## 2. git reset --soft HEAD^
reset 명령은 HEAD 브런치를 이동 시킨다. 여기서 ```--soft``` 옵션은 HEAD에서 첫번째 뒤로 이동을 하게하는데 이때 HEAD^ 커밋이 되기 전 가르키도록 업데이트(취소..?) 하게 해 준다.

## 3. git reset HEAD {filePath}
1번에서 커밋 된 영역의 파일을 다시 unstaged 로 보내기 위해 위 명령어를 사용한다.
