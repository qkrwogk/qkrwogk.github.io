# 231005

MIMO (Multi-Input Multi-Output)

## 목차

- 리뷰
- Contents
- MIMO
  - What is MIMO
  - The propagation channel
  - MIMO and Shannon Capacity
  - **MIMO modes**
    - **Diversity**
    - **Beamforming**
    - **Spatial multiplex**
  - MU-MIMO (LTE)
  - Massive MIMO (5G NR)
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

#### The Propagation Channel is still a Linear System – a complex number

#### Estimating the Channel State

- "s" is known to receiver
  - "s"는 수신자에게 알려진다.
- CSI-RS and SRS are for this purpose
  - CSI-RS와 SRS는 이를 위한 것이다.

#### Multiple Propagation Channels (다중 전파 채널)

<img width="866" alt="스크린샷 2023-10-22 오후 6 25 53" src="https://user-images.githubusercontent.com/138586629/277156167-c35b3114-03c7-41fd-8140-66f144d34915.png">

#### General Channel Matrix (일반 채널 매트릭스)

<img width="952" alt="스크린샷 2023-10-22 오후 6 27 10" src="https://user-images.githubusercontent.com/138586629/277156220-53fc05f3-d096-4cb5-af8a-dd5980ffd61d.png">

#### Shannon Capacity

- Over path from one Tx antenna to one Rx antenna
  - Data rate limit over which error free communication is impossible.

<img width="982" alt="스크린샷 2023-10-22 오후 6 30 10" src="https://user-images.githubusercontent.com/138586629/277156336-cab6beb0-3740-42e1-8f10-fa72d8ad2f04.png">

#### General MIMO Capacity

<img width="957" alt="스크린샷 2023-10-22 오후 6 31 14" src="https://user-images.githubusercontent.com/138586629/277156391-0629c523-6180-4d69-a7dd-c3060325991c.png">

- Note that we will compare SISO and MIMO capacity with the same transmit power.
  - 앞으로 같은 전송 전력에서 SISO와 MIMO 용량을 비교할것임.

#### Parallel Non-coupled Channels

<img width="954" alt="스크린샷 2023-10-22 오후 6 33 47" src="https://user-images.githubusercontent.com/138586629/277156511-efb80869-3f1d-4f38-9a58-642f1f92b12b.png">

#### Before discussing three MIMO modes - Polarization of Electromagnetic Wave

- For the electromagnetic wave the polarization is effectively the plane in which the electric wave vibrates
- Antennas are sensitive to polarization, and generally only receive or transmit **a signal with a particular polarization**

<img width="410" alt="스크린샷 2023-10-22 오후 6 35 46" src="https://user-images.githubusercontent.com/138586629/277156590-e1e5d5ec-007d-43ee-a48a-d87db78ed2eb.png">

#### Antenna Polarization(안테나 양극화)

- Many mobile communication systems may rely on the fact that there are likely to be many reflections between the transmitter and the receiver and these will tend to mean that a signal will have a particular polarization when it reaches the receiver
  - 많은 이동 통신 시스템은 송신기와 수신기 사이에 많은 반사가 있을 수 있다는 사실에 의존할 수 있으며 이는 신호가 수신기에 도달할 때 특정 편파를 갖게 된다는 것을 의미하는 경향이 있다.
- Most base stations have dual-polarized antennas : +45o and - 45o
  - 대부분의 기지국에는 45도 및 -45도의 이중 편파 안테나가 있다.
  - Avoid no effective electric field at the receiver
    - 수신기에서 효과적인 전기장이 발생하지 않도록 해야 함.
  - Combined before ADC – baseband signal processing does not take this into account.
    - ADC 이전에 결합 - 기저대역 신호 처리에서는 이를 고려하지 않음.

## MIMO Mode

### 1. Diversity

#### MIMO Mode (1/3) - Diversity

- 시간/주파수 다양성

- 공간 (안테나) 다양성 - 스펙트럼 효율성 손실 없이 달성됨
  - 수신 다양성 (다중 수신 안테나)
  - 전송 다양성 (다중 전송 안테나)

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

#### Maximal Ratio Combining (MRC) for Receive Diversity

<img width="1002" alt="스크린샷 2023-10-22 오후 6 49 15" src="https://user-images.githubusercontent.com/138586629/277157172-c5f077ae-73cb-4d83-93e6-43a777ddec5d.png">

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

#### Transmit Diversity in Space-Time Block Code

- 2개의 안테나, 2개의 time instance
- STBC, a.k.a Alamouti Code

#### Decoding of Alamouti Code

<img width="844" alt="스크린샷 2023-10-22 오후 7 01 34" src="https://user-images.githubusercontent.com/138586629/277157677-8dc0fc03-6e8c-4772-b335-4efec3987f71.png">

### 2. Beamforming

#### MIMO Mode (2/3) - Beamforming

- Definition of the beamforming : Focusing the transmitted energy toward the intended receiver rather than spraying the energy indiscriminately.
- 빔포밍 정의 : 무분별하게 에너지를 뿌리는 것이 아니라, 송신된 에너지를 원하는 수신자에게 집중시키는 것.
- Spatial multiplexing is also possible to increase system capacity
  - 시스템 용량 증가를 위한 공간 다중화도 가능.

#### Analog Beamforming – theory

<img width="787" alt="스크린샷 2023-10-22 오후 7 05 03" src="https://user-images.githubusercontent.com/138586629/277157820-b1c394b2-b51d-462d-8579-c8ca45ecfe97.png">

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
