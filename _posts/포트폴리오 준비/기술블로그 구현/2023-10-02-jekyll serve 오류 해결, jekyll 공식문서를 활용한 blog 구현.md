# 231002

## 목차

- jekyll serve 오류 해결
- 1. setup, 2. liquid, 3. front matter : jekyll 기초
- 4. layouts : _layout 경로에 .md/.html을 렌더하기 위한 레이아웃 생성
- 5. includes : navigation 추가하기
- 6. data files : _data 경로의 데이터 로딩하여 페이지 구성하기
- 7. assets : css, js, image 로드
- 8. blogging : _posts 경로로 .md 파일 렌더
- 9. collections : series별, category별로 별도 페이지 만들기 (미완료)
- 10. deployment : jekyll 빌드해서 배포

## jekyll serve 오류 해결

<img width="577" alt="스크린샷 2023-10-02 오후 4 16 15" src="https://user-images.githubusercontent.com/138586629/271905325-4b015f19-ac4c-42b6-8097-244d10370f1d.png">

갑자기 요상한 에러가 뜨면서 jekyll serve가 안되더라

```
/opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/runtime.rb:304:in `check_for_activated_spec!': You have already activated rexml 3.2.6, but your Gemfile requires rexml 3.2.5. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/runtime.rb:25:in `block in setup'
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/spec_set.rb:165:in `each'
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/spec_set.rb:165:in `each'
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/runtime.rb:24:in `map'
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler/runtime.rb:24:in `setup'
        from /opt/homebrew/lib/ruby/site_ruby/3.2.0/bundler.rb:162:in `setup'
        from /opt/homebrew/lib/ruby/gems/3.2.0/gems/jekyll-4.3.2/lib/jekyll/plugin_manager.rb:52:in `require_from_bundler'
        from /opt/homebrew/lib/ruby/gems/3.2.0/gems/jekyll-4.3.2/exe/jekyll:11:in `<top (required)>'
        from /opt/homebrew/lib/ruby/gems/3.2.0/bin/jekyll:25:in `load'
        from /opt/homebrew/lib/ruby/gems/3.2.0/bin/jekyll:25:in `<main>'
```

학습메모 1을 참고하여 해결했다. 
구구절절한 설명이 많은데 결국 sudo bundle update로 바로 오류가 해결되었다. 

```bash
sudo bundle update
```

<img width="570" alt="스크린샷 2023-10-02 오후 4 17 48" src="https://user-images.githubusercontent.com/138586629/271905581-7727f401-a705-4c17-a48f-e593486937e7.png">

## 1. setup, 2. liquid, 3. front matter : jekyll 기초

jekyll tutorial step 1, 2, 3은 정말 기본적인 내용이므로 쭉 따라해보시면 되겠다! 

### 1. setup

```bash
gem install jekyll bundler
bundle init
bundle add jekyll
bundle
```

프로젝트 폴더에 jekyll이랑 bundler 설치하고, bundle init으로 gemfile 만들고, 
bundle add jekyll로 jekyll 의존성 추가해서 bundle로 jekyll (프로젝트에) 설치한단 뜻. 

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

웰컴 페이지 만들고 `jekyll serve`로 돌리면 `http://localhost:4000`로 접근가능한 웹서버 열린다.

- `jekyll build` : 빌드하여 _site 경로에 배포파일 떨궈줌
- `jekyll serve` : `jekyll build` 수행 후 `http://localhost:4000`에 로컬웹서버 구동!

### 2. liquid

liquid는 templating language로, 자바스프링의 thymeleaf, express의 ejs같은 템플릿 엔진 생각하면 됨. 

- object : 변수 출력. {{ page.title }} 하면 page.title 변수 내용으로 변환됨.
- tags : if/endif, for 같은 흐름제어문 사용 가능 {% if ~~ %} ㅇㅇ {% endif %} 하면 조건부로 ㅇㅇ.
- filters : [liquid filters](https://jekyllrb.com/docs/liquid/filters/)로 변환된 아웃풋을 반환함. | 구분자 사용해서 {{ "hi" | capitalize }} 하면 HI.

### 3. front matter

파일 최상단에 YAML로 값을 등록해놓으면, 내외부에서 접근할 수 있는 변수가 됨. 

```yaml
---
my_number: 5
---
```

이러면 

```html
{{ page.my_number }}
```

요런식으로 접근 가능하단 말씀. 앞으로 계속 활용할 예정. 

---

## 4. layouts : _layout 경로에 .md/.html을 렌더하기 위한 레이아웃 생성

```html
<!-- _layouts/default.html -->
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```

`_layouts/default.html`에 위와 같이 파일을 추가해주면, 이제 front matter를 통해 
.md이나 .html 파일 렌더 시 자동으로 저렇게 템플레이팅을 해주는거다 이말씀. 

```html
---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>
```

html이면 이런식으로

```md
---
layout: default
title: About
---
# About page

This page tells you a little bit about me.
```

마크다운이면 이런식으로! 

<img width="848" alt="스크린샷 2023-10-03 오전 2 00 19" src="https://user-images.githubusercontent.com/138586629/272036130-c3bc6a65-8e56-4dda-aa03-dc8ce13b1cda.png">


<img width="356" alt="스크린샷 2023-10-03 오전 1 59 13" src="https://user-images.githubusercontent.com/138586629/272035857-066c25d0-4b38-4cfa-8385-6f751bd8d287.png">

그러면 이렇게 잘 보인다.


## 5. includes : navigation 추가하기

root폴더에 _includes 디렉토리를 만들어주고, 
`_includes/navigation.html`을 작성한다.

```html
<!-- _includes/navigation.html -->
<nav>
    <a href="/">Home</a>
    <a href="/about.html">About</a>
  </nav>
```

이후 default.html에 navigation.html을 "include"해준다. (liquid 템플릿 엔진의 기능인걸로)

```html
<!-- _layouts/default.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }}</title>
</head>
<body>
    {% include navigation.html %}
    {{ content }}
</body>
</html>
```

https://user-images.githubusercontent.com/138586629/271906095-5586a602-14ab-4f03-86e0-ffbdade7244d.mov

상단에 nav바가 잘 보이고, 링크도 잘 작동한다.

---

현재 페이지를 하이라이팅해보자. 
Jekyll에서 제공하는 `page.url`이라는 변수를 활용하면 현재 상대경로를 확인할 수 있다.

```html
<!-- _includes/navigation.html -->
<nav>
    <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>
      Home
    </a>
    <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>
      About
    </a>
  </nav>
```

<img width="591" alt="스크린샷 2023-10-02 오후 4 26 54" src="https://user-images.githubusercontent.com/138586629/271907276-3af44d83-1565-421a-bbd6-de7d5edf259e.png">

현재 페이지가 빨갛게 표시된다. CSS는 다음에 한번에 편집해보자~

## 6. data files : _data 경로의 데이터 로딩하여 페이지 구성하기

_data 폴더에 YAML, JSON, CSV 파일을 추가하면 데이터를 파일에서 불러와 활용할 수 있다. <br /><br />

YAML 파일을 활용해보자. _data 폴더를 만들고 `navigation.yml` 파일을 추가한다.

```yml
# _data/navigation.yml
- name: Home
  link: /
- name: About
  link: /about.html
```

불러올 때는 `site.data.navigation`과 같이 사용할 수 있다. 아래에 사용 예시. 

```html
<!-- _includes/navigation.html -->
<nav>
    {% for item in site.data.navigation %}
        <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
        {{ item.name }}
        </a>
    {% endfor %}
</nav>
```

for문을 돌아 item으로 받고, item.name, item.link 등으로 각 속성에 접근할 수 있는 것을 확인할 수 있다.

<img width="321" alt="스크린샷 2023-10-02 오후 4 48 47" src="https://user-images.githubusercontent.com/138586629/271911556-08f81d82-5aaf-4dd0-b889-91c97e624c95.png">


똑같이 잘 동작하는 거 보니 잘 되나보다 그쵸?

## 7. assets : css, js, image 로드

<img width="234" alt="스크린샷 2023-10-02 오후 5 32 00" src="https://user-images.githubusercontent.com/138586629/271920810-af205dd0-7892-4684-bff2-b4f98458e409.png">

위와 같이 root폴더 아래에 폴더를 만들어 상대경로로 정적 assets에 접근할 수 있다.

```css
/* assets/css/style.css */
@import "nav";
```

```css
/* assets/css/nav.css */
.current {
    color: green;
}
```

위와 같이 예시 css를 추가해주고, styles.css를 link태그로 default.html에 추가해보자.

```html
<!-- _layouts/default.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/style.css">
</head>
<body>
    {% include navigation.html %}
    {{ content }}
</body>
</html>
```

이제 현재 경로랑 같으면 style속성으로 글자색을 red로 변경하는 것에 더해, 현재 경로가 아니면 
`class="current"`로 설정해 글자가 초록색으로 바뀌는지 확인해보자.

```html
<!-- _includes/navigation.html -->
<a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% else %}class="current"{% endif %}>
```

https://user-images.githubusercontent.com/138586629/271926510-73e91e91-28d5-4733-a21d-15e7deda8659.mov

잘되고~

## 8. blogging : _posts 경로로 .md 파일 렌더

_posts 폴더 내에 .md 파일을 추가하면 블로그 포스트를 렌더하고 접근할 수 있다.

<img width="394" alt="스크린샷 2023-10-02 오후 6 01 18" src="https://user-images.githubusercontent.com/138586629/271927729-5dc045ca-2bc1-4663-875e-971eb2f5b911.png">

한글 테스트 겸 위와 같은 .md파일을 활용해보았다. <br /><br />

`YYYY-MM-DD-포스트 제목.md`형식이면 `page.date`, `page.title` 이런식으로 날짜와 제목에 접근할 수 있고, 
layout: post외에 `author: qkrwogk` 같은 항목은 커스텀으로 추가해서 `page.author`와 같이 접근할 수 있다. 
내용은 `content`. 간편하군! 

```html
<!-- _layouts/post.html -->
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```

layout: post에 대응하는 포스트 레이아웃을 만들어준다. 
위에서 말한 속성들을 모두 활용하여 접근해준다. 
(`date_to_string` 필터는 날짜를 예쁘게 표시해준대~)

---

이제 포스트를 리스트업해주는 코드를 작성! root에 blog.html을 작성해보자.

```html
<!-- /blog.html -->
---
layout: default
title: Blog
---
<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
```

- post.url : jekyll에 의해 자동으로 post의 경로를 얻을 수 있음
- post.title : post의 파일명으로부터 타이틀을 파싱해옴
- post.excerpt : content의 첫 번째 문단을 가져옴

`_data/navigation.yml`에도 Blog 탭을 추가하자고?

```yml
# _data/navigation.yml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
```

그리고~ 여러 포스트가 잘 리스트업 되는지 확인하기 위해 md파일 몇개를 더 추가해보자. 학습메모 3에서 가져옴

![스크린샷 2023-10-03 오전 1 04 34](https://user-images.githubusercontent.com/138586629/272023658-bdce73c8-d84a-4fe2-8697-edf21978dfa2.png)

`jekyll serve`! 두구두구

https://user-images.githubusercontent.com/138586629/272024094-f3ba2a85-107c-4480-b0f5-15bb878017ed.mov

얼마나 멋있냐 이말씀이야~

## 9. collections : series별, category별로 별도 페이지 만들기 (미완료)

튜토리얼엔 author로 분류하지만, 보통 만드는 개인 블로그에선 카테고리나 시리즈별로 분류하니까 그렇게 하겠음.

### 번외 (의외의 발견)

```md
---
layout: post
author: jill
series: 색 시리즈
category: 빨간색
---
REDREDRED
```

```md
---
layout: post
author: jill
series: 과일시리즈
category: 빨간색
---
An apple is a sweet, edible fruit produced by an apple tree.
```

```md
---
layout: post
author: jill
series: 과일시리즈
category: 노란색
---
BANANA
```

```md
---
layout: post
author: ted
series: 과일시리즈
category: 초록색
---
Kiwifruit (often abbreviated as kiwi), or Chinese gooseberry is the
```

```md
---
layout: post
author: qkrwogk
---

# 본인에 대해서 잘 설명할 수 있는 대표적인 프로젝트 경험
```

뭐 있는것도 있고 없는 것도 있고 이렇게 막 실험해보자. 

```yml
# /_config.yml
collections:
  series:
  categories:
```

collections 사용은 이렇게 root 폴더에 `/_config.yml`파일을 만들어서 요런식으로 추가해주면 됨. 
자동으로 page.series, page.categories 값들을 읽어서 분류해주나봄..?

![스크린샷 2023-10-03 오전 2 29 26](https://user-images.githubusercontent.com/138586629/272042147-df3f28a7-17c6-4b82-a640-cfad71473f0c.png)

`jekyll serve`로 다시 빌드해보면, 분류가 날짜가 아닌 색으로 먼저 분류되고, 이후에 날짜로 분류되는 것을 
확인할 수 있다! 두 개 이상의 collection은 안되고 가장 마지막것만 되는 것 같다..? <br /><br />

라고 생각했는데, 가만 보니 각 포스트에 `categories:`가 아닌 `category:`라고 적어서 저렇게 된거고, 
한마디로 **collections와는 아무 상관 없는 거였다** ㅎ 대박 <br /><br />

하여간 collections 없이 자동으로 폴더 분류를 하고싶다면 category 변수에 저렇게 값을 할당해주면 되는걸로. 
이제 다시 `categories:`로 바꾸고 진짜 collections를 해보자.

### collections 분류 결과 확인 (실패)

stepbystep 진행하다 author.url 링크가 걸리지 않아 끝내 실패! 
내일 다시 해보자. series 말고 author로 튜토리얼대로 진행해보고 실제 블로그 배포때 바꾸는 게 좋을듯. 

## 10. deployment : jekyll 빌드해서 배포

여태까지 만든 것들을 복습하자면, 기본적인 Jekyll 사이트는 다음과 같은 디렉터리 구조임.

<img width="704" alt="스크린샷 2023-10-03 오전 1 22 06" src="https://user-images.githubusercontent.com/138586629/272027611-0ff55c78-3867-48c6-8bb5-d714e195ee3c.png">

### Gemfile

이미 한 내용이지만, 복습 차원에서 다시 보자면, Gemfile은 종속성을 위한 파일이다. 
js의 package.json, python의 requirements.txt!

```bash
bundle init
bundle add jekyll
```

요거 하면 이런 Gemfile이 나옴

```gemfile
# Gemfile
# frozen_string_literal: true
source "https://rubygems.org"

gem "jekyll"
```

- `bundle install` 또는 `bundle` : 의존성대로 설치해서 Gemfile.lock이 나옴
- `bundle update` : 설치됨 gem들의 버전 업데이트

Gemfile이 있으면, `jekyll serve`같은 명령 앞에 prefix `bundle exec`를 자동으로 붙여줌. 
이때까지 쓰던 jekyll serve는 사실 `bundle exec jekyll serve`였던거임. 헉! 

### Plugins

jekyll 플러그인들이 있는데, 대표적인 3개를 사용해보자.

- `jekyll-sitemap` : 검색 엔진을 위한 사이트맵 만들어줌
- `jekyll-feed` : RSS feed 만들어줌
- `jekyll-seo-tag` : SEO를 위한 메타태그 붙여 줌

Gemfile에 요렇게 추가해주면 설치할 수 있단다.

```gemfile
# Gemfile
# frozen_string_literal: true

source "https://rubygems.org"

gem "jekyll"

group :jekyll_plugins do
    gem 'jekyll-sitemap'
    gem 'jekyll-feed'
    gem 'jekyll-seo-tag'
  end
```

그다음 `_config.yml`에 이거 추가

```yml
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
```

그다음 터미널에 bundle update!

```bash
sudo bundle update
```

![스크린샷 2023-10-03 오전 1 35 43](https://user-images.githubusercontent.com/138586629/272030593-f7f6197d-e205-4755-b3c5-2ffee15dcd82.png)

좋고요, feed랑 seo-tag 넣는 건 `_layouts/default.html`에 요렇게 두줄 추가해주면 된단다

```html
<!-- _layouts/default.html -->
<head>
    ...
    {% feed_meta %}
    {% seo %}
</head>
```

<img width="1430" alt="스크린샷 2023-10-03 오전 1 39 10" src="https://user-images.githubusercontent.com/138586629/272031494-1aeedf4c-a121-49b5-b5c8-870ad542693d.png">

head태그 안에 피드 경로랑 SEO tag 추가된거 보이시죠?

<img width="1500" alt="스크린샷 2023-10-03 오전 1 40 14" src="https://user-images.githubusercontent.com/138586629/272031704-49e784c6-46c6-470f-aa4d-44fd8539a17c.png">

RSS Feed는 요건가 봅니다~ 굳굳

### Environments & Deployment

이건 배포 단계에서 production으로 build하는 방법을 보여주는 건데요, 터미널에

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

이러면 된답니다. 결국 `bundle exec jekyll build` 하는데 환경변수를 default인 `development`가 아닌 
`production`으로 한단거겠죠 뭐 별거아님. 

![스크린샷 2023-10-03 오전 1 45 25](https://user-images.githubusercontent.com/138586629/272032871-af7c5d13-79cf-44a2-9121-45afce6e3a1d.png)

진짜 별거아님 이제 걍 `_site/` 통째로 프론트서버 올려라 이거임.

![스크린샷 2023-10-03 오전 1 47 23](https://user-images.githubusercontent.com/138586629/272033317-2701a9de-be84-4b9d-a10d-dd0963247ea5.png)

이렇게 이것저것 필요한거 잘 있는거죠 뭐. 이 production 단계에서만 무언가 스크립트를 실행하고 싶다? 
뭐 예를 들어 조회수 분석이라던가? 그러면 이렇게 조건문을 달 수도 있다네요 

```html
{% if jekyll.environment == "production" %}
  <script src="my-analytics-script.js"></script>
{% endif %}
```


## 학습메모

1. [bundle update로 오류 해결](https://haereeroo.tistory.com/12)
2. [liquid template language, if/else문](https://shopify.github.io/liquid/tags/control-flow/)
3. [jekyll step by step, 8. blogging](https://jekyllrb.com/docs/step-by-step/08-blogging/)
4. [liquid filters](https://jekyllrb.com/docs/liquid/filters/)