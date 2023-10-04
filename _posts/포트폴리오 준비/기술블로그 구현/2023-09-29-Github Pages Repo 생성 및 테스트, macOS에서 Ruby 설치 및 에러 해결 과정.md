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