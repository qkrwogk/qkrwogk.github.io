# Radio Protocol

## 12주차

이제 Upper Layer의 Protocol들에 대해서 설명할거임

- 1~10까지가 UE <-> gNB 간의 통신
- 11을 통해 Mobility를 통해 이동하며 통신가능(gNB 간의 네트워크가 있다. RAN)
- 12는 PHY Layer말고 그 위의 Layer들
- 13은 재밌음. 진정한 5G 네트워크는 오지 않았다. EN-DC(5G와 4G의 이상한 만남)
- 14~15는 진정한 5G. 5GC=5G Core Network

컨텐츠 of "Radio Protocol Architecture"

- User-Plane Protocols
  - SDAP
  - PDCP
  - RLC
  - MAC
  - PHY Layer
- Control-Plane Protocols
  - RRC State Machine
  - Idle-State and Inactivity-State Mobility
  - Connected-State Mobility
- RAN Functionality Split (Open RAN)
  - 이 gNB의 기능들을 모두 공개하고 기능적으로 분리!

## 12주차, 다시

![스크린샷 2023-12-14 오후 8 47 36](https://gist.github.com/assets/138586629/fb0e8604-e5f4-49d1-be91-ecbb0b477b6a)

RAN이 사실은 gNB(RRU) 뿐만 아니라, CU, DU도 있음

어떤 데이터가 실제로 전송되어야 하는지(UP/CP data)

PDSCH/PUSCH & PDCCH/PUSCH에 더불어, 어떻게 연결이 셋업되고 실제로 어떤 데이터가 오가는지

- Upper-Layer Radio Protocols
- RAN and Core Network

## How does the Core Network look?

![스크린샷 2023-12-14 오후 8 51 34](https://gist.github.com/assets/138586629/27a16f97-2b01-4500-8e05-750fef17dc1b)

![스크린샷 2023-12-14 오후 8 54 16](https://gist.github.com/assets/138586629/3ccecbe5-4c22-4223-a1f0-6dd1a0c7cff8)

## Service-Based Architecture

<img width="658" alt="스크린샷 2023-12-14 오후 8 55 59" src="https://gist.github.com/assets/138586629/66118a5b-e27e-4740-89fe-3c58fbd4bca7">

자. 이런식으로 5G는 구성된다. 서비스 기반으로.

UE, NG-RAN, CPF(AMF, SMF, ...), UPF, DN

# Radio Protocol Architecture

- 어떻게 데이터가 송수신되나?
- PDCCH/PDSCH/PUSCH/PUSCH 전후로 데이터는 어떻게 구성되는가?

## Radio Protocol Stack

![스크린샷 2023-12-14 오후 9 04 06](https://gist.github.com/assets/138586629/26ded36e-22cd-47f0-8dc8-ae87f48ffc94)

gNB상에서 스케쥴링이 되면, SDAP을 통해서 적절한 QoS flow로 UPF로 전달을 하게 됩니다.

UPF는 IP(Internet Packet)을 전달하게 되는데, gNB에서 이걸 또 SDAP부터 샤샤샤샥 해서 Physical Layer에 있는 symbol로 변환돼서 UE로 최종적으로 전달하게 됩니다.

RRC는 뭐냐면 radio resource에대한 control에 대한 정보들. 이런건 사용자 데이터가 아니잖아? 그래서 CP에 있는거임. scheduling을 어떻게 해야하겠다 통신상태는 어떻다 이런~~ 얘는 SDAP을 통하지 않음

아무튼 UP, CP는 각각 SDAP, RRC를 통해서 통신하는데, 그 아래 레이어에 PDCP, RLC, MAC, PHY는 공통이다 이말씀.

SNS 메시지를 보내고싶은데 연결이 안돼있어. 왜냐 나(UE)를 관리하는 gNB가 없으니까. 그럼 paging message를 gNB들에게 뿌리고, 상태 보고 random access를 해서, 그 뒤에 연결이 되면 그때 데이터 송수신이 가능함.
결과적으로 이것도 AMF가 있어야 가능한거임 이것이 NAS(Non-Access Stratum)

## Quick Overview of Radio Protocol Stack

- protocol stack이란 protocol들의 집합!
  - PHY, MAC, RLC, PDCP, SDAP/RRC 각각 역할이 있음
  - C가 되려면 B가 되어야하고 B가 되려면 A가 되어야 하고 이런 의존관계가 있어서 이것이 Hierarchy 구조가 된 것.
  - 일반적으로 PHY 외엔 대부분 SW로 구현됨.
- User Plane and Control Plane
  - Data/Traffic - User Plane
  - Signaling/Overhead Message - Control Plane

## 5G NR DL UP Protocol -> 왜 이렇게 많은 레이어가 필요한가

<img width="596" alt="스크린샷 2023-12-14 오후 9 17 59" src="https://gist.github.com/assets/138586629/9595a3af-1c60-41bd-b438-625ca4ff0d45">

**중요**

- Hybrid ARQ(HARQ)가 계속 성공 못하면?
  - retransmission 시도의 최댓값을 정해야 함
  - 그래서 나중에 다시 시도하거나 문제를 고치도록 "RLC" 레이어 SW가 필요함
- IP 패킷을 송수신해야하지만, PDCCH/PDSCH는 무선 채널 환경에서만 정의되어 있음
  - IP 패킷으로 변환(convert)하도록 "PDCP" 레이어 SW가 필요함
- SNS, 통화, 스트리밍 등 서로 다른 성격의 통신이 있을거아냐? 하나의 단말에서? 동시다발적으로?
  - 그래서 이를 구별해주기 위해 "SDAP" 레이어 SW가 필요함

**중요**

## User-Plane Data Flow Example

유튜브와 SNS txt 통신을 동시에 한다고 쳐.
그럼 이걸 Logically해서 구별을 해줘.

이렇게 통신 타입별로 구분된 Logical 채널을 `Radio Bearer`라고 함.

![스크린샷 2023-12-14 오후 9 20 15](https://gist.github.com/assets/138586629/c32d5c1c-699d-4f20-8627-5ead4d2da3d6)

근데 또 보면 MAC 레이어 아래로는 그런걸 구분하지 않음

그냥 통신 상태에 따라 붙여서 전송 ㅇㅇ

RLC에서도 마찬가지로 쪼개서 전송할수도 있는거고.

그러니까 서로 다른 레이어들의 동작에 대해서는 신경쓰지 않음.
이것이 역할의 분리 이것이 계층구조

# User-Plane Protocols

SDAP, PDCP, RLC에 대해 주로 설명하겠음
MAC, PHY는 이미 설명했으니까

## Service Data Adaptation Protocol (SDAP)

UE <-> gNB <-> UPF
Core Network 중에서도 UPF! 와 하는 통신

QoS flow(from 5GC)와 Radio Bearer를 매핑함

<img width="650" alt="스크린샷 2023-12-14 오후 9 25 48" src="https://gist.github.com/assets/138586629/e9d4a1cc-ed82-495c-8003-f95fe35b1583">

QoS flow와 Radio bearer가 무조건 매치되지 않을 수도 있음. 이것은 SMF에서 설명할거임

## Packet Data Convergence Protocol (PDCP)

PDCP는 내용까지 관장을 해서, duplicated됐다면 없애주고, handover 된다면 뭐 처리해주고

- ROHC를 통한 IP 헤더 압축
- 암호화, 무결성 보호
- Duplicate Removal, IP 패킷의 순서 처리
  - duplicate는 handover시 발생할 수 있다 이말씀

### Dual Connectivity with Split Bearer

PDCP의 더 중요한 건 이거임. Dual Connectivity (다음 시간인 EN-DC에서 다룰 내용)

단말 하나에 대해서 LTE + 5GNR을 동시에 연결한 상태면,
PDCP가 이걸 담당을 해 준다.

<img width="515" alt="스크린샷 2023-12-14 오후 9 32 05" src="https://gist.github.com/assets/138586629/a3ad9459-b1df-4c72-ab43-dcd8c5740b6f">

## Radio-Link Control (RLC)

얘는 그야말로 bytes를 보내줌.

IP 패킷인지 아닌지, 암호, 무결성 보호.. 이런거 신경안씀

MAC/PHY 프로토콜, PLC 프로토콜을 사용하니
스케쥴링, PDCCH, 뭐 이런것도 신경 안씀 "그냥 bytes 송수신"

- RLC는 그냥 나름대로
  - RLC PDU만큼 보내!(정해진 사이즈)
  - RLC PDU만큼 보낼게!(정해진 사이즈)
  - 수신측에서는 RLC단에서 재전송을 요청할 수도 있음

그래서 PDU(Protocol Data Unit) 사이즈랑 SDU(Service Data Unit) 사이즈가 다르니 뭐 쪼개지기도 하고, 합쳐지기도 하고 하겠지?

그냥 데이터의 전송효율때문에 정해진 사이즈만큼 Data Unit(IP에서 패킷같이)을 구성한다고 생각하면 될듯?

## Medium-Access Control & Physical Layer

<img width="414" alt="스크린샷 2023-12-14 오후 9 37 53" src="https://gist.github.com/assets/138586629/01b03efe-1094-412e-b4c6-2b2cda82f941">

- MAC 레이어에서는
  - CA(Carrier Aggregation) => 다음시간에
- PHY 레이어에서는
  - 이전에 다 배운것들 ㅇㅇ

## Logical & Transport Channels

- Logical Channel -> RLC layer
- Transport Channel -> MAC layer
- Physical Channel -> PHY layer

<img width="615" alt="스크린샷 2023-12-14 오후 9 39 01" src="https://gist.github.com/assets/138586629/ea793b36-83b6-4295-9e4a-0d6e2bbf5670">

레이어에 따라 다루는 채널들이 다르기 때문에, 각 레이어에 따라서 RLC면 Logical 채널이라 부르고, MAC이면 Transport ... 암튼 이렇게 부른다고 ㅇㅇ

## Multiple Parallel Hybrid ARQ(H-ARQ)

이건 생략 ... 하려다가 다시 ㄱ

<img width="627" alt="스크린샷 2023-12-14 오후 10 41 20" src="https://gist.github.com/assets/138586629/5273513e-1f95-4018-b128-ee0462472ae3">

multiple stop & wait protocol에 대해 알아보자.

Tx -> Rx -> Tx 전송시간 때문에 빈 공간이 많아지잖아.
그래서 Multiple H-ARQ channels를 사용해서
언제 올지 모르는 애들을 기다리지 않고 계속 보내

ACK만 받으면 좋겠지만, NACK이면 다시 전송하고 하겠지
그렇게 순서가 바뀌게 될 수도 있으니 이 순서를 다시 맞춰주는 것도 필요할거임

이런게 RLC에서 사용해주는 것이다.
retransmission관리, 순서(in-sequence) 관리

# Control-Plane Protocols

비슷한 거라도 살짝 다르니 다시 다루어보자.

- RRC State Machine
- Idle-State and Inactivity-State Mobility
- Connected-State Mobility

CP에서는 유저 데이터가 아니니까 QoS같은걸 관리할 필요가 없음. 대신 UE와 gNB간에 "나 16QAM이상은 해석못하니까 주지 마세요, 너 통신상태 안좋으니까 얼마이상 리소스 할당 안할거야" 같은 Control 데이터가 필요함. 이런걸 RRC에서 하는거임

## More details on Conntection Setup, Mobility and Security

- NAS(Non-Access Stratum)

  - UE와 AMF간의 통신
  - gNB의 개입은 없지만 결국 gNB를 통해서 전달됨
  - 다음을 담당함
    - Authentication
    - Security
    - Idle-mode 프로시저 (페이징 등)
    - IP 주소 할당

- RRC(Radio-Resource Control) = AS
  - UE와 gNB간의 통신
  - 연결된 단말의 RAN과 관련된 프로시저를 담당함
    - 시스템 정보 브로드캐스트와 획득
    - 페이징 메시지 전송
    - configuration & reporting..

## RRC State Machine (device states per traffic activity)

- RRC_IDLE
  - device-controlled mobility
    - 단말이 "여기 뭐 좋은 gNB 없나~"
- RRC_INACTIVE
- RRC_CONNECTED
  - network-conrolled mobility
    - gNB에 의해 "너 이쪽으로 handover해!"

가장 중요한건 현재 dedicated된 radio resource가 있냐 없냐임. IDLE일땐 없음

CONNECTED일 땐 C-RNTI 할당 => UL/DL를 위한 임시 ID
C-RNTI(C-Radio Network Temporary ID)

## Mobility

이직준비하는 직장인마냥 언제나 gNB 갈아탈 준비를 한다.

## Cell Reselection in RRC_IDLE && RRC_INACTIVE

UE가 주기적으로 난 어디있어요~ 뭐 이런거 하면 gNB가

## Paging in RRC_IDLE && RRC_INACTIVE

...

## Connected_State Mobility

단말은 연결 중에도 항상 새로운 gNB를 찾느라 바빠.
가끔 gNB는 이웃 cell들에 대한 정보를 소개해 주기도 한다.

## LTE and 5G NR Protocol Aspects

결론적으로 오늘 배운 PDCP, RLC, MAC, PHY는 공통!
UP에선 SDAP, CP에선 RRC + NAS!

# RAN Functionality Split

이제까지는 RAN이 gNB들의 집합인것처럼 설명했죠?
뭐 gNB가 리소스를 알아서 관리하고~

실제로는

- CU(Central Unit)
- DU(Distributed Unit)
- RRU(Radio Resource Unit)

요런식으로 나뉘어져서 지역별로 관리되는 식이거든?

근데 gNB <-> UE 인터페이스는 표준이 정해져 있는데,
gNB 안에서는 걍 제조사가 알아서 하는 부분이였거든?

근데 그 안에서의 특정 process의 인터페이스를 표준화시키면,
서로 다른 supplier에서 부품을 다양하게 수급할 수 있어!
그렇게 표준화시켜서 오픈하는 것을 open RAN이라고 합니다.

이게 요즘 굉장히 핫합니다.

화웨이가 가격도 싸고 성능이 좋은데,
언제까지 쌀지 모르잖아 독점이 되어버리면! (보안 문제도 있고)

그래서 위 처럼 Layer마다 인터페이스 표준을 정해버리면
이통사 입장에서 Vendor를 다각화시킬 수 있고
그를 통해 경쟁입찰제로 가격도 더 다운시킬 수 있을거다!

<img width="717" alt="스크린샷 2023-12-14 오후 11 11 58" src="https://gist.github.com/assets/138586629/61ec65b6-e23b-4a62-a0b1-13821a585212">

뭐 그렇다 ㅇㅇ

## User Plane Protocol Stacks

- UE <-> gNB
  - RRC/SDAP - PDCP - RLC - MAC - PHY
- gNB <-> UPF
  - IP기반 전송 네트워크 표준 스택을 따름
  - GPRS Tunneling Protocol
    - User Plane(GTP-U)/UDP/TCP/IP/ETH/L1
- WWW서버와 연결되었다면, http 패킷을 만들거고, 그러면 UPF <-> WWW서버와의 연결은
  - HTTP/TCP/IP/.../L1 프로토콜 스택을 따른거임!

## High-Layer Split (HLS)

PDCP와 High RLC 사이를 나누는 것

## Lower-Layer Split (LLS)

- High-PHY와 Low-PHY를 분리시키는 거임 RAN Functional Split 중에서.
- 표준은 evolved Common Public Radio Interface(eCPRI)

## 정리 (OFDM Block Diagram)

<img width="588" alt="스크린샷 2023-12-14 오후 11 21 45" src="https://gist.github.com/assets/138586629/fd1126bf-1d2e-443f-bf51-5b43d55f6bdd">

여기서 A파트 부분은 하드웨어 없이 Cloud에서 가상화 시킬 수 있겠다 이말씀이야!

요즘 이게 대세래 ㅇㅇ Virtual RAN이라 함
Physical하게 구현해야 하는 부분을 최대한 줄이는 것

## Questions

- How User Equipment is connected to the Data Network in 5G Mobile Communication System and why is it different from WiFi?
- Explain User Plane and Control Plane
- What is the protocol “stack” – the layered structure and why is it described so
- Explain each 5G NR radio protocol layer’s functions
- Explain dual connectivity with bearer split – (More on week-13)
- Explain multiple ARQ channels and RLC
- Explain RRC and NA stratum
- Explain RAN functionality split

![스크린샷 2023-12-10 오후 9 43 34](https://gist.github.com/assets/138586629/247c1f40-bd47-470f-a014-bc24ba45164f)

## How User Equipment is connected to the Data Network in 5G Mobile Communication System and why is it different from WiFi?

> 5G 모바일 통신에서 어떻게 사용자의 장비가 데이터 네트워크에 연결되는지, 그리고 WiFi와 어떻게 다른지 설명하라

```
UE는 "항상 연결이 되어있기"를 바람
그래서 이게 좀 복잡한데 단말도 해야할일이 많음.
항상 gNB를 listen해줘야하고,
만약 단말이 위치를 이동하면, 그걸 근처 기지국에
알리고 뭐시기저시기 ㅇㅇ

아무튼 "always connected"를 달성하기 위해서
Control Plane까지의 통신 등으로,
어마어마한 인프라스트럭쳐로 많은 역할들을 해줘야함.

와이파이는 컴퓨터는 랜선으로 연결하고 있는데,
이걸 거실에서 랩탑에서도 하고싶다. 여기서 시작한거임. 전화가 항상 올 수 있다.
그래서 뭐랄까 훨씬 단순한가봄? ㅇㅇ
```

## Explain User Plane and Control Plane

> 유저 플레인, 컨트롤 플레인에 대해 설명하라

![스크린샷 2023-12-10 오후 9 43 34](https://gist.github.com/assets/138586629/247c1f40-bd47-470f-a014-bc24ba45164f)

### 유저 플레인 Data Flow 예시

<img width="488" alt="스크린샷 2023-12-11 오전 11 39 33" src="https://gist.github.com/assets/138586629/aa5977d9-1dca-4f19-89f6-2e5605f490ad">

- User-Plan Protocols
  - SDAP : Service Data Adaptation Protocol
    - QoS flow와 Radio Bearer를 연결(mapping)해주는 역할
      <img width="511" alt="스크린샷 2023-12-11 오전 11 42 02" src="https://gist.github.com/assets/138586629/9bb7be77-e103-4138-9744-156413ebd0a0">
  - PDCP
  - RLC
  - MAC
  - PHY Lauer

## What is the protocol “stack” – the layered structure and why is it described so

> 프로토콜 "스택"이 무엇인가? - 계층 구조와 왜 이렇게 표현되는지

<img width="673" alt="스크린샷 2023-12-11 오전 11 46 35" src="https://gist.github.com/assets/138586629/ee80401d-dc5d-4bb6-aba5-3544f6ae3ed4">

- 계층적으로 NAS, RRC, SDAP, PDCP, RLC, MAC, PHY 레이어로 나누어져있음
- User / Control Plane 영역으로 횡방향으로 나뉨
  - Data/Traffic -> User Plane
  - Signaling/Overhead Message -> Control Plane

<img width="671" alt="스크린샷 2023-12-11 오전 11 47 26" src="https://gist.github.com/assets/138586629/42168185-eb3c-4c38-be2d-cb8d67bcd471">

- "프로토콜 스택"이란 컴퓨터 네트워킹 프로토콜 집합, 프로토콜 패밀리의 구현체임.
  - 무슨 말이냐면 `OSI 7 Layer`처럼 각 레이어가 하나의 목적으로 하나의 역할을 하도록 **디자인을 단순화**시켜서 분리하는 것.
  - 낮은 계층의 프로토콜은 Low-level(더 하드웨어와 가까운) interaction을 담당한다고 보면 됨. PHY, MAC
- 공통 영역은 PDCP, RLC, MAC, PHY 까지로 보면 됨
  - User Plane은 그 위에 SDAP
  - Control Plane은 그 위에 NAS, RRC가 추가됨

## Explain each 5G NR radio protocol layer’s functions

> 각 5G NR 무선 프로토콜 레이어의 functions에 대해 설명하라

### SDAP: Service Data Adaptation Protocol

- QoS flow와 Radio Bearer를 연결(mapping)해주는 역할

### PDCP: Packet Data Convergence Protocol

- ROHC를 이용한 IP 헤더 압축
- 암호화, 무결성 보호
- IP 패킷의 사본 삭제, in-sequence 전송

### RLC: Radio-Link Control

- 단순하게 Bytes를 send/receive 해주는거임.
- 잘 못보내면 다시보내고 뭐 이런거 해주는거임. MAC/PHY레이어를 사용

### MAC: Medium-Access Control & PHY: Physical Layer

이때까지 계속 배웠던거임

- MAC
  - Logical-channel(RLC) multiplexing
  - H-ArQ, Scheduling
  - Carrier Aggregation을 함. 다음시간에 함
- PHY
  - 중간고사까지 계속 배웠던 것들
  - Coding, H-ARQ, Modulation, Multi-antenna processing, ..

### 정리하면

- Logical Channel -> RLC layer
  - BCCH: Broadcast Control Channel
  - PCCH: Paging Control Channel
  - CCCH: Common Control Channel
  - DCCH: Dedicated Control Channel
  - DTCH: Dedicated Traffic Channel
- Transport Channel -> MAC layer
  - BCH: Broadcast Channel
  - PCH: Paging Channel
- Physical Channel -> PHY layer
  - PDSCH : Physical Downlink Shared Channel
  - PDCCH : Physical Downlink Control Channel
  - PBCH : Physical Broadcast Channel
  - PRACH : Physical Random Access Channel
  - PUSCH : Physical Uplink Shared Channel
  - PUCCH : Physical Uplink Control Channel

<img width="1247" alt="스크린샷 2023-12-11 오후 12 28 04" src="https://gist.github.com/assets/138586629/ba8c6a56-524c-49d6-a07d-c78500c89175">

## Explain dual connectivity with bearer split – (More on week-13)

> 이중 연결과 bearer 분할에 대해 설명하라 (week13에 추가설명함)

```
이중 연결, 특히 EN-DC의 경우 4G Core(EPC)를 Master로 활용하기 때문에, Radio Bearer는 최초에 Master eNB(=LTE) 방식으로 셋업됨.
```

## Explain multiple ARQ channels and RLC

> 다중 ARQ 채널과 RLC에 대해 설명하라

### Multiple parallel H-ARQ

<img width="642" alt="스크린샷 2023-12-11 오후 12 26 29" src="https://gist.github.com/assets/138586629/e0136561-cc8d-4e80-840e-4ff15f6de5b5">

- soft-combining H-ARQ는 "multi stop-and-wait" 프로세스로 동작한다.
  - 재전송은 DL, UL에 비동기적으로 일어남
  - 16 H-ARQ 프로세스까지 지원됨

<img width="627" alt="스크린샷 2023-12-14 오후 10 41 20" src="https://gist.github.com/assets/138586629/5273513e-1f95-4018-b128-ee0462472ae3">

```
## Multiple Parallel Hybrid ARQ(H-ARQ)

이건 생략 ... 하려다가 다시 ㄱ

multiple stop & wait protocol에 대해 알아보자.

Tx -> Rx -> Tx 전송시간 때문에 빈 공간이 많아지잖아.
그래서 Multiple H-ARQ channels를 사용해서
언제 올지 모르는 애들을 기다리지 않고 계속 보내

ACK만 받으면 좋겠지만, NACK이면 다시 전송하고 하겠지
그렇게 순서가 바뀌게 될 수도 있으니 이 순서를 다시 맞춰주는 것도 필요할거임

이런게 RLC에서 사용해주는 것이다.
retransmission관리, 순서(in-sequence) 관리
```

## Explain RRC and NA stratum

> RRC와 NA 계층군에 대해 설명하라

<img width="645" alt="스크린샷 2023-12-11 오후 12 26 51" src="https://gist.github.com/assets/138586629/c9c89b53-45fe-45b2-a275-15832e1cd7ae">

- NAS(Non-Access Stratum)
  - 단말과 AMF 사이를 연결함 (gNB 없어도됨)
  - 인증, 보안, Idle모드 프로시져(페이징 등), IP주소 할당
- RRC(Radio-Resource Control)
  - = AS(Access Stratum)
  - 단말과 gNB 사이를 연결함
  - 연결된 단말의 RAN과 관련된 프로시저
    - 시스템 정보 등 브로드캐스트
    - 페이징 메시지 전송
    - 연결 관리 -> bearer & mobility 세팅 -> RRC 컨텍스트 수립
    - measurement 설정과 리포트
    - 단말의 capabilities 리포트

## Explain RAN functionality split

> RAN(Radio Access Network) 기능 분할에 대해 설명하라

<img width="627" alt="스크린샷 2023-12-11 오후 12 28 50" src="https://gist.github.com/assets/138586629/4634622b-69d6-4d1b-b0c5-cfbc1c75acf0">

- gNB는 원래 표준에서 정의하지 않음
  - 단말과 gNB사이의 통신만 정하면 되지 내부 동작은 영향을 주지 않으니까
- 하지만 gNB를 만든다고 했을 때, 장비, 성능, 비용 등 여러가지를 고려했을 때 독점하는 화웨이 등 한 회사에서 모든 것을 구매하는 것 보다,
  - 표준화해서 기능을 분리해서 안테나, Physical Layer, MAC Layer등 functaional split하면 따로따로 다른 Vendor사에서 살 수 있음!
- 그러면 이통사업자들이 Vendor사를 다각화 시킬 수 있고, 그러면 경쟁구도가 생기면서

  - 후발주자들고 판매할 기회를 얻고, 이통사업자들도 경쟁으로 더 저렴한 가격에 gNB를 구성할 수 있을거임

- 기존의 RAN 아키텍처는 Baseband Unit(BBU)가 모든 RAN 프로토콜 스택을 구현함
- 5G 표준에서, 이 RAN 기능을 쪼개자는 의견이 3GPP에서 다루어졌고, 배포의 유연함과 효율성을 위함임. CU(Central Unit), DU(Distributed/Data Unit), RU(Radio Unit) 이렇게 나누어진다나

- virtual RAN이라고 요즘 핫한 이슈임

### 추가

- OFDM Block Diagram

<img width="1185" alt="스크린샷 2023-12-11 오후 12 46 38" src="https://gist.github.com/assets/138586629/9360bcd8-23ac-4f48-97bf-72baac3b5a5d">

- 이번 시간과 다음 시간

<img width="442" alt="스크린샷 2023-12-11 오후 12 49 05" src="https://gist.github.com/assets/138586629/0309d223-ccf4-410e-80d6-55b0b3bad0c1">
