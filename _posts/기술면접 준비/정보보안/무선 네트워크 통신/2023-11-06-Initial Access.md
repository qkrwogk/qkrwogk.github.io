# Initial Access

## Initial Access

- 오늘은 주로 단말 입장.
- 다음 주는 gNB 입장.
  - Uplink 스케쥴링, Downlink 스케쥴링

## 10장 요약: 단말 입장의 Initial Access

### Cell Search

- `Synchronization Signal Block (SSB)`
- Frequency-Domain Position of SS Block
- SS Block Periodicity
- SS Burst Set : Multiple SS Blocks in the Time-Domain
- Details of PSS, SSS, and PBCH
- Proving Remaining System Information

### Random Access

- Preamble Transmission
- Random-Access Response
- Message 3: Contention Resolution
- Message 4: Contention Resolution and Connection Set Up
- Random Access for Supplementary Uplink

## 설명

모든 책임은 gNB에게 있다.
radio resource block이든 element든 책임(스케쥴링)은 gNB이 지고 주도해서 결정함.

<img width="682" alt="스크린샷 2023-12-14 오후 2 34 20" src="https://gist.github.com/assets/138586629/b52c3594-e9bc-4e13-adea-00de1fc82fe1">

5G Frame Structure를 보면 Channel과 Signal이 있잖아.

- 여기서 Channel은 실제 데이터가 전송되는 영역이고
- Signal은 데이터라기보단 신호 세기, 위상, 패턴 등으로 채널을 잘 해석하도록 돕는 기준점같은 역할이라고 보면 됨

중간 전에는 PDSCH, PDCCH, PUSCH, PUCCH 이런거 설명했었음

하여튼 PSS, PBCH, SSB, SSS 이부분이랑
RACH 이부분을 중간에선 설명을 안했거든? 이부분 설명해드림

Schedule 반대가 Random이죠.
데이터 통신할땐 Scheduled 인데 처음 스케쥴링해달라고는 Random Access!

## Initial Access Protocol in this week is used when

- 단말(= A device, Mobile station, User Equipment, UE)은

  - 전원이 켜질 때 cell을 찾음
  - idle/inactive 상태일 때는, set-up을 요청함 (이게 Random Access 과정)

- idle 상태일때도 full로는 아니지만 뜨문뜨문 읽음. PDCCH에서 오는 메시지로만 해결이 안되면 gNB는 단말보고 일어나라고 함
  - 그러면 이럴 때 단말이 gNB로 Initial Access를 요청하는 거임

## Cell Search By SSB(Synchronous Signal Block)

- 단말은 SSB를 계속 찾으려고 노력함.
  - 파워만 켜져있으면 통신을 하건 안하건.
  - 언제 통신할지, 언제 이동할지 모르기 때문에

## SSB (Synchronous Signal Block)

- 다음으로 구성됨
  - PSS : Primary Synchronous Signal
  - SSS : Secondary Synchronous Signal
  - PBCH : Physical Broadcasting Channel
- DL에서 주기적으로 전달됨
- SSB는 5G NR에서의 새로운 개념 (PSS/SSS/PBCH 4G에도 있긴함)

## Where are the SSB?

너무 많으면 오버헤드가 있으니 20ms당 한번씩 보냄
근데 한번 보낼때 여러개 보냄 왜? Beam Sweeping때문!

## Beam Sweeping by SSB

기지국과 단말의 상대적 위치가 어디일진 알 수가 없지.
그래서 다 똑같은 SSB 8개를 보내는데 다 다른방향으로 보내.

그래서 SSB Index 0~8중 신호 세기가 어디가 센지에 따라
단말에서 기지국 위치가 어느 방향에 있는지를 알아냄!

이 8개 세트를 Burst라고 함.

## What Information is in SS Block?

- Signals - PSS and SSS
  - 정보 없음
  - 그냥 고정된 패턴을 보내서 단말이 탐색할 수 있게 하는 것
  - 전달받은 세기가 레퍼런스가 됨
  - Common/Broadcasting/Not a device-specific
    - CSI-RS는 반대로 단말 특화된 정보
- Channel - PBCH
  - Basic/Common/Broadcasting Information (시스템 정보 등)
  - 단말은 이걸 탐색하진 않지만 해석하려고 함

대강 PSS를 가지고 OFDM Symbol Boundary를 찾는다!
이것이 PSS의 역할 (correlation을 계산하고 그게 제일 큰 인덱스를 찾아 그걸 바운더리로 해석한다나)

다시 말하자면 timing을 정확히 맞춰주는 게 PSS의 역할

## 이 뒤로 슥슥슥 넘어감

## Secondary Synchronous Sequence(SSS)

이제 vertical, horizontal 위치를 맞췄으니까 정확하게 SSS를 읽을 수 있겠죠?

3\*336 = 1008개 중 하나. PCI(=Physical Cell ID)

기지국 ID라고 생각하면 됨 기지국은 1008개보다 훨씬 많을테니 가까운 지리적 위치에 있으면 PCI 다르도록 구성을 잘 해놨겠죠?

## Physical Broadcast CHannel(PBCH)

정확한 내용은 몰라도되지만 아무튼 기지국에 대한 주요 정보가 들어있음. ㅇㅇ Signal이 아니라 Channel이니깐~

PSS, SSS 거치면 이제부턴 마음껏 메모리 속 채널 데이터를 받아볼 수 있는거겠죠? PBCH에 CRC도 들어있으니 채널코딩 폴라코딩도 되어있단 거임

CRC가 왜있냐? PBCH에 있는 정보 매우 중요하니 CRC 틀리면 이 정보 믿지마라 ㅇㅇ 무결성을 위해 있는거라고 보면됨.

## 여기까지 정리

<img width="675" alt="스크린샷 2023-12-14 오후 3 28 08" src="https://gist.github.com/assets/138586629/2c45400f-8e75-4bb9-88d3-eff0ce3cb8f8">

아무튼 SSB를 설명을 드렸음.

1. PSS로 horizontal, vertical 오프셋 맞추고
2. PSS의 3, SSS의 336 으로 1008개중 하나인 PCI읽고
3. 나머지 PBCH부분 읽어서 CRC 체크해서 맞으면 gNB 정보 얻음

이제부터 랜덤 액세스 ㄱ ㄱ

## Just for Reference 5G NR PHY Channels

- Logical Channels
- Transport Channels
- Physical Channels

<img width="558" alt="스크린샷 2023-12-14 오후 3 33 29" src="https://gist.github.com/assets/138586629/c387c56a-139f-47fd-9b51-a71c2520d870">

이제 여기서 PRACH에 대해서 말씀드리면서 Random Access를 설명할거예요

Initial Access => Random Access 밖에 없음 ㅇㅇ

이제 SSB 통해서 단말이 잘 들을 수 있으니 이제 단말은 보내기만 하면 됨

## Random Access Channel(RACH)

- Random Access를 원하는 단말이 요청메시지를 쓰는곳
  - 여긴 자유게시판 같은 곳이라 아무나 쓸 수 있는거
  - 근데 그렇게 간단하지 않음
- 1. 여러 명이 동시에 여기다 쓸 수도 있다.
- 2. 신호 세기가 약해서 gNB가 못들을수도 있다.

## Random-Access Protocol

- 4가지 스텝이 있음
  - Step-1 : Preamble(PRACH) transmission
  - Step-2 : Random Access Response
  - Step-3/4 : Message 3/4 are exchanged
- Random-Access Protocol이 끝나면
  - 단말은 "연결된 상태" 가 됨

## Four-step random-access procedure

<img width="259" alt="스크린샷 2023-12-14 오후 4 01 43" src="https://gist.github.com/assets/138586629/f14661c4-4169-457a-9f6d-6efeb7a8a0e6">

### Step 1: Device transmission of a preamble

"hello"

모든 단말에서 정해진 contents를 전송함.
PRACH 사이즈가 크지 않아서 많은 정보를 담지 못함

타이밍과 관련된 이슈가 있는데, gNB와 UE 사이의 거리에 따라 PRACH가 보내지는 latency가 있어서, 다음 10ms block에 보내져버리면 무시되어버려서 안됨. 그래서 PRACH도 long과 short가 있음

PBCH에 RACH의 위치에 대한 정보도 있음

### Step 2: Network Transmission of RAR(Random Access Response)

RAR를 받지 못했단 건 충분히 파워가 크지 않았거나, 충돌이 났거나 등.

gNB 입장에선 제대로 PRACH 받았다 싶으면 RAR을 보내줌 PDCCH/PDSCH를 통해.
RA-RNTI라는 id를 가짐. 단말에서는 PDCCH/PDSCH를 listen하겠지.

### Step 3/4: Device and network exchange of messages

여러 단말이 같은 셀에 송신하는 충돌을 해결함
정말 한명인지를 확인하는. Step 2까지는 주고받은 요청 단말이 하나라는 보장이 없음

- Message 3: Contention Resolution
  - RAR에서 부여된 값을 UL-SCH(PUSCH)로 Message 3를 전송함
- Message 4: Contention Resolution & Connection Set Up
  - PDDCH를 통해서 오게됨. C-RNTI라는 id로.

## 나머지는 슥 넘어가서 끝남

## Questions

- Explain Synchronous Signal Block
  - What it is. Why it is needed. How PSS/SSS/PBCH works, How often it is transmitted.
  - How SSB is related to beamforming?
- Explain Random Access Protocol
  - What it is. Why it is needed. How it works - explain Message 1/2/3/4

## Explain Synchronous Signal Block

> 동기 신호 블록에 대해 설명하라

### What it is. Why it is needed. How PSS/SSS/PBCH works, How often it is transmitted.

> 이게 뭔지. 왜 필요한지. PSS/SSS/PBCH가 어떻게 동작하는지, 얼마나 자주 송신되는지

Synchronous Signal Block(SSB). 동기 신호 블록.

1. PSS로 horizontal, vertical 오프셋 맞추고
2. PSS의 3, SSS의 336 으로 1008개중 하나인 PCI읽고
3. 나머지 PBCH부분 읽어서 CRC 체크해서 맞으면 gNB 정보 얻음

- UE 입장에서 gNB의 Cell Search를 하기 위해 있음.
- 모바일 단말은 SSB를 listen함으로써 new cell(gNB)을 찾는다.
- 다음으로 구성됨
  - PSS : Primary Synchronous Signal
  - SSS : Secondary Synchronous Signal
  - PBCH : Physical Broadcasting Channel
- DL에서 주기적으로 전달됨 20ms에 한 차례. 그런데 여러번!
  - 왜? beam sweeeping 때문

### How SSB is related to beamforming?

> SSB는 빔포밍과 어떻게 관련되어 있는가?

Beam Sweeping이라고 함.

기지국과 단말의 상대적 위치가 어디일진 알 수가 없지.
그래서 다 똑같은 SSB 8개를 보내는데 다 다른방향으로 보내.

그래서 SSB Index 0~8중 신호 세기가 어디가 센지에 따라
단말에서 기지국 위치가 어느 방향에 있는지를 알아냄!

이 8개 세트를 Burst라고 함.

## Explain Random Access Protocol

> 랜덤 액세스 프로토콜에 대해 설명하라.

### What it is. Why it is needed. How it works - explain Message 1/2/3/4

> 이게 뭔지. 왜 필요한지. 어떻게 동작하는지 - 메세지 1/2/3/4에 대해 설명하라

UE가 gNB와 제대로된 통신을 하려면 결국 gNB의 radio resource scheduling에 UE가 껴들어야 함. 그걸 위한 정해진 자유 게시판(RACH)이 있음.

Initial Access => Random Access 밖에 없음 ㅇㅇ
이제 SSB 통해서 단말이 잘 들을 수 있으니 이제 단말은 RACH에 메시지를 보내기만 하면 됨

## Random Access Channel(RACH)

- Random Access를 원하는 단말이 요청메시지를 쓰는곳
  - 여긴 자유게시판 같은 곳이라 아무나 쓸 수 있는거
  - 근데 그렇게 간단하지 않음
- 1. 여러 명이 동시에 여기다 쓸 수도 있다.
- 2. 신호 세기가 약해서 gNB가 못들을수도 있다.

## Random-Access Protocol

- 4가지 스텝이 있음
  - Step-1 : Preamble(PRACH) transmission
  - Step-2 : Random Access Response
  - Step-3/4 : Message 3/4 are exchanged
- Random-Access Protocol이 끝나면
  - 단말은 "연결된 상태" 가 됨

## Four-step random-access procedure

<img width="259" alt="스크린샷 2023-12-14 오후 4 01 43" src="https://gist.github.com/assets/138586629/f14661c4-4169-457a-9f6d-6efeb7a8a0e6">

### Step 1: Device transmission of a preamble

"hello"

모든 단말에서 정해진 contents를 전송함.
PRACH 사이즈가 크지 않아서 많은 정보를 담지 못함

타이밍과 관련된 이슈가 있는데, gNB와 UE 사이의 거리에 따라 PRACH가 보내지는 latency가 있어서, 다음 10ms block에 보내져버리면 무시되어버려서 안됨. 그래서 PRACH도 long과 short가 있음

PBCH에 RACH의 위치에 대한 정보도 있음

### Step 2: Network Transmission of RAR(Random Access Response)

RAR를 받지 못했단 건 충분히 파워가 크지 않았거나, 충돌이 났거나 등.

gNB 입장에선 제대로 PRACH 받았다 싶으면 RAR을 보내줌 PDCCH/PDSCH를 통해.
RA-RNTI라는 id를 가짐. 단말에서는 PDCCH/PDSCH를 listen하겠지.

### Step 3/4: Device and network exchange of messages

여러 단말이 같은 셀에 송신하는 충돌을 해결함
정말 한명인지를 확인하는. Step 2까지는 주고받은 요청 단말이 하나라는 보장이 없음

- Message 3: Contention Resolution
  - RAR에서 부여된 값을 UL-SCH(PUSCH)로 Message 3를 전송함
- Message 4: Contention Resolution & Connection Set Up
  - PDDCH를 통해서 오게됨. C-RNTI라는 id로.
