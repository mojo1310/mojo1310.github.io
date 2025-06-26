---
title: "3 Github의 Jekyll테마 수정하기"

categories: github   
tags: [github블로그, jekyll]

excerpt: "Jekyll 기본 테마를 변경해 블로그 맞춤 설정하기"   # 미리보기 텍스트

post-order: 4     # 날짜순이 아닌 임의로 포스트 정렬하기 위해 코드 추가

toc: true         # table of contents. 우측 상단의 목차
toc_sticky: true  # toc 고정(true) 시 스크롤에도 우측 상단 고정
toc_label: "목차"

date: 2025-06-25
last_modified_at: 2025-06-26
---


## 1. 블로그 기본 정보 설정 : _config.yml 파일에서 수정



- config.yml 파일에서 Site Settings/Site Author/default 3개 영역 수정

```
minimal_mistakes_skin    : "dark" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"



# Site Settings : 초화면 설정
locale                   : "ko-KR" # "en-US"
rtl                      : # true, false (default) # turns direction of the page into right to left for RTL languages
title                    : "무한히 반짝이는 것"  # 좌측 상단 블로그명
title_separator          : "-"
subtitle                 : "※관심사 저장 공간 : 글, 그림, 코딩, 수학, 여행, 음악" # site tagline that appears below site title in masthead
name                     : "모조(Mojo)"
description              : 
url                      : "https://mojo1310.github.io" # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
baseurl                  : # the subpath of your site, e.g. "/blog"
repository               : "mojo1310/mojo1310.github.io" # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
teaser                   : # path of fallback teaser image, e.g. "/assets/images/500x300.png"
logo                     : "assets/logo_mojo_dark.png" # 우측상단 블로그명 옆에 표시 path of logo image to display in the masthead, e.g. "/assets/images/88x88.png"
masthead_title           : # overrides the website title displayed in the masthead, use " " for no title
breadcrumbs              : # true, false (default)
words_per_minute         : 200
enable_copy_code_button  : # true, false (default)
copyright                : "모조(Mojo)" # "copyright" name, defaults to site.title
copyright_url            : "https://mojo1310.github.io" # "copyright" URL, defaults to site.url
```

- 로고 이미지는 assets 폴더에 저장하여 사용
- _config.yml에서 아래 부분 변경하여 저자 정보 설정 

```
# Site Author
author:
  name             : "모조(Mojo)"
  avatar           : "assets/logo_mojo.png" # path of avatar image, e.g. "/assets/images/bio-photo.jpg"
  bio              : "취미로 블로그 운영하는 직장인"
  location         : "대한민국 서울"
```

``` 
defaults:                 # 페이지의 머리말에 선언하지 않아도 아래 내용들은 기본값으로 적용
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single        
      author_profile: true   # 내 프로필을 사이드바에 표시
      read_time: true        # "한 포스트를 다 읽은데 n분" 표시
      comments: true       # 댓글 기능 활성화-댓글 제공자(utterance/giscus/disqus) 설정 필요
      share: true            # 소셜 공유 기능 활성화
      related: true          # 관련 포스트 추천 기능 활성화
      toc: true              # (김민정 추가) 블로그 목차 보기 기능 활성화-글 작성 시 .md파일의 front matter에 추가 설정 필요
      sidebar:     # (김민정 추가) 사이드바 카테고리 생성-navigation.yml 파일과 연동 필요
        nav: "sidebar-category"
```
★ 주의: layout이 posts일 경우 글 내 toc, 태그, 소셜 공유 기능이 표시 안될 수 있음
 
## 2. 사이드바 카테고리 생성: 사이드바 카테고리 구성 + 각 카테고리별 페이지 생성 + _config.yml 수정



①_data/navitaion.yml 파일에 사이드바 카테고리 구성 추가
<예시>
```
sidebar-category:
  - title: "카테고리Lv2"
    children: 
      - title: "카테고리Lv2"
        url: /categories/url1
      - title: "다른 카테고리Lv2"
        url: /categories/url2
```

②로컬 폴더에 _pages/sidebar-categories 경로 생성하고 카테고리별 페이지 생성 (.md파일)
```
---
title: " 카테고리Lv2
layout: archive
permalink: categories/url1
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['url1']%}     #posts 작성시 카테고리가 url1인 글 저장
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
```

③ _config.yml의 default 영역에 코드 추가
```
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: # true
      share: true
      related: true
      sidebar:                      # 새로 추가한 2줄
        nav: "sidebar-category"
```

④_navigation.yml 수정하고 _includes/nav_list 파일에서 메뉴별 포스트 수 표시되도록 코드 추가
- navigation.yml파일에서 각 children밑에 category 추가
```
sidebar-category:
  - title: "배움 모음"
    children: 
      - title: "Database: MS-SQL"
        url: /learn/mssql
        category: "mssql"
```
- nav_list파일을 통째로 아래 코드로 변경
```
{% assign navigation = site.data.navigation[include.nav] %}
{% assign sum = site.posts | size %}

<nav class="nav__list">
  {% if page.sidebar.title %}<h3 class="nav__title" style="padding-left: 0;">{{ page.sidebar.title }}</h3>{% endif %}
  <input id="ac-toc" name="accordion-toc" type="checkbox" />
  <label for="ac-toc">{{ site.data.ui-text[site.locale].menu_label | default: "Toggle Menu" }}</label>
  <li> 전체 글 수 ({{sum}})개 </li>
  <ul class="nav__items">
    {% for nav in navigation %}
      
      <li>
        {% if nav.url %}
          <a href="{{ nav.url | relative_url }}"><span class="nav__sub-title">{{ nav.title }}</span></a>
        {% else %}
          <span class="nav__sub-title">{{ nav.title }}</span>
        {% endif %}

        {% if nav.children != null %}
        <ul>
          {% for child in nav.children %}
          
          {% comment %}
             아래 부분은 카테고리 옆에 해당 카테고리에 해당하는 포스트 수를 표시하기 위해 수정되었습니다.
             navigation.yml에서 children 부분에 하위 속성으로 category를 추가합니다.
             이를 통해 category 명을 가져 올 수 있고, site.categories를 통해 해당 카테고리의 포스트 갯수를 가져올 수 있습니다.
          {% endcomment %}
          {% assign post_cnt = 0 %}
          {% for category in site.categories %}
            {% if category[0] == child.category  %}
                {% assign post_cnt = category[1].size %}
            {% endif %}
          {% endfor %}

            <li><a href="{{ child.url | relative_url }}"{% if child.url == page.url %} class="active"{% endif %}>{{ child.title }}({{ post_cnt }})</a></li>
          {% endfor %}
        </ul>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</nav>
```



## 3. 상단 드롭다운 메뉴 설정 : _data/navigation.yml 파일에서 카테고리 정의+ _pages/main 폴더 내 카테고리별 페이지 생성 + (필요 시) 레이아웃 추가



①_data/navigation.yml 파일에서 카테고리 정의



- 저는 상단에 연도별/태그별 글을 모아보는 메뉴와 소개글 페이지로 넘어가는 메뉴를 넣으려 합니다.
- navigation.yml 파일에서 카테고리별 url을 정의합니다: 연도별/태그별/소개의 3개 목록 분류
```
main:
  - title: "Quick-Start Guide"
    url: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/

main:
  - title: "연도별"
    url: /annual-archive/
```



②_pages/main 폴더 내 연도별/태그별 글로 가는 url 페이지 생성 (.md)



```
---
title: "연도별 글" 
layout: posts                   #_layouts 폴더에 있는 기본 레이아웃
permalink: /annual-archive
author_profile: true
---
```



```
---
title: "태그별 글" 
layout: tags                   #_layouts 폴더에 있는 기본 레이아웃
permalink: /tag-archive
author_profile: true
---
```



③_pages/main 폴더 내 소개글 페이지 생성 (.md)



```
---
title: "안녕하세요! 모조(Mojo)입니다"
layout: single
permalink: /about
author_profile: true
---

<div>
    <img src="/assets/이미지.jpg" alt="about_me" width="70%" min-width="700px" itemprop="image">
</div>

<body>
    <font size="3" face="굴림체">
    <p>소개글~~
    </p>

<div style="border-left: 2px solid rgba(199, 198, 198, 0.7); margin: 0.5em 0 0 0.5em; padding-left: 1.5em; font-weight: 500;">
    <ul class="author__urls social-icons">
        <li itemprop="homeLocation" itemscope itemtype="https://schema.org/Place">
          <i class="fas fa-fw fa-map-marker-alt" aria-hidden="true"></i> <span itemprop="name">  서울, 대한민국</span>
        </li>
        <li>
          <a href="https://www.instagram.com/131011k/" itemprop="sameAs" rel="nofollow noopener noreferrer">
            <i class="fab fa-fw fa-instagram" aria-hidden="true"></i><span class="label">  인스타그램 </span>
          </a>
        </li>
        
<!—숨김 처리       
        
        <li>
          <a href="깃허브 주소" itemprop="sameAs" rel="nofollow noopener noreferrer">
            <i class="fab fa-fw fa-github" aria-hidden="true"></i><span class="label">  Github</span>
          </a>
        </li>
        <li>
          <a href="mailto:메일 주소">
            <meta itemprop="email" content="메일 주소" />
            <i class="fas fa-fw fa-envelope-square" aria-hidden="true"></i><span class="label">  Email</span>
          </a>
        </li>
-->
    </ul>
</div>
```



## 4. 블로그 내 검색 기능 구현
- minimal mistakes에서 제공한 lunr source 사용하면 검색 기능을 구현할 수 있습니다.
- _config.yml 파일을 아래와 같이 수정하면 됩니다.
```
search                   : true # true, false (default)
search_full_content      : true # true, false (default)
search_provider          : "lunr" # lunr (default), algolia, google
lunr:
search_within_pages    : false # true, false (default)
```



## 5. 게시글 작성 : _posts폴더에서 markdown 형식으로 글 작성
- 로컬 폴더에 _posts 경로 생성 
- _posts 폴더 내 yyyy-mm-dd-title.md 파일 생성
- markdown 형태의 머리말 작성
```
---
layout: posts      # 보통 _layout폴더의 single과 posts 중 하나 선택
title: "Github 기본 도메인 만들기"

categories: github   # _pages 폴더의 카테고리별 .md파일 참조
tags: [github블로그]

excerpt: "기본 페이지 만들기"   # 미리보기 텍스트

post-order: 2       # 카테고리 내 포스트 순서

toc: true         # table of contents. 우측 상단의 목차
toc_sticky: true   # toc 고정(true) 시 스크롤에도 우측 상단 고정
toc_label: "목차"  # toc 제목

date: 2025-06-25
last-modified-at: 2025-06-25
---
```
- markdown 형태의 본문 작성
로컬 폴더 변경사항을 브라우저에서 확인
Github에 로컬 폴더 변경 사항 반영

<hr/>
<hr/>

## 참조 
- [왕초보를 위한 Github 블로그 만들기 (1)](https://zeddios.tistory.com/1222)
- [[Github 블로그] Minimal-Mistakes 테마의 디렉터리 구조 - 평생 공부 블로그](Today I Learned 🌙 : https://ansohxxn.github.io/blog/jekyll-directory-structure/)
- [깃허브 블로그 카테고리 만들기 초간단 방법 (minimal mistakes) | Yogurt Office] (https://tes-b.github.io/etc/minimal_mistakes_categories/)
- [minimal-mistakes sidebar 에 카테고리 추가 작업 - Sunghwan’s blog] (https://sunghwan7330.github.io/blog/blog_sidebar/)
- [[Git Page Jekyll Blog] - [13] Minimal-Mistakes 왼쪽 사이드바 만들기 - ExtraBrain] (https://seungwubaek.github.io/blog/left_sidebar/)
- [Github 블로그 검색 기능 만들기 (minimal mistake) - Yang`s Blog] (https://yangchanghee2251.github.io/jekyll/search/)


  