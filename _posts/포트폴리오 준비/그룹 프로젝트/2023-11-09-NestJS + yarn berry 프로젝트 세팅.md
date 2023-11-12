## 설명

프론트엔드에서 yarn berry 사용을 결정한 후, 백엔드에서도 의존성 관리 패키지의 통일을 위해 동일하게 yarn berry를 사용하기로 결정했다. NestJS의 `@nestjs/cli`에서는 기본적으로 yarn berry로 새 프로젝트를 생성하는 기능을 `nest new`로 제공하지 않기 때문에, 우선 `yarn` 옵션으로 프로젝트를 생성한 후 다음과 같은 일련의 과정들을 거쳐야 한다.

## 설정 방법

1. upstream 주소 등록

```bash
git remote add upstream [Repository 주소]
# [Repository 주소] : https://github.com/boostcampwm2023/web16-B1G1
```

2. yarn 설치

```bash
brew install yarn
```

[Nest.js에 Yarn Berry + Zero Install 적용하기](https://blog.naver.com/PostView.naver?blogId=biud436&logNo=223211308347&categoryNo=199&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)

3. 프로젝트 폴더(`WEB16-B1G1/BE/`)에서 nest init project 설치

```bash
nest new .
```

4. 같은 폴더에서 yarn berry 활성화

```bash
yarn set version berry
```

5. `yarn —version`으로 정상적으로 버전이 변경되었는지 확인

```bash
yarn --version
```

정상적으로 변경되었다면 아래와 같이 변경된다(현재 환경의 경우 4.0.1)

<img width="564" alt="스크린샷 2023-11-07 오후 9 21 35" src="https://user-images.githubusercontent.com/138586629/281048114-6e674c41-1a71-4a16-a86b-55d0fd2db68a.png">

6. `.gitignore`에 yarn 관련 파일 등록하여 git 추적에서 제거

```
# yarn
.yarn/*
!.yarn/cache
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/versions
```

7. `node_modules` 폴더 삭제

<img width="332" alt="스크린샷 2023-11-07 오후 9 25 50" src="https://user-images.githubusercontent.com/138586629/281048166-089220d7-89a2-409d-afde-92273407c084.png">

8. **yarn install**을 통해 다시 의존성 설치
   → 이제 yarn berry에 의해 `node_modules/`가 아닌 `.yarn/releases/yarn-[version].cjs` 에 zip파일 형식으로 설치됨

```bash
yarn install
```

<img width="626" alt="스크린샷 2023-11-07 오후 9 37 17" src="https://user-images.githubusercontent.com/138586629/281048623-eb043f60-ac84-4fe1-a105-1bc501df8808.png">

9. `.yarnrc.yml`에 nodeLinker 속성을 주석 처리

```bash
# nodeLinker: node-modules

yarnPath: .yarn/releases/yarn-4.0.1.cjs
```

10. 다시 남아있는 `node_modules/` 폴더를 지우고 **yarn install** 하면 끝

<img width="449" alt="스크린샷 2023-11-07 오후 9 42 31" src="https://user-images.githubusercontent.com/138586629/281048689-ed786d4e-924a-43d3-b2fa-435a5a1e8476.png">

```bash
yarn install
```

## 결과 확인 (nest init 프로젝트 실행)

```bash
yarn run start:dev
```

<img width="1120" alt="스크린샷 2023-11-07 오후 9 45 29" src="https://user-images.githubusercontent.com/138586629/281049055-f500f8b7-7c69-4873-adca-71954a7e3c44.png">

<img width="750" alt="스크린샷 2023-11-07 오후 9 45 39" src="https://user-images.githubusercontent.com/138586629/281049072-1cb6ba7f-85cd-4bb3-9c5e-1bf8f6903239.png">

`node_modules/` 가 없는데도 프로젝트가 정상적으로 잘 동작하는 것을 확인할 수 있다!

## VSCode TypeScript 버전 설정

### 모노레포상에서의 트러블 슈팅 과정

위 스크린샷에서도 확인할 수 있듯이, 각 FE, BE 프로젝트는 `yarn run` 등으로 프로젝트를 빌드하거나 실행할 때는 문제없이 잘 작동하지만, VSCode IDE 상에서 모듈을 찾을 수 없다는 에러메시지가 계속해서 발생하였다.

그래서 VSCode가 `node_modules/` 폴더가 아닌 `.yarn/` 폴더에 **ZipFS** 형식으로 관리되는 모듈을 제대로 인식하지 못해서 생기는 문제가 아닐까 하는 추측을 해보았다.

[yarn berry + vscode 설정 방법](http://kimyanglogging.tistory.com/m/8)

관련하여 자료조사 중 비슷한 문제에 대한 해결을 TypeScript 버전 설정을 VSCode 자체 설정이 아닌 Workspace 내의 `.yarn/sdks/typescript/lib` 에 명시된 버전으로 이용하도록 바꾸면 모듈 인식 문제가 해결된다는 사실을 발견하고, 비슷한 방식으로 설정을 시도해 보았다.

하지만 여기서 "Use Workspace Version" 옵션이 활성화되지 않아 이 `.yarn/sdks/typescript/lib` 경로를 **모노레포** 형식의 프로젝트 특성 상 **VSCode에서 인식하지 못하는 것이 아닐까** 하는 의구심을 가지게 되었다.

따라서 일반적인 프로젝트 구조와 동일하게 만들기 위해 모노레포인 프로젝트 루트가 아닌 **FE, BE 폴더 내부**에서 VSCode를 다시 실행해보았더니 잘 동작했다!

해당 설정을 적용하면 `.vscode/` 폴더에 `settings.json` 이란 파일이 생성되어 아래와 같은 설정이 적용되는데,

```json
{
  "typescript.tsdk": ".yarn/sdks/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true
}
```

이를 모노레포 프로젝트 루트에 옮기고, 상대경로를 (`FE/...`, `BE/...` 등으로)잘 설정해주면 VSCode에서 TypeScript 설정 시 해당 경로를 인식하게 해 줄 것이라고 생각되었고, 실제로 잘 동작했다!

```json
// project root 폴더에서 .vscode/settings.json을 만들어 다음과 같이 경로 지정
{
  "typescript.tsdk": "BE/.yarn/sdks/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true
}
```

### 설정 방법

```bash
yarn dlx @yarnpkg/sdks vscode
```

설치 후 다음 중 하나의 방법으로 해결한다.

- 설치 후 VSCode에서 TypeScript 관련 alert창이 보이면 Allow
- `cmd + shift + p`
  - -> TypeScript: Select TypeScript Version
  - -> Use Workspace Version
- `.vscode/settings.json` 생성
  - ```json
    {
      "typescript.tsdk": ".yarn/sdks/typescript/lib",
      "typescript.enablePromptUseWorkspaceTsdk": true
    }
    ```
  ```

  ```
