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