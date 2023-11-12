## 목표

- NestJS의 기초적인 CRUD 구현을 TDD로 개발하기 위한 테스트 코드 작성법을 익혀본다.
- 현재 NestJS 공식문서 가이드대로, Repository없이 Module-Controller-Service 아키텍처를 준수하며, Controller와 Service에 대한 jest 테스트 코드를 작성하는 방법을 알아보도록 한다.

# NestJS 테스트 코드 작성 (Unit Test)

## 방법론

1. `nest g module/controller/service`를 통해 뼈대 만들기
2. 실패하는 테스트 코드(Controller, Service) 작성
3. 테스트가 성공하도록 기능(Controller, Service의 메소드) 구현

## 뼈대 만들기

board 모듈을 예시로 들어보자. `@nestjs/cli`의 `nest g` 명령을 활용할건데,
동일 이름으로 module(mo), controller(co), service(s) 파일을 만들어 준다.

```bash
nest g mo board
nest g co board
nest g s board
```

## Controller

아래는 자동 생성된 Controller코드. 암것도 없고 Service만 들어가 있다.

```ts
// board.controller.ts
import { Controller } from "@nestjs/common";
import { BoardService } from "./board.service";

@Controller("board")
export class BoardController {
  constructor(private readonly boardService: BoardService) {}
}
```

실패하는 테스트 코드를 만들어 줘야 한다. `nest g` 명령에 `--no-spec` 옵션같은 걸 주지 않았다면,
기본적으로 다음과 같은 테스트 코드가 생성되어 있다.

```ts
// board.controller.spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { BoardController } from "./board.controller";
import { BoardService } from "./board.service";

describe("BoardController", () => {
  let controller: BoardController;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [BoardController],
      providers: [BoardService],
    }).compile();

    controller = module.get<BoardController>(BoardController);
  });

  it("should be defined", () => {
    expect(controller).toBeDefined();
  });
});
```

`Test.createTestingModule` 메소드를 통해 생성된 TestingModule 인스턴스를 활용하는 형태다.
모든 테스트 코드에서 위와 같은 방식으로 beforeEach가 구성될거기 때문에 눈으로 익혀두자.

의존성은 `@nestjs/testing` 모듈을 devDependencies로 추가해주면 되는데,
이것도 기본적으로 `nest new`로 프로젝트 세팅하면 설치되어 있을 거임. 안돼있다면 뭐

```bash
yarn add @nestjs/testing --dev
npm i -D @nestjs/testing
```

위 initial 코드에선 Controller가 정의되어있는지만 보기 때문에 당연히 통과된다.
이제 적절하게 `describe-it-expect` 구문들을 추가해주면 된다.

보통은 describe로 `메소드명`, it으로 `처리해줘야 할 동작`을 명시해준다. 예를 들면

```ts
// board.controller.spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { BoardController } from "./board.controller";
import { BoardService } from "./board.service";
import { Board } from "./entities/board.entity";

describe("BoardController", () => {
  let controller: BoardController;
  let service: BoardService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [BoardController],
      providers: [BoardService],
    }).compile();

    controller = module.get<BoardController>(BoardController);
    service = module.get<BoardService>(BoardService);
  });

  it("should be defined", () => {
    expect(controller).toBeDefined();
  });

  describe("findAll", () => {
    it("should be defined", () => {
      expect(controller.findAll).toBeDefined();
    });

    it("should return an array of boards", async () => {
      const board = new Board();
      board.id = 1;
      board.title = "test";
      board.content = "test";
      board.image = null;
      board.star_style = "test";
      board.star_position = "POINT(0, 0, 0)";
      board.author = "test";
      board.created_at = new Date();
      board.modified_at = new Date();
      const boards = [board];

      jest.spyOn(service, "findAll").mockImplementation(async () => boards);

      expect(await controller.findAll()).toBe(boards);
    });
  });
});
```

이렇게 말이다. 후 이거 여기저기 에러가 너무 많이 떠서 배보다 배꼽이 더 큰 느낌이다. TDD 이거 맞아?

하여간 이걸 통과하려면

1. entity가 정의되어 있어야 하고, 그 속성에 id, title, ..., modified_at이 다 들어있어야 하고
2. controller의 `findAll`메소드가 정의되어 있어야 하고
3. service 및 service의 `findAll`메소드가 정의되어 있어야 하고
4. service `findAll` 메소드의 return 타입이 `Board[]`로 정의되어 있어야 하고
5. 그러고나서야 `findAll`을 실행시켰을 때 boards가 리턴되는지를 검사하고, 이게 맞으면 테스트 통과다.

이 작은 함수에 전제조건들이 너무 많아 이것들을 다 테스트로 만들어야 하나 싶은데,
그래도 에러나는 건 마찬가지니, 각 메소드를 빈 함수로 선언해주고 테스트 코드 작성을 시작하는 것도 나쁘지 않을 것 같다.

```ts
import { Controller } from "@nestjs/common";

@Controller("board")
export class BoardController {
  constructor(private readonly boardService: BoardService) {}
  findAll() {}
}
```

```ts
// board.service.ts
import { Injectable } from "@nestjs/common";

@Injectable()
export class BoardService {
  findAll() {}
}
```

예를 들면 이정도까지만.

<img width="1179" alt="스크린샷 2023-11-12 오후 5 27 55" src="https://user-images.githubusercontent.com/138586629/282287313-449111b5-83eb-4fb4-b816-e263ab9d350a.png">

하여튼 이런 에러들 잔뜩 뜨다가

```ts
import { Controller, Get } from "@nestjs/common";

@Controller("board")
export class BoardController {
  constructor(private readonly boardService: BoardService) {}

  @Get()
  findAll() {
    return this.boardService.findAll();
  }
}
```

<img width="1023" alt="스크린샷 2023-11-12 오후 6 29 41" src="https://user-images.githubusercontent.com/138586629/282290929-68935c88-740e-4472-ad7a-d54875e26819.png">

이렇게 코드만 작성해주면 테스트가 통과된다. TDD 완성!

```ts
jest.spyOn(service, "findAll").mockImplementation(async () => boards);
```

Service 메소드 findAll을 구현하지 않아도 되는 이유는 이 `함수 mocking`을 해주었기 때문이다. 아래에 설명!

### 함수 mocking에 대해 : mockImplementation()

이 시점에서 Controller에서 `findAll` 메소드는 있지만, Service `findAll`은 제대로 동작하지 않은 채로 Controller를 구현 및 테스트할 수 있어야 한다.

이걸 가능하게 하기 위해 Controller 테스트 코드에서, Service 동작이 제대로 구현되었다는 가정을 하고!
다시 말하면 Service의 구현 여부를 배제한 채로!
테스트를 수행할 수 있게 가상 메소드를 구현해 주는 것이 바로 이 `mockImplementation()`이다.

```ts
let service: BoardService;
...
service = module.get<BoardService>(BoardService);
...
jest.spyOn(service, 'findAll').mockImplementation(async () => boards);
```

위 코드는 실제 BoardService 인스턴스인 service의 `findAll` 메소드를 mockImplementation()의 인자로 넣어준 `async () => boards`로 덮어써버리는 함수라고 해석하면 된다.

에러가 나지 않으려면 앞서 언급하였듯 service 및 findAll 메소드가 정의되어 있어야 하고,
덮어쓰는 함수 `async () => boards`와 input/output 타입이 맞아야 한다. `any`로도 가능.

자세한 내용은 학습메모 3, 4를 참고하자.

## Service

```ts
// board.service.spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { BoardService } from "./board.service";

describe("BoardService", () => {
  let service: BoardService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [BoardService],
    }).compile();

    service = module.get<BoardService>(BoardService);
  });

  it("should be defined", () => {
    expect(service).toBeDefined();
  });
});
```

마찬가지로 기본 생성되는 Service에 대한 테스트 코드이다.
초기엔 Service가 정의되어있는지만 보기 때문에 바로 통과된다.

마찬가지로 findAll 메소드에 대한 테스트 코드를 추가해보자.

```ts
// board.service.spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { BoardService } from "./board.service";
import { Board } from "./entities/board.entity";

describe("BoardService", () => {
  let service: BoardService;
  let repository: Repository<Board>;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        BoardService,
        {
          provide: getRepositoryToken(Board),
          useClass: Repository,
        },
      ],
    }).compile();

    service = module.get<BoardService>(BoardService);
    repository = module.get<Repository<Board>>(getRepositoryToken(Board));
  });

  it("should be defined", () => {
    expect(service).toBeDefined();
  });

  describe("findAll", () => {
    it("should be defined", () => {
      expect(service.findAll).toBeDefined();
    });
    it("should return an array of boards", async () => {
      const board = new Board();
      board.id = 1;
      board.title = "test";
      board.content = "test";
      board.image = null;
      board.star_style = "test";
      board.star_position = "POINT(0, 0, 0)";
      board.author = "test";
      board.created_at = new Date();
      board.modified_at = new Date();
      const boards = [board];

      jest.spyOn(repository, "find").mockImplementation(async () => boards);

      expect(await service.findAll()).toBe(boards);
    });
  });
});
```

Controller와 큰 차이 없지만, Repository Mocking이 생각보다 좀 어려워서 헤맸다. 학습메모 7, 8 참고.

```ts
import { Test, TestingModule } from '@nestjs/testing';
import { BoardService } from './board.service';
import { Board } from './entities/board.entity';
import { Repository } from 'typeorm';
import { getRepositoryToken } from '@nestjs/typeorm';
...

let service: BoardService;
let repository: Repository<Board>;

beforeEach(async () => {
  const module: TestingModule = await Test.createTestingModule({
    providers: [
      BoardService,
      {
        provide: getRepositoryToken(Board),
        useClass: Repository,
      },
    ],
  }).compile();

  service = module.get<BoardService>(BoardService);
  repository = module.get<Repository<Board>>(getRepositoryToken(Board));
});
```

하여간 여러 자료들 찾아보니 이런 식으로 구성해서 필요한 메소드 `mockImplementation()`하는 게 국룰.

<img width="1024" alt="스크린샷 2023-11-12 오후 11 48 55" src="https://user-images.githubusercontent.com/138586629/282306428-be8a3b9e-7d1a-453a-8fe5-314b4825a9ca.png">

아까 메소드는 만들었으니까, 메소드 정의는 통과되고, return값은 failed! 이게 정상

이제 통과되도록 service의 findAll 코드를 수정해주면 되시겠다.

```ts
// board.service.ts
import { Injectable } from "@nestjs/common";
import { Board } from "./entities/board.entity";
import { InjectRepository } from "@nestjs/typeorm";
import { Repository } from "typeorm";

@Injectable()
export class BoardService {
  constructor(
    @InjectRepository(Board)
    private boardRepository: Repository<Board>
  ) {}

  findAll(): Promise<Board[]> {
    return this.boardRepository.find();
  }
}
```

깔끔해!

<img width="542" alt="스크린샷 2023-11-13 오전 12 22 41" src="https://user-images.githubusercontent.com/138586629/282308197-551f949c-7f3f-4710-9ab6-bdf7c46842da.png">

잘 통과도 되더라.

별개로 학습메모 9에 CRUD 쭉 따라가는 게 있으니 참고해보자.

### DB에 실제로 들어갔는지를 테스트하려면?

create, update는 제대로 생성/수정됐는지 확인해야되는 작업이 들어가서 findOne이 일단 작동을 해야된다는 전제조건이 있다. 뭐 이것도 mocking하면 되긴 하겠지만 글쎄. DB에 제대로 들어갔는지도 확인하고 싶다.

- Entity, DTO를 처리해줘야 함
- create, update에서 리턴되는 값을 제대로 확인해줘야 함. 실제로 DB에 들어갔는지

위 항목은 어찌저찌 할 수 있겠다만, 아래 항목은 Repository 테스트를 따로 실시해줘야 하는 게 아닐까?
하지만 Repository는 Template문법으로 이미 NestJS에서 제공되는 함수를 쓰니 테스트 코드를 작성하기도 애매하다(`Repository<Board>`). 학습메모 10에 E2E 테스트에서 이걸 수행하는 내용도 있긴하다..만 애매

이 고민은 앞으로 더 해보자.

## Coverage

```bash
yarn run test:cov
```

참고로 위 명령으로 커버리지를 통계를 볼 수 있다. 주요 모듈에 대해서라도 100%를 채우는 걸 목표로 하면 좋겠다!

<img width="633" alt="스크린샷 2023-11-13 오전 12 33 03" src="https://user-images.githubusercontent.com/138586629/282309014-b35f55b7-4a80-441f-8fdc-5d695f06fc0d.png">

참고로 현재 상태 ㅋ 막 테스트하다보니 시뻘겋고..

# E2E Test

Testing 모듈을 통해 파일별 Unit Test 외에도 E2E(End-to-End) 테스트라는 것을 할 수 있다.
Unit Testing과 달리 클래스와 모듈 전체의 동작을 HTTP 요청에서 응답까지 전체 과정에서 보는 것.

백문이 불여일견 NestJS 공식문서에 소개된 cats라는 예시모듈에 대한 e2e 테스트 코드를 보자.

```ts
// cats.e2e-spec.ts
import * as request from "supertest";
import { Test } from "@nestjs/testing";
import { CatsModule } from "../../src/cats/cats.module";
import { CatsService } from "../../src/cats/cats.service";
import { INestApplication } from "@nestjs/common";

describe("Cats", () => {
  let app: INestApplication;
  let catsService = { findAll: () => ["test"] };

  beforeAll(async () => {
    const moduleRef = await Test.createTestingModule({
      imports: [CatsModule],
    })
      .overrideProvider(CatsService)
      .useValue(catsService)
      .compile();

    app = moduleRef.createNestApplication();
    await app.init();
  });

  it(`/GET cats`, () => {
    return request(app.getHttpServer()).get("/cats").expect(200).expect({
      data: catsService.findAll(),
    });
  });

  afterAll(async () => {
    await app.close();
  });
});
```

이렇게 Service 단에서의 메소드가 HTTP 요청에 대한 응답까지 잘 오는지를 볼 수 있다.

# CRUD Generator

앞서 module, controller, service를 따로따로 만들었지만,
nest g resource로 이를 한번에 만들 수 있다. 이건 지난번에도 알았는데, 찾아보니
`CRUD Generator` 옵션을 추가하면 간단한 CRUD 메소드까지 뼈대를 잡아준다.

<img width="506" alt="스크린샷 2023-11-12 오후 5 59 54" src="https://user-images.githubusercontent.com/138586629/282291474-502f6eaa-e772-4bb6-acb5-626db94ff04b.png">

CRUD에 대한 테스트 코드는 안만들어주니, CRUD Generator로 생성된 것을 기점으로
CRUD에 대한 테스트 코드 작성을 시작하는 것이 훨씬 더 효율적이겠다! 굳

```ts
// test.controller.ts
import {
  Controller,
  Get,
  Post,
  Body,
  Patch,
  Param,
  Delete,
} from "@nestjs/common";
import { TestService } from "./test.service";
import { CreateTestDto } from "./dto/create-test.dto";
import { UpdateTestDto } from "./dto/update-test.dto";

@Controller("test")
export class TestController {
  constructor(private readonly testService: TestService) {}

  @Post()
  create(@Body() createTestDto: CreateTestDto) {
    return this.testService.create(createTestDto);
  }

  @Get()
  findAll() {
    return this.testService.findAll();
  }

  @Get(":id")
  findOne(@Param("id") id: string) {
    return this.testService.findOne(+id);
  }

  @Patch(":id")
  update(@Param("id") id: string, @Body() updateTestDto: UpdateTestDto) {
    return this.testService.update(+id, updateTestDto);
  }

  @Delete(":id")
  remove(@Param("id") id: string) {
    return this.testService.remove(+id);
  }
}
```

```ts
// test.service.ts
import { Injectable } from "@nestjs/common";
import { CreateTestDto } from "./dto/create-test.dto";
import { UpdateTestDto } from "./dto/update-test.dto";

@Injectable()
export class TestService {
  create(createTestDto: CreateTestDto) {
    return "This action adds a new test";
  }

  findAll() {
    return `This action returns all test`;
  }

  findOne(id: number) {
    return `This action returns a #${id} test`;
  }

  update(id: number, updateTestDto: UpdateTestDto) {
    return `This action updates a #${id} test`;
  }

  remove(id: number) {
    return `This action removes a #${id} test`;
  }
}
```

참고로 코드는 대강 이런식이다. 협업할 때 논란의 여지도 없겠고, 아름답다! (뭐 메소드 이름정도는 고치는 게 좋을지도)

자세한 내용은 학습메모 6 참고~

## 더 알아보기

학습메모 9에 CRUD 테스트 코드의 전체적인 흐름이 잘 나와 있다. 코드는 조금씩 다르지만!

다음 주 페어 프로그래밍 때 오늘 작성한 자료와 이 자료를 같이 보며 쭉 TDD를 진행해보면 좋을 듯!

**실제 DB에 잘 반영되었는지**를 테스트하는 코드는 어떻게 작성할 지 더 고민해보자!

## 학습 메모

1. [NestJS Testing 공식 문서](https://docs.nestjs.com/fundamentals/testing)
2. [TDD로 NestJS API 만들기](https://devkly.com/nodejs/simple-tdd-with-nestjs/)
3. [mockImplementation()](https://jestjs.io/docs/mock-function-api#mockfnmockimplementationfn)
4. [mockImplementation, mockResolvedValue 설명](https://4sii.tistory.com/623)
5. [DTO로 Entity 생성하기](https://seungtaek-overflow.tistory.com/14)
6. [CRUD Generator](https://docs.nestjs.com/recipes/crud-generator)
7. [Repository Mocking 방법](https://velog.io/@lsjbh45/Nest.jsTypeORM-Repository%EC%9D%98-%EC%9D%BC%EB%B6%80%EB%A7%8C%EC%9D%84-mocking%ED%95%B4-Custom-Repository%EC%9D%98-method%EB%93%A4-test%ED%95%98%EA%B8%B0)
8. [Repository Mocking (Stack Overflow)](https://stackoverflow.com/questions/55366037/inject-typeorm-repository-into-nestjs-service-for-mock-data-testing)
9. [NestJS CRUD 테스트 코드 작성](https://velog.io/@1yongs_/NestJS-Testing-Jest)
10. [rollback database in e2e test](https://github.com/nestjs/nest/issues/1843)
11. [TypeORM Transactional Rollback 활용 방법](https://bk0625.tistory.com/6)
