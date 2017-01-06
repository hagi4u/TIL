## Git의 pathspec 에서 deleted 혹은 modified 에 대한 상태가 여러개 인 경우

```
#    deleted:    file1.txt
#    deleted:    file2.txt
#    deleted:    file3.txt
#    deleted:    file4.txt
```

이러한 경우, 혹은 modified 가 많은 경우에는 `add` 명령어의 update 옵션인 -u 를 적어준다.

```
git add -u
```

그리고 난 후 added 된 파일들에 대한 명령을 다시 입력하여 commit 시킨다.

```
git add .
```