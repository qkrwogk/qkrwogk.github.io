# qkrwogk.github.io

`qkrwogk portfolio page` 입니다.

- 기술블로그 준비, Jekyll기반 블로그 구현 및 배포
- 카테고리 구성 및 요구사항 정립
- 카테고리별 블로그 포스트 작성 및 발행

## 카테고리 구성

### 코딩 테스트 준비

- 바킹독 알고리즘 강의 기반 기초 알고리즘/자료구조 정리 + 관련 BOJ 문제풀이 과정
- 프로그래머스 구현문제 풀이 과정 기록

### 포트폴리오 준비

- 멤버십 스프린트 기반 뮤직 라이센싱 프로젝트 (Java Spring)
- 멤버십 그룹프로젝트 (과정 기록 및 코드 첨부)
- 대학원 논문 기반 AI 포렌식 서비스 프로젝트
- 취약점 점검 웹 기반 자동화 프로젝트 (보안 + 웹구현)

### 기술면접 준비

- 챌린지 학습정리 기반 기본 CS지식 정리 (OS, 네트워크, 컴파일러)
- 대학원 석사, 보안전문가 7년 경력 증빙을 위한 보안/해킹 지식 정리
- 기본 프로필, 경력 기술서, 소개글 작성


---
---


# 230929

## 목차

- GitHub Pages repository 생성 및 테스트 
- macOS에서 Ruby 설치 및 에러 해결 과정

## GitHub Pages repository 생성 및 테스트 

markdown 파일을 활용할 수 있는 블로그를 검색해보다, 다음 정도의 방법으로 추려보았다. 

1. Tistory : CSS 편집 가능하지만 조금 불편함.  수익화는 가능.
2. Velog : 깔끔하지만 고정된 테마 사용. 수익화 불가.
3. Github Pages + Jekyll : 완전히 자유롭게 html/css를 구성할 수 있지만 Jekyll 사용법을 학습해야 하므로 시간이 많이 소요됨. 
4. 직접 markdown 파서 구현 : 마찬가지로 완전히 자유롭게 구성할 수 있지만 구현에 시간이 더 오래 걸림.

결국 gfm을 공식적으로 지원하는 github pages + jekyll을 활용하기로 했다. 추가적인 장점은 다음과 같다. 

- md 파일을 커밋하여 바로 게시가 가능. 
- 그러므로 vscode로 편집가능.
- 잔디 채울 수 있음 ㅎ

로컬에서 .md파일로 관리할 수 있다는 장점이 가장 컸다. 부캠 챌린지/멤버십 수행에서 익숙해진 작업방식으로 그대로 작성 가능! 

---

학습메모 1을 참고하여 qkrwogk.github.io 이름으로 repo를 만들어줬다.

<img width="1061" alt="스크린샷 2023-10-01 오전 12 57 45" src="https://user-images.githubusercontent.com/138586629/271782961-5238e166-040a-483f-b1d2-c3c32bc5feee.png">

<img width="1288" alt="스크린샷 2023-10-01 오전 1 12 26" src="https://user-images.githubusercontent.com/138586629/271783592-be00c481-26ad-456c-b3b9-d6e5465f3d6c.png">

`Settings - Pages`에서 live로 게시 중인 [https://qkrwogk.github.io](https://qkrwogk.github.io) 링크를 확인할 수 있고, README.md 내용이 화면에 잘 표시됨.


## macOS에서 Ruby 설치 및 에러 해결 과정

학습메모 2 Jekyll 공식문서의 getting started 항목을 쭉 따라가며 사용 및 적용 방법을 알아보자. <br /><br />

사실은 gh pages에서 직접 정적파일을 jekyll로 렌더해주는 형태이기 때문에 로컬에서 빌드하거나 실행할 필요가 없는거더라.. 하지만 정상 동작 및 에러 추적을 위해서는 localhost에서 빌드와 배포를 테스트해볼 필요가 있다고 판단되어 한번 깔아보기로 했다. 

<img width="712" alt="스크린샷 2023-10-01 오전 1 21 51" src="https://user-images.githubusercontent.com/138586629/271784006-b77cc9d7-4870-4ce8-81f5-992c7dd44231.png">

<img width="564" alt="스크린샷 2023-10-01 오전 1 24 38" src="https://user-images.githubusercontent.com/138586629/271784145-bb0cb376-695c-432b-991f-7aa0ba4a5031.png">

requirements대로 확인해보니, macOS 기준으로 /usr/bin/ruby에 이미 루비가 설치되어 있고 ruby 2.6.10이라 별 이상이 없긴 했다. 

<img width="836" alt="스크린샷 2023-10-01 오전 1 27 03" src="https://user-images.githubusercontent.com/138586629/271784235-0859ed30-858b-46a5-a3e8-1edf5244a2d8.png">

근데 [installation guide for mac os](https://jekyllrb.com/docs/installation/macos/)에서 3.1.3 기준으로 설치하라고 해서... 이때부터 모든 것이 꼬이기 시작함 ㅎ

---

<img width="566" alt="스크린샷 2023-10-01 오전 1 32 35" src="https://user-images.githubusercontent.com/138586629/271784502-091c750e-0943-43d6-b82f-e2445e92be9f.png">

정말 이상한 에러가 뜬다. 

```
compiling ossl_ts.c
In file included from ossl_ts.c:10:
In file included from ./ossl.h:171:
./openssl_missing.h:195:11: warning: 'TS_VERIFY_CTS_set_certs' macro redefined [-Wmacro-redefined]
#  define TS_VERIFY_CTS_set_certs(ctx, crts) ((ctx)->certs=(crts))
          ^
/opt/homebrew/Cellar/openssl@3/3.1.2/include/openssl/ts.h:426:11: note: previous definition is here
#  define TS_VERIFY_CTS_set_certs(ctx, cert) TS_VERIFY_CTX_set_certs(ctx,cert)
          ^
ossl_ts.c:829:5: error: incomplete definition of type 'struct TS_verify_ctx'
    TS_VERIFY_CTX_set_certs(ctx, x509inter);
    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./openssl_missing.h:215:46: note: expanded from macro 'TS_VERIFY_CTX_set_certs'
#  define TS_VERIFY_CTX_set_certs(ctx, crts) TS_VERIFY_CTS_set_certs(ctx, crts)
                                             ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./openssl_missing.h:195:52: note: expanded from macro 'TS_VERIFY_CTS_set_certs'
#  define TS_VERIFY_CTS_set_certs(ctx, crts) ((ctx)->certs=(crts))
                                              ~~~~~^
/opt/homebrew/Cellar/openssl@3/3.1.2/include/openssl/ts.h:407:16: note: forward declaration of 'struct TS_verify_ctx'
typedef struct TS_verify_ctx TS_VERIFY_CTX;
               ^
1 warning and 1 error generated.
make[2]: *** [ossl_ts.o] Error 1
make[1]: *** [ext/openssl/all] Error 2
make: *** [build-ext] Error 2
!!! Compiling ruby 3.1.3 failed!
```

openssl 문제라고 해서 openssl에러를 찾아보기도 하다가~ <br /><br />
[ruby 설치 다양한 방법](https://www.ruby-lang.org/ko/documentation/installation/#homebrew)들을 뒤져보며 rbenv로도 해보고, rvm으로도 해보고~ <br /><br />

학습메모 4와 똑같은 문제여서 이렇게 해봐도 안되고~ 저렇게 해봐도 안되고~ 한참을 뒤져보다 내일로..

## 학습메모

1. [github pages 사이트 만들기 공식문서](https://docs.github.com/ko/enterprise-server@3.7/pages/getting-started-with-github-pages/creating-a-github-pages-site)
2. [jekyll docs](https://jekyllrb.com/docs/)
3. [markdown guide github pages 소개](https://www.markdownguide.org/tools/github-pages/)
4. [macOS Apple Sillicon + brew에서 ruby 3.1.3 설치 안되는 문제](https://medium.com/@canerten/building-ruby-3-1-3-fails-with-openssl-1-0-2o-1-on-m1-apple-silicon-mac-with-brew-89d7e550420b)
5. [rbenv와 rvm](https://jayhooney.github.io/ruby/rvm-and-rbenv/)
6. [ruby 설치 다양한 방법](https://www.ruby-lang.org/ko/documentation/installation/#homebrew)

---
---


# 230930 

## 목차

- brew install ruby로 ruby 설치 (성공)
- jekyll 공식문서 활용하여 사용법 학습 및 GH Pages에 배포

## brew install ruby로 ruby 설치 (성공)

결국 brew로 직접 ruby 최신버전을 설치하는 것으로 해결했다. 

<img width="338" alt="스크린샷 2023-10-01 오전 1 39 52" src="https://user-images.githubusercontent.com/138586629/271784816-769dd6da-0bab-44cd-ba9b-7e308b126475.png">

3.2.2버전인 것이 찝찝해서 특정 버전으로 설치하는 방법도 찾아봤는데 

```bash
brew search ruby
```

<img width="564" alt="스크린샷 2023-10-01 오전 1 42 20" src="https://user-images.githubusercontent.com/138586629/271784934-6c2302f5-927e-4bf5-958a-1b72a69d7164.png">

대충 요런식으로 하면 됨 (학습메모 2)

<img width="566" alt="스크린샷 2023-10-01 오전 1 44 57" src="https://user-images.githubusercontent.com/138586629/271785050-e13481b9-edcc-4bcd-a967-5693e92d8ccd.png">


```bash
brew install ruby@3.1
```

이걸로 하니 3.1.3처럼 세분화된 버전까진 안되고 3.1 최신버전인 3.1.4로 설치됨. <br /><br />

이런거면 걍 최신버전 해서 되나 보기로 하고 `brew install ruby`로 설치 후에

```bash
open -e ~/.zshrc
```

학습메모 1에 나와있는대로 ruby 기본PATH 변경을 위해 반드시 해야하는 .zshrc편집! <br /><br />

참고로 terminal open명령은 개꿀이다. 반드시 기억하자

> `open [폴더명]` 하면 파인더가 뜨고 <br />
> `open -e [파일명]` 하면 텍스트 편집기! 


```bash
# ~/.zshrc 파일 편집
...

if [ -d "/opt/homebrew/opt/ruby/bin" ]; then
  export PATH=/opt/homebrew/opt/ruby/bin:$PATH
  export PATH=`gem environment gemdir`/bin:$PATH
fi
```

설명하자면 macOS는 기본적으로 /usr/bin/ruby가 설치돼 있어서 이걸 변경하거나 삭제하면 시스템에 영향이 갈 위험이 있고, 그래서 사용자가 따로 다른 버전을 사용하려면 지금처럼 brew같은걸로 새로 설치한 후에 쉘에서 환경변수 설정해서 `경로 우선순위`를 `homebrew 설치경로`로 바꿔줘야하는거다. 

<img width="569" alt="스크린샷 2023-10-01 오전 1 25 06" src="https://user-images.githubusercontent.com/138586629/271784165-d8cc3f8b-d81b-4165-8ed7-4a9c0ed08a57.png">

그래야 ruby가 `/usr/bin/ruby`가 아닌 `/opt/homebrew/opt/ruby/bin/ruby`가 되는거다. <br /><br />

완벽해 끝.


## jekyll 공식문서 활용하여 사용법 학습 및 GH Pages에 배포

이제 [jekyll 공식문서 Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)을 활용하여 Setup을 마무리하고, 블로그 구현을 쭉 해나가보자. 

```bash
sudo gem install jekyll bundler
bundle init
open -e ./Gemfile
```

<img width="566" alt="스크린샷 2023-10-01 오전 2 02 10" src="https://user-images.githubusercontent.com/138586629/271785791-3ca74ecc-6222-4867-99c4-410ac38dc955.png">

<img width="232" alt="스크린샷 2023-10-01 오전 2 03 01" src="https://user-images.githubusercontent.com/138586629/271785818-0a885b0e-630f-4ca9-afc0-b942a31108b5.png">

<img width="451" alt="스크린샷 2023-10-01 오전 2 04 07" src="https://user-images.githubusercontent.com/138586629/271785866-7e6543a2-dc53-450b-982d-aa37a0db0c08.png">

열어보면 3줄 있다. `gem "jekyll"` 추가해주고 

```bash
sudo bundle
```

<img width="568" alt="스크린샷 2023-10-01 오전 2 07 13" src="https://user-images.githubusercontent.com/138586629/271785980-9041fc9f-3b49-4a17-9dd8-2d6961f88116.png">

Gemfile.lock이 추가되더라. 
근데 이친구 그냥 `bundle`했을 때 퍼미션 에러 떠넣고 root로 실행하지 말라구 뭐라하네;; 어이없 

<img width="401" alt="스크린샷 2023-10-01 오전 2 13 24" src="https://user-images.githubusercontent.com/138586629/271786299-d239b52e-c825-46ee-b11a-a3411347df8e.png">

지킬 들어간 거 보이시죠? 

---

암튼 이제 대망의 첫 페이지인 Home 페이지(index.html)을 만들어 보 자!

```html
<!-- index.html -->
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

index.html을 루트 폴더에 저장하고 

```bash
jekyll serve
```

빌드만 하고싶으면 `jekyll build`하면 되는데 위 명령은 빌드 후 배포까지 해줌. `http://localhost:4000`에다 해줌.

<img width="305" alt="스크린샷 2023-10-01 오전 2 14 45" src="https://user-images.githubusercontent.com/138586629/271786367-e019aa3d-dfb5-4d93-8153-0ec2a82829ae.png">

너무 잘되고


## 학습메모

1. [macOS Sillicon, brew install ruby](https://mac.install.guide/ruby/13.html)
2. [brew로 특정 버전의 패키지 설치](https://www.44bits.io/ko/post/install-specific-version-package-homebrew)
3. [jekyll 공식문서 Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
4. [jekyll includes](https://jekyllrb.com/docs/step-by-step/05-includes/)


---
---


# 231001
## 목차

- main branch protection

## main branch protection

<img width="928" alt="스크린샷 2023-10-01 오전 2 34 06" src="https://user-images.githubusercontent.com/138586629/271787239-e7c9e0a6-0e7d-442e-bb83-7cf7beda65b1.png">

이런 경고가 뜨길래 아 그러고보니 main에 바로 push 못하게 막고 
지금처럼 PR(Pull Request)로만 merge 가능하게 설정해놔야겠다 싶었다. 

<img width="1172" alt="스크린샷 2023-10-01 오전 2 32 36" src="https://user-images.githubusercontent.com/138586629/271787170-4e81a37b-07b4-476f-bb9d-53eb83935123.png">

기본 권장인 위 `Require a pull request before merging` 옵션만 주고 저장. 이제 조금은 안전해졌달까! 

## 학습메모



---
---


# 231002

## 목차

- jekyll serve 오류 해결
- 1. setup, 2. liquid, 3. front matter : jekyll 기초
- 4. layouts : _layout 경로에 .md/.html을 렌더하기 위한 레이아웃 생성
- 5. includes : navigation 추가하기
- 6. data files : _data 경로의 데이터 로딩하여 페이지 구성하기
- 7. assets : css, js, image 로드
- 8. blogging : _posts 경로로 .md 파일 렌더
- 9. collections : series별, category별로 별도 페이지 만들기
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

## 9. collections : series별, category별로 별도 페이지 만들기

튜토리얼엔 

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

---
---


# 231003
## 목차
## 학습메모
