그룹프로젝트에서 사용되는 기술 스택은 다음과 같다.

|    구분    |                기술 스택                 |
| :--------: | :--------------------------------------: |
|  Frontend  | React, TypeScript, R3F, Emotion, Zustand |
|  Backend   |       NestJS, TypeScript, TypeORM        |
|     DB     |          Redis, MySQL, MongoDB           |
|   CI/CD    |              GitHub Actions              |
| Deployment |   Docker, NGINX, Naver Cloud Platform    |

본 문서에서는 위 기술스택 중 백엔드(Backend), 배포(Deployment) 영역에서 사용되는 기술 및 서비스에 대한 소개와 채택 이유에 관해 설명해본다.

# Backend

## NestJS

[NestJS](https://nestjs.com/)

[NestJS는 왜 개발되었을까? 사용하는 이유를 알려드립니다! I 이랜서 블로그](https://www.elancer.co.kr/blog/view?seq=197)

Node.js 기반의 백엔드 프레임워크 중 가장 대중적으로 사용되는 Express는 프레임워크의 간결성을 중요시하고 로직 구성이 매우 자유롭다는 특징이 있습니다.

때문에 컨벤션을 까다롭게 지정하지 않는 이상 타인의 코드를 이해하는 데 시간이 많이 소요되는 등 협업에 유리하지 않다고 판단했습니다.

또한 프레임워크의 간결성으로 인해, 단기간에 많은 기능을 개발해야 하는 이번 프로젝트의 특성상 다른 프레임워크에 비해 Express는 개발 신속성이 떨어진다고 판단했습니다.

따라서 저희는 이러한 단점을 보완하기 위해 Express를 기반으로 개발된 NestJS를 선정하였습니다.

`NestJS`는 사전에 모듈 구조가 정의되어 있으며 데코레이터 기반으로 이를 사용하기 때문에 **서비스 확장성과 유지보수성**이 좋으며, **코드 스타일을 통일**하기가 쉽습니다.

또한 HTTP, 웹 소켓, 각종 미들웨어와 가드, 예외 필터, 로깅 등 서버 동작에 **필수적인 기능을 프레임워크에 포함**하여 제공하기 때문에, 직접 설치하거나 구현해서 사용해야 하는 Express에 비해 **의존성 관리**나 **개발 신속성** 면에서 유리합니다.

## TypeORM

[TypeORM](https://typeorm.io/)

[TypeORM 리뷰](https://velog.io/@leo3179/TypeORM-리뷰)

단순 CRUD(Create, Read, Update, Delete) 기능 구현이 대부분이기 때문에 **개발 신속성** 면에서 유리한 ORM의 사용을 채택했습니다.

프로젝트의 특성상 복수 개의 DB(MySQL, MongoDB)를 활용하며, SQL문이 아닌 클래스의 메소드를 통해 일관된 인터페이스로 데이터베이스를 조작할 수 있는 ORM의 장점을 더욱 가져갈 수 있습니다. 이 점은 코드 일관성 및 유지보수 측면에서도 좋기 때문에 협업하여 개발하는 본 프로젝트에서 더 효과적일거라 기대됩니다.

`TypeORM`은 **NestJS에서 공식 지원**하는 ORM입니다. 프로젝트에서 NestJS를 사용하기로 결정하였기 때문에, 가장 호환성이 좋은 TypeORM을 채택하였습니다.

이후, 성능 문제가 발생하는 부분은 쿼리 최적화 과정을 거친 후 해당 메소드만 ORM이 아닌 SQL 쿼리를 사용해 직접 구현할 예정입니다.

# Deployment

## Docker

[Docker](https://www.docker.com/)

[Docker란 무엇입니까? | AWS](https://aws.amazon.com/ko/docker/)

`Docker`는 어플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼입니다.

Docker의 가장 큰 특징은 **서버 운영체제를 가상화**(컨테이너라고 부름)하여 그 안에서 어플리케이션을 실행하는 방식으로 동작한다는 것입니다. 개발한 소프트웨어가 표준화된 실행 환경에서 동작하기 때문에, **실행 환경**으로 인해 발생할 수 있는 예기치 않은 **오류나 의존성 문제를 미연에 방지**할 수 있습니다.

또한 컨테이너 이미지를 **웹에 빌드, 저장 및 공유**할 수 있는 **Docker Hub**를 활용할 수 있기 때문에, Docker를 사용하면 직접 클라우드 인스턴스에 어플리케이션을 배포하는 것 보다 더 효과적으로 배포를 수행할 수 있습니다.

## GitHub Actions

[GitHub Actions](https://github.com/features/actions)

[[CI/CD] Jenkins 과 GitHub Actions의 개념, 차이점](https://choseongho93.tistory.com/295)

[GitHub Actions의 소개와 핵심 개념](https://www.daleseo.com/github-actions-basics/)

6주 간 애자일 방식으로 단기간에 많은 기능을 개발, 빌드, 테스트 및 배포를 반복해야 하는 이번 프로젝트의 특성상 Jenkins, GitHub Actions와 같은 소스코드 Repository에 대한 **지속적인 통합과 지속적인 배포(CI/CD)** 서비스를 이용하면 구현 외 작업에 소요되는 시간을 획기적으로 단축할 수 있다.

그 중에서도 `GitHub Actions`는 대표적인 코드 Repository 서비스인 GitHub에서 직접 제공하는 CI/CD 서비스로, 특정 branch가 push되는 등 Repository와 관련된 다양한 event를 트리거로 앞서 언급한 빌드, 테스트 및 배포를 자동화할 수 있는 가상환경 내의 스크립트 실행 기능을 제공합니다.

해당 기능을 활용하여 **Docker 이미지를 생성**하거나, **SSH로 클라우드 인스턴스에 접근**하여 원격 서버에서 **스크립트를 실행**할 수도 있기 때문에, 이번 프로젝트와 같은 소규모 프로젝트에서 GitHub Actions가 가장 신속하게 효과적으로 사용할 수 있을 것으로 기대되어 채택하였습니다.

Git Repository에서 GitHub Actions Workflow 파일(YAML 파일)을 함께 관리할 수 있고, 로그도 GitHub 페이지에서 바로 확인할 수 있다는 점도 큰 장점입니다.
