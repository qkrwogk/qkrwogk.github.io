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