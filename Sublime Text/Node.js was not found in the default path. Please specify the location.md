# Node.js was not found in the default path. Please specify the location 에러
HTML CSS JS Prettify에서 Node.js 경로를 지정하지 못하여 발생되는 오류로서, 실제 경로를 지정하였음에도 해당 에러가 뜨는 이유는 윈도우 환경에서 경로가 정상적으로 확인되지 않고, Prettify 를 하려는 파일의 경로가 한글인 경우가 대체적이다.

## 해결법
해당 플러그인을 사용하는 핵심적인 파이썬 파일에서 한글을 인식할 수 있는 코드를 추가 해야한다.

> C:\Users\{{UserName}}\appdata\Roaming\Sublime Text 2\Packages\HTML-CSS-JS Prettify 에서 HTMLPrettify.py 을 연다.


```Python
import sys
reload(sys)
sys.setdefaultencoding('utf-8')
```

가장 상위에 위 코드를 붙여주면 해결