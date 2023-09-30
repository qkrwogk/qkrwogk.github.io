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
## 학습메모


---
---


# 231002
## 목차
## 학습메모


---
---


# 231003
## 목차
## 학습메모
