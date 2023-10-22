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

#### Frequency Selective Filter

<img width="710" alt="스크린샷 2023-10-22 오후 7 26 55" src="https://user-images.githubusercontent.com/138586629/277158831-fb6a8b09-a9c3-4fa9-bf04-6f9af55bdf37.png">

#### Smooth vs. Not Smooth

- Suppose that you are allowed to use 3.5 GHz. What you can do ?
  - 3.5GHz를 사용할 수 있다고 가정하자. 무엇을 할 수 있나?

#### Resistance plus Capacitor makes frequency selective filter

저항과 커패시터를 더해 주파수 선택 필터를 만듬.

- At the transmitter
  - 송신기에서
  - In addition to the low frequency (smooth waveform)
    - 저주파에 추가 (부드러운 파형)
  - Limit the frequency range of the transmitted signal
    - 전송된 신호의 주파수 범위를 제한한다.
  - Do not want to interfere frequency band (spectrum) others
    - 다른 주파수 대역(스펙트럼)을 간섭하고 싶지 않음
- At the receiver
  - 수신기에서
  - Reject other users’ signal – do not be interfered by other frequency band (spectrum) users
    - 다른 사용자의 신호를 거부한다 - 다른 주파수 대역(스펙트럼) 사용자의 간섭을 받지 않음
  - Recover the baseband signal by rejecting 2 times carrier frequency component generated by cos/sin square
    - cos/sin square에 의해 생성된 2배의 반송파 주파수 성분을 제거하여 기저대역 신호를 복구함

#### How about wireline communication?

유선 통신에서는 어떤가?

- In order to avoid co-channel (=same frequency) interference, which cannot be nullified by frequency-selective filter, bandwidth are artificially limited in wireless communication
  - 주파수 선택 필터로 무효화할 수 없는 동일 채널(=동일 주파수) 간섭을 피하기 위해 무선 통신에서는 대역폭을 인위적으로 제한함.
  - Such a regulatory bandwidth limitation practically limits the data rate
- No interference from other frequency band (spectrum) users
  - 이러한 규제 대역폭 제한은 데이터 속도를 실질적으로 제한함.
  - No regulatory bandwidth limitation in wireline communication
    - 다른 주파수 대역(스펙트럼) 사용자의 간섭이 없음
  - Infinite bandwidth and therefore infinite capacity in wireline communication ?
    - 유선 통신의 대역폭이 무한하므로 용량도 무한한가?

## 대역폭 (bandwidth)

- 동일 채널 간섭을 피하기 위해, 대역폭은 당국에 의해 반드시 인위적으로 조정되어야 한다.

#### 대한민국 주파수 분배도표

<img width="807" alt="스크린샷 2023-10-21 오후 4 33 38" src="https://user-images.githubusercontent.com/138586629/277094826-dfd1bc70-2182-477f-832e-b8edd4227a8f.png">

#### Radio Regulation

- 무선 규제 : 국제 무선 컨퍼런스(WRC)에서 정함.

### World Radio Conference (WRC)

- 여기서 무선 규제 제/개정함.

## Spectrum for 5G

- Spectrum for Mobile Systems (모바일 시스템을 위한 스펙트럼)
- Frequency Bands for NR (NR(New Radio)을 위한 주파수 대역)
- RF Exposure Above 6GHz (6GHz를 초과한 무선 노출)

### 모바일 통신에서의 주파수 스펙트럼

#### (Frequency) Spectrum for Mobile Communication

- 1G & 2G : 800~900 MHz
- 3G : ~ 2GHz
- 4G : 450 MHz ~ around 6GHz
- 5G :
  - ~3.5GHz and
  - High Speed Communication -> Large BW : enhanced Mobile BroadBand (eMBB)
  - No global large bandwidth for 450 MHz ~ around 6GHz
  - Let’s go 24 GHz and above ~~

#### WRC-identified IMT-frequency

#### 28GHz for 5G

- 27.5 ~ 29.5 GHz, mmWave 대역
- Wide bandwidth for high-speed communication
  - 고속 통신을 위한 넓은 대역폭
- Propagation characteristics is not good, especially for Non-Line of Sight (NLoS) communication
  - 특히 NLoS(Non-Line of Sight) 통신의 경우 전파 특성이 좋지 않음.
  - Suitable for dense urban, hotspot area
    - 밀집된 도시, 핫스팟 지역에 적합

#### 대역폭 경매 낙찰

- 5G도 실질적으로는 3.5GHz 대역을 가장 많이 이용하며, 찐 5G라고 불리는 28GHz는 결국 안씀.
  - 반쪽짜리 5G라고 함 그래서

### RF Characteristics

#### RF Characteristics : Spectrum Flexible

- 3G/4G/5G에 사용되는 주파수는 다양하며, 특히 5G의 경우
  - 대역폭 : 5MHz ~ 3GHz
  - 캐리어 주파수 1GHz ~ 86GHz
  - FDD/TDD
- 고려해야 할 사항
  - LTE/5G NR은 동일한 주파수에서 공존할 수 있음
  - 부반송파 간격은 15~240kHz로 다양할 수 있음
    - RF 회로에 영향을 줌

#### RF Characteristics : RF requirements by 3GPP

- Not only the requirement limits but also the definitions and conformance testing aspects may be quite different at different frequency ranges.
  - 요구사항 제한뿐만 아니라 정의 및 적합성 테스트 측면도 주파수 범위에 따라 상당히 다를 수 있음.
  - FR1 : 450 ~ 6,000MHz, coexist(공존) with LTE
  - FR2 : 24,250 ~ 52,600MHz, only for NR (NR 전용) – mmWave
- FR1 vs. FR2
  - Path loss(경로 손실) and Wavelength(파장) for Massive MIMO
  - Impacted RF components : A/D & D/A converters, LO generator, PA efficiency, filtering
    - 영향을 받는 RF 구성 요소 : A/D 및 D/A 변환기, LO 생성기, PA 효율, 필터링

#### RF Characteristics : Channel BW and Transmission BW

- The spectrum utilization expressed as a fraction is up to 98% for the widest channel bandwidths and it is above 90% for all cases, except for the smaller bandwidths
  - 분수로 표현된 스펙트럼 활용도는 가장 넓은 채널 대역폭의 경우 최대 98%이며 더 작은 대역폭을 제외한 모든 경우에 대해 90%를 초과함.
- Subcarrier Spacing = delta f, typically 15~240 kHz
  - 부운반파 간격 = delta f, 일반적으로 15~240kHz
- Lots of (sub)carriers are used within a single transmission bandwidth
  - 단일 전송 대역폭 내에서 많은 (부)운반파가 사용됨

#### RF Characteristics : Device & BS(TX) requirements

- They must not invade other spectrum
  - 다른 스펙트럼을 침범해서는 안됨.
- Within the bandwidth, they have to be very accurate
  - 대역폭 내에서는 매우 정확해야 함.

출력 전력 레벨, 전송 신호 품질, 원치 않는 출력

기지국 요구사항, 장비 요구사항 별로..

<img width="701" alt="스크린샷 2023-10-22 오후 8 18 05" src="https://user-images.githubusercontent.com/138586629/277161176-fce2b28c-74af-4b9a-8350-a1885469d7ac.png">

- Receiver should accurately operate, but not a regulatory issue
  - 수신기는 정확하게 작동해야 하지만 규제 문제는 아님

<img width="717" alt="스크린샷 2023-10-22 오후 8 18 16" src="https://user-images.githubusercontent.com/138586629/277161185-45a8d48a-46fa-48a4-b098-cc1b4ed0fcfd.png">

#### RF Characteristics : How their requirements are checked?

- Conducted Requirements are checked
  - 전도 요구 사항을 확인함
  - Defined and measured at an antenna connector
    - 안테나 커넥터에서 정의 및 측정됨
  - For LTE and previous generations, FR1
    - LTE 및 이전 세대의 경우, FR1
- Radiated Requirements are checked
  - 방사 요구사항을 확인함
  - requirements and testing are done OTA (Over-the-Air), newly for FR2
    - 요구사항 및 테스트는 FR2에 대해 새로 수행된 OTA(Over-The-Air)로 수행됨
  - With the higher number of antenna elements for operation in FR2 and the high level of integration expected when using mm-wave technology, conducted requirements are no longer seen as feasible.
    - FR2에서 작동하기 위한 더 많은 수의 안테나 요소와 mm-wave 기술을 사용할 때 예상되는 높은 통합 수준으로 인해 전도 요구사항은 더 이상 실현 가능한것으로 간주되지 않음.

#### RF Characteristics : How they look?

- Zero-IF

<img width="748" alt="스크린샷 2023-10-22 오후 8 41 40" src="https://user-images.githubusercontent.com/138586629/277162245-e6199567-45e0-47d7-a338-9a1032418d46.png">

## Questions

- What is the Maxwell equation and how is it related to the wireless communication?
  - Maxwell 방정식은 무엇이며 무선 통신과 어떤 관련이 있는가?
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
  - 간섭이란 무엇이고 왜 중요한가?
- Explain source/channel coding, modulation in wireless communication.
  - 무선 통신의 소스/채널 코딩, 변조에 대해 설명하시오.

#### What is the Maxwell equation and how is it related to the wireless communication?

> Maxwell equation은 무엇이고, 무선 통신과 어떤 관련성이 있는가?

<img width="498" alt="스크린샷 2023-10-05 오후 9 47 46" src="https://user-images.githubusercontent.com/138586629/272906916-d02cd16f-102d-44db-aa2b-8e9fbcc17779.png">

<img width="468" alt="스크린샷 2023-10-05 오후 9 49 11" src="https://user-images.githubusercontent.com/138586629/272907286-ba7d357b-4600-4cff-abea-8adf072a7b21.png">

학습메모 1 참고. 맥스웰 방정식은 결국 전자기파의 존재를 증명했다. <br /><br />

이로 인해 전력이 발생하면 신호가 전파되고 무선 통신이 가능한 것이다.

#### Explain a wave’s frequency and wavelength (=파장).

> 파동의 주파수와 파장에 대해 설명하시오.

- 주파수 (Frequency)
  - 주파수는 파동이 한 단위 시간 동안 진동하는 횟수를 나타내는 물리적 양입니다. 주로 헤르츠(Hz) 단위로 표현됩니다.
- 파장 (Wavelength)
  - 파장은 파동의 한 주기에서 한 번의 진동에서 다음 진동까지의 거리 또는 공간입니다. 파장은 주로 미터(m) 단위로 표현됩니다.
- 파장 = 속도 / 주파수

#### What are the 5G mobile communication frequencies?

> 5G 모바일 통신 주파수는 어떻게 되는가?

1. 하이 밴드 (mmWave):

- mmWave 주파수 대역은 24GHz 이상의 매우 고주파수 대역에서 작동합니다. 이러한 주파수 대역은 고대역폭과 빠른 데이터 전송 속도를 제공합니다.
- mmWave는 주로 도시 밀집 지역과 스타디움과 같은 밀집된 지역에서 사용되며, 단거리 통신 및 초고속 데이터 전송에 적합합니다.

2. 중간 밴드 (Sub-6 GHz):

- 중간 밴드는 5G의 주요 주파수 대역 중 하나로, 주로 2GHz에서 6GHz 범위에 속하는 주파수를 사용합니다.
- 중간 밴드는 mmWave보다 더 긴 전파 거리를 제공하며, 도시 내 및 외부 지역에서 널리 사용됩니다.

3. 저주파수 밴드 (Low Band):

- 저주파수 밴드는 주로 600MHz에서 2GHz 범위의 주파수를 사용하며, 광범위한 무선 커버리지를 제공합니다.
- 이 주파수 대역은 높은 전파 거리를 갖고 있어 시골 및 농촌 지역과 같은 지역에서 사용되며, 5G 커버리지 확장을 지원합니다.

각 국가 및 통신 사업자는 5G 네트워크를 구축할 때 사용할 주파수 대역을 결정하며, 이로 인해 국가 및 지역마다 다른 주파수 대역이 사용된다. 따라서 실제로 사용되는 5G 주파수 대역은 국가 및 지역에 따라 다를 수 있다.

#### Why is a high frequency needed and how high is it?

> 통신에 높은 주파수가 왜 필요하며 얼마나 높아야 하는가?

1. 대역폭 확보 및 데이터 처리량 증가:

- 높은 주파수를 사용하면 더 넓은 대역폭을 사용할 수 있습니다. 대역폭은 데이터 전송 속도와 데이터 처리량을 결정하는 중요한 요소입니다. 더 높은 주파수는 더 많은 데이터를 더 빠르게 전송할 수 있도록 합니다. 이는 대용량 미디어 스트리밍, 초고화질 비디오 통화, 대용량 파일 다운로드와 같은 고대역폭 요구 사항을 충족하는 데 도움이 됩니다.

2. 밀집된 지역 및 다중 접속 관리:

- 높은 주파수를 사용하면 더 많은 안테나 및 기지국을 작은 지역에 배치할 수 있습니다. 이는 도시의 밀집된 지역 또는 이벤트 장소에서 다중 사용자 접속 관리에 유용합니다. 더 많은 안테나를 사용하면 무선 신호를 더 세밀하게 조정하고 다중 사용자 간의 간섭을 줄일 수 있습니다.

3. 고속 데이터 및 저지연 통신:

- 높은 주파수는 고속 데이터 전송과 낮은 통신 지연을 지원합니다. 이는 실시간 영상 스트리밍, 가상 현실(VR), 원격 의료 및 자율 주행 자동차와 같은 응용 분야에서 중요합니다. 더 높은 주파수는 데이터를 빠르게 전송하고 신속한 응답 시간을 제공합니다.

4. 초고해상도 통신:

- 높은 주파수는 초고해상도 통신을 지원합니다. 이것은 4K 및 8K 비디오 스트리밍, 가상 현실, 홀로그래피 및 3D 텔레비전과 같은 고해상도 응용 분야에서 필수적입니다.

그러나 높은 주파수에는 한계가 있습니다. 높은 주파수 신호는 전파가 짧은 파장을 갖고 있어, 전파가 장애물에 의해 쉽게 차단될 수 있으며, 전파의 전파 거리가 짧을 수 있습니다. 따라서 통신에서는 다양한 주파수 대역을 조합하여 최적의 성능을 얻도록 설계합니다.

일반적으로 하이 밴드(mmWave), 중간 밴드(Sub-6 GHz), 그리고 저주파수 밴드를 조합하여 전체 네트워크를 구축합니다. 이렇게 다양한 주파수 대역을 활용하면 고대역폭, 빠른 데이터 전송 속도 및 효과적인 접속 관리를 조화롭게 조절할 수 있습니다.

#### Explain high-level pros and cons of FR1 and FR2.

> FR1과 FR2가 high-level일 때의 장단점은 무엇인가?

FR1 (Release 15)와 FR2 (Release 16)은 5G 통신의 릴리즈 버전을 나타냅니다. 이러한 릴리즈 간에는 다양한 특징과 장단점이 존재합니다. 이에 대한 high-level(고수준)한 장단점은 다음과 같습니다:

#### FR1 (Release 15)의 장단점:

장점:

1. 초기 5G 표준: FR1은 초기 5G 표준으로, 5G 네트워크의 초기 구축과 상용화에 중요한 역할을 했습니다. 따라서 초기 5G 서비스의 제공에 사용될 수 있습니다.
2. 기본 5G 기능 포함: FR1에는 기본 5G 기능과 기술이 포함되어 있으며, 초고속 데이터 전송, 초저지연 통신, 대용량 연결 및 다중 접속 등의 핵심 기능을 지원합니다.

단점:

1. 몇몇 추가 기능 부재: FR1은 초기 5G 표준이지만 모든 5G 기능이 포함되지 않았습니다. 따라서 미래 업그레이드가 필요하며, 일부 추가 기능은 FR2와 같은 뒤늦은 릴리즈에서 추가되었습니다.

#### FR2 (Release 16)의 장단점:

장점:

1. 기능 확장: FR2는 FR1을 확장하고 향상시킨 버전으로, 다양한 5G 기능이 추가되었습니다. 이로 인해 5G 네트워크의 성능과 기능이 향상되었습니다.
2. 고주파수 대역 지원: FR2에는 밀리미터웨이브 (mmWave) 주파수 대역을 지원하는 기능이 추가되었습니다. 이는 초고속 데이터 전송과 대용량 연결을 지원합니다.

단점:

1. 업그레이드 필요성: 기존 5G 네트워크에서 FR2를 지원하려면 하드웨어와 소프트웨어 업그레이드가 필요할 수 있습니다. 이로 인해 추가 비용과 복잡성이 발생할 수 있습니다.

FR1과 FR2의 선택은 통신 사업자와 네트워크 운영자에게 달려 있으며, 서비스 요구 사항, 네트워크 인프라, 비용 및 지원 가능한 하드웨어에 따라 다를 수 있습니다. 일반적으로 FR2는 더 많은 5G 기능과 성능을 제공하지만 업그레이드 및 추가 투자가 필요할 수 있습니다.

#### How is a high frequency EM wave used for wireless communication?

> 고주파 EM 파동이 무선통신에 어떻게 사용되는가?

고주파수 전자기(EM) 파동은 무선 통신에서 다양한 방식으로 사용됩니다. 무선 통신에서 고주파수 EM 파동을 사용하는 주요 방법과 그 활용 사례에 대한 설명은 다음과 같습니다:

1. 무선 통신과 고속 데이터 전송:

- 고주파수 EM 파동, 특히 밀리미터웨이브 (mmWave) 주파수 대역,는 고속 데이터 전송을 지원하는 데 사용됩니다. 이러한 무선 통신은 초고속 브로드밴드 서비스를 제공하며, 대용량 파일의 빠른 다운로드, UHD 및 4K 비디오 스트리밍, 가상 현실(VR) 및 홀로그래피와 같은 응용 분야에 적합합니다.

2. 5G 네트워크:

- 5G 네트워크는 고주파수 밴드를 활용하여 초고속 무선 통신을 제공합니다. mmWave 주파수 대역은 5G의 일부로, 특히 도시 밀집 지역 및 스타디움과 같은 밀집된 지역에서 사용됩니다. mmWave는 초고속 데이터 및 저지연 통신을 제공하는 데 기여합니다.

무선 통신에서 고주파수 EM 파동의 활용은 고속 데이터 전송, 저지연 통신, 고해상도 미디어 스트리밍 및 혁신적인 응용 분야를 위한 중요한 요소로써 계속적으로 발전하고 있습니다.

#### Explain the bandwidth.

> 대역폭에 대해 설명하시오.

대역폭(Bandwidth)은 무선 통신, 유선 통신 및 신호 처리 분야에서 중요한 개념입니다. 이것은 주파수 스펙트럼에서 사용 가능한 주파수 대역의 너비를 나타냅니다. 대역폭은 신호의 정보 전송률 및 데이터 처리량을 결정하는 중요한 매개변수 중 하나입니다.

대역폭에 대한 주요 포인트:

1. 주파수 스펙트럼:

- 대역폭은 주파수 스펙트럼에서 신호가 사용할 수 있는 주파수 범위를 나타냅니다. 주파수 스펙트럼은 일정한 주파수 범위에서 신호를 전송하는 데 사용됩니다.

2. Hz (헤르츠) 단위:

- 대역폭은 일반적으로 헤르츠(Hz)로 측정됩니다. 예를 들어, 20kHz 대역폭은 20,000Hz의 주파수 범위를 나타냅니다.

3. 데이터 전송률과 관련:

- 대역폭은 데이터 전송률에 직접적인 영향을 미칩니다. 대역폭이 넓을수록 더 많은 데이터가 동시에 전송될 수 있으며, 높은 데이터 전송률을 지원합니다.

4. 신호 대역폭:

- 물리적인 신호의 대역폭은 그 신호의 주파수 구성 요소를 결정합니다. 대역폭이 넓으면 신호는 더 빠르게 변화하며, 고주파수 신호는 빠르게 진동합니다.

5. 무선 통신:

- 대역폭은 무선 통신에서 중요한 요소로, 무선 채널의 대역폭을 통해 동시에 전송될 수 있는 데이터 양을 결정합니다. 예를 들어, 더 넓은 대역폭을 사용하면 더 빠른 데이터 전송 속도를 달성할 수 있습니다.

#### What is the interference and why is it important?

> 무선통신에서 간섭이란 무엇이고 왜 중요한가?

무선통신에서 "간섭"은 다른 무선 신호나 잡음이 원하는 신호의 수신 또는 전송을 방해하는 현상을 가리킵니다. 간섭은 무선 통신에서 중요한 이슈이며, 그 중요성은 다음과 같은 이유로 설명됩니다:

1. 신호 품질 저하: 간섭으로 인해 수신되는 신호의 품질이 저하될 수 있습니다. 이로 인해 데이터 손실, 오류, 신호의 왜곡 및 통화 품질 저하 등이 발생할 수 있습니다. 간섭 없는 환경에서 신호의 정확한 수신이 중요한 경우, 간섭은 문제의 근원이 될 수 있습니다.

2. 데이터 전송 속도 감소: 간섭으로 인해 데이터 전송 속도가 감소할 수 있습니다. 데이터의 신뢰성과 안정성을 유지하기 위해 간섭을 관리하고 최소화해야 합니다.

3. 스펙트럼 관리: 주파수 스펙트럼은 한정된 자원입니다. 간섭 없이 무선 기기와 서비스를 효과적으로 관리하려면 주파수 스펙트럼을 효율적으로 할당하고 관리해야 합니다. 간섭은 스펙트럼 사용의 효율성을 감소시킬 수 있습니다.

4. 다중 접속 관리: 많은 무선 기기와 사용자가 동일한 주파수 대역에서 동작하는 경우, 간섭 관리가 중요합니다. 다중 접속 환경에서 신호간 간섭을 최소화하고 다중 접속을 관리하는 기술과 알고리즘은 필수적입니다.

5. 무선 네트워크 성능: 무선 네트워크의 성능과 안정성에 직접적인 영향을 미칩니다. 특히 대용량 데이터 전송, 영상 및 음성 통화, 위치 기반 서비스 및 다중 사용자 접속 상황에서 간섭은 큰 문제가 될 수 있습니다.

6. 무선 통신의 미래: 5G 및 이후의 무선 통신 기술에서는 스마트한 간섭 관리가 특히 중요합니다. 고주파수 밴드와 mmWave 스펙트럼을 사용하는 새로운 기술은 간섭 관리와 주파수 관리의 어려움을 증가시킬 수 있습니다.

간섭 관리와 주파수 관리는 무선 통신 기술의 핵심 요소로, 효율적인 무선 통신을 제공하고 무선 네트워크의 안정성과 성능을 유지하는 데 중요합니다.

#### Explain source/channel coding, modulation in wireless communication.

> 무선 통신의 소스/채널 코딩, 변조에 대해 설명하시오.

무선 통신에서 소스 코딩(Source Coding), 채널 코딩(Channel Coding), 그리고 변조(Modulation)는 중요한 단계로, 데이터를 전송하는 과정에서 정보의 압축, 오류 검출 및 수정, 그리고 신호의 변환을 수행합니다.

1. 소스 코딩 (Source Coding):

- 소스 코딩은 원시 데이터나 정보를 압축하는 과정으로, 데이터의 효율적인 저장 및 전송을 위해 필요합니다. 주요 목표는 데이터 압축과 정보 손실 최소화입니다. 주로 사용되는 소스 코딩 기술에는 Run-Length Encoding (RLE), Huffman Coding, Arithmetic Coding, 및 Lempel-Ziv-Welch (LZW) 알고리즘 등이 포함됩니다. 압축된 데이터는 무선 통신을 통해 보내거나 저장할 때 효율적으로 활용됩니다.

2. 채널 코딩 (Channel Coding):

- 채널 코딩은 데이터를 전송 중에 발생할 수 있는 오류에 대비하여 데이터에 추가 정보를 추가하는 과정입니다. 이것은 오류 검출 및 오류 정정을 위한 기술로, 데이터의 무결성을 보장합니다. 채널 코딩은 주로 무선 통신에서 중요하며, 고속 데이터 전송에서는 더욱 중요합니다. 일반적인 채널 코딩 방법에는 순환 중복 부호 (Convolutional Codes) 및 BCH, Reed-Solomon, Turbo Codes, LDPC (Low-Density Parity-Check) Codes 등이 있습니다. 채널 코딩은 오류 검출 및 오류 정정을 통해 송신자와 수신자 간의 신뢰성 있는 통신을 보장합니다.

3. 변조 (Modulation):

- 변조는 디지털 데이터를 아날로그 신호로 변환하는 과정으로, 데이터를 전송 가능한 신호로 변경합니다. 이것은 무선 통신에서 데이터를 전파의 주파수, 위상, 진폭 등의 특성으로 변환하여 전송하는 역할을 합니다. 주요 변조 기술에는 Amplitude Shift Keying (ASK), Frequency Shift Keying (FSK), Phase Shift Keying (PSK), Quadrature Amplitude Modulation (QAM) 등이 포함됩니다. 변조를 통해 데이터는 무선 매체를 통해 전송됩니다.

이러한 과정들은 무선 통신 시스템에서 데이터의 신뢰성, 효율성 및 품질을 유지하기 위해 필수적입니다. 소스 코딩은 데이터를 효율적으로 압축하여 저장 및 전송할 수 있게 하며, 채널 코딩은 오류에 대비하여 신뢰성 있는 통신을 제공합니다. 변조는 데이터를 무선 매체로 변환하여 전송하는 역할을 합니다. 이러한 기술들은 무선 통신의 핵심 요소이며, 고급 무선 통신 시스템에서는 신호 처리 및 알고리즘을 결합하여 최적의 성능을 제공합니다.

## 학습메모

1. [Maxell 방정식](https://blog.naver.com/wisdom0719/221260269943)
