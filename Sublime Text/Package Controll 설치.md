# Sublime Text Package Controll 설치
Sublime Text 기본으로 제공하는 기능 외 다른 기능을 사용하고 싶을 때 package control 을 이용하여 추가적인 기능을 사용할 수 있다.

## 설치
### For Mac
```fn``` + ```Control``` + ``` ` ```키를 눌러 아래 코드를 버전에 맞게 붙여넣기

### For Windows
```Ctrl``` + ``` ` ``` 키를 눌러 아래 코드를 버전에 맞게 붙여넣기

### Sublime Text 2
```Python
import urllib2,os,hashlib; h = '2deb499853c4371624f5a07e27c334aa' + 'bf8c4e67d14fb0525ba4f89698a6d7e1'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

### Sublime Text 3
```Python
import urllib.request,os,hashlib; h = '2deb499853c4371624f5a07e27c334aa' + 'bf8c4e67d14fb0525ba4f89698a6d7e1'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```


## 사용법
### For Mac
```Command``` + ```Shift``` + ```p``` 키를 눌러 ```package```를 입력

### For Windows
```Ctrl``` + ```Shift``` + ```p``` 키를 눌러 ```package``` 를 입력

Package Controll: * 으로 패키지와 관련된 명령들이 아래와 같이 나타난다.

- Install Package: 패키지를 설치
- List Package: 설치 된 패키지 목록 확인
- Remove Package: 패키지 삭제

이 외 다양한 명령어가 존재한다.

## ImportError: No module named urllib2 로 인해 설치가 되지 않는 경우!
[https://packagecontrol.io/installation](https://packagecontrol.io/installation) 에서 제공해주는 코드를 이용하여 Sublime text 내 Console 에서 복붙을 하게되면 위 에러가 뜨는데, 부득이하게 수동으로 설치를 해야한다.

> 이유는 Python 이 업그레이드 되면서 urllib2 가 모두 urllib 로 통합되었기 때문, Python 을 깊게 쓰지 않는 나로서는 urllib 만으로 통합시켜서 별도로 해결방법이 존재하리라 믿지만 그건 추후 정리 하는걸로.

1) [Package Control.sublime-package](https://packagecontrol.io/Package%20Control.sublime-package) 를 다운

2) 서브라임에서 ```Preference > Browse Packages``` 를 클릭한 후 ```Installed Packages/ ``` 폴더로 이동

3) *1)* 에서 받은 파일을 해당 폴더로 이동

4) 서브라임 재시작



## 패키지 검색
[http://wbond.net/sublime_packages/community](http://wbond.net/sublime_packages/community)