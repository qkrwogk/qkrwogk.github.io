# # 231005

MIMO (Multi-Input Multi-Output) (2/2)

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

<img width="966" alt="스크린샷 2023-10-28 오후 2 35 19" src="https://user-images.githubusercontent.com/138586629/278793392-6bd2e844-7461-4d58-ac6e-9f0f4776b218.png">

## Contents

### MIMO (Multi-Input Multi-Output)

- What is MIMO
- The propagation channel
- MIMO and Shannon Capacity
- **MIMO modes**
  - **Diversity**
  - **Beamforming**
  - **Spatial multiplex**
- MIMO in LTE : MU-MIMO (LTE)
- MIMO in 5G NR : Massive MIMO (5G NR)

## MIMO modes

#### Spatial Multiplexing : 공간(=antenna) 다중화

- 수신 안테나 개수 >= 송신 안테나 개수
  - 이 그림에는 두 개의 별도 "스트림(레이어)"가 있음.
  - 동일한 시간 및 동일한 주파수(= 하나의 resource element)에도 불구하고 두개의 분리된 채널을 얻을 수 있음. (매트릭스 H를 잘 해석해서) -> LTE에선 8개 채널까지 가능
- 프리코딩(Precoding, 송신측)과 쉐이핑(Shaping, 수신측) 설계가 필요함

<img width="1029" alt="스크린샷 2023-10-28 오후 2 49 33" src="https://user-images.githubusercontent.com/138586629/278793883-8c2d594b-e934-40f7-8e38-b2fbf310f4a8.png">

#### Singular Value Decomposition (SVD) (자세히 몰라도됨)

> H matrix를 이용해서 multiplexing을 하는 두 가지 수학적 이론 <br />
>
> 1. SVD <br />
> 2. Pseudo-Inverse <br />

<img width="928" alt="스크린샷 2023-10-28 오후 2 54 38" src="https://user-images.githubusercontent.com/138586629/278794052-47d8b62d-1ed4-4854-aad7-011678751a8a.png">

<img width="537" alt="스크린샷 2023-10-28 오후 4 04 30" src="https://user-images.githubusercontent.com/138586629/278797001-2c6fb8b9-b8eb-46ca-b1ed-8f403b825df5.png">

하느님이(?) 주신 H 매트릭스는 SVD에 의해 V^H, Sigma, U의 곱으로 나타낼 수 있음ㅋ

그래서 x -> y가 되는 과정을 x에 저 3개의 행렬이 순차적으로 곱해지는 것으로 나타낼 수 있는거.

그래서 여기서 우리가 시그마를 잘 이용하려고

- Precoding (V를 곱해주는 과정) 과
- Shaping (U^H를 곱해주는 과정)을 추가해줘서

V^H, U를 I로 만들어서 없애버리는 것!!!

그러면 시그마(diagonal matrix)만 남으니까 s1, s2, ...은 서로 영향을 주지 않고
고대로 다시 나온다 이거야 (scalar만 곱해져서). 하여튼 그래서 multiplexing이 가능하다.

#### Single User Spatial Multiplexing (SU-MIMO)

<img width="807" alt="스크린샷 2023-10-28 오후 2 59 22" src="https://user-images.githubusercontent.com/138586629/278794231-510503c1-1c8b-465f-ba4b-8896bde6d690.png">

#### Multi-User Spatial Multiplexing (MU-MIMO)

<img width="408" alt="스크린샷 2023-10-28 오후 2 59 36" src="https://user-images.githubusercontent.com/138586629/278794249-f3747d04-b049-48ac-983a-78898c001bc6.png">

자 이제 두 번째로 Pseudo-Inverse를 이용해 줄건데

자연적으로 발생한 H matrix의 inverse(역행렬)를 구할 수 있다면,
s 벡터 대신에 H^(-1)\*s를 x로 보내주면은 H랑 관게없이 s+noise가 y가 된다!

근데 역행렬은 square matrix라야 가능해.

그러면 우리가(square가 아닌 matrix를 위해) inverse대신 pseudo-inverse를 사용하자.

H^H(여기서 ^H는 Hermitian허미션)을 구하면 (H*H^H)는 square matrix임
그래서 `(H*H^H)*(H*H^H)^(-1)`=`I`가 됨!

그래서 s에다가 `H^H*(H*H^H)^(-1)`를 곱해서 (수신측에서만!) x로 보내면
수신측 y는 s+n가 y가 된다!! 대박

<img width="524" alt="스크린샷 2023-10-28 오후 4 18 38" src="https://user-images.githubusercontent.com/138586629/278797682-e42ddbe4-4591-43e0-8193-743c8301f431.png">

<img width="528" alt="스크린샷 2023-10-28 오후 4 18 56" src="https://user-images.githubusercontent.com/138586629/278797685-a6945d89-0297-4dd1-9502-d0d25f3aef39.png">

반대로 수신측에서 전달받을 거를 (H^H*H)^(-1)*H^H를 곱해주면 이번에도 I가 됩니다!!

이건 송신 안테나 수가 더 작을 때. 이렇게 해줘야 하죠 .

하여튼 송수신 안테나 수 차이에 따라 이렇게 한쪽에서 정해진 행렬을 곱해주기만 하면
각 채널이 섞이지 않고 온전히 신호를 전달 받을 수 있게 된다.

<img width="519" alt="스크린샷 2023-10-28 오후 4 27 20" src="https://user-images.githubusercontent.com/138586629/278798046-49b21d00-dbcd-46fd-824e-10c5ed45cc6d.png">

#### MU-MIMO DL

문제:

- n (=in this figure, Two) users want to be multiplexed
- Using the same resource element – time H and frequency are shared
- Making use of m (>=n) transmit antennas
  - Channel matrix **H is a fat matrix**
- Consider Downlink
  - Larger number of transmit antenna than multiplexed users
  - Information on H is available at the base station
  - **Receiver** has a single antenna – **no shaping operation**

송신 안테나가 유저 수보다 더 많다고 치면!

H matrix는 fat matrix가 되는거고요.

<img width="329" alt="스크린샷 2023-10-28 오후 4 29 45" src="https://user-images.githubusercontent.com/138586629/278798133-03a7496f-da33-4c0b-8153-9aa0c838ee7a.png">

#### How to do Precoding – Pseudo-Inverse

앞서 설명한 송신 측에서의 Pseudo-Inverse를 이용하는 방법을
에러를 제로를 만들어준다! 해서 **ZERO-FORCING Precoding** 이라고 한다.

수신 측에서 해야 할 일은 없게되는거임!

#### MU-MIMO DL with Zero-Forcing Precoding

<img width="869" alt="스크린샷 2023-10-28 오후 3 00 49" src="https://user-images.githubusercontent.com/138586629/278794314-e1f8ece8-b665-40e1-a004-caa4b85e2a09.png">

#### MU-MIMO UL

문제:

- n (=in this figure, Two) users want to send simultaneously to the base station (=multiplexed)
- Using the same resource element – time H and frequency are shared
- Making use of m (>=n) `receive` antennas
  - Channel matrix **H is a fat matrix**
- Consider Uplink
- Larger number of **receive** antenna than multiplexed users
- Information on H is available at the base station
- **Transmitter** has a single antenna – **no precoding operation**

#### How to do Equalization – Pseudo-Inverse

#### MU-MIMO UL with ZF equalizer

H가 skinny 한 matrix (그러니까 수신 측 안테나가 다중화된 유저보다 더 많다고 치면!)

<img width="668" alt="스크린샷 2023-10-28 오후 3 01 30" src="https://user-images.githubusercontent.com/138586629/278794336-c137a5d1-7343-4209-b487-302622c7f1ba.png">

앞서 설명한 수신 측에서의 Pseudo-Inverse를 이용하는 방법을
에러를 제로를 만들어준다! 해서 **ZERO-FORCING Equalizer** 이라고 한다.

이때는 송신 측에서는 해야 할 일이 없는 거임!

### Wrap-Up the MIMO modes (MIMO modes 정리)

3가지 모드에 대해 이제 살펴봤어요.

- Diversity (다중성)
  - 통신 스펙에 영향을 주지 않고. transmitter에게 아무런 정보 주지도 않고 할수 있음.
  - Receive diversity
  - Transmit diversity – STBC(space time block code) (Alamouti Code)
- Analog Beamforming (아날로그 빔포밍)
  - 안테나를 일렬로 나열시키고, 똑같은 신호 대신 phase를 다르게 해서, 멀리서 봤을때는 하나의 beam을 쏘는 것 처럼 보이게 (신호를 강하게) 하는 것
  - Array antenna with phase control at carrier frequency
- Spatial Multiplexing (=separate channels) – Time/Frequency/Spatial
  - 위에서 time과 frequency를 통해 MIMO를 했듯 이번엔 공간적으로 분리를 해서 다중 채널을 가능하게 함!
  - Single-User MIMO based on SVD of the channel matrix
  - MU-MIMO DL/UL based on Pseudo-Inverse of the channel matrix

강조드리고 싶은 것은 다 여러 안테나를 사용하지만 Analog Beamforming은 phase로 신호를 강하게 해주는거고, spatial multiplexing은 다중 채널(multiplexing)을 가능하게 해주는거임!

## MIMO in LTE

- Digital Beamforming with SVD based spatial multiplexing

#### Different Viewpoints

- 그럼 analog beamforming이 multiplexing이 가능할까?
  - 당연히 가능하다! 어짜피 특정 방향으로만 레이저처럼 쏴주는거라 다른 방향에 영향을 별로안줌!
- MU-MIMO가 user-specific(특정 유저에게만 집중하는)한 송신 시그널 집중 역할로 활용이 가능한가?
  - 가능하다! 결국 이걸(spatial multiplexing)을 digital beamforming이라 한다!

<img width="676" alt="스크린샷 2023-10-28 오후 4 47 58" src="https://user-images.githubusercontent.com/138586629/278799110-139b88aa-7d0d-4d84-a423-5b2fa53914e0.png">

시작은 다르지만 결국 analog beamforming, digital beamforming(spatial multiplexing)은 모두 같은 목적을 가지게 된다 두둥

#### Practical Issues

- Analog Beamforming
  - 정말 최고인 것처럼 보이지만 Line of Sight(직선 방향)으로 송수신 할 수 있는 경우는 사실상 거의 없음. None Line of Sight (NLOS).
- H matrix is hard to get (Digital Beamforming)
  - 실질적으로 H를 알기도 어렵고 SVD 계산하고 뭐시기.. 어렵다.
  - 결국 단말 아니면 기지국이 해야되는데 그게 어렵다.

#### LTE Reference Signals for MIMO

#### Single User DL - 8 Tx antennas and 2 Rx antennas (1/2)

<img width="958" alt="스크린샷 2023-10-28 오후 3 03 46" src="https://user-images.githubusercontent.com/138586629/278794502-46107254-8ba8-4dd4-a92e-c8fc16dba4f2.png">

7a5d1-7343-4209-b487-302622c7f1ba.png">
<img width="940" alt="스크린샷 2023-10-28 오후 3 03 53" src="https://user-images.githubusercontent.com/138586629/278794508-2c6c0cd0-0783-46a8-860d-d43514b7bf1f.png">

#### Multi-User DL - 8 Tx antennas and 2 Rx antennas

<img width="935" alt="스크린샷 2023-10-28 오후 3 04 39" src="https://user-images.githubusercontent.com/138586629/278794555-21043191-4f07-4be0-88f8-5d438c644b6d.png">

#### LTE Downlink Transmission Structure

<img width="955" alt="스크린샷 2023-10-28 오후 3 05 02" src="https://user-images.githubusercontent.com/138586629/278794569-25ff8e95-fb3d-43d8-ad72-94bbf845c672.png">

#### LTE MIMO Modes

<img width="856" alt="스크린샷 2023-10-28 오후 3 06 09" src="https://user-images.githubusercontent.com/138586629/278794608-e5c99ab1-6171-492a-85c9-0bd6dbc32a93.png">

## MIMO in 5G NR

- Massive MIMO
- Digital & Analog Beamforming

#### Massive MIMO for 5G NR

- “Large” number of Base Station antennas M
  - K users with typically one antenna per user
  - M >> K
- Builds on MU-MIMO
- Full-Dimensional (FD) MIMO
  - Use 2D-array antenna for 3D analog beamforming
- Generally, TDD
- Original deployment 6 GHz

<img width="504" alt="스크린샷 2023-10-28 오후 3 17 02" src="https://user-images.githubusercontent.com/138586629/278794988-25d238d0-2e4e-4f0a-9021-3d976021cbc9.png">

#### Digital Beamforming

<img width="491" alt="스크린샷 2023-10-28 오후 3 17 32" src="https://user-images.githubusercontent.com/138586629/278795003-1b4a9829-bf3c-4b25-bcb6-61d335a1bfa1.png">

#### Analog Beamforming

<img width="577" alt="스크린샷 2023-10-28 오후 3 18 04" src="https://user-images.githubusercontent.com/138586629/278795019-4ce84311-6320-488d-b3f2-50d336a6856a.png">

#### Massive MIMO Beamforming Architectures

<img width="838" alt="스크린샷 2023-10-28 오후 3 18 27" src="https://user-images.githubusercontent.com/138586629/278795042-9279f1cb-14c8-48b6-a33d-e232a553db1c.png">

#### Practical aspects of 5G NR in Low-Band (<1GHz)

<img width="620" alt="스크린샷 2023-10-28 오후 3 18 52" src="https://user-images.githubusercontent.com/138586629/278795065-b9029ce0-8ae1-429e-b03a-01922c154934.png">

#### 5G NR in Mid-Band (e.g. 3.5 GHz)

- Digital beamforming allows multiple beam directions at the same time
  from the same Array Antenna Module

<img width="603" alt="스크린샷 2023-10-28 오후 3 19 15" src="https://user-images.githubusercontent.com/138586629/278795081-1a6ae86c-589a-4d98-bbb0-2a15756e2bd3.png">

#### 5G NR in High-Band (e.g. 28 GHz)

- Due to high numbers of Tx/Rx ports, analog beamforming is used, most
  commonly in the form of hybrid beamforming.

#### MIMO Operation – High Band

<img width="764" alt="스크린샷 2023-10-28 오후 3 20 16" src="https://user-images.githubusercontent.com/138586629/278795131-4edfc387-29e0-4004-a717-29601cf1ca8d.png">

#### SSB Beam Sweeping and P1 Beam Management

#### Synchronization and System Information (3/3)

#### SSB Beam Sweeping and P2 Beam Management

#### Beam Management P3

## Questions

- Explain spatial multiplexing
  - 공간 다중화(spatial multiplexing)에 대해 설명하시오.
- Explain Zero-Forcing Precoding and Zero-Forcing Equalizer
  - Zero-Forcing Precoding과 Zero-Forcing Equalizer에 대해 설명하시오.
- What is multi-user (MU) MIMO ?
  - 다중 사용자 MIMO (MU-MIMO)란 무엇입니까?
- How can analog beamforming be used for multi-user?
  - 다중 사용자에게 아날로그 빔포밍(analog beamforming)을 어떻게 사용할 수 있나요?
- Why is the spatial multiplexing considered a beamforming?
  - 공간 다중화(spatial multiplexing)을 beamforming으로 간주하는 이유는 무엇입니까?
- What is the main difficulty (drawback) of digital beamforming compared to analog beamforming in massive (>64) MIMO ?
  - 대규모 MIMO (Massive MIMO, >64)에서 아날로그 빔포밍(analog beamforming)에 비해 디지털 빔포밍(digital beamforming)의 가장 큰 어려움(단점)은 무엇입니까?

### Explain spatial multiplexing

> 공간 다중화(spatial multiplexing)에 대해 설명하시오.

공간 다중화는 다중 안테나를 사용하여 여러 독립적인 데이터 스트림을 동시에 전송하는 무선 통신 기술이며, 데이터 전송 효율성을 향상시킵니다. 이는 다중 경로에서의 신호 품질을 향상시키고 높은 대역폭 효율성을 제공합니다.

ㄴㄴ다시 설명하면

결국 spatial multiplexing은 같은 시간, 같은 주파수임에도 불구하고 여러 개의 신호를
동시에 전송할 수 있게 해주는 것으로, SVD를 활용하여, s1, s2, ... 여러개의 채널이
서로 간섭되지 않고 얻을 수 있도록 하는 것임.

하느님으로부터(?) 주어진 매트릭스 H는 SVD에 의해 U, Sigma, V^H의 곱으로 표현할 수 있어
송신 측에서 V를 곱하고(Precoding), 수신 측에서 U^H를 곱하면 각 채널이 섞이지 않고
diagonal matrix인 Sigma의 각 값들만 곱해진 s1', s2', ... 를 얻을 수 있음.

### Explain Zero-Forcing Precoding and Zero-Forcing Equalizer

> Zero-Forcing Precoding과 Zero-Forcing Equalizer에 대해 설명하시오.

Zero-Forcing Precoding과 Zero-Forcing Equalizer는 다중 안테나 시스템에서 다중 경로 간섭을 줄이고 데이터 전송을 향상시키는 무선 통신 기술의 한 형태입니다.

**Zero-Forcing Precoding (ZFP)**:

- **역할**: Zero-Forcing Precoding은 송신 측에서 다중 안테나를 사용하여 전송하는 신호의 방향성을 조절하고 다중 경로 간섭을 줄입니다. 주로 다중 안테나 시스템에서 사용되며, 수신 측에서의 Zero-Forcing Equalizer와 함께 사용됩니다.
- **작동**: 송신기는 전송할 데이터를 안테나 간의 상호 간섭을 최소화하기 위해 가중치를 계산하여 다중 안테나에서의 각 신호를 형성합니다. 이 가중치는 신호가 수신기에서 독립적으로 처리될 수 있도록 설계됩니다.

**Zero-Forcing Equalizer (ZFE)**:

- **역할**: Zero-Forcing Equalizer는 수신 측에서 신호를 처리하여 다중 경로 간섭을 줄이고 데이터를 복원합니다. 송신 측의 Zero-Forcing Precoding과 함께 사용되며, 다중 경로에서의 신호를 복원하기 위해 설계됩니다.
- **작동**: 수신기는 수신된 다중 안테나에서의 신호를 독립적으로 처리하고 각 안테나에서의 데이터를 복원하기 위해 가중치를 계산합니다. 이 가중치는 송신기에서의 Zero-Forcing Precoding과 반대로 작동하여 각 안테나의 신호 간 상호 간섭을 최소화합니다.

Zero-Forcing Precoding과 Zero-Forcing Equalizer는 다중 안테나 시스템에서의 데이터 전송 품질을 향상시키는 데 사용됩니다. 이들은 다중 경로 간섭을 줄이고 다중 안테나에서의 신호를 효율적으로 처리하여 무선 통신 시스템의 성능을 향상시킵니다.

### What is multi-user (MU) MIMO ?

> 다중 사용자 MIMO (MU-MIMO)란 무엇입니까?

다중 사용자 MIMO (Multi-User Multiple Input, Multiple Output 또는 MU-MIMO)는 무선 통신 시스템에서 여러 사용자에게 동시에 데이터를 전송하는 기술입니다. 이 기술은 다중 안테나 시스템과 다중 사용자 환경을 결합하여 효율적인 데이터 전송을 실현하며, 다음과 같은 특징을 가집니다:

1. **다중 안테나(MIMO)**: MU-MIMO는 다중 안테나(MIMO) 기술을 활용합니다. 다중 안테나는 송신기와 수신기 모두에서 다수의 안테나를 사용하여 데이터 전송과 수신을 병렬로 처리하는 기술로, 안테나 간의 독립성을 활용하여 데이터 전송 효율성을 높입니다.

2. **동시 다중 사용자 지원**: MU-MIMO는 다수의 사용자에게 동시에 데이터를 전송할 수 있습니다. 이는 사용자 간의 동시 데이터 스트림을 지원하고 각 사용자에게 높은 대역폭을 할당할 수 있음을 의미합니다.

3. **공간적 분리**: MU-MIMO는 다수의 안테나를 사용하여 공간적으로 분리된 사용자에게 데이터를 전송할 수 있습니다. 이를 통해 서로 다른 방향에 있는 사용자 간의 간섭을 줄이고 신호 품질을 향상시킵니다.

4. **빔포밍**: MU-MIMO는 빔포밍 기술을 사용하여 각 사용자로 데이터를 정확하게 방향성을 조절하여 전송합니다. 이를 통해 데이터를 효과적으로 전달하고 다중 경로 환경에서의 간섭을 줄일 수 있습니다.

MU-MIMO는 주로 Wi-Fi 라우터, LTE, 5G, WiMAX 및 다른 무선 통신 시스템에서 사용됩니다. 이 기술은 다중 사용자 환경에서 데이터 전송 효율성을 향상시키며, 사용자 간의 데이터 전송 속도와 신호 품질을 향상시킵니다. MU-MIMO는 무선 네트워크의 성능을 높이고 다수의 동시 접속을 지원하는 데 기여합니다.

### How can analog beamforming be used for multi-user?

> 다중 사용자에게 아날로그 빔포밍(analog beamforming)을 어떻게 사용할 수 있나요?

다중 사용자에게 아날로그 빔포밍 (Analog Beamforming)을 사용하는 주요 방법은 다중 사용자 MIMO (MU-MIMO) 시스템에서 데이터 스트림을 특정 방향으로 집중시키는 것입니다. 아날로그 빔포밍을 통해 서로 다른 사용자에 대한 빔을 형성하고 사용자 간의 간섭을 최소화할 수 있습니다. 다음은 다중 사용자에게 아날로그 빔포밍을 사용하는 일반적인 절차입니다:

1. **다중 안테나 시스템 구성**: 먼저, 다중 안테나 시스템을 송신기 측과 수신기 측 모두에 구성합니다. 이는 다중 안테나 MIMO 시스템의 일부로, 안테나 배열이 있어야 합니다.

2. **사용자 식별 및 채널 정보 획득**: 시스템은 서로 다른 다중 사용자를 식별하고, 각 사용자 간의 채널 상태 정보를 수집합니다. 이 정보는 각 사용자의 위치, 신호 전달 경로 및 신호 품질을 나타내는 데 사용됩니다.

3. **빔포밍 벡터 설계**: 아날로그 빔포밍은 특정 방향으로 신호를 집중시키기 위한 빔포밍 벡터를 설계하는 단계입니다. 이 벡터는 다수의 안테나 중 몇 개의 안테나를 활용하여 특정 사용자의 신호를 강화하고 다른 사용자의 신호를 약화시키는 데 사용됩니다.

4. **빔 형성 및 데이터 전송**: 설계된 빔포밍 벡터를 사용하여 빔을 형성하고, 각 사용자에게 데이터를 전송합니다. 이는 각 사용자에게 신호를 특정 방향으로 전송하는 것을 의미하며, 이를 통해 간섭을 최소화하고 사용자 간의 데이터 전송 품질을 향상시킬 수 있습니다.

5. **수신 및 복원**: 수신기에서는 수신된 다중 사용자 신호를 복원하고 각 사용자의 데이터 스트림을 분리합니다. 이러한 과정은 빔포밍 벡터를 사용하여 각 사용자의 신호를 특정 안테나로부터 강조하고 다른 사용자의 간섭을 줄이는 방식으로 작동합니다.

다중 사용자에게 아날로그 빔포밍을 사용하면 여러 사용자 간의 간섭을 최소화하고 데이터 전송 품질을 향상시킬 수 있습니다. 이는 무선 통신 시스템에서 고밀도 다중 사용자 환경에서 유용하며, 5G와 같은 다음 세대 무선 통신 시스템에서도 중요한 역할을 합니다.

### Why is the spatial multiplexing considered a beamforming?

> 공간 다중화(spatial multiplexing)을 beamforming으로 간주하는 이유는 무엇입니까?

공간 다중화 (Spatial Multiplexing)와 빔포밍 (Beamforming)은 둘 다 다중 안테나 시스템을 사용하는 무선 통신 기술이지만 목표와 작동 방식에서 차이가 있습니다. 그럼에도 불구하고 이 두 개념을 종종 혼동하거나 함께 언급하는 이유는 몇 가지 이유가 있습니다:

1. **다중 안테나 사용**: 두 기술 모두 다중 안테나 시스템을 사용하여 데이터 전송을 향상시킵니다. 공간 다중화에서는 안테나 간의 독립성을 활용하여 다수의 데이터 스트림을 동시에 전송하고 수신하는 것이 목표입니다. 빔포밍에서도 다중 안테나를 사용하여 신호를 특정 방향으로 집중시키거나 간섭을 줄이는 것이 중요합니다.

2. **안테나 배열**: 두 기술은 안테나 배열을 활용합니다. 공간 다중화에서는 안테나 배열을 사용하여 다수의 데이터 스트림을 전송하고 수신합니다. 빔포밍에서는 안테나 배열을 사용하여 빔을 형성하거나 특정 방향으로 신호를 전파합니다.

3. **안테나 가중치**: 빔포밍과 공간 다중화 모두 안테나 간의 가중치를 조절하여 데이터 전송을 제어합니다. 공간 다중화에서는 각 안테나에 대한 가중치를 사용하여 다중 데이터 스트림을 조절합니다. 빔포밍에서는 안테나 간의 가중치를 사용하여 빔의 방향성을 조절합니다.

4. **무선 통신 향상**: 이 두 기술은 모두 무선 통신 시스템의 성능을 향상시키는 데 중요하며, 다중 안테나를 효과적으로 활용하여 데이터 전송 품질을 개선합니다.

그러나 빔포밍과 공간 다중화는 목표와 작동 방식에서 다르며, 주요한 차이가 있습니다. 빔포밍은 주로 신호의 방향성을 제어하고 간섭을 줄이는 데 사용되며, 공간 다중화는 다수의 데이터 스트림을 동시에 전송하는 데 사용됩니다. 종종 이러한 두 개념이 함께 사용되거나 혼동되기도 하지만, 각각의 목표와 적용 시나리오를 이해하는 것이 중요합니다.

### What is the main difficulty (drawback) of digital beamforming compared to analog beamforming in massive (>64) MIMO ?

> 대규모 MIMO (Massive MIMO, >64)에서 아날로그 빔포밍(analog beamforming)에 비해 디지털 빔포밍(digital beamforming)의 가장 큰 어려움(단점)은 무엇입니까?

공간 다중화 (Spatial Multiplexing)와 빔포밍 (Beamforming)은 둘 다 다중 안테나 시스템을 사용하는 무선 통신 기술이지만 목표와 작동 방식에서 차이가 있습니다. 그럼에도 불구하고 이 두 개념을 종종 혼동하거나 함께 언급하는 이유는 몇 가지 이유가 있습니다:

1. **다중 안테나 사용**: 두 기술 모두 다중 안테나 시스템을 사용하여 데이터 전송을 향상시킵니다. 공간 다중화에서는 안테나 간의 독립성을 활용하여 다수의 데이터 스트림을 동시에 전송하고 수신하는 것이 목표입니다. 빔포밍에서도 다중 안테나를 사용하여 신호를 특정 방향으로 집중시키거나 간섭을 줄이는 것이 중요합니다.

2. **안테나 배열**: 두 기술은 안테나 배열을 활용합니다. 공간 다중화에서는 안테나 배열을 사용하여 다수의 데이터 스트림을 전송하고 수신합니다. 빔포밍에서는 안테나 배열을 사용하여 빔을 형성하거나 특정 방향으로 신호를 전파합니다.

3. **안테나 가중치**: 빔포밍과 공간 다중화 모두 안테나 간의 가중치를 조절하여 데이터 전송을 제어합니다. 공간 다중화에서는 각 안테나에 대한 가중치를 사용하여 다중 데이터 스트림을 조절합니다. 빔포밍에서는 안테나 간의 가중치를 사용하여 빔의 방향성을 조절합니다.

4. **무선 통신 향상**: 이 두 기술은 모두 무선 통신 시스템의 성능을 향상시키는 데 중요하며, 다중 안테나를 효과적으로 활용하여 데이터 전송 품질을 개선합니다.

그러나 빔포밍과 공간 다중화는 목표와 작동 방식에서 다르며, 주요한 차이가 있습니다. 빔포밍은 주로 신호의 방향성을 제어하고 간섭을 줄이는 데 사용되며, 공간 다중화는 다수의 데이터 스트림을 동시에 전송하는 데 사용됩니다. 종종 이러한 두 개념이 함께 사용되거나 혼동되기도 하지만, 각각의 목표와 적용 시나리오를 이해하는 것이 중요합니다.
