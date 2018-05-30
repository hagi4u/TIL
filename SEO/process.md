#SEO (google 기준) 작업 프로세스


##1. 시멘틱한 마크업파일 제작
HTML은 마크업 랭기지, 의미있는 마크업을 통해서 문서를 만든다고 가정하고 각 내용에 적당하게 알맞는 태그를 통해 문서 작성을 한다.

- ```<head></head>``` 사이에 TDK (Title, Description, Keywords, og:TDK) 를 적당히 작성
- ```<hn></hn>```태그를 통해 문서의 목차 (색인)을 잘 꾸려나가 구조를 잘 잡는것이 핵심


##2. robots.txt
robots.txt 는 웹 크롤러와 같은 봇들의 접근을 제어하기 위한 규약, url level 에서 가장 상위에 있어야 함(ex: https://example.org/robots.txt) 

### Example

```txt
User-Agent: *
Allow: *
```

```txt
User-Agent: *
Disallow: /foo/bar/
```


##3. sitemap.xml 제작
robots.txt 는 크롤러의 접근을 허용하는 것이라면, ```sitemap.xml```은 구글과 같은 검색엔진 봇이 사이트의 쉽게 구조파악을 하고 쉽게 발견되지 않는 페이지도 크롤링을 시도할 수 있게 해준다.

참고사이트: https://www.sitemaps.org/ko/protocol.html


##콘텐츠 잘 쓰게 갈구기.