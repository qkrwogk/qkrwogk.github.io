# Mobility, Scheduling, QoS

## 11장에서는

주로 gNB의 스케쥴링, 그리고 그 전에 모빌리티에 대해 설명함.

# Mobility

단말의 이동성!

## 5G Network Architecture (1/2)

<img width="599" alt="스크린샷 2023-12-14 오후 4 34 33" src="https://gist.github.com/assets/138586629/bf577222-ec2f-4944-8a18-d0b28a65a8f1">

UE <-> gNB <-> Internet

WiFi와 VoIP를 통해 굳이 이동통신없어도 전화통화는 할 수 있음.
근데 왜 이동통신이 필요한가? 결국 "이동(Mobility)"때문임.

## 5G Network Architecture (2/2)

단말의 역할에 대해 정리하는 내용 ㅇㅇ

단말의 핵심은 "나는 항상 연결되어있"는 것처럼 느끼게 해줘야 함.
(실제론 한정된 자원으로 실제로 그렇게 하진 않음.)

- 파워는 항상 켜져있어야 하고
- 연결되어 있거나
- Idle 상태이거나

중요한 건 gNB도 관리를 받아야 함. 여러개의 gNB들이 서로 통신을 하면서
단말이 다른 gNB 관할로 넘어갈 때 잘 넘겨주거나 하는 등.

그래서 gNB끼리 연결된 Radio Access Network(RAN)과,
gNB 뒷단, Internet 앞단에 `Core Network`라는 게 있어야 함!!

Core Network의 역할은 크게 2가지

1. RAN(gNB들)을 제어 control 하는 역할 => Control Plane (CP)
2. 유저 데이터를 Internet으로 송수신해주는 역할 => User Plane (UP)

ㅇㅋ? 제어 평면과 유저 평면~ 4G에서는 MM이라고 하고, 5G에선 세분화되어 여러 Function들로 정의 및 구현되어 있음.

<img width="881" alt="스크린샷 2023-12-14 오후 5 06 07" src="https://gist.github.com/assets/138586629/fef9a7b8-9348-45de-8546-3ba4afd3b473">

WiFi와 이동통신의 가장 큰 차이는 또 WiFi는 일단 컴터를 쓸때만 연결하면 되는건데
이동통신은 always-connected가 필요함. "언제 전화가 올 지 모르기 때문에!"

그래서 기지국(gNB)가 단말을 깨우는 게 가능해야 함.
그래서 전원이 켜져있으면 항상 idle 상태로 기본적인 listen을 하고, 제대로 된 연결 상태를 따로 만들어두는 그런 식임.

idle => connected와 disconnected의 중간상태라고 보면 됨

`RAN`, `CP`, `UP` 이 세개가 제일 핵심 개념이니까 익숙해지세요.

## What UE needs to do

=> "to think that I am always connected"
나는 항상 연결되어 있다고 생각하게 끔 해야함.

뭐 물론 진짜 항상 연결할 수도 있겠지만 radio resource도 낭비되고
단말의 전력문제도 있을거고 ㅇㅇ 그러니까 그 안에서 효율을 찾아야지.

<img width="876" alt="스크린샷 2023-12-14 오후 5 23 59" src="https://gist.github.com/assets/138586629/6fbae87b-a956-4bfc-839f-82eecb5550dc">

mobility때문에, 단말이 연결하는 gNB를 전환해야 할(handover) 상황이 생김.
그래서 gNB끼리는 RAN으로 연결되어 있고. 그 통신 인터페이스를 X2 인터페이스라함.
"X2 handover"

- In connection
  - 단말은 계속 더 강한 gNB를 찾음
  - 만약 더 나은 gNB를 찾으면, RACH로 handover를 요청함
  - 만약 새로운 gNB가 수락하면, 옛날 gNB에게 X2 handover를 요청함

## UE's states

- Power-OFF
- Power-ON
  - Not-Registered
  - Registered
    - Connected (RRC_CONNECTED)
    - Not Connected (RRC_IDLE)

## More details on Connection Setup, Mobility and Security

- NAS(Non-Access Stratum)
  - 단말과 AMF간의 통신
- RRC(Radio-Resource Control) = AS(Access Staratum)
  - 단말과 gNB와의 통신

## RRC State Machine

- RRC_IDLE
- RRC_CONNECTED
- RRC_INACTIVE : IDLE과 CONNECTED의 중간 단계

## ISSUE

- RRC_INACTIVE -> RRC_CONNECTED
  - 왜 gNB가 paging 이후에도 "Random Access"를 해야 하나?
    - paging은 여러 gNB가 보낼 수 있음
    - Rnadom Access : 하나의 UE가 하나의 gNB에만 접속 시도

## Paging in RRC_IDLE & RRC_INACTIVE

- Paging 메시지 = saying "일어나 & 너의 가장 가까운 gNB에 연락해"
  - 이것이 여러 gNB로부터 전송된다. (RAN area 또는 Tracking area, UE 주변)

## Connected-State Mobility

"X2 interface를 통해"

- 목표 : 방해없이, RAN 네트워크 내에서 단말이 이동해도 계속 연결될 수 있게.
- core network는 모르게 한다.

### Part1 요약

뭐 대충 Part1에선 모빌리티를 달성하기 위해
단말이 뭘 해줘야 하는지를 설명했음.

Part2 내용은 이제 gNB 입장에서 어떻게 스케쥴링을 하고 어찌저찌하는지를 배워보겠음ㅇㅇ

# Scheduling

![스크린샷 2023-12-14 오후 7 50 17](https://gist.github.com/assets/138586629/e4b12d80-6a11-456b-bbc2-801f8c6859fb)

결국 gNB가 가장 메인으로 해주는 일은 **Radio Resource를 관리**하는 일임

- PDSCH를 통해, 무선자원을 보내고/받고
  - CP, UP로 보내고
  - UE에게서 받고 (self resolve, transfer to UP/CP)

QoS얘기도 잠깐 하자면 (Quality of Service)
품질 관리를 해야한단 건데, gNB가 UP로부터 데이터를 받을때,
"이 데이터를 이 UE에 보내줘. 근데 이런이런 데이터 특성이 있으니까 이런 특성을 고려해서 요러요러하게 스케쥴링 해줘봐" 이런 정보를 규격화해서 테이블로 만들어놓음.

delay가 엄청 작아야 한다, error rate은 어느정도 높아도 된다 등등

## DCI(Downlink Control Information) Multiplexing on PDSCH

![스크린샷 2023-12-14 오후 7 57 38](https://gist.github.com/assets/138586629/c6a2ae83-6ac4-4578-a484-bfafb9c699e7)

## UCI (Uplink Control Information) Multiplexing on PUSCH

![스크린샷 2023-12-14 오후 8 01 04](https://gist.github.com/assets/138586629/6c3b2fae-6df1-4c9e-ac41-63ef2287247f)

보통은 PUCCH로 하겠지만 HARQ-ACK, CSI 이런걸 PUSCH로도 전송 가능하다 정도만 알아두셈

## Radio Channel <- 대충 Scheduling에 대한 전반적인 설명을 드리겠음

채널의 gain이 좋아졌다 나빠졌다 하는게 1초동안에 엄청 왔다갔다함 (signal power가)

range도 굉장히 크고(widely), 퀄리티 변화도 굉장히 빠름(Fastly)

fading channel.

## Opportunistic Scheduling

무선 채널이 퀄리티가 좋고 나쁜거를 오히려 기회(opportunistic)라고 생각한다.

<img width="524" alt="스크린샷 2023-12-14 오후 8 10 12" src="https://gist.github.com/assets/138586629/606c70a3-9061-42de-87e4-a9eb618a3689">

기회를 봐서 ㅇㅇ 채널 상태를 봐서 기다려서 채널 상태가 좋은 유저한테 우선적으로
보내주는 식으로 스케쥴링을 하는거임.

## Spectral Efficiency and Fairness are Opposite Goals

단말-기지국의 채널 상태는 다 좋고 나쁘고 하는데요. 근데 또 단말 위치에 따라
계속 상태가 안좋을 수 있잖아. 그래서 spectral efficiency만 생각하면
그렇게 스케쥴링이 공평해질 수 없음.

신호 대 잡음비만 보고 하는건 오히려 쉽지만 사용자들에겐 공평하지 않으니까

## Proportional Fair (PF) Scheduler

그래서 나온게 이거임. 메인 아이디어 :
Maximize "the product of data rates of user." 유저 데이터 rate의 곱을 보자

메인 구현방식 :

1. channel quality의 이력을 각 유저들로부터 보고받아.
2. 그 다음 현재 이 유저의 channel quality가 전체 이력중 얼마나 좋은 상태인지 계산
3. 그래서 절대적으로 높은 퀄리티가 아니라, 각 유저의 상대적인 퀄리티로 우선순위 부여

- 3G때부터 사실상 표준으로 사용중

# Dynamic DL Scheduling

## PDCCH and CORESET

문제가 있는데 5G NR에서는, 대역폭(bandwidth)이 커짐에 따라,
gNB가 전체 대역폭을 BWP(Bandwidth Parts)로 나누고,
UE를 또 그룹핑해가지고 좋은 모델이나 안좋은 모델 이렇게 나누고,
어떤 UE가 어떤 대역폭안에서 할당할 건지를 전체 slot에서 좀 나누는 단위라고 하나

이게 a Control Resource Set(CORESET)이라는 개념임

## How PDCCH is sent

PDCCH를 어케 보내느냐

![스크린샷 2023-12-14 오후 8 26 18](https://gist.github.com/assets/138586629/9afa4aaa-29c1-4a9e-b560-a99dc2f4b2d7)

CRC 본연의 error detection 역할을 하면서
RNTI masking을 통해 누가 보냈는지를 도청당해도 알려지지 않는~

이런 나이스한 방식이다~ 그렇대 ㅇㅇ

## 이 뒤론 샤샥 넘어감

### downlink preemption - motivation

1ms = 14 OFDM symbols잖아? LTE의 경우 15kHz, 1msec 14 OFDM symbols

근데 5G에서 60kHz까지 가면 딜레이가 문제가 된다 했잖아.

그래서 downlink preemption이 뭐냐면, latency-critical한 data가 있으면
즉각적으로 그 단말(B)에 scheduled 될 수도 있다. (A에 보내는 데이터 위에)

근데 A는 데이터를.. 어떻게 받겠어 CRC도 HARQ도 안되겠지 그러면 뭐 다시요청하겠지
ㅋ ㅋ 쏘리쏘리~

### Uplink Scheduling by gNB

UE한테 물어봄. 너 보낼 데이터(buffer state)가 있는지,
충분한 파워로 보낼 수 있는지(power headroom) 등등

### PUCCH

크게 변한 건 없음. UCI(Uplink Control Information)이 여기에 담기는데
UCI는 PUCCH 뿐만 아니라 PUSCH에도 담길 수 있음
DCI는 반면에 PDCCH를 통해서만 전해짐

### UL Grant ...

뭐 다 대충 넘어감. 결국 QoS는 설명 못했네 다음시간에 ㄱㄱ

## Questions

- Explain handover procedure when
  - UE is in idle
  - UE is in connection
- Explain the mobile station operation in the idle state
  - Explain Control Plane and User Plane
- Explain opportunistic scheduling and proportional fair scheduler
- Why RNTI is exclusive OR-ed with CRC of PDCCH?
- What is CORESET and why is it needed?

## Explain handover procedure when

> 다음 상황에서의 핸드오버(양도) 절차에 대해 설명하라

```
단말은 사용자가 "언제나 연결된 것 처럼" 생각되길 원하기 때문에, 연결 상태에서는 항상 더 나은 gNB를 찾아 갈아타고, idle 상태에서도 그러함.
```

### UE is in idle

> UE가 idle 상태일 때

```
일단 UE는 User Equipment. 사용자 단말

- Power-OFF
- Power-ON
  - not-registered (등록 안됨, 긴급통화만됨)
  - registered (등록, USIM필요)
    - connected (rrc_connected)
    - not connected (rrc_idle)

이제 idle상태(연결 안돼있을 때)

단말이 "나는 항상 연결되어 있어"라고 느끼게 하려면 Registered 상태에서 연결 안돼있어도 신경을 써줘야 함.

#### RRC_IDLE

- 특정한 셀에 종속되어있지 않다(gNB에서 관리안한다). 그치만 코어 네트웤에선 idle인 애들이구나 하고 관리함
- 페이징 메시지를 주기적으로 체크하고, 여러 gNB로 계속 보내짐
- 랜덤 액세스를 통해 RRC_CONNECTED로 갈 수 있음
```

### UE is in connection

> UE가 연결되어 있을 때

```
#### RRC_CONNECTED

- RRC context가 수립되고, 코어 네트워크도 얘가 active구나 하고 알고 있음
  - CN_CONNECTED (CN은 코어 네트워크)
- C-RNTI가 할당됨

#### RRC_INACTIVE

RRC_IDLE과 RRC_CONNECTED의 중간 상태
```

## Explain the mobile station operation in the idle state

> idle 상태일 때의 모바일 기지국 운용에 대해 설명하라

```
idle 상태일 때도 paging message를 받을 준비를 하고 있음. 그러니 특정 cell에 연결되어 있진 않지만, CN에서는 idle인 단말을 관리함.

UE는 idle 상태일 때도 gNB가 paging message를 보낼 수 있게 device report를 gNB에게 보냄
```

### Explain Control Plane and User Plane

> 컨트롤 플레인(제어 평면), 유저 플레인에 대해 설명하라

```
단말의 역할에 대해 정리하는 내용 ㅇㅇ

단말의 핵심은 "나는 항상 연결되어있"는 것처럼 느끼게 해줘야 함.
(실제론 한정된 자원으로 실제로 그렇게 하진 않음.)

- 파워는 항상 켜져있어야 하고
- 연결되어 있거나
- Idle 상태이거나

중요한 건 gNB도 관리를 받아야 함. 여러개의 gNB들이 서로 통신을 하면서
단말이 다른 gNB 관할로 넘어갈 때 잘 넘겨주거나 하는 등.

그래서 gNB끼리 연결된 Radio Access Network(RAN)과,
gNB 뒷단, Internet 앞단에 `Core Network`라는 게 있어야 함!!

Core Network의 역할은 크게 2가지

1. RAN(gNB들)을 제어 control 하는 역할 => Control Plane (CP)
2. 유저 데이터를 Internet으로 송수신해주는 역할 => User Plane (UP)

ㅇㅋ? 제어 평면과 유저 평면~ 4G에서는 MM이라고 하고, 5G에선 세분화되어 여러 Function들로 정의 및 구현되어 있음.

<img width="881" alt="스크린샷 2023-12-14 오후 5 06 07" src="https://gist.github.com/assets/138586629/fef9a7b8-9348-45de-8546-3ba4afd3b473">

WiFi와 이동통신의 가장 큰 차이는 또 WiFi는 일단 컴터를 쓸때만 연결하면 되는건데
이동통신은 always-connected가 필요함. "언제 전화가 올 지 모르기 때문에!"

그래서 기지국(gNB)가 단말을 깨우는 게 가능해야 함.
그래서 전원이 켜져있으면 항상 idle 상태로 기본적인 listen을 하고, 제대로 된 연결 상태를 따로 만들어두는 그런 식임.

idle => connected와 disconnected의 중간상태라고 보면 됨

`RAN`, `CP`, `UP` 이 세개가 제일 핵심 개념이니까 익숙해지세요.
```

## Explain opportunistic scheduling and proportional fair scheduler

> 기회주의적 스케줄링과 비례 공정 스케줄러에 대해 설명하라

```
채널의 gain이 좋아졌다 나빠졌다 하는게 1초동안에 엄청 왔다갔다함 (signal power가)

range도 굉장히 크고(widely), 퀄리티 변화도 굉장히 빠름(Fastly)

fading channel.

## Opportunistic Scheduling

무선 채널이 퀄리티가 좋고 나쁜거를 오히려 기회(opportunistic)라고 생각한다.

<img width="524" alt="스크린샷 2023-12-14 오후 8 10 12" src="https://gist.github.com/assets/138586629/606c70a3-9061-42de-87e4-a9eb618a3689">

기회를 봐서 ㅇㅇ 채널 상태를 봐서 기다려서 채널 상태가 좋은 유저한테 우선적으로
보내주는 식으로 스케쥴링을 하는거임.

## Spectral Efficiency and Fairness are Opposite Goals

단말-기지국의 채널 상태는 다 좋고 나쁘고 하는데요. 근데 또 단말 위치에 따라
계속 상태가 안좋을 수 있잖아. 그래서 spectral efficiency만 생각하면
그렇게 스케쥴링이 공평해질 수 없음.

신호 대 잡음비만 보고 하는건 오히려 쉽지만 사용자들에겐 공평하지 않으니까

## Proportional Fair (PF) Scheduler

그래서 나온게 이거임. 메인 아이디어 :
Maximize "the product of data rates of user." 유저 데이터 rate의 곱을 보자

메인 구현방식 :

1. channel quality의 이력을 각 유저들로부터 보고받아.
2. 그 다음 현재 이 유저의 channel quality가 전체 이력중 얼마나 좋은 상태인지 계산
3. 그래서 절대적으로 높은 퀄리티가 아니라, 각 유저의 상대적인 퀄리티로 우선순위 부여

- 3G때부터 사실상 표준으로 사용중
```

## Why RNTI is exclusive OR-ed with CRC of PDCCH?

> 왜 RNTI는 PDCCH의 CRC와 XOR되는가?

<img width="667" alt="스크린샷 2023-12-15 오후 10 34 29" src="https://gist.github.com/assets/138586629/9bd7b240-3537-4ba8-81e0-4628353c2263">

```
PDCCH에서는 DCI(Downlink Control Information)를 보내는데,

CRC XOR RNTI(UE Identifier)를 통해 CRC 본연의 error detection 역할도 하면서, 특정 UE가 자신의 PDCCH만 받아볼 수 있도록 하는 접근제어의 역할도 같이 해주는 1석2조 효과.

본인 RNTI를 알아야 CRC 체크섬도 알 수 있으니까!
```

## What is CORESET and why is it needed?

> CORESET이란 무엇이고, 왜 필요한가?

```
5G NR에서는, 대역폭(bandwidth)이 커짐에 따라,
gNB가 전체 대역폭을 BWP(Bandwidth Parts)로 나누고,
UE를 또 그룹핑해가지고 좋은 모델이나 안좋은 모델 이렇게 나누고,
어떤 UE가 어떤 대역폭안에서 할당할 건지를 전체 slot에서 좀 나누는 단위라고 하나

이게 a Control Resource Set(CORESET)이라는 개념임

CORESET은 특정 단말이 전체가 아닌 특정 Control Channel에서 내 값을 찾을 수 있도록 time-frequency resource 쪼개놓은 단위라고 보면 됨
```
