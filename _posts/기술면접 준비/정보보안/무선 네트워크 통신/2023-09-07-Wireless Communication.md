# 230907

## 목차

- Contents of Week1
- Wireless Communication
  - 주파수
    - Propagation (전파)
    - Modulation (변조)
    - Radio Frequency and Baseband (무선 주파수(radio=wireless)와 기저대역)
  - 대역폭 (bandwidth)
  - Spectrum for 5G
    - Spectrum for Mobile Systems (모바일 시스템을 위한 스펙트럼)
    - Frequency Bands for NR (NR(New Radio)을 위한 주파수 대역)
    - RF Exposure Above 6GHz (6GHz를 초과한 무선 노출)
- Questions

## Contents of Week1

- 주파수 (frequency)

  - Propagation(전파)
  - Modulation(변조)
  - Radio Frequency and Baseband (무선 주파수(radio=wireless)와 기저대역)

- 대역폭 (bandwidth)

- Spectrum of 5G
  - Spectrum for Mobile Systems (모바일 시스템을 위한 스펙트럼)
  - Frequency Bands for NR (NR(New Radio)을 위한 주파수 대역)
  - RF Exposure Above 6GHz (6GHz를 초과한 무선 노출)

## 주파수 - 전파

### Wireline Communication과 Wireless Communication 간엔 어떤 차이가 있을까?

### Electric Circuit과 그로 인한 Electromagnetic Wave (전자기 유도)

- Gauss' Law
- Gauss' Law for magnetism
- Faraday's Law
- Ampere-Maxwell Law

### Signal Propagation Basic (신호 전파의 기본)

- RF(무선 주파수) 신호는 빛의 속도로 공간을 통해 전파한다 (`c = 3*10^8 m/s`)

  - 빛의 속도
  - `Wavelength(파장) = c/frequency`
  - Physical size is discussed in terms of wavelength(파장)
    -> propagation characteristics vary with frequency
    - 300 MHz -> 1 meter
    - 3 GHz -> 10 cm
    - 30 GHz -> 1 cm (이 이상은 mmWave)

- Power Density and dB (전력 밀도와 데시벨)
  - 전파 손실은 in-out(입력과 출력의) 전력 비율로 설명한다.
    - `dB = 10 log (P_2/P_1)`
  - 전압은 루트로 다루어짐.

### Free Space Propagation (자유공간 전파)

- 두 개의 안테나 사이에 장애물이 없는 경우 안테나 사이의 전파 방식

  - 전송 안테나는 등방성(isotropic, 모든 방향으로 동일한 전파를 보냄)이여야 함.

- 등방성 전송(tx) 안테나와의 거리가 r일 때, 전달받는 전력 밀도는

  - <img width="287" alt="스크린샷 2023-10-21 오후 3 51 41" src="https://user-images.githubusercontent.com/138586629/277093281-e6266f45-c4b5-4f64-9001-39234e3fd208.png">

- 등방성 수신 안테나의 **Effective area** 는 다음으로 나타낼 수 있다.

  - <img width="46" alt="스크린샷 2023-10-21 오후 3 54 29" src="https://user-images.githubusercontent.com/138586629/277093389-2031f383-9c74-4015-a832-b9737add2969.png">

- 전달받는 전력,

<img width="690" alt="스크린샷 2023-10-21 오후 3 55 34" src="https://user-images.githubusercontent.com/138586629/277093429-d15ac488-2eb1-47a8-b2e5-af22f4f229f0.png">

### 측정 활동

그냥 여기저기 위치에서 측정하곤 한다.

### Ray Tracing Approach(전파 추적 기술)

무선 통신에서 전파의 전파/반사를 모델링하고 예측하기 위해 사용되는 시뮬레이션 기술

- 결과값이 이러이러하게 나왔단걸 보여주심.

## 주파수 - 변조, 무선 주파수와 기저대역

- 우린 이제 전기 신호가 회로 없이도 전파될 수 있단 걸 알았다. "무선"으로!
- 그럼 어떻게 무선으로 전파되는 신호를 `변조`할 수 있을까?

### 메세지를 전달하기 위해서

- 우리는 전자기장(elctromagnetic fields)을 변조해야 한다.

- 높은 주파수 신호는 낮은 주파수에 의해 변조가 된다!
  - 안테나 크기는 파장(wavelength)의 순서대로다. (안테나의 크기와 사용되는 무선 주파수 파장이 서로 관련이 있다)
  - 메시지의 주파수는 일반적으로 carrier signal의 주파수보다 훨씬 낮다. 특히 아날로그 통신에서 그렇다.

<img width="406" alt="스크린샷 2023-10-21 오후 4 08 15" src="https://user-images.githubusercontent.com/138586629/277093921-8057d50f-82fe-4763-809e-f1eacf9744a4.png">

### 디지털 커뮤니케이션 시스템 (Digital Communication System) _(매우 중요)_

<img width="914" alt="스크린샷 2023-10-21 오후 4 11 57" src="https://user-images.githubusercontent.com/138586629/277094055-9a25c061-079d-404b-9774-2100709d7f4b.png">

### Digital Communication

- 디지털 변조와 복조란?

<img width="478" alt="스크린샷 2023-10-21 오후 4 14 24" src="https://user-images.githubusercontent.com/138586629/277094138-817c040d-894b-4f9b-940a-7c1d5a283b9b.png">

- 결국 상대로부터 수신한 신호가 어떤 메세지를 담고 있는지를 유추하는 것이다.

  - a는 0은 아무 신호도 없는 것으로 구분
  - b는 주파수로 0, 1 구분
  - c도 뭐시기 저시기로 구분

- **핵심 : 높은 주파수(수 GHz)의 EM wave를 통하여 digital information을 전달할 수 있다.**

### 무선 주파수와 기저대역(Radio Frequency and Baseband)

- 무선 주파수(RF) 신호는 송신되고 수신된다.

- RF-회로는 RF-아날로그 신호와 기저(baseband) 디지털 신호 간의 `변환`을 처리한다.

  - RF-신호는 `Carrier`라고 부름
  - Digital = 메모리에 저장되는 것
  - cos-square & sin-square 이 수신기에 쓰인다.

- 기저대역(Baseband) 신호는 우리의 주요 관심사이다.

  - discrete time, discrete value (이산 시간, 이산 값. 불연속적이라는 뜻)
  - 여기에 노이즈가 섞이기 때문에 노이즈의 영향을 받지 않고 이산 값을 복구하는 게 주요 이슈임

- 2개의 스트림이 있음 : In-phase(같은 주파수와 위상), Quadrature(In-phase와 90도 위상 차이)
  - 이들은 서로 직교 짝(orthogonal pair)로 사용되며, 서로 간섭이 없음.

### 더 나아가기 전에

- 우리가 할 수 있는 것은

  - 한 가지 유한한 RF 파형(전자기파)를 대기로 전송하여 메시지를 전달하는 것.

- 이슈는 뭐냐
  - 나 혼자만 전송하는 게 아님.
  - 수신기가 발신기의 의도를 어떻게 인식할 수 있는지? 이것이 문제.

### Multiplexing(다중화)

- 지금까지의 가정은 단일 사용자일 때였음. 여러명이라면?

### Frequency Selective Filter

19p.

### Smooth vs. Not Smooth

### Resistance plus Capacitor makes frequency selective filter

### How about wireline communication?

## 대역폭 (bandwidth)

### 대한민국 주파수 분배도표

<img width="807" alt="스크린샷 2023-10-21 오후 4 33 38" src="https://user-images.githubusercontent.com/138586629/277094826-dfd1bc70-2182-477f-832e-b8edd4227a8f.png">

### Radio Regulation

### World Radio Conference (WRC)

... 쓸데없음 말만 들어

## Spectrum for 5G

- Spectrum for Mobile Systems (모바일 시스템을 위한 스펙트럼)
- Frequency Bands for NR (NR(New Radio)을 위한 주파수 대역)
- RF Exposure Above 6GHz (6GHz를 초과한 무선 노출)

### 모바일 통신에서의 주파수 스펙트럼

#### WRC-identified IMT-frequency

#### 28GHz for 5G

#### 대역폭 경매 낙찰

### RF Characteristics

#### RF Characteristics : Spectrum Flexible

#### RF Characteristics : RF requirements by 3GPP

#### RF Characteristics : Channel BW and Transmission BW

#### RF Characteristics : Device & BS(TX) requirements

#### RF Characteristics : How their requirements are checked?

#### RF Characteristics : How they look?

## Questions

### What is the Maxwell equation and how is it related to the wireless communication?

> Maxwell equation은 무엇이고, 무선 통신과 어떤 관련성이 있는가?

<img width="498" alt="스크린샷 2023-10-05 오후 9 47 46" src="https://user-images.githubusercontent.com/138586629/272906916-d02cd16f-102d-44db-aa2b-8e9fbcc17779.png">

<img width="468" alt="스크린샷 2023-10-05 오후 9 49 11" src="https://user-images.githubusercontent.com/138586629/272907286-ba7d357b-4600-4cff-abea-8adf072a7b21.png">

학습메모 1 참고. 맥스웰 방정식은 결국 전자기파의 존재를 증명했다. <br /><br />

이로 인해 전력이 발생하면 신호가 전파되고 무선 통신이 가능한 것이다.

- Explain a wave’s frequency and wavelength (=파장).
  - 파동의 주파수와 파장에 대해 설명하시오.
- What are the 5G mobile communication frequencies?
  - 5G 모바일 통신 주파수는 어떻게 되는가?
- Why is a high frequency needed and how high is it?
  - 통신에 높은 주파수가 왜 필요하며 얼마나 높아야 하는가?
- Explain high-level pros and cons of FR1 and FR2.
  - FR1과 FR2가 high-level일 때의 장단점은 무엇인가?
- How is a high frequency EM wave used for wireless communication?
  - 고주파 EM 파동이 무선통신에 어떻게 사용되는가?
- Explain the bandwidth.
  - 대역폭에 대해 설명하시오.
- What is the interference and why is it important?

- Explain source/channel coding, modulation in wireless communication.

## 학습메모

1. [Maxell 방정식](https://blog.naver.com/wisdom0719/221260269943)
