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