---
title: "2 Github에 Jekyll테마 적용하기"

categories: github   
tags: [github블로그, jekyll, ruby]

excerpt: "Ruby, Jekyll 설치 후 선택한 Jekyll 테마를 Github블로그에 적용하기"   # 미리보기 텍스트

post-order: 3     # 날짜순이 아닌 임의로 포스트 정렬하기 위해 코드 추가

toc: true         # table of contents. 우측 상단의 목차
toc_sticky: true  # toc 고정(true) 시 스크롤에도 우측 상단 고정
toc_label: "목차"

date: 2025-06-25
last_modified_at: 2025-06-25
---

Ruby언어로 동작하는 정적 사이트 생성기 Jekyll 기반으로 기본 도메인 개설 후 테마 커스텀



## 1. 로컬 폴더에 Ruby 설치 및 확인


  
여기서부터는 Jekyll이라는 github pages를 지원하는 정적 사이트 생성기를 이용해 블로그 레이아웃을 꾸며줍니다. Jekyll은 Markdown 및 HTML 파일을 가져와 선택한 레이아웃으로 정적 웹사이트를 만듭니다. (출처: Github 공식홈페이지)
(참고 : https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
①	Ruby 설치 : Jekyll은 Ruby라는 언어 위에서 작동하므로 우선 루비 공식 설치 사이트에서 devkit 포함된 Ruby를 다운받습니다. 윈도우 비트에 맞는 버전을 선택합니다. 
②	Ruby 설치 확인 : 모두 설치한 후 명령 프롬프트(win+R 후 cmd 입력) 에서 ver ruby 입력했을 때 Ruby의 버전이 확인되면 정상적으로 설치되었습니다. 
루비 공식 사이트: https://rubyinstaller.org/downloads/



## 2. 로컬 폴더에 Jekyll 설치 및 확인



①	로컬 블로그 폴더 내 Jekyll, bundler 패키지 설치
Jekyll 다운로드 명령어 : gem install Jekyll (gem : ruby에서 사용하는 명령어)
* hello world.html 및 README.md 파일 삭제 후 다음 단계 진행
Jekyll 설치 명령어 : jekyll new .
bundler 설치 명령어 : gem install jekyll bundler (bundler를 이용하면 로컬에서 jekyll을 직접 실행 가능)
 

 
②	Jekyll 설치&동작 확인 : 
커맨드 창에 bundle exec jekyll serve를 입력
브라우저에서 localhost:4000을 입력했을 때 
기본화면이 나오면 정상적으로 진행되고 있습니다. 
 
 

## 3. Github에 로컬 폴더 변경 사항 반영



git add . 
git commit -m “메시지”
git push -u origin main
  


## 4. Jekyll 테마 선택



Jekyll이 편한 이유는 이미 만들어진 블로그 템플릿 중 마음에 드는 것을 선택할 수 있기 때문입니다. Jekyll 테마는 아래 사이트에서 확인할 수 있고, 인터넷에 테마 추천글도 많이 있습니다. 
https://jamstackthemes.dev/ssg/jekyll/
http://jekyllthemes.org/
https://jekyllthemes.io/
https://jekyll-themes.com/
저는 minimal mistakes를 선택했습니다. 



## 5. 로컬 폴더에 Jekyll 테마 내려받기



①	Jekyll 테마 제공하는 Github 페이지로 이동
( ex : https://github.com/mmistakes/minimal-mistakes/releases/tag/4.27.0)
②	 Code 버튼 클릭  Download Zip 버튼 클릭  로컬PC에 Jekyll 테마 .zip파일 내려받기




③	내려받은 폴더 열기  파일 전체 선택&복사  로컬폴더에 붙여넣기
(동일한 파일명은 덮어쓰기)
 


## 6. 기본 도메인에 Jekyll 테마 적용되었는지 확인



①	커맨드 창에 bundle install
②	커맨드 창에 bundle exec Jekyll serve
③	브라우저 검색창에 localhost:4000 




<hr/>
<hr/>
### 참조
[Google](https://google.com)
  