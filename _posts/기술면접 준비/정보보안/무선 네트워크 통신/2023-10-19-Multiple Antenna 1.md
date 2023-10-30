# 231005

MIMO (Multi-Input Multi-Output) (1/2)

## 목차

- 리뷰
- Contents
- MIMO

### MIMO (Multi-Input Multi-Output) (1/2)

- What is MIMO
- The propagation channel
- MIMO and Shannon Capacity
- **MIMO modes**
  - **Diversity**
  - **Beamforming**

### MIMO (Multi-Input Multi-Output) (2/2)

- **MIMO modes**
  - **Spatial multiplex**
- MIMO in LTE : MU-MIMO (LTE)
- MIMO in 5G NR : Massive MIMO (5G NR)

- Questions

## 리뷰

#### Review Week 1/2/3 & 5/6 – 5GNR OFDM System

<img width="1021" alt="스크린샷 2023-10-22 오후 6 08 34" src="https://user-images.githubusercontent.com/138586629/277155370-eb3016b0-dda0-4ec7-8bf4-15afdb678a01.png">

## Contents for Week 7/8

- What is MIMO
- The propagation channel
- MIMO and Shannon Capacity
- **MIMO modes**
  - **Diversity**
  - **Beamforming**
  - **Spatial multiplex**
- MU-MIMO (LTE)
- Massive MIMO (5G NR)

## MIMO

#### What is MIMO?

- Multi-Input Multi-Output (MIMO) uses arrays of multiple antennas on one or both ends of a wireless communication link to enhance signal to noise ratio, reduce fading, or to create multiple communication paths in order to significantly boost channel capacity
  - MIMO는 무선 통신 링크의 한쪽 또는 양쪽 끝에서 여러 안테나 배열을 사용하여 신호 대 잡음비를 향상시키고, 페이딩을 줄이거나, 채널 용량을 크게 늘리기 위해 여러 통신 경로를 생성한다.

#### Configurations and Modes

- MIMO can increase range, data rate, reliability, and facilitate multiple channels
  - MIMO는 범위, 데이터 속도, 신뢰성을 높이고 다중 채널을 활성화할 수 있다.
- Modes(모드):
  - spatial diversity(공간적 다양성)
  - beam forming(빔포밍)
  - spatial multiplex(공간 다중화)
- Spatial or polarization separation of antennas is necessary for performance benefits (esp. for spatial diversity/multiplex)
  - 성능 이점(특히 공간 다양성/다중화)을 위해서는 안테나의 공간적 또는 양극화 분리가 필요하다.

#### Multipath and Fading

- Multiple received antenna increase received signal power
  - 다중 수신 안테나는 수신 신호 전력을 증가시킨다.
- Multipath may or may not increase the received signal power
  - 다중 경로(Multipath)는 수신 신호 전력을 증가시킬 수도 있고 증가시키지 않을 수도 있다.

뭐 하여튼 free space가 아니면 다중 경로로 도달한 신호간의 간섭 때문에 신호다 더 세지기도 약해지기도 한다.

#### The Propagation Channel is still a Linear System – a complex number

#### Estimating the Channel State

- "s" is known to receiver
  - "s"는 수신자에게 알려진다.
- CSI-RS and SRS are for this purpose
  - CSI-RS와 SRS는 이를 위한 것이다.

<img width="656" alt="스크린샷 2023-10-30 오후 8 52 00" src="https://user-images.githubusercontent.com/138586629/279046101-510b6bb9-cce8-4626-b9ef-8b710917a850.png">

채널의 상태를 예측하려면 하여튼 CSI-RS와 SRS을 통해서 h의 상태를 알아야 함.
하여튼 그걸로 H 매트릭스를 알 수 있음(?)

#### Multiple Propagation Channels (다중 전파 채널)

<img width="866" alt="스크린샷 2023-10-22 오후 6 25 53" src="https://user-images.githubusercontent.com/138586629/277156167-c35b3114-03c7-41fd-8140-66f144d34915.png">

멀티 안테나를 활용해서 H 매트릭스를 더 크게 만들자나? 그럼 여러 h 정보를 알 수 있지

#### General Channel Matrix (일반 채널 매트릭스)

<img width="952" alt="스크린샷 2023-10-22 오후 6 27 10" src="https://user-images.githubusercontent.com/138586629/277156220-53fc05f3-d096-4cb5-af8a-dd5980ffd61d.png">

<img width="538" alt="스크린샷 2023-10-30 오후 8 58 35" src="https://user-images.githubusercontent.com/138586629/279047596-142c0e26-c06f-4d55-9c10-036d9962ee9d.png">

뭐 이걸가지고 H의 inverse matrix를 구해서 estimate 할 수 있겠죠?

#### Shannon Capacity

- Over path from one Tx antenna to one Rx antenna
  - Data rate limit over which error free communication is impossible.

<img width="982" alt="스크린샷 2023-10-22 오후 6 30 10" src="https://user-images.githubusercontent.com/138586629/277156336-cab6beb0-3740-42e1-8f10-fa72d8ad2f04.png">

하여튼 이걸로 SISO일 때 C/B에 대한 값을 알 수 있죠?

그니까 C/B를 spectral efficiency라고 하는데, Bandwidth 대비

S/N은 신호 대 노이즈 비(ratio)고요, 여기서 N은 noise를 의미합니다잉.

#### General MIMO Capacity

<img width="957" alt="스크린샷 2023-10-22 오후 6 31 14" src="https://user-images.githubusercontent.com/138586629/277156391-0629c523-6180-4d69-a7dd-c3060325991c.png">

- Note that we will compare SISO and MIMO capacity with the same transmit power.
  - 앞으로 같은 전송 전력에서 SISO와 MIMO 용량을 비교할것임.

위의 shannon capacity를 통해서 MIMO일 때 확장을 해봣죠

여기서 N은 위에 있는 noise가 아니라 송신 안테나 개수 N임요 ㅇㅇ

#### Parallel Non-coupled Channels

<img width="954" alt="스크린샷 2023-10-22 오후 6 33 47" src="https://user-images.githubusercontent.com/138586629/277156511-efb80869-3f1d-4f38-9a58-642f1f92b12b.png">

이제 SISO인 게 여러개라는, 그러니까 서로간에 간섭이 아예 없는 ideal한 상황을 가정했을 때
요렇게 식을 구해보면 S/N = rho (signal-to-noise ration)가 N이 무한일 때 14.4에 수렴.
하여튼 MIMO가 SISO보다 더 좋다는 것!

다시 얘기하면 송신 N개 수신 N개고 송수신 1개씩 짝을 지어서 다른 짝에게 간섭하지 않고 데이터를 송수신한다는 가정하에 전체 Capacity를 계산해보니까, 송수신 1개만 전송할 때(SISO)에 비교할 때 요런 Capacity의 증가 추세를 보이더라.

rho가 10이라고 가정할 때 14.4에 수렴하더라.

#### Before discussing three MIMO modes - Polarization of Electromagnetic Wave

- For the electromagnetic wave the polarization is effectively the plane in which the electric wave vibrates
- Antennas are sensitive to polarization, and generally only receive or transmit **a signal with a particular polarization**

<img width="410" alt="스크린샷 2023-10-22 오후 6 35 46" src="https://user-images.githubusercontent.com/138586629/277156590-e1e5d5ec-007d-43ee-a48a-d87db78ed2eb.png">

안테나가 송신 신호와 수직 방향이면 신호가 수신되지 않을 수 있음.

#### Antenna Polarization(안테나 양극화)

- Many mobile communication systems may rely on the fact that there are likely to be many reflections between the transmitter and the receiver and these will tend to mean that a signal will have a particular polarization when it reaches the receiver
  - 많은 이동 통신 시스템은 송신기와 수신기 사이에 많은 반사가 있을 수 있다는 사실에 의존할 수 있으며 이는 신호가 수신기에 도달할 때 특정 편파를 갖게 된다는 것을 의미하는 경향이 있다.
- Most base stations have dual-polarized antennas : +45o and - 45o
  - 대부분의 기지국에는 45도 및 -45도의 이중 편파 안테나가 있다.
  - Avoid no effective electric field at the receiver
    - 수신기에서 효과적인 전기장이 발생하지 않도록 해야 함.
  - Combined before ADC – baseband signal processing does not take this into account.
    - ADC 이전에 결합 - 기저대역 신호 처리에서는 이를 고려하지 않음.

그래서 수직하게 안테나 두개를 배치해서 이러한 현상을 방지하는 것.

avoid no effective electric field(전기장) at the receiver!

## MIMO Mode

### 1. Diversity

#### MIMO Mode (1/3) - Diversity

- 시간/주파수 다양성

- 공간 (안테나) 다양성 - 스펙트럼 효율성 손실 없이 달성됨
  - 수신 다양성 (다중 수신 안테나)
  - 전송 다양성 (다중 전송 안테나)

<img width="671" alt="스크린샷 2023-10-30 오후 9 31 43" src="https://user-images.githubusercontent.com/138586629/279056276-45368d9a-cba8-4f6f-9f00-95a2a23de574.png">

#### Receive Diversity

- Multiple antennas at the receiver
  - 수신기의 다중 안테나
  - Multiple channels
    - 다중 채널
  - Transmitter does not have to know that there are multiple receive antennas
    - 송신기는 수신 안테나가 여러 개 있다는 사실을 알필요가 없다.
- Receiver needs to combine the received signal/symbol at the receiver
  - 수신기는 수신기에서 수신된 신호/기호를 결합해야 함
  - Selective combining
    - 선택적 결합
  - Optimally combining – MRC
    - 최적의 결합 - MRC

<img width="652" alt="스크린샷 2023-10-30 오후 9 32 10" src="https://user-images.githubusercontent.com/138586629/279056394-321c0ce3-b884-430c-8279-c9c115d0cc72.png">

- h1, h2, ... 이 서로 독립적이려면 충분히 공간적으로 떨어져 있어야 해요
- 이게 파장 길이인데 3GHz이 carrier frequncy니, 10^9 = 10cm. 단말에선 어렵겠죠?

#### Maximal Ratio Combining (MRC) for Receive Diversity

<img width="1002" alt="스크린샷 2023-10-22 오후 6 49 15" src="https://user-images.githubusercontent.com/138586629/277157172-c5f077ae-73cb-4d83-93e6-43a777ddec5d.png">

- 뭐시기저시기 y1, y2를 가지고서 x를 알아내는 것을 combine이라고 할 수 있는건데요
- maximum likelihood detector라는 것은 h1, h2을 가중치로 해서 구하는거임요.
- 그 정확한 가중치 값은 channel estimator에서 구하는거임요.

Receiver Diversity는 중요한 게 transmitter가 그걸 알 필요가 없다 이말씀.

#### Transmit Diversity (전송 다양성)

- How to use multiple transmit antennas for transmit diversity?
  - 전송 다양성을 위해 다중 전송 안테나를 사용하는 방법은 무엇인가?
- Receiver does not know of Transmit Diversity
  - 수신기는 전송 다양성을 모른다.
  - Same symbol transmit by the multiple transmit antenna
    - 다중 전송 안테나에 의한 동일 심볼 전송
  - Simple, no combining difficulty – inherently added at the radio frequency
    - 간단하고 결합 난이도가 없음 - 본질적으로 무선 주파수에 추가됨
  - No need to discuss
    - 논의할 필요가 없음
- Consider a better Transmit Diversity scheme
  - 더 나은 전송 다양성 체계를 고려하시오.
  - Over a multiple times and/or frequencies
    - 여러 번 및/또는 여러 주파수에 걸쳐
  - Should be a simple modification – no difficulty at the combining
    - 간단한 수정이여야 함 - 결합에 어려움이 없을 것

<img width="253" alt="스크린샷 2023-10-30 오후 9 32 37" src="https://user-images.githubusercontent.com/138586629/279056503-554767ab-d08b-4d4b-a6f3-5976e774fc0f.png">

역시 이것도 receiver가 알 필요가 없음.

#### Transmit Diversity in Space-Time Block Code

- 2개의 안테나, 2개의 time instance
- STBC, a.k.a Alamouti Code

<img width="685" alt="스크린샷 2023-10-30 오후 9 46 24" src="https://user-images.githubusercontent.com/138586629/279060178-7da79989-daf5-4e77-8e59-3bbfd77197e9.png">

알라무티라는 사람이 만든 STBC라는 것은 2개의 안테나, 2개의 time instance.

두개의 심볼을 보내는데 처음엔 s1, s2, 두번째는 -s2, s1을 보내 왜그러냐면

<img width="533" alt="스크린샷 2023-10-30 오후 9 48 01" src="https://user-images.githubusercontent.com/138586629/279060588-570a09a9-7df6-44af-b12e-533fe0e06de1.png">

time diversity를 이용함!

이러저러하게 계산을 하면요 s1, s2를 저 연립방정식으로 계산을 할 수 있다나요?

#### Decoding of Alamouti Code

<img width="844" alt="스크린샷 2023-10-22 오후 7 01 34" src="https://user-images.githubusercontent.com/138586629/277157677-8dc0fc03-6e8c-4772-b335-4efec3987f71.png">

계산 결과는 여기에 있죠? 하여튼 간단하면서 실제로도 많이 사용됩니다.
이렇게 수신측에서 s1, s2 계산해냄.

### 2. Beamforming

#### MIMO Mode (2/3) - Beamforming

- Definition of the beamforming : Focusing the transmitted energy toward the intended receiver rather than spraying the energy indiscriminately.
- 빔포밍 정의 : 무분별하게 에너지를 뿌리는 것이 아니라, 송신된 에너지를 원하는 수신자에게 집중시키는 것.
- Spatial multiplexing is also possible to increase system capacity
  - 시스템 용량 증가를 위한 공간 다중화도 가능.

<img width="643" alt="스크린샷 2023-10-30 오후 9 59 27" src="https://user-images.githubusercontent.com/138586629/279063483-e1096f27-299a-4a94-b935-a483cb7adca2.png">

horn antenna라는 건데 이렇게 특정 방향으로 레이저빔처럼 더 집중시킬 수 있습니다.

기지국과 기지국간의 통신에는 (우리나라는 광케이블로 하지만) 섬나라 같은 경우는 저런걸로 함.

Fixed Service => Wrieless Comm. 이지만 tx&rx 움직이지 않는 상황 (ex 기지국 간의 통신)

#### Analog Beamforming – theory

<img width="787" alt="스크린샷 2023-10-22 오후 7 05 03" src="https://user-images.githubusercontent.com/138586629/277157820-b1c394b2-b51d-462d-8579-c8ca45ecfe97.png">

그래서 빔포밍은 어떻게 하나? 오늘 말씀드릴 빔포밍은 analog beamforming인데요

microwave는 sine wave로 전달이 되잖아요? 거리를 잘 맞춰서

<img width="530" alt="스크린샷 2023-10-30 오후 10 05 57" src="https://user-images.githubusercontent.com/138586629/279065064-9af53eb6-44bc-48ba-b62f-63aa46c8604b.png">

<img width="487" alt="스크린샷 2023-10-30 오후 10 06 21" src="https://user-images.githubusercontent.com/138586629/279065144-665fe807-2181-4f52-a663-eed0aef8ed85.png">

#### Transmit vs. Receive Beamforming

- Tx Beamforming : Splitting a signal into multiple identical copies, weighting those copies with a complex gain and phase weight and then sending the weighted signal copies to the respective antennas.
  - Tx 빔포밍 : 신호를 여러 개의 동일한 복사본으로 분할하고, 복소 게인 및 위상 가중치로 해당 복사본에 가중치를 부여한 다음 가중치가 부여된 신호 복사본을 각 안테나로 보낸다.
- Rx Beamforming : Taking the signals received from multiple antennas, weighting them with complex gain and phase weights and then summing the weighted signals to form a single output.
  - Rx 빔포밍 : 여러 안테나에서 수신된 신호를 가져와서 복잡한 이득 및 위상 가중치로 가중치를 부여한 다음 가중치가 부여된 신호를 합산하여 단일 출력을 형성합니다.

#### Analog Beamforming Example

- 역전파(사이드로브)가 차단될 수 있음.

<img width="922" alt="스크린샷 2023-10-22 오후 7 17 25" src="https://user-images.githubusercontent.com/138586629/277158361-23f035d3-b959-4857-a17a-e47e278b431a.png">

<img width="641" alt="스크린샷 2023-10-22 오후 7 17 37" src="https://user-images.githubusercontent.com/138586629/277158373-594e8cd0-2953-4c6c-970f-17942463aea5.png">

### 3. Spatial Multiplexing

#### MIMO Modes (3/3) – Spatial Multiplexing

- Number of received antenna >= Number of transmit antenna
  - In this figure, there are two separate “streams” (a.k.a layers)
  - Same Time and Same Frequency (= one resource element) but two separate channels despite interfering channel matrix H
- Precoding and Shaping need to be designed

<img width="648" alt="스크린샷 2023-10-22 오후 7 19 47" src="https://user-images.githubusercontent.com/138586629/277158497-b4a25846-8c77-4adf-83ae-5242814430e0.png">

## Questions

keywords : MIMO modes(diversity, beamforming, spatial multiplexing),
receiver diversity, transmit diversity(STBC), SISO channel capacity(shannon capacity), parallel non-coupled channel, antenna polarization.

- Explain 3 modes of MIMO operations
  - MIMO 동작의 3가지 모드에 대해 설명하시오.
- Explain receiver diversity and STBC
  - 수신기의 다양성 및 STBC에 대해 설명하시오.
- What is the SISO channel capacity and what does that mean?
  - SISO 채널 용량이란 무엇이며, 이는 무엇을 의미하는가?
- What is the parallel non-coupled channel and what is its capacity? What does that mean?
  - 병렬 비결합 채널이란 무엇이며 용량은 어떻게 되는가? 어떤 의미를 가지는가?
- Explain antenna polarization
  - 안테나 양극화에 대해 설명하시오.
- Explain (analog) beamforming operation – transmitter and receiver
  - (아날로그) 빔포밍의 작동원리에 대해 설명하시오. 송신기 및 수신기에 대해.

### Explain 3 modes of MIMO operations

> MIMO 동작의 3가지 모드에 대해 설명하시오.

MIMO (Multiple-Input Multiple-Output)는 무선 통신에서 다중 안테나를 사용하여 데이터 전송 및 수신 품질을 향상시키는 기술입니다.
MIMO 동작은 다양한 모드로 구현될 수 있으며, 주요한 세 가지 모드는 다음과 같습니다:

1. **SU-MIMO (Single-User MIMO)**:

   - **역할**: SU-MIMO 모드는 단일 사용자와의 통신을 위해 사용됩니다. 하나의 사용자 장치에 대한 데이터 전송을 개선하고 다중 안테나를 사용하여 다중 경로 페이딩 효과를 완화합니다.
   - **작동**: 기지국과 단일 사용자 간의 MIMO 통신에서 다중 안테나를 사용하여 데이터 전송을 개선합니다. SU-MIMO는 단일 사용자와의 통신에서 성능을 향상시키는 데 사용됩니다.

2. **MU-MIMO (Multi-User MIMO)**:

   - **역할**: MU-MIMO 모드는 다중 사용자와의 동시 통신을 지원하며, 여러 사용자 간의 동시 데이터 전송을 허용합니다. 이는 대역폭 효율성과 다중 접속성을 개선합니다.
   - **작동**: 기지국은 여러 사용자에게 다중 안테나를 사용하여 동시에 데이터를 전송하고 수신합니다. MU-MIMO는 다중 사용자 환경에서 다양한 사용자 간의 데이터 전송을 조정하고 대역폭을 효율적으로 활용합니다.

3. **Massive MIMO**:
   - **역할**: Massive MIMO는 대규모 안테나 배열을 사용하여 무선 통신을 향상시키는데 사용됩니다. 이 모드는 대역폭 효율성과 신호 범위를 확장하며, 신호 간섭을 줄이는 데 중요합니다.
   - **작동**: 기지국은 대규모 안테나 어레이를 사용하여 다중 사용자와의 통신을 수행하며, 빔포밍과 방향성 통제를 사용하여 신호를 조절합니다. Massive MIMO는 무선 통신 시스템의 범위와 성능을 향상시킵니다.

각 MIMO 모드는 특정 사용 사례 및 환경에서 성능을 최적화하는 데 사용됩니다.
SU-MIMO는 단일 사용자와의 통신을 향상시키며,
MU-MIMO는 다중 사용자 환경에서 대역폭을 효율적으로 활용합니다.
Massive MIMO는 대규모 안테나 어레이를 사용하여 범위와 성능을 향상시킵니다.

---

ㄴㄴ 이거 아니고요.

- MIMO modes
  - Diversity
  - Beamforming
  - Spatial Multiplex

이렇게 3개 말하는 겁니다. ㅇㅇ

- Diversity는 그냥 여러개의 안테나로
  - receiver : transmitter 알 필요 없다
    - selective combining
    - optimally combining (MRC, maximal ratio combining)
  - transmitter
- Beamforming
  - 똑같은 신호를 똑같은 주파수로 쏴주기는 하되, 위상과 안테나간 거리를 잘 조정해서 특정 방향으로의 에너지를 세게 몰아주는 방식이다. 레이저빔 같은거.
- Spatial Multiplexing
  - 위에 설명했던 Multiple Antenna(Parallel Non-coupled Channel) 상황에서
    - receive antenna 개수가 transmit antenna 개수보다 많은 상황에서 서로간의 간섭도 있을 때, 전처리/후처리를 적절히 해서 이 알 수 없는 H를 해결하는 방법!
    - 그러니까 1채널은 1채널로, 2채널은 2채널로만 신호가 가게 한번 해보자!
    - 주파수를 더 사는 것과 같은 효과가 되어버리죠 채널이 여러개가 되어버리니!

### Explain receiver diversity and STBC

> 수신기의 다양성 및 STBC에 대해 설명하시오.

수신기의 다양성(Diversity)와 Space-Time Block Coding (STBC)은 무선 통신 시스템에서 신호 품질을 향상시키는 방법입니다. 다양성은 신호의 안정성을 향상시키고 오류를 줄이며, STBC는 다중 안테나 시스템에서 데이터 전송 효율성을 개선합니다.

1. **수신기의 다양성 (Diversity)**:

   - **역할**: 수신기의 다양성은 다중 경로 환경에서 신호의 안정성을 향상시키는 데 사용됩니다. 신호가 다양한 경로를 통해 수신되는 경우, 각 경로에서의 신호를 복제하고 조합하여 신호 품질을 향상시킵니다.
   - **작동**: 수신기의 다양성은 시간 다양성과 공간 다양성으로 나뉩니다. 시간 다양성은 시간에 따라 신호를 복제하고 조합하여 다양한 시간 지연에서 발생하는 신호 감쇠를 극복합니다. 공간 다양성은 다중 안테나 시스템을 사용하여 다양한 안테나로 신호를 수신하고 조합하여 신호 감쇠를 극복합니다.

2. **Space-Time Block Coding (STBC)**:

   - **역할**: STBC는 다중 안테나 시스템에서 데이터 전송 효율성을 개선하고 다중 경로에서의 신호 품질을 향상시킵니다. 이를 통해 신호 간섭을 줄이고 오류를 감소시킵니다.
   - **작동**: STBC는 다중 안테나에서 데이터를 인코딩하여 다양한 공간 및 시간 상태에서 다중 경로 환경에서의 신호를 조합합니다. STBC는 수신기에서 데이터를 디코딩할 때 다양한 안테나와 시간 슬롯에서 수신된 신호를 활용하여 신호 품질을 향상시킵니다.

수신기의 다양성과 STBC는 무선 통신 시스템에서 신호의 안정성을 향상시키고 다중 경로 환경에서의 성능을 개선하는 데 사용됩니다.
수신기의 다양성은 주로 신호의 안정성을 향상시키며,
STBC는 다중 안테나 시스템에서 데이터 전송 효율성을 향상시킵니다.

---

한 바구니에 모든 계란을 담지 말아라. 채널 자체가 불안정하니 한 채널로만 보내면 안좋은 상태가 존재.

그걸 극복하기 위한 가장 효과적인 방법이 diversity(다양성)임.

- time diversity : 하나의 심볼을 여러 시간에 걸쳐 보내는 거
- frequency diversity : 하나의 심볼을 여러 주파수에 걸쳐 보내는 거

각 시간, 주파수에 따라서 통신 상태가 좋을 때 안좋을 때가 있으니 여러번 보내는거 ㅇㅇ
당연히 비효율적임 ㅇㅇ

그래서 spatial(antenna) diversity도 등장. 공간적으로 분리된 여러 안테나들에 같은 신호를
보내서 without loss of spectral efficiency(효율성을 떨어뜨리지 않는 선에서) 전송 품질을 보장!?

##### receiver diversity

수신 안테나가 여러개인거임. transmitter랑 노상관이고요 ㅇㅇ

- selective combining
  - 여러 수신 안테나에 온 신호 중 가장 receive power가 센거를 그냥 고르는거임 ㅇㅇ
- optimally combining - MRC, Maximal Ratio Combining
  - 이거는 뭐냐하면 각각의 수신안테나의 gain(h1, h2, ...)을 가중치로 해서 각각의 estimator에서 나온 결과를 계산한 결과를 가지고 실제 original 정보를 예측하는 것

##### transmit diversity

- receiver가 transmit을 모른다면 걍 multipath처럼 생각하는 건데.. 걍 good luck
- 근데 이렇게 운빨에 맡기는 건 별로겠죠? STBC를 이용해서 좀더 transmit diversity 성능을 높이는 방법을 연구함요.

- spatial diversity(2개의 안테나로) + time diversity(2 차례 전송)로 효율 저하 없이
  - h1, h2 채널 하나가 망가지더라도 뭐 하여튼 값을 구할 수 있는거죠.

### What is the SISO channel capacity and what does that mean?

> SISO 채널 용량이란 무엇이며, 이는 무엇을 의미하는가?

SISO 채널 용량(SISO Channel Capacity)은 SISO (Single-Input Single-Output) 무선 통신 시스템에서 전송할 수 있는 최대 정보 비트 수를 나타내는 개념입니다. SISO 채널 용량은 주어진 채널 환경에서 데이터 전송의 한계를 나타내며, 채널의 특성과 노이즈 환경에 따라 달라집니다.

SISO 채널 용량을 이해하기 위해 몇 가지 중요한 개념을 설명하겠습니다:

1. **SISO 채널**: SISO는 단일 안테나로 데이터를 전송하는 무선 통신 시스템을 나타냅니다. 이는 단일 송신 안테나와 단일 수신 안테나를 사용하여 통신하는 형태로, 데이터는 단일 경로로 전송됩니다.

2. **채널 용량**: 채널 용량은 주어진 무선 채널에서 단위 시간 동안 전송할 수 있는 최대 정보 비트 수를 나타냅니다. 채널 용량은 비트/초 (bps) 단위로 표현되며, 채널 대역폭과 신호 대 노이즈 비율(SNR)에 따라 결정됩니다.

3. **SNR**: SNR은 신호 대 노이즈 비율로, 전송 신호의 강도와 주변 노이즈 수준의 비율을 나타냅니다. 높은 SNR 환경에서는 노이즈에 비해 신호가 더 강하기 때문에 높은 채널 용량을 달성할 수 있습니다.

SISO 채널 용량은 Shannon-Hartley 정리를 기반으로 계산됩니다. 이 정리는 다음과 같이 표현됩니다:

\[C = B \cdot \log_2(1 + \text{SNR})\]

<img width="231" alt="스크린샷 2023-10-28 오후 2 20 06" src="https://user-images.githubusercontent.com/138586629/278792615-8148354d-5ede-40d2-b863-92b000a8d34b.png">

여기서:

- \(C\)는 채널 용량 (bps)입니다.
- \(B\)는 채널 대역폭 (Hz)입니다.
- SNR은 신호 대 노이즈 비율입니다.

SISO 채널 용량은 채널 대역폭과 SNR에 의해 결정되므로, 채널 환경에 따라 다양한 값을 가질 수 있습니다. 높은 대역폭과 높은 SNR 환경에서는 더 높은 채널 용량을 달성할 수 있으며, 무선 통신 시스템의 성능과 효율성을 나타내는 중요한 지표 중 하나입니다.

---

SISO 채널 용량은 Shannon Capacity라고도 하며,

- C = B log (1 + S/N)
  - 이게 무슨얘기냐면 SISO communication channel에서, `maximum data rate (C)`가
    B(bandwidth)와 log_2(1+S/N)의 곱으로 나타낼 수 있다.
    - S/N은 signal to noise ration.
  - C/B = log_2 (1 + S/N)으로 표현하기도 함.
    - C/B는 `spectral efficiancy(bits/sec/Hz)`라고 함 `단위 대역폭당 maximum data rate`

### What is the parallel non-coupled channel and what is its capacity? What does that mean?

> 병렬 비결합 채널이란 무엇이며 용량은 어떻게 되는가? 어떤 의미를 가지는가?

병렬 비결합 채널 (Parallel Independent Channels)은 여러 독립적인 채널이 병렬로 동작하는 통신 환경을 나타내는 개념입니다. 이러한 채널은 서로 독립적으로 정보를 전송하며, 각 채널은 다른 채널과 독립적으로 작동합니다. 병렬 비결합 채널은 정보 이론에서 중요한 개념이며, 이를 통해 전체 시스템의 용량을 계산하고 이해할 수 있습니다.

병렬 비결합 채널의 용량은 다음과 같이 계산됩니다:

\[C\_{\text{total}} = C_1 + C_2 + \ldots + C_n\]

<img width="257" alt="스크린샷 2023-10-28 오후 2 21 06" src="https://user-images.githubusercontent.com/138586629/278792649-95dccccb-2eec-492d-a3a7-a4b888697e60.png">

여기서:

- \(C\_{\text{total}}\)은 병렬 채널의 전체 용량입니다.
- \(C_1, C_2, \ldots, C_n\)은 각각의 독립적인 채널의 용량입니다.

병렬 비결합 채널은 다음과 같은 의미를 가집니다:

1. **독립적인 정보 전송**: 각 채널은 서로 독립적으로 정보를 전송하므로 서로에게 영향을 미치지 않습니다. 이는 각 채널이 서로 간섭 없이 동작할 수 있음을 의미합니다.

2. **전체 용량 증가**: 병렬 채널의 전체 용량은 각 독립적인 채널의 용량의 합으로 계산됩니다. 따라서 채널 수가 증가하면 전체 용량도 증가하게 됩니다.

3. **신뢰성 향상**: 병렬로 동작하는 독립적인 채널은 오류 레벨이 각 채널에 대해 분산되므로 전체 통신 시스템의 신뢰성을 향상시킬 수 있습니다.

병렬 비결합 채널은 다양한 통신 시나리오에서 사용될 수 있으며, 각 채널이 독립적으로 동작하는 환경에서 통신 용량 및 신뢰성을 최적화하는 데 도움을 줍니다. 이러한 채널 구조는 정보 이론 및 통신 공학 분야에서 중요한 개념 중 하나이며, 다중 경로 및 다중 안테나 시스템에서도 유용하게 적용됩니다.

---

`parallel non-coupled channels`는요 서로간의 간섭 없이 N개의 송신 N개의 수신
안테나에서 송수신 1개씩 쌍을 이뤄서 송수신이 가능하다는 ideal한 가정하에 `spectral efficiency`를 계산해봐요.

그러면 아까 말했던 SISO의 channel capacity인 `shannon capacity`의 `* N`만 해주면됨.

계산을 해보니 같은 power에서 안테나를 많이 쓰는 게 좋기는 하지만 너무너무 좋지는 않더라.
N이 무한으로 수렴해도 x log (1 + 10/x) => 14.4 정도!

### Explain antenna polarization

> 안테나 양극화에 대해 설명하시오.

안테나 양극화 (Antenna Polarization)는 무선 통신 및 전파 공학에서 중요한 개념으로, 무선 신호의 방향성 및 품질을 제어하는 데 사용됩니다. 안테나 양극화는 안테나에서 전파의 진폭과 위상을 조절하는 것을 의미하며, 두 가지 주요 형태로 나타납니다: 선형 양극화와 원형 양극화.

1. **선형 양극화 (Linear Polarization)**:

   - **역할**: 선형 양극화는 전파를 직선 또는 수평 방향, 수직 방향 또는 어떤 각도로 전송하는 것을 의미합니다. 이를 통해 안테나는 특정 방향에서 품질 있는 통신을 지원하며, 다른 방향에서는 신호가 약화될 수 있습니다.
   - **예시**: 일반적으로 무선 통신에서 사용되며, 모바일 휴대폰 안테나나 Wi-Fi 라우터 안테나는 선형 양극화를 사용하여 수직 또는 수평 방향으로 전파를 방송합니다.

2. **원형 양극화 (Circular Polarization)**:
   - **역할**: 원형 양극화는 전파를 원형 또는 타원형 패턴으로 전송하는 것을 의미합니다. 이는 신호가 다양한 방향에서 고르게 전파되며, 다중 경로에서의 다중 경로 간섭을 줄이는 데 도움을 줍니다.
   - **예시**: GPS 안테나 및 위성 통신에 사용될 수 있으며, GPS 수신기는 원형 양극화를 활용하여 위성 신호를 안정적으로 수신합니다.

안테나 양극화는 통신 환경 및 필요한 안테나 특성에 따라 선택됩니다. 선형 양극화는 일반적으로 특정 방향의 통신에 사용되며, 원형 양극화는 다양한 방향에서의 안정성을 개선하고 다중 경로에서의 신호를 향상시킵니다. 적절한 양극화를 선택하여 무선 통신 시스템의 성능을 최적화할 수 있습니다.

---

ㄴㄴ
걍 송신 신호와 직교하는 방향으로 안테나를 배치하면 안테나가 받는 신호가 0이 되버리기 때문에,
이러한 상황을 방지하기 위해서 수신 안테나를 90도 차이나게(+45, -45) 세트로 배치를 하는 것을
안테나의 양극화라고 함.

### Explain (analog) beamforming operation – transmitter and receiver

> (아날로그) 빔포밍의 작동원리에 대해 설명하시오. 송신기 및 수신기에 대해.

빔포밍 (Beamforming)은 무선 통신에서 안테나 배열을 사용하여 무선 신호를 특정 방향으로 집중시키거나 수신하는 기술입니다. 빔포밍은 다음과 같이 송신기와 수신기에서 작동합니다:

**송신기에서의 빔포밍**:

1. **안테나 배열 구성**: 송신기에서 여러 안테나를 배열로 구성합니다. 안테나 배열은 물리적으로 다양한 위치에 있는 안테나를 포함하며, 이러한 안테나는 신호를 조합하거나 분리하기 위해 사용됩니다.

2. **신호 가중치 적용**: 빔포밍은 각 안테나에 대한 신호 가중치를 적용하여 특정 방향으로 전파할 신호를 형성합니다. 이 가중치는 신호를 집중시키고 원하는 방향으로 방출하는 데 사용됩니다. 각 안테나는 다른 가중치를 가질 수 있으며, 이를 통해 신호 방향이 제어됩니다.

3. **신호 합성**: 가중치가 적용된 신호는 안테나 배열을 통해 합성되어 빔(직선 또는 방향)으로 형성됩니다. 이 빔은 특정 방향으로 집중되고, 다른 방향에서는 상대적으로 약화됩니다.

**수신기에서의 빔포밍**:

1. **안테나 배열 구성**: 수신기에서도 송신기와 유사한 안테나 배열을 구성합니다. 이러한 안테나 배열은 수신되는 신호를 다양한 방향에서 수신할 수 있도록 합니다.

2. **신호 가중치 적용**: 수신기는 수신되는 신호에 대한 가중치를 적용하여 원하는 방향에서의 신호를 강화하고 다른 방향에서의 간섭을 줄입니다. 이러한 가중치는 수신된 신호를 분석하여 조절됩니다.

3. **신호 합성**: 가중치가 적용된 수신된 신호는 안테나 배열을 통해 합성되어 원하는 방향으로의 신호를 추출합니다. 이는 특정 방향에서의 신호를 강화하고 다른 방향에서의 간섭을 감소시킵니다.

송신기와 수신기에서의 빔포밍을 통해 특정 방향으로의 신호 집중 및 간섭 제어가 가능해집니다. 이 기술은 무선 통신 시스템에서 품질 및 성능을 향상시키며, 특히 대역폭 효율성을 개선하고 다중 경로 간섭을 줄이는 데 도움이 됩니다. 빔포밍은 5G와 같은 다음 세대 무선 통신 시스템에서 중요한 역할을 합니다.

---

똑같은 신호를 똑같은 주파수로 쏴주기는 하되, 위상과 안테나간 거리를 잘 조정해서 특정 방향으로의 에너지를 세게 몰아주는 방식이다. 레이저빔 같은거.
