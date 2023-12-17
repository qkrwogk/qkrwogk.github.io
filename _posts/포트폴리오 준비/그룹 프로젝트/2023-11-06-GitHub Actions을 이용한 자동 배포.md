# GitHub Actions을 이용한 자동 배포

# GitHub Actions란?

[GitHub Actions 설명서 - GitHub Docs](https://docs.github.com/ko/actions)

- `GitHub Actions`는 GitHub Repository에서 **보안 검사, 빌드 및 테스트, 자동 배포** 등 소프트웨어 개발 워크플로(workflow)와 관계된 각종 `자동화`를 구현할 수 있는 기능임
- **CI/CD**를 포함하여 원하는 작업을 YAML 파일에 작성해두면 GitHub에서 이를 실행해 줌

# Quickstart

[GitHub Actions용 빠른 시작 - GitHub Docs](https://docs.github.com/ko/actions/quickstart)

## 예제

1. GitHub Repository에 `.github/workflows` 디렉터리 만들기
2. `filename.yml` 파일 만들기
3. 예제 코드

   ```yaml
   name: GitHub Actions Demo
   run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
   on: [push]
   jobs:
     Explore-GitHub-Actions:
       runs-on: ubuntu-latest
       steps:
         - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
         - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
         - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
         - name: Check out repository code
           uses: actions/checkout@v4
         - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
         - run: echo "🖥️ The workflow is now ready to test your code on the runner."
         - name: List files in the repository
           run: |
             ls ${{ github.workspace }}
         - run: echo "🍏 This job's status is ${{ job.status }}."
   ```

4. **commit** 후 **push** → `push` 이벤트 트리거에 의해 **워크플로**가 실행됨

## 결과 보기

1. GitHub Repository에서 `Actions` 탭으로 이동

   ![1](https://user-images.githubusercontent.com/138586629/281243044-3636cdd0-96e2-404a-ba60-f7208f0e135f.png)

2. 사이드바에서 결과를 해당 **워크플로** 클릭, 실행 목록에서 해당 **실행** 클릭

   ![2](https://user-images.githubusercontent.com/138586629/281243053-fc8797af-4eb3-4f32-a54d-21771363b438.png)

3. 워크플로 실행 페이지의 사이드바에서 `Explore-GitHub-Actions` **작업** 클릭

   ![3](https://user-images.githubusercontent.com/138586629/281243059-aca32d1d-4800-4b1e-9d33-56930b8c9f0d.png)

4. **로그**를 볼 수 있음

   ![4-1](https://user-images.githubusercontent.com/138586629/281243279-af4631b5-9f00-40c4-9c07-68ad0648d7d2.png)

   로그의 각 단계를 클릭하면 **세부 정보**를 볼 수 있음

   ![4-2](https://user-images.githubusercontent.com/138586629/281243287-6723d3fa-b8ae-4657-937e-322882accfa6.png)

# 빌드 및 테스트

[Node.js 빌드 및 테스트 - GitHub Docs](https://docs.github.com/ko/actions/automating-builds-and-tests/building-and-testing-nodejs)

## 저장 경로

시작 워크플로 파일(ex. `node.js.yml`)을 리포지토리의 `.github/workflows` 디렉터리에 추가

## Repository에 push한 경우 자동으로 빌드 및 테스트하는 예시

```yaml
name: Node.js CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "20.x"
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
```

# 배포

[Azure App Service에 Node.js 배포 - GitHub Docs](https://docs.github.com/ko/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-nodejs-to-azure-app-service)

## 웹 브라우저를 통한 접근 방법

<img width="1374" alt="배포" src="https://user-images.githubusercontent.com/138586629/281243412-7b0a0af0-afaf-4f0c-b14d-e6b15e647a5c.png">

## Repository에 push한 경우 자동으로 배포하는 예시(Azure)

```yaml
on:
  push:
    branches:
      - main

env:
  AZURE_WEBAPP_NAME: MY_WEBAPP_NAME # set this to your application's name
  AZURE_WEBAPP_PACKAGE_PATH: "." # set this to the path to your web app project, defaults to the repository root
  NODE_VERSION: "14.x" # set this to the node version to use

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: "npm"

      - name: npm install, build, and test
        run: |
          npm install
          npm run build --if-present
          npm run test --if-present
      - name: Upload artifact for deployment job
        uses: actions/upload-artifact@v3
        with:
          name: node-app
          path: .

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: "production"
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v3
        with:
          name: node-app

      - name: "Deploy to Azure WebApp"
        id: deploy-to-webapp
        uses: azure/webapps-deploy@85270a1854658d167ab239bce43949edb336fa7c
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: ${{ env.AZURE_WEBAPP_PACKAGE_PATH }}
```

- `${{ env.NODE_VERSION }}`, `${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}` 등은 GitHub에서 제공하는 **환경 변수 등록 및 사용 기능**을 활용한 것임. 환경 사용 방법은 아래 참고

## 배포에 환경 사용

[배포에 환경 사용 - GitHub Docs](https://docs.github.com/ko/actions/deployment/targeting-different-environments/using-environments-for-deployment)

### 웹 브라우저를 통한 접근 방법

<img width="1246" alt="환경" src="https://user-images.githubusercontent.com/138586629/281243420-31a562e3-14a8-4a27-9e8f-6795b9352cf1.png">

## GitHub Secret을 사용하여 인증 정보 저장해두기

[GitHub Actions에서 비밀 사용하기 - GitHub Docs](https://docs.github.com/ko/actions/security-guides/using-secrets-in-github-actions?tool=webui)

### 웹 브라우저를 통한 접근 방법

<img width="1236" alt="시크릿" src="https://user-images.githubusercontent.com/138586629/281243418-58b79f7e-d5e3-42e4-9120-846f6d96737e.png">

# 예시 스크립트

## ChatGPT에 질의한 GitHub Actions 스크립트

> github의 main 브랜치에 push할 경우 ubuntu-latest에 node.js로 docker 이미지를 생성하고 이를 SSH로 특정 서버에 접속해 자동 배포하는 GitHub Actions 스크립트를 짜줘.

```yaml
name: Build and Deploy via SSH

on:
  push:
    branches:
      - main

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 14 # 원하는 Node.js 버전으로 변경

      - name: Build Docker image
        run: |
          docker build -t your-docker-image-name:latest .
          docker login -u ${{ secrets.DOCKERHUB_USERNAME }} -p ${{ secrets.DOCKERHUB_PASSWORD }}
          docker push your-docker-image-name:latest

      - name: Deploy via SSH
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SSH_HOST }}
          username: ${{ secrets.SSH_USERNAME }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            # SSH로 접속하여 서버에서 실행할 스크립트를 작성합니다.
            # 이 스크립트는 Docker 이미지를 업데이트하는 과정을 포함해야 합니다.
            ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null ${{ secrets.SSH_USERNAME }}@${{ secrets.SSH_HOST }} 'bash -s' << 'ENDSSH'
              # 여기에 서버에서 실행할 스크립트를 작성합니다.
              # 예를 들어, Docker 이미지 업데이트 및 컨테이너 재시작과 관련된 명령어를 실행합니다.
              docker pull your-docker-image:latest
              docker stop your-container-name
              docker rm your-container-name
              docker run -d --name your-container-name -p 80:80 your-docker-image:latest
            ENDSSH
```

## GitHub Actions + NCP 활용 사례

### GitHub Actions + NCP + NGINX

[Github Action + NCP + Nginx로 간단 CI / CD 구성하기](https://heo-it-til.tistory.com/91)

```yaml
name: deploy

on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: SSH-deploy
        uses: appleboy/ssh-action@master
        with:
          host: ${{secrets.REMOTE_IP}}
          username: ${{secrets.SSH_ID}}
          password: ${{secrets.REMOTE_SSH_KEY}}
          port: ${{secrets.REMOTE_SSH_PORT}}
          script: |
            whoami
            cd /app/sara-frontend
            git pull origin main
            npm install --force
            npm run build
            nginx -s reload
```

### GitHub Actions + Node.js + Docker

[CI/CD 구축하기 with Nodejs, Docker, Github Action(2)](https://railend.tistory.com/89?category=913402)

```yaml
name: Node.js CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-20.04

    strategy:
      matrix:
        node-version: [14.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - name: Docker build
	  run: |
		docker login -u ${{ secrets.USERNAME }} -p ${{ secrets.PASSWORD }}
		docker build --platform linux/amd64 -t node-example .
  		docker tag node-example rheech22/node-example:${GITHUB_SHA::7}
	  	docker push rheech22/node-example:${GITHUB_SHA::7}
```

### GitHub Actions + NCP + Java Spring

[[Web] NCP + Github Actions 배포 자동화](https://velog.io/@seongwop/Web-NCP-Github-Actions-배포-자동화)

```yaml
name: Auto deploy to NCP
run-name: Running
on:
  push:
    branches:
      - develop

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # 체크아웃 및 JDK 세팅
      - name: Checkout
        uses: actions/checkout@v3
        with:
          ref: develop
      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: "17"
          distribution: "zulu"
      # Secret YML 파일 생성
      - name: Setting secret
        run: |
          mkdir -p src/main/resources
          echo "${{ secrets.SECRET_YML }}" | base64 --decode > src/main/resources/application-secret.yml
          find src
        shell: bash
      # Gradle 권한 부여
      - name: Grant permission for gradlew
        run: chmod +x ./gradlew
      # Test 없이 빌드
      - name: Build with Gradle
        run: ./gradlew clean build -x test
      #빌드한 jar 파일을 도커 이미지로 빌드하고 도커 허브에 푸시
      - name: web docker build and push
        run: |
          docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
          docker build -t ${{ secrets.DOCKER_REPO }}/my-project .
          docker push ${{ secrets.DOCKER_REPO }}/my-project

  deploy:
    # needs를 통해 build job이 수행 성공시에 작업되도록 설정
    needs: build
    runs-on: ubuntu-latest

    steps:
      # NCP 로그인 / docker image pull & run
      - name: NCP login and docker image pull and run
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.NCP_HOST }}
          username: ${{ secrets.NCP_USERNAME }}
          password: ${{ secrets.NCP_PASSWORD }}
          port: ${{ secrets.NCP_PORT }}
          script: |
            sudo docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
            sudo docker stop $(sudo docker ps -a -q)
            sudo docker rm -f $(sudo docker ps -a -q)
            sudo docker pull ${{ secrets.DOCKER_REPO }}/my-project
            sudo docker run -d -p 8080:8080 ${{ secrets.DOCKER_REPO }}/my-project
            sudo docker image prune -f
            ps -ef | grep
```

### GitHub Actions + AWS + Java Spring + Docker

[[Infra] Github Actions + Docker를 이용한 자동 배포](https://kth990303.tistory.com/444)

```yaml
name: Java CD with Gradle and Docker

on:
  push:
    branches:
      - develop # develop 브랜치에 push될 경우를 트리거로 설정

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      # Java JDK 11 버전을 이용합니다.
      - name: Set up JDK 11
        uses: actions/setup-java@v3
        with:
          java-version: "11"
          distribution: "temurin"

      # github secret 환경변수로 적어둔 PROD_YML로 application-prod.yml파일을 생성합니다.
      # 환경변수가 지나치게 많아짐을 방지하기 위해 PROD_YML 변수를 만들었습니다.
      - name: make application-prod.yml
        run: |
          cd ./src/main/resources
          touch ./application-prod.yml
          echo "${{ secrets.PROD_YML }}" >> ./application-prod.yml
        shell: bash

      # gradlew에 실행 권한을 부여합니다.
      - name: Grant execute permisson for gradlew
        run: chmod +x gradlew

      # test는 CI 과정에서 수행되므로 여기서는 `-x`로 테스트를 생략했습니다.
      # `--stacktrace`로 더 자세한 로그가 출력되게 해줍니다.
      - name: Build with Gradle (without Test)
        run: ./gradlew clean build -x test --stacktrace

      # docker hub에 로그인하고 이미지를 빌드합니다. 이후에 push를 진행합니다.
      # docker_username을 적지 않으면 push 시에 요청이 거부될 수 있습니다.
      - name: Docker Hub build & push
        run: |
          docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
          docker build -t ${{ secrets.DOCKER_USERNAME }}/${{ secrets.DOCKER_REPO }} .
          docker images
          docker push ${{ secrets.DOCKER_USERNAME }}/${{ secrets.DOCKER_REPO }}

      # EC2에 접속하고 배포합니다.
      - name: Deploy to Prod WAS Server
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.WAS_HOST }}
          username: ${{ secrets.WAS_USERNAME }}
          key: ${{ secrets.WAS_KEY }}
          port: ${{ secrets.WAS_SSH_PORT }}
          # docker-compose가 있는 디렉토리로 이동해야 수행됩니다.
          script: |
            cd /home/ubuntu/Mocacong-Backend/
            sudo docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
            sudo docker rm -f $(sudo docker ps -qa)
            sudo docker pull ${{ secrets.DOCKER_USERNAME }}/${{ secrets.DOCKER_REPO }}
            sudo docker-compose up -d
            sudo docker image prune -f
```

# 결론

## 요약

결국 다음과 같은 GitHub Actions 워크플로를 등록하면 됨 :

- `event`(main 브랜치에 push 등)가 트리거되면 (`on` 속성)
  → 등록된 작업들이 실행됨 (`jobs` 속성)
  → `build` 작업의 경우 특정 VM에서 npm build, npm test 등 빌드 및 테스트 실행
  → `deploy` 작업의 경우 docker 배포
  → docker build, docker push 등 도커 이미지 생성 후 `도커 허브`에 배포
  → ssh 접속하여 docker, pull/stop/rm/run 등 도커 이미지 갱신하여 실행

## 더 알아볼 것

- docker 이미지 **build**, **push**, **pull** 등 기본적인 관리 방법 학습
- 배포 시 실행해야 할 **docker 이미지 목록** 정리
  - Web서버(NGINX), FE/BE(Node.js), DB(Redis, MySQL, MongoDB) 등
- `docker-compose`를 통해 여러 docker 이미지를 통합하여 관리하는 방법 학습
  [Docker) Docker Compose에 대해서 간단하게 알아보기](https://data-newbie.tistory.com/930)
  [Docker-compose 란](https://velog.io/@baeyuna97/Docker-compose-란)
- **클라우드 아키텍쳐** 결정하고 **시스템 구성도** 그리기

  [Cloud Infrastructure Draw](https://dalgun.dev/blog/2020-05-03/cloud-craft)

  [클라우드 시스템 아키텍처 구성도 작성하기(draw.io)](https://jjakang2.tistory.com/44)

  [NAVER CLOUD PLATFORM](https://www.ncloud.com/intro/architecture/3)

  - 이후 draw.io를 이용해 다음과 같은 아키텍처 구조도를 그릴 수 있었다! 뿌듯

    ![아키텍처 구조도2 drawio](https://user-images.githubusercontent.com/138586629/281244022-eaf556c7-f3d9-4126-b3f1-8a94c46a5770.png)
