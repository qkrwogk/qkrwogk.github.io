# qkrwogk.github.io

`qkrwogk portfolio page` 입니다.

- 기술블로그 준비, Jekyll기반 블로그 구현 및 배포
- 카테고리 구성 및 요구사항 정립
- 카테고리별 블로그 포스트 작성 및 발행

## 카테고리 구성

### 코딩테스트 준비

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

---
---


# 231003

## 목차

- 9. collections : author별로 포스트 묶기
- topics별로 분류하여 post 자동 관리하기

## 9. collections : author별로 포스트 묶기

차근차근 다시 진행해보자.

```yml
# /_config.yml
collections:
  authors:
```

```md
<!-- _authors/jill.md -->
---
short_name: jill
name: Jill Smith
position: Chief Editor
---
Jill is an avid fruit grower based in the south of France.
```

```md
<!-- _authors/ted.md -->
---
short_name: ted
name: Ted Doe
position: Writer
---
Ted has been eating fruit since he was baby.
```

```html
<!-- /staff.html -->
---
layout: default
title: Staff
---
<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2>{{ author.name }}</h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```

```yml
# _data/navigation.yml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
- name: Staff
  link: /staff.html
```

<img width="530" alt="스크린샷 2023-10-03 오전 11 53 25" src="https://user-images.githubusercontent.com/138586629/272134612-ae16b7b4-28f2-4a29-9f2d-a7fce12f796a.png">

Staff 페이지 잘 출력됨

---

`collections`는 default로 page를 전달하지 않는 것으로 설정되어 있어서, 이를 커스텀하려면 

```yml
# /_config.yml
collections:
  authors:
    output: true
```

`output: true`를 추가해주면 된다고 한다. 그러면 `author.url`로 접근할 수 있다는데!

```html
<!-- /staff.html -->
---
layout: default
title: Staff
---
<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2><a href="{{ author.url }}">{{ author.name }}</a></h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```

a 태그로 링크 달아줌. 

<img width="476" alt="스크린샷 2023-10-03 오전 11 56 41" src="https://user-images.githubusercontent.com/138586629/272135068-dcd18882-68c6-4e92-8afc-f9735c268560.png">

링크 생겼고~

<img width="497" alt="스크린샷 2023-10-03 오전 11 57 07" src="https://user-images.githubusercontent.com/138586629/272135151-93a1bfc8-45d5-4c9c-a740-dc797b68b10f.png">

클릭하면 각 author별 페이지로 잘 들어가지고~~ 어제는 왜 안됐던거야 ㅋ

---

author 페이지의 레이아웃도 편집해보자. 

```md
---
layout: author
short_name: qkrwogk
name: Jaeha Park
position: Hacker Programmer
---
# Jaeha Park is a genius.
```

`layout: author` 추가 후에

```html
<!-- _layouts/author.html -->
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}
```

`_layouts/author.html` 작성

<img width="471" alt="스크린샷 2023-10-03 오전 11 59 40" src="https://user-images.githubusercontent.com/138586629/272135536-38bf3ad5-3fb9-4487-aef6-1b20dffa2f0b.png">

잘 됨

![스크린샷 2023-10-03 오후 12 11 36](https://user-images.githubusercontent.com/138586629/272137063-ca757baa-7c00-4aef-8509-0bd7349b0f1b.png)


참고로 build 결과인 _site에서 이렇게 별도 폴더에 보관된다.

### Front matter defaults

여기서는 `_config.yml` 설정을 통해 post면 post 레이아웃, author면 author 레이아웃, 둘 다 아니면 
default 레이아웃 이런식으로 디폴트 레이아웃 설정을 하는 법에 대해서 배운다. 이런건 빨리좀 가르쳐줘 

```yml
# /_config.yml
collections:
  authors:
    output: true

defaults:
  - scope:
      path: ""
      type: "authors"
    values:
      layout: "author"
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  - scope:
      path: ""
    values:
      layout: "default"
```

대충 scope->type이 `authors`면 value->layout으로 `author`를 deafult로 설정하라!는 뜻. 

<img width="498" alt="스크린샷 2023-10-03 오후 3 01 01" src="https://user-images.githubusercontent.com/138586629/272160584-2f804f2d-e9dd-4cc0-9d24-696f5d108bd7.png">

이제 `layout: "post"`를 설정하지 않은 다른 author page도 레이아웃이 적용되어 보여진다. 성공!

### List author's posts

`_layouts/author.html`을 다시 한 번 편집해보자. 

```html
<!-- _layouts/author.html -->
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}

<h2>Posts</h2>
<ul>
  {% assign filtered_posts = site.posts | where: 'author', page.short_name %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```

where절로 author 이름이 같은 posts를 필터해서, 해당 author의 post를 리스팅해준다! 

<img width="450" alt="스크린샷 2023-10-03 오후 12 08 52" src="https://user-images.githubusercontent.com/138586629/272136685-bf0381cf-0383-4752-846e-eec6275d6498.png">

너무 멋지다! 드디어 조금씩 블로그스러운 기능들이..! 

### Link to authors page

각 포스트에서도 author page에 접근할 수 있도록 링크를 걸어 보자.

```html
<!-- _layouts/post.html -->
---
layout: default
---
<h1>{{ page.title }}</h1>

<p>
  {{ page.date | date_to_string }}
  {% assign author = site.authors | where: 'short_name', page.author | first %}
  {% if author %}
    - <a href="{{ author.url }}">{{ author.name }}</a>
  {% endif %}
</p>

{{ content }}
```

<img width="936" alt="스크린샷 2023-10-03 오후 3 01 17" src="https://user-images.githubusercontent.com/138586629/272160635-2016aa94-c924-47c3-bcb3-58fbd306c98e.png">

post page에 활성화된 author 버튼. 클릭하면

<img width="920" alt="스크린샷 2023-10-03 오후 3 01 26" src="https://user-images.githubusercontent.com/138586629/272160666-c0f18ed3-e19a-4204-9516-20922aa0003f.png">

author page로! 이제 다 된다 요호호


## topics별로 분류된 post 관리

### Directory Nesting 테스트

_posts 폴더 안에 포스팅을 다 넣고 필요한 것만 분류하고 싶었는데, 
학습메모 2, 3 참고하여 확인해보니 결국 front matter로 분류를 해놓고 collection을 
쓰는거지 폴더 내에 넣는 건 안되나보다 관련없는 얘기였음. <br /><br />

그래도 어느 정도 유용한 것은 collections 방식으로 topics를 만들고(_topics/), 
topic별 게시물은 _posts가 아니라 다른 폴더(_lectures/)에 넣어둔다던가 
그런건 가능하겠더라. 음... 좀 더 고민해볼 필요가 있겠어.

---

찾았다! 학습메모 4!

<img width="683" alt="스크린샷 2023-10-03 오후 3 31 56" src="https://user-images.githubusercontent.com/138586629/272166821-befd5fd6-0025-4bbe-9f2b-9271e9301576.png">

결론은 _posts에 폴더를 만들어서 .md 넣어도 알아서 모두 posts로 조회가 되며, 
이를 조건문에서 판별하고 싶다면 `a.path contains '폴더명'`과 같이 판별해주면 됨. 

<img width="232" alt="스크린샷 2023-10-03 오후 3 33 37" src="https://user-images.githubusercontent.com/138586629/272167175-281f06dd-6d46-4e85-846a-527437b454c4.png">

해보자. 파일 넣어두고

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
    {% if post.path contains 'tests' %}
        <h1>hey</h1>
    {% endif %}
  {% endfor %}
</ul>
```

`/blog.html`에서 tests가 경로에 포함된 post면 hey! 한번 날려주자.

```html
<!-- /test.html -->
---
layout: default
title: Tests
---
<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    {% if post.path contains 'tests' %}
      <li>
        <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
        {{ post.excerpt }}
      </li>
    {% endif %}
  {% endfor %}
</ul>
```

추가로 `/test.html`을 만들어 tests에 있는 친구들만 보여주는 페이지를 따로 만들어주자. 

```yml
# /_data/navigation.yml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
- name: Staff
  link: /staff.html
- name: Test
  link: /test.html
```

nav에도 추가시켜 주면~ 

<img width="807" alt="스크린샷 2023-10-03 오후 3 42 04" src="https://user-images.githubusercontent.com/138586629/272168854-8ec546ab-53ce-4911-85da-acab81d003db.png">

hey 잘 보이고!

<img width="387" alt="스크린샷 2023-10-03 오후 3 43 09" src="https://user-images.githubusercontent.com/138586629/272169051-0e1a34e4-0550-4392-be2b-b98bdcee9ca2.png">

Test 페이지에서도 잘 걸러져 나온다! 굳 


### 계획된 카테고리 구성대로 Topics에 리스팅

이제 미리 구성해 둔 카테고리 구성대로 폴더를 배치하고 파일 몇 개를 테스트로 넣어보자.

<img width="223" alt="스크린샷 2023-10-03 오후 5 22 50" src="https://user-images.githubusercontent.com/138586629/272194405-f4740981-ed36-465e-ba64-6868fc4902ab.png">

학습메모 5를 참고하여, Topic과 하위 Subtopic 정보를 데이터파일로 만들어줬다. 앞으로 추가/제거할때도 폴더랑 일치하게 해당 파일만 편집해주면 되겠다. 

```json
// /_data/topics.json
[
  {
    "name": "기술면접 준비",
    "subtopics": [
      {
        "name": "정보보안"
      },
      {
        "name": "프로필"
      },
      {
        "name": "CS 기본지식"
      }
    ]
  },
  {
    "name": "코딩테스트 준비",
    "subtopics": [
      {
        "name": "문제풀이"
      },
      {
        "name": "자료구조와 알고리즘"
      }
    ]
  },
  {
    "name": "포트폴리오 준비",
    "subtopics": [
      {
        "name": "문제풀이"
      },
      {
        "name": "기술블로그 구현"
      }
    ]
  }
]
```

yml 대신 json으로 한 번 해봤다. 이제 이 데이터를 활용해서 path에 해당 문자열이 포함되면 리스팅하도록 topic.html을 작성해보자. 
`/topic.html`이 핵심!

```html
<!-- /topic.html -->
---
layout: default
title: Topics
---
<h1>Topics</h1>

<div>
  {% for topic in site.data.topics %}
    <h2>{{ topic.name }}</h2>
    <ul>
      {% for post in site.posts %}
        {% if post.path contains topic.name %}
          <li>
            <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
            {{ post.excerpt }}
          </li>
        {% endif %}
      {% endfor %}
    </ul>
    <br /><br />
  {% endfor %}
</div>
```

마지막으로 navigation에도 Test대신 Topic을 넣어준다. 

```yml
# /_data/navigation.yml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
- name: Staff
  link: /staff.html
- name: Topics
  link: /topic.html
```

이제 실행해보자!

<img width="482" alt="스크린샷 2023-10-03 오후 5 16 19" src="https://user-images.githubusercontent.com/138586629/272192710-42390a6b-1d64-4f3d-b116-ed3aba81b374.png">

리스트 잘 출력되고

<img width="468" alt="스크린샷 2023-10-03 오후 5 33 57" src="https://user-images.githubusercontent.com/138586629/272197863-92c394f1-f184-4425-b587-573adccec4cd.png">

링크도 잘 들어가진다! 굳!

### 앞으로 더 발전시킬 포인트

- class 속성 넣고 CSS 편집
- Topic별 페이지 만들어서 백링크까지 만들기


## 학습메모

1. [jekyll step by step, 9. collections](https://jekyllrb.com/docs/step-by-step/09-collections/)
2. [nested collection 가능한가?](https://stackoverflow.com/questions/37277738/can-i-create-nested-collections-in-jekyll)
3. [nested collection 예제](https://github.com/paddycarver/jekyll-nested-collections-example/blob/master/_config.yml)
4. [nested directory 속 post 불러오는 법](https://stackoverflow.com/questions/15279147/how-does-jekyll-treat-posts-in-posts-subdir)
5. [jekyll datafile](https://jekyllrb.com/docs/datafiles/)


---
---


# 231004

## 목차

- class 속성 넣고 CSS 만들기

## class 속성 넣고 CSS 만들기

비주얼이 도저히 못봐주겠어서 (왼쪽에 붙어있으니 잘 읽히지도 않더라) 레이아웃부터 바꿔줬다.

```html
<!-- default.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/default.css">
    {% feed_meta %}
    {% seo %}
</head>
<body>
    <nav class="nav">
        {% include navigation.html %}
    </nav>
    <div class="content">
        {{ content }}
    </div>
</body>
</html>
```

`default.html`은 크게 nav, content로 나뉘며 각각 default.css에서 위치를 absolute로 잡아줌. 

```css
/* default.css */
@import "navigation.css";
@import "topic.css";

.nav {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    gap: 1rem;
    box-sizing: border-box;

    width: 90vw;
    height: 2rem;

    position: absolute;
    left: 50%;
    top: 1rem;
    transform: translate(-50%, 0%);

    border: 1px solid black;
}

.content {
    width: 90vw;

    padding: 2rem 3rem;
    box-sizing: border-box;

    position: absolute;
    left: 50%;
    top: 5rem;
    transform: translate(-50%, 0%);

    border: 1px solid black;
}
```

navigation과 topic(+blog)탭에 대한 css는 별도의 파일로 관리해줬다. 

```css
/* navigation.css */
.nav {
    & .menu {
        width: 10vw;
        height: 1rem;

        background: rgb(180, 221, 192);

        & a {
            width: 100%;

            font-size: 1.25rem;
            font-weight: 700;
        }
    }
    & .current {
        color: green;
    }
}
```

가독성을 좋게 하고 싶어서 학습메모 2를 참고하여 `css nesting`을 적극 활용해봄! 
이전엔 `.nav .menu a`이런식으로 매번 타고들어가줬는데 nesting을 하니 확실히 div 포함관계가 명확하다. <br /><br />

일전에 개발하는 동료가 nesting이 유지보수나 재사용성이 힘들다고 했는데, 나는 반대다. 
경험해보니 재사용 가능한 건 따로 빼두면 되는 것이고, 위와 같이 골격을 만들어주는 코드는 nesting이 나음. 
<br /><br />

button style이나 input style처럼 서버 전체에서 통일할 부분은 nesting 없이 
별도의 파일로 import 해서 해결해주면 된다. 

```css
/* topic.css */
.topic {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    box-sizing: border-box;

    & .topic-container {
        border-top: 0.031rem solid black;
    }

    & .topic-name {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    & ul {
        display: flex;
        flex-direction: column;
        align-items: center;

        width: 100%;
        
        list-style-type: none;
        margin-block-start: 0;
        margin-block-end: 0;
        margin-inline-start: 0;
        margin-inline-end: 0;
        padding-inline-start: 0;

        & li {
            display: flex;
            flex-direction: column;
            gap: 0px;
            box-sizing: border-box;

            width: 70vw;

            & .post-head {
                display: flex;
                flex-direction: row;
                justify-content: space-between;
                padding: 0.2rem 1rem;
                gap: 2rem;
                box-sizing: border-box;

                height: 2rem;
                background: lightgray;

                & .title {
                    font-weight: 500;
                    font-size: 1.5rem;
                    & a {
                        color: black;
                        text-decoration: none;

                        width: 100%;
                    }
                }
                & .date {
                    font-weight: 200;
                    font-size: 0.75rem;
                    line-height: 2.25rem;
                }

            }
            & .preview {
                display: flex;
                flex-direction: row;
                justify-content: flex-start;
                padding: 1rem;
                box-sizing: border-box;

                & *  {
                    font-weight: 200;
                    font-size: 1rem;
                }

                border: 0.031rem solid lightgray;
            }
        }
    }
}
```

마지막 `topic.css`. 포인트 3개 잡고 간다. 

1. 고칠 게 많아도 `px`가 아닌 `rem, %, vw` 등 상대적인 단위를 많이 사용하도록 노력했다. 
이렇게 해야 모바일 등 다른 환경에서 적절한 크기로 보여주기 용이하다고 함. 
2. 반응형도 고려하여 이전에 고정 width를 했던 것과는 달리, %, vw로 width를 설정해주고 gap 대신 
flex의 `space-between` 속성 등을 이용하도록 노력했다. 폭이 달라져도 예쁘게 보임
3. 화면 가운데 위치하기 위해 직접 `calc`로 계산하는 것이 아닌 `left: 50%`, 
`transform: translate(-50%, 0)`을 활용했다. 화면 크기나 기타 환경에 영향받지 않고 깔끔하게 가운데 정렬. 

---

<img width="1507" alt="스크린샷 2023-10-04 오후 11 34 16" src="https://user-images.githubusercontent.com/138586629/272612218-8a73a19e-f2c0-4878-add2-f2622af46191.png">

<img width="1512" alt="스크린샷 2023-10-04 오후 11 34 54" src="https://user-images.githubusercontent.com/138586629/272612328-b97730c0-fceb-44a0-bdf4-814d9e4fce3a.png">

훨씬 낫다! 

<img width="608" alt="스크린샷 2023-10-04 오후 11 49 49" src="https://user-images.githubusercontent.com/138586629/272616826-f8c754b0-94c3-484e-8117-0e74da5897f3.png">

화면 크기가 줄어들어도 예쁘게 배치됨을 확인할 수 있다. 


## 학습메모

공식문서만 보도록 노력함. 

1. [liquid filter, upcase](https://shopify.github.io/liquid/filters/upcase/)
2. [CSS Nesting](https://developer.chrome.com/articles/css-nesting/)
3. [translate css](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate)


---
---

# 231005

jekyll 코드블럭 highlight 처리 및 liquid 템플릿 처리 escaping

## 목차

- [x] liquid 템플릿 처리 escaping
- [x] jekyll 코드블럭 하이라이팅 (syntax highlighter)

## liquid 템플릿 처리 escaping

<img width="1026" alt="스크린샷 2023-10-05 오전 12 27 02" src="https://user-images.githubusercontent.com/138586629/272628071-1756c2e9-a59a-4107-9bb3-8169c67c9c9e.png">

블로그 배포하고나서 알게 된 사실인데, jekyll에서 `{{ ~ }}`, `{% ~ %}`문법 등으로 템플레이팅해놓은 
html은 md 파일에 코드 블락으로 넣어도 Liquid 템플릿 엔진이 이를 해석하고 값으로 치환해버려서, 
위와 같이 엄청나게 더러운 코드로 변환되어버린다.. (설치해놓은 SEO tag 플러그인 때문..) <br /><br />

이를 해결하기 위해 여러 모로 검색해봤는데, 대부분 학습메모 3의 `{% raw %}` ~ `{% endraw %}` 문법으로 
직접 Escaping 해줘야 한다고 하더라. 그런데 이걸 어떻게 일일이 다 해????

---

그러던 와중에 단서를 찾았다.

```
---
render_with_liquid: false
---
```

바로 `Front Matter`를 이용하여 위와 같이 `render_with_liquid` 값을 설정하면 해당 파일의 렌더링을 
아예 안한다는 건데, 이것도 md 파일마다 일일이 넣는 것이 곤란하다고 생각하던 차에, `_config.yml`에서 
`defaults`를 설정할 수 있다는 게 기억났다! 

```yml
# _config.yml
...
defaults:
  ...
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
      render_with_liquid: false
  ...
```

그래서 post에 해당하는 녀석에 모두 이걸 붙여주면 된다. 난 진짜 천재가 맞는 것 같다. 진심으로. 

---

<img width="794" alt="스크린샷 2023-10-05 오전 12 55 40" src="https://user-images.githubusercontent.com/138586629/272636479-b15b808c-5e5d-42a2-869a-c2d4bbc721b9.png">

보시다시피 templating이 싹 무시되고 제대로 코드 블록만 보인다! 문제 해결 성공 !


## jekyll 코드블럭 하이라이팅 (syntax highlighter)

덧붙여서 이쁜 코드 블럭을 위해 하이라이팅도 추가해보자. 학습메모 1 참고함.  

```bash
sudo gem install kramdown rouge
```

![스크린샷 2023-10-05 오전 12 24 20](https://user-images.githubusercontent.com/138586629/272627240-3fdb53cc-be69-4e72-bb9e-23f3af64f5a3.png)

우선 kramdown이랑 rouge를 설치해준다.

```yml
# _config.yml

markdown: kramdown
kramdown:
  input: GFM
  syntax_highlighter: rouge
```

다음으로 `_config.yml` 가장 하단에 markdown 관련 설정을 추가해준다. 
내가 원했던 건 Github Flavored Markdown이므로 기입해주고, syntax_highlighter는 방금 설치한 rouge. 

```bash
rougify style base16.monokai.dark > assets/css/syntax.css 
```

다음으로 설치한 rouge에서 제공하는 `rougify` 명령으로 블로그에서 추천받은 `base16.monokai.dark` 테마를 
다운받아준다. 이쁘더라. 다른 테마를 고르고 싶으면 [학습메모 2](https://spsarolkar.github.io/rouge-theme-preview/) 참조. 

![스크린샷 2023-10-05 오전 12 56 35](https://user-images.githubusercontent.com/138586629/272636749-ecfcd285-167c-4a9c-9314-a66532c9b488.png)


아무튼 이렇게 하면 assets/css에 syntax.css폴더가 다운받아진다. 

---

<img width="1332" alt="스크린샷 2023-10-05 오전 12 57 16" src="https://user-images.githubusercontent.com/138586629/272636999-c94d6292-5b3a-452a-b20e-6e3755f884da.png">

만족 만족 대만족! 패딩만 살짝 더 줘야겠다. 

## 학습메모

1. [syntax highlighter in jekyll](https://hard-carry.com/how-to-change-syntax-highlighter-in-jekyll/)
2. [rouge theme preview page](https://spsarolkar.github.io/rouge-theme-preview/)
3. [liquid raw (특정 영역을 liquid escaping)](https://shopify.github.io/liquid/tags/template/#raw)
4. [redner_with_liquid: false (file 전체를 liquid escaping)](https://talk.jekyllrb.com/t/any-way-to-exclude-files-directories-from-liquid-processing/6282)


---
---


# 231006

## 목차

- Github 페이지 수동 Rebuild

## Github 페이지 수동 Rebuild



## 학습메모

1. [Repository의 Github Page 반영 상태 알아보기](https://goodgid.github.io/Github-Blog-Status-Check/)


---
---


# ${날짜}

## 목차

## 학습메모