# 230914

## 목차

- 복습
- Contents
- Digital Modulation
  - 변복조 이론 (BPSK)
  - 다양한 변복조 방법 / 송수신기 설계 및 수신기 성능
- Questions

## 복습

### Review of Week-1 and Story for Week-2

- High frequency (~GHz) signal can be transmitted over the air (=wireless)
  - 고주파(~GHz) 신호를 공기중(=무선)으로 전송할 수 있다.
- How can that high frequency signal be modulated to indicate a digital information?
  - 고주파 신호를 어떻게 변조하여 디지털 정보를 정보를 담을 수 있을까?

<img width="978" alt="스크린샷 2023-10-21 오후 4 43 08" src="https://user-images.githubusercontent.com/138586629/277095158-b1a6d8d1-5e99-44c6-b0da-7cc516599ab2.png">

### BPSK(Binary Phase Shift Keying) 변복조

<img width="944" alt="스크린샷 2023-10-21 오후 4 43 45" src="https://user-images.githubusercontent.com/138586629/277095181-a2e86cbd-263f-4b42-8243-0475a9ad5519.png">

## Contents

- 변복조 이론 (BPSK)

  - 무선디지털통신에서 변복조는 보내고자 하는 디지털 정보에 따라 (이미 약속된 방법으로) 초고주파 신호를 변화시켜 송신하고, 초고주파를 수신한 측에서는 변화된 신호를 보고 보내고자 했던 디지털 정보를 유추하는 과정이다
  - 무선디지털통신에서 BPSK 변복조시스템은 아래 그림과 같다
    - <img width="623" alt="스크린샷 2023-10-21 오후 4 47 14" src="https://user-images.githubusercontent.com/138586629/277095305-78a70e1f-cb85-4521-afaa-aec76cef0899.png">

- 다양한 변복조 방법 / 송수신기 설계 및 수신기 성능
  - BPSK, On-Off Keying, PAM
  - QPSK
  - 8PSK, 16 QAM, 64 QAM

## 변복조 이론 (BPSK)

### BPSK 변복조 시스템

- 무선디지털통신에서 변복조는 보내고자 하는 디지털 정보에 따라 (이미 약속된 방법으로) 초고주파 신호를 변화시켜 송신하고, 초고주파를 수신한 측에서는 변화된 신호를 보고 보내고자 했던 디지털 정보를 유추하는 과정이다
- 무선디지털통신에서 BPSK 변복조시스템은 아래 그림과 같다

  - <img width="623" alt="스크린샷 2023-10-21 오후 4 47 14" src="https://user-images.githubusercontent.com/138586629/277095305-78a70e1f-cb85-4521-afaa-aec76cef0899.png">

- 다양한 변복조 방법/송수신기 설계 및 수신기 성능

### BPSK 변복조시스템 고려사항

- 변조 하는 방법

  - 1 -> + sin(2 pi 10^9 t)
  - 0 -> - sin(2 pi 10^9 t)
  - 매 10^(-6)초마다 둘 중 하나를 전송

- 복조 하는 방법

  - - sin(2 pi 10^9 t)이 수신되었는지 - sin(2 pi 10^9 t)이 수신되었는지 매 10^(-6) 판단
  - 1초에 10^6회 판단

- 복조의 성능 분석 (Bit Error Rate, BER)

  - 1초에 10^6개의 random bits를 보내고 Noise가 추가된 data중에 잘못 판단된 bits는 평균 몇 개인가

### Digital Circuit vs. RF Analog Circuit

- Digital Circuit for Digital (baseband) Signal Processing <br />
  디지털 (기저대역) 신호 처리를 위한 디지털 회로

  - Memory (RAM) read and write <br />
    메모리(RAM) 읽기와 쓰기
  - Flip-flop and combinational circuit (=digital logic) <br />
    플립플롭과 조합회로 (=디지털 로직)
  - Discrete-time (clock-based) and quantized value <br />
    이산시간 (clock기반) 및 양자화된 값
  - Several Mega Hz clocks per second <br />
    초당 수 메가헤르츠 클럭
  - Addition/Multiplication by digital logic <br />
    디지털 로직에 의한 덧셈/곱셈

- (RF) Analog Circuit for Analog Signal Processing <br />
  아날로그 신호 처리를 위한 아날로그 회로
  - Voltage-in/Voltage-out <br />
    전압 입력 / 전압 출력
  - No memory for analog signal (=time-varying voltage) <br />
    아날로그 신호에 대한 메모리 없음 (=시간에 따라 변하는 전압)
  - Transistor/CMOS based <br />
    트랜지스터/CMOS 기반
  - Continuous time with no quantization <br />
    양자화가 없는 연속 시간
  - Up to tens of GHz signal generation <br />
    최대 수십 GHz 신호 생성
  - RF signal multiplication (=mixer) and integration <br />
    RF 신호 증폭(=믹서) 및 통합
  - Antenna input/output are all analog signal <br />
    안테나 입력/출력은 모두 아날로그 신호

<img width="261" alt="스크린샷 2023-10-28 오후 7 16 10" src="https://user-images.githubusercontent.com/138586629/278807059-b0b824ad-b546-4fbc-94e0-e52548118801.png">

### DAC and ADC

- DAC (at the modulator) : 변조기에서
  - Digital circuit writes +1 or -1 at the memory (or circular buffer)
  - Based on the memory contents +sin(2𝜋10^9t) or −sin(2𝜋10^0t) signal is fed into the transmit antenna for every 10^(-6) second
  - Filter/Amplifier are following
- ADC (at the demodulator) : 복조기에서
  - Integration results are sampled and reset every 10^(-6) second
  - Sampled integration result (analog voltage) is quantized and written into a RAM (one symbol every 10-6 second)
    - AGC (Automatic Gain Control) before the quantization

<img width="264" alt="스크린샷 2023-10-28 오후 7 24 41" src="https://user-images.githubusercontent.com/138586629/278807490-abaefdd4-2e5f-4aeb-8965-6a6cd6b6f604.png">

### BPSK 복조 알고리즘 - 문제

- 지난 10^(-6)초 동안 아래와 같은 신호 r(t)가 수신되었음.

  - <img width="451" alt="스크린샷 2023-10-28 오후 7 30 13" src="https://user-images.githubusercontent.com/138586629/278807778-9e26edbe-a513-4747-bc61-b0224ba8adb4.png">

- 수신된 신호는 +sin(2𝜋10^9t) 혹은 −sin(2𝜋10^0t) 중 하나가 송신되었지만, noise가 추가되어 r(t)가 수신된 것임.
  - r(t) = +sin(2𝜋10^9t) + n(t)로 보는 것이 타당할까, 혹은
  - r(t) = -sin(2𝜋10^9t) + n(t)로 보는 것이 타당할까

### BPSK 복조 Key Idea

<img width="593" alt="스크린샷 2023-10-28 오후 7 31 06" src="https://user-images.githubusercontent.com/138586629/278807834-60cfbec5-8de4-489a-a1dc-1db9cfa87bbc.png">

- 수신된 r(t)와 sin(2𝜋10^9t) 를 10^(-6)초 동안 곱하면서 적분한 결과 값을 확인 한다.
- Noise가 없는 상황에서, +sin(2𝜋10^9t)으로 변조된 경우라면, 적분한 결과값이 양수 값 이 되고, -sin(2𝜋10^9t)으로 변조된 경우라면, 적분한 결과값이 음수값이 된다.
- BPSK 복조 과정은 따라서,
  1. sin(2𝜋10^9t) 를 10^(-6) 초 동안 곱한다.
  2. 10^(-6) 초 동안 적분한다.
  3. 10^(-6) 초 동안 적분한 값의 부호를 확인한다.

### BPSK 변복조 시스템 – 설명

<img width="497" alt="스크린샷 2023-10-28 오후 7 34 56" src="https://user-images.githubusercontent.com/138586629/278808013-e55018cf-6da1-4cce-8b8f-5534e8d4d68e.png">

- fc=10^9 정도 초고주파
  - 그래야,전자기파를 이용한 무선통신 가능
- Binary 정보는 1초에 106 번 정도
  - 1Mbps 정도의 속도로 정보가 전달
  - 더 빠른 속도 가능함, 그러나 Bandwidth 문제로 제한
- Noise는 수신기가 반도체로 만들어진 전자기기이면 없어질 수 없음
  - Noise가 판단 오류를 하게 할 수 있음
  - 랜덤 신호 n(t)로 modeling되며, 실제로는 적분된 값의 통계적 특성만 중요함
  - 큰 진폭의 변조신호(±Asin(2𝜋10^9t), A를 크게)를 보내어 오류 확률을 낮출 수 있음

### 무선 변복조 모뎀 (BPSK시스템) 구현

<img width="647" alt="스크린샷 2023-10-28 오후 7 40 07" src="https://user-images.githubusercontent.com/138586629/278808274-1e22a9a1-9f85-4fb1-a3f7-9d83c83ad979.png">

### 다른 고려 사항

- Filter

  - 타 반송파를 수신단에서 제거해야 함
  - 저항과 커패시터를 이용한 Filter를 사용

- Coherence & Synchronization

  - 1초에 10^9 을 정확하게 맞추기 어려움
  - 10^(-6) 초마다 정확하게 새로운 Bits의 수신을 맞추기 어려움
  - 약속된 bit 나열을 주기적으로 보내주어서 tuning 할 수 있게 함

- Energy per bit

  - 전송되는 Waveform의 크기가 클수록 Error 확률이 줄어 든다
  - Bit 하나가 전송되는 시간이 길수록 Energy per bit는 늘어난다
  - Bit 당 수신된 Energy (Eb) 의 Square Root가 Waveform 의 크기를 결정한다

- Noise

  - Zero-mean Gaussian noise가 더해지는 것으로 modeling한 것이 일반적임
  - Additive White Gaussian Noise (AWGN) channel 이라고 함
  - Gaussian noise의 variance 는 N0/2 로 나타낸다
  - 여기서 N0는 주파수대역에 균일하게 퍼져 있는 noise 밀도로 수신기의 절대 온도에 비례한다 – 일반 적으로 상수. (1/2 는 이후에)

### BPSK performance

<img width="301" alt="스크린샷 2023-10-28 오후 7 42 11" src="https://user-images.githubusercontent.com/138586629/278808403-6e406f42-ed7a-4f18-bbb4-cd72be263161.png">

## 다양한 변복조 방법 / 송수신기 설계 및 수신기 성능

- BPSK, On-Off Keying, PAM
- QPSK
- 8PSK, 16 QAM, 64 QAM
- 변조 방식 비교

### BPSK, On-Off Keying, PAM

#### BPSK의 다른 관점

<img width="458" alt="스크린샷 2023-10-28 오후 7 42 48" src="https://user-images.githubusercontent.com/138586629/278808431-1c1d87ea-9946-4a11-976d-7333e1e38485.png">

#### On-Off Keying (OOK)

<img width="517" alt="스크린샷 2023-10-28 오후 7 43 07" src="https://user-images.githubusercontent.com/138586629/278808445-04d6697f-21bd-462d-a697-f761596d16ee.png">

#### Pulse Amplitude Modulation (PAM), 예시 4-PAM

BPSK를 기준으로, 진폭을 기준으로 0, 1이 아닌 00, 01, 10, 11 총 4개의 신호를
구분하도록 설계하는 방식임.

<img width="529" alt="스크린샷 2023-10-28 오후 7 43 38" src="https://user-images.githubusercontent.com/138586629/278808463-3bbe3e79-8b78-4346-91ce-e5f5fe01be3d.png">

좀 더 정확히는 에러율을 최대한 낮추기 위해 00, 01, 11, 10 순서대로 신호를 배치함.

#### BER Performance of PAMs

<img width="347" alt="스크린샷 2023-10-28 오후 7 46 19" src="https://user-images.githubusercontent.com/138586629/278808598-f1dcdeb0-fbf2-4168-923a-f32f382cb913.png">

### QPSK

#### Quadrature Phase Shift Keying (QPSK)

- QPSK에서는 sin(2𝜋10^9t)와 (sin(2𝜋10^9t))^2에 대해서 논의함.

- 삼각함수 공식

  - <img width="171" alt="스크린샷 2023-10-28 오후 7 48 14" src="https://user-images.githubusercontent.com/138586629/278808686-4cfd78af-6a52-40a0-a172-40da218dc0d7.png">

- 알 수 있는 사실

  - sine과 cosine은 약간(1/4 x 10^(-9) 초) 이동한 차이임
  - Sine에 맞추어 보내고 Sine으로 곱하면 BPSK 구현
  - 마찬가지로 Cosine에 맞추어 보내고 Cosine을 곱해도 BPSK 구현
  - 변조하는것과 복조하는것이 다르면 적분 후에 쌓이는 것이 없음
  - 결론 : Sine과 Cosine을 동시 (10-6초 동안)에 변조하고 각각 복조해도 서로 영향 없음
    - -> **10-6초 동안 두 개의 Binary Bits를 변/복조할 수 있음**

- QPSK는 이를 통해 동일 시간, 동일 주파수로 2 개의 BPSK 송수신을 수행하는 방식.

#### BPSK 과 QPSK

<img width="558" alt="스크린샷 2023-10-28 오후 7 51 40" src="https://user-images.githubusercontent.com/138586629/278808848-af7f2cde-647f-4e1d-833d-df824f433cc2.png">

#### Complex Numbers

- 왜 복소수인가?

  - 오일러의 공식!

- 무선으로 전송되는 신호는 초고주파(RF) 신호로 10^9Hz 정도의 신호이지만, 이 RF 신호를 변조하는 신호는 저주파(10^(-6)초는 같은 값을 유지하는)저주파신호이고,복소신호 m_1(t) - im_Q(t)로 간주한다.

<img width="668" alt="스크린샷 2023-10-28 오후 7 52 13" src="https://user-images.githubusercontent.com/138586629/278808873-0cf5cf5e-f9ba-438c-939e-b4a8a515a7d9.png">

뭐 하여튼 결론은 QPSK가 sin() BPSK, cos() BPSK 두 개를 동시에 보내는 거니까
특정 값을 표현할 때 복소수 값 `cos x + i sin x = e^(ix)`로 표현한단거임.

그러니까 특정 값을 원 위의 한 점으로 표현할 수 있음.

#### QPSK = 2개의 BPSK

<img width="431" alt="스크린샷 2023-10-28 오후 7 53 19" src="https://user-images.githubusercontent.com/138586629/278808923-27b2bc33-aa6f-4ecb-bf07-9df4a223854f.png">

#### QPSK Signal Constellation

<img width="656" alt="스크린샷 2023-10-28 오후 8 06 38" src="https://user-images.githubusercontent.com/138586629/278809524-67069bd9-65da-49fc-8884-d97b9af26fb6.png">

### 8PSK, 16 QAM, 64 QAM

#### 8PSK Signal Constellation

<img width="315" alt="스크린샷 2023-10-28 오후 8 08 35" src="https://user-images.githubusercontent.com/138586629/278809602-5798df02-dceb-4f04-86bc-8d4cd09de9e3.png">

> 특정 값을 원 위의 한 점으로 표현할 수 있음.

라고 아까 했잖아? 그래서 sin BPSK, cos BPSK의 조합으로 원 위의 어떤 위치인지에 따라
신호를 저렇게 구분할 수 있는 거임. 이건 8개 신호가 가능하니까 8PSK임.

#### PSK + PAM = QAM System

<img width="562" alt="스크린샷 2023-10-28 오후 8 09 39" src="https://user-images.githubusercontent.com/138586629/278809662-a3e52ce8-46f2-49b9-9037-61842d59badf.png">

아까 진폭 범위를 더 늘려서 신호를 4개까지로 늘린 게 4-PAM이라고 했잖아? ~PAM
이제 ~PSK 까지 더하면 더 많은 신호를 담을 수 있겠지? 두 개는 독립적인 거니까!

이걸 PSK + PAM = QAM이라고 함.

#### 16-QAM & 64-QAM Constellation

그래서 16-QAM은 총 16개의 신호를 PSK, PAM을 둘 다 써서 영역을 나눈 거고,
64-QAM은 뭐 유사하게 64개의 신호를 영역을 나누어 놓은거지.

<img width="615" alt="스크린샷 2023-10-28 오후 8 10 12" src="https://user-images.githubusercontent.com/138586629/278809685-1e315e31-3679-4ce1-9739-7425478503ef.png">

#### 64-QAM Constellation 및 복조과정

<img width="404" alt="스크린샷 2023-10-28 오후 8 14 01" src="https://user-images.githubusercontent.com/138586629/278809854-a17958be-3157-46c0-aa1e-dbfb0265cf39.png">

#### Symbol Error Rate (SER) Curve

<img width="332" alt="스크린샷 2023-10-28 오후 8 14 24" src="https://user-images.githubusercontent.com/138586629/278809882-5dcc1323-878f-44c3-bf2e-8fd2908a6338.png">

그래서 신호를 무한히 많이 넣을 수 있냐? 그렇진 않음

### 변조 방식 비교

<img width="540" alt="스크린샷 2023-10-28 오후 8 14 55" src="https://user-images.githubusercontent.com/138586629/278809912-91883237-b3b7-49e3-85fe-0356cf54c070.png">

기억해 PAM은 진폭(수직선), PSK는 sin\*cos 복소평면

#### Radio Frequency and Baseband - Summary

- Radio Frequency (RF) signal is sent and received
- RF-circuit takes care of the conversion between RF-analog signal and baseband digital signal
  - RF-signal is called “Carrier”
  - Digital = stored in memory
  - cos-square and sin-square will be used at the receiver
- Baseband signal is our main concern
  - Discrete time, discrete value
- There are two streams – In-phase and quadrature

- 무선 주파수(RF) 신호가 송수신됩니다.
- RF 회로는 RF 아날로그 신호와 베이스밴드 디지털 신호 간의 변환을 담당합니다.
  - RF 신호를 “캐리어(Carrier)”라고 합니다.
  - 디지털 = 메모리에 저장됨
  - cos-square와 sin-square가 수신기에서 사용됩니다.
- 베이스밴드 신호가 우리의 주요 관심사입니다.
  - 이산시간, 이산값
- 동위상(In-Phase) 및 직교위상(Quadrature)의 두 가지 스트림이 있습니다.

#### Communication System and BPSK

<img width="677" alt="스크린샷 2023-10-28 오후 8 18 38" src="https://user-images.githubusercontent.com/138586629/278810106-2119f623-d10d-49ad-9ab6-95aca0d52dfc.png">

#### Communication System and QPSK

<img width="672" alt="스크린샷 2023-10-28 오후 8 20 02" src="https://user-images.githubusercontent.com/138586629/278810171-84fbef44-b224-4369-a34b-285b128dce82.png">

#### Communication System and QAM

<img width="674" alt="스크린샷 2023-10-28 오후 8 20 26" src="https://user-images.githubusercontent.com/138586629/278810182-86b64f6c-2d03-4978-a09c-7a154e092991.png">

## Questions

- What is digital modulation?
  - 디지털 변조란 무엇인가?
- What is the source coding and why is it needed?
  - 소스 코딩이란 무엇이며 왜 필요한가?
- What is the channel coding and why is it needed?
  - 채널 코딩이란 무엇이며 왜 필요한가?
- Explain BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM, 64QAM
  - BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM, 64QAM에 대해 설명하시오.
  - How is the symbol related to binary information?
    - 심볼은 바이너리 정보와 어떻게 관련되어 있는가?
  - How are they modulated?
    - 각 방식은 어떻게 변조되는가?
  - How are they demodulated?
    - 각 방식은 어떻게 복조되는가?
  - Pros and Cons of them ... example 16 QAM vs. QPSK
    - 각 방식의 장단점은 어떻게 되는가?
- Why do we discuss about complex symbol (or a complex number) in wireless communication?
  - 무선 통신에서 복소 심볼(또는 복소수)을 논하는 이유가 무엇인가?
- Where is the digital modulation in wireless communication system
  - 무선 통신 시스템에서 디지털 변조는 어디서 이루어지는가
  - Answer is between channel encoding/decoding and DAC/ADC
    - 정답: 채널 인코딩/디코딩과 DAC/ADC 사이에서 일어남

### What is digital modulation?

> 디지털 변조란 무엇인가?

Digital Modulation(디지털 변조)은 디지털 데이터를 아날로그 신호로 변환하여 무선 통신에서 전송하는 과정을 가리키는 용어입니다. 이것은 디지털 비트열을 아날로그 신호의 주파수, 위상, 진폭 등과 같은 특성으로 변환하는 프로세스를 포함하며, 이를 통해 디지털 데이터를 무선 매체를 통해 전송할 수 있게 됩니다.

디지털 변조의 주요 특징과 개념은 다음과 같습니다:

1. 디지털 데이터 변환: 디지털 데이터는 이진 코드(0과 1의 조합)로 표현되며, 디지털 변조를 통해 이진 비트열은 아날로그 신호로 변환됩니다. 변조 과정은 디지털 비트열의 특정 패턴을 아날로그 파형으로 변환하는 데 사용됩니다.

2. 주파수, 위상, 진폭 변조: 디지털 변조는 다양한 방식으로 수행될 수 있으며, 이것은 주파수 변조(Frequency Shift Keying, FSK), 위상 변조(Phase Shift Keying, PSK), 진폭 변조(Amplitude Shift Keying, ASK)와 같은 기술을 사용합니다. 각각의 변조 기술은 데이터를 다른 방식으로 변환합니다.

3. 비트 속도와 심볼 속도: 디지털 변조에서는 비트 속도와 심볼 속도라는 두 가지 속도 개념이 중요합니다. 비트 속도는 초당 전송되는 이진 비트 수를 나타내며, 심볼 속도는 초당 전송되는 디지털 심볼의 수를 나타냅니다. 심볼은 일반적으로 여러 비트를 나타내는데 사용되므로 비트 속도와 심볼 속도는 서로 관련이 있습니다.

4. 변조 스키마: 디지털 변조에는 다양한 변조 스키마가 있으며, 어떤 스키마가 사용되느냐에 따라 데이터의 전송 효율성 및 신호 처리 방식이 다를 수 있습니다. 일반적으로 사용되는 변조 스키마에는 BPSK (Binary Phase Shift Keying), QPSK (Quadrature Phase Shift Keying), 16-QAM (16-Quadrature Amplitude Modulation) 등이 포함됩니다.

디지털 변조는 무선 통신, 유선 통신 및 광통신과 같은 다양한 통신 시스템에서 사용되며, 데이터를 효율적으로 전송하고, 신호 간 간섭을 최소화하고, 통신의 신뢰성을 보장하기 위한 핵심 기술 중 하나입니다.

### What is the source coding and why is it needed?

> 소스 코딩이란 무엇이며 왜 필요한가?

`소스 코딩(Source Coding)`은 데이터를 효율적으로 압축하여 저장 및 전송 공간을 절약하고 전송 시간 및 비용을 최소화하기 위한 과정입니다. 필요한 이유는 데이터를 효율적으로 다루기 위해 저장 공간 및 대역폭을 절약하고 데이터 전송 비용을 감소시키기 위함입니다.

---

소스 코딩은 "압축"이 핵심

> Data <-> Source Coding <-> Channel Coding <-> Modulation <-> DAC/ADC <-> RF Circuit

### What is the channel coding and why is it needed?

> 채널 코딩이란 무엇이며 왜 필요한가?

`채널 코딩(Channel Coding)`은 데이터 전송 중에 발생할 수 있는 오류에 대비하여 데이터를 보호하고 오류 검출 및 수정을 위한 과정입니다. 필요한 이유는 데이터 전송의 신뢰성을 유지하기 위해 오류에 대비하고 품질을 향상시키기 위함입니다.

---

채널 코딩은 "에러 검출/수정"이 핵심

> Data <-> Source Coding <-> Channel Coding <-> Modulation <-> DAC/ADC <-> RF Circuit

### Explain BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM, 64QAM

> BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM, 64QAM에 대해 설명하시오.

다양한 디지털 변조 방식에 대한 자세한 설명은 다음과 같습니다:

1. BPSK (Binary Phase Shift Keying):

- BPSK는 이진 위상 변조로, 0과 1 비트를 서로 다른 위상의 신호로 변환하여 전송합니다. 하나의 비트는 0 또는 π 라디안의 위상을 가지며, 이는 복소 평면에서 두 개의 다른 신호로 매핑됩니다.

2. QPSK (Quadrature Phase Shift Keying):

- QPSK는 2개의 비트를 함께 그룹화하여 4가지 다른 위상 신호로 변조합니다. 이진 비트 집합 (00, 01, 10, 11)은 다른 위상 간의 차이로 매핑됩니다.

3. 2^k-PAM (k-등급 진폭 변조):

- 2^k-PAM은 k개의 진폭 레벨을 사용하여 데이터를 전송합니다. 예를 들어, 2-PAM은 BPSK와 동일하며, 4-PAM은 4개의 다른 진폭 레벨을 사용하여 데이터를 표현합니다.

4. 8PSK (8-등급 위상 변조):

- 8PSK는 3비트 데이터를 8개의 다른 위상으로 매핑하여 전송합니다. 이것은 QPSK보다 더 많은 비트를 한 번에 전송할 수 있으며, 더 높은 전송률을 제공합니다.

5. 16QAM (16-등급 진폭 변조):

- 16QAM은 4비트 데이터를 16개의 다른 진폭 및 위상 조합으로 매핑하여 전송합니다. 이것은 BPSK 및 QPSK보다 훨씬 높은 데이터 전송률을 제공합니다.

6. 64QAM (64-등급 진폭 변조):

- 64QAM은 6비트 데이터를 64개의 다양한 진폭 및 위상 조합으로 매핑하여 전송합니다. 이것은 16QAM보다 더 높은 전송률을 제공하지만, 노이즈에 민감할 수 있습니다.

이러한 디지털 변조 방식은 통신 시스템에서 데이터를 효과적으로 전송하고 다양한 환경에서 성능을 최적화하는 데 사용됩니다. 선택된 변조 방식은 전송률, 스펙트럼 사용, 노이즈 및 간섭 관리 등을 고려하여 결정됩니다.

#### How is the symbol related to binary information?

> 심볼은 바이너리 정보와 어떻게 관련되어 있는가?

심볼은 바이너리 정보와 관련이 있습니다. 심볼은 디지털 통신에서 데이터를 나타내는 기본 단위로, 주로 비트와 연관이 있습니다. 각 심볼은 하나 이상의 비트를 나타내며, 이진 (바이너리) 정보의 단위로 사용됩니다.

예를 들어, `BPSK (Binary Phase Shift Keying)` 변조 방식에서, 각 심볼은 1개의 비트를 나타냅니다. 0과 1 비트는 서로 다른 위상의 신호로 매핑되어 전송됩니다. 따라서 BPSK에서는 심볼이 바이너리 정보의 단위입니다.

`QPSK (Quadrature Phase Shift Keying)`와 같은 다른 변조 방식에서는 각 심볼이 2개의 비트를 나타냅니다. 2개의 비트는 서로 다른 조합의 진폭과 위상으로 매핑되어 전송됩니다. 따라서 QPSK에서는 각 심볼이 2비트 정보를 표현합니다.

이와 같이 디지털 통신에서는 데이터를 비트에서 심볼로 변환하고, 심볼은 이진 정보를 다양한 방식으로 표현하는 데 사용됩니다. 심볼의 수, 비트의 나타내는 방식, 그리고 심볼과 비트 간의 관계는 사용되는 변조 방식에 따라 다를 수 있습니다.

#### How are they modulated?

> 각 방식은 어떻게 변조되는가?

다양한 디지털 변조 방식(BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM, 64QAM)은 데이터를 아날로그 신호로 변조하는 방식이 다르며, 각각의 방식은 다음과 같이 변조됩니다:

1. **BPSK (Binary Phase Shift Keying)**:

   - BPSK는 이진 위상 변조로, 0과 1 비트를 서로 다른 위상의 신호로 변조합니다. 0은 0 라디안 위상을 가지며, 1은 π 라디안 위상을 가집니다.

2. **QPSK (Quadrature Phase Shift Keying)**:

   - QPSK는 2개의 비트를 함께 그룹화하여 4가지 다른 위상 신호로 변조합니다. 두 비트쌍 (00, 01, 10, 11)은 서로 다른 위상 간의 차이로 매핑됩니다.

3. **2^k-PAM (k-등급 진폭 변조)**:

   - k-등급 진폭 변조는 k개의 진폭 레벨을 사용하여 데이터를 전송합니다. 2-PAM (Binary Amplitude Shift Keying)은 0과 1을 두 가지 다른 진폭 레벨로 변조합니다. 4-PAM, 8-PAM 등은 더 많은 진폭 레벨을 사용합니다.

4. **8PSK (8-등급 위상 변조)**:

   - 8PSK는 3비트 데이터를 8개의 다른 위상으로 매핑하여 전송합니다. 각 비트 그룹은 서로 다른 위상을 가집니다.

5. **16QAM (16-등급 진폭 변조)**:

   - 16QAM은 4비트 데이터를 16개의 다른 진폭 및 위상 조합으로 매핑하여 전송합니다. 진폭과 위상은 복소 수평에서 결정됩니다.

6. **64QAM (64-등급 진폭 변조)**:

   - 64QAM은 6비트 데이터를 64개의 다양한 진폭 및 위상 조합으로 매핑하여 전송합니다. 진폭과 위상은 복소 수평에서 결정됩니다.

각 변조 방식은 데이터를 아날로그 신호로 변조하는 방법과 비트를 심볼 또는 비트 패턴으로 매핑하는 방법에 따라 다릅니다. 이러한 방식은 데이터 전송률, 스펙트럼 사용, 노이즈에 대한 강건성 등을 고려하여 선택됩니다.

#### How are they demodulated?

> 각 방식은 어떻게 복조되는가?

BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM 및 64QAM과 같은 다양한 디지털 변조 방식은 수신 측에서 복조되어 디지털 비트로 복원됩니다. 각 방식은 다음과 같이 복조됩니다:

1. **BPSK (Binary Phase Shift Keying)**:

   - BPSK의 복조는 수신된 신호의 위상을 검출하여 0 또는 1의 이진 비트를 복원합니다. 위상이 π 라디안 이상인지 여부에 따라 비트가 결정됩니다.

2. **QPSK (Quadrature Phase Shift Keying)**:

   - QPSK의 복조는 4가지 다른 위상을 감지하여 2개의 비트를 복원합니다. 위상 차이에 따라 비트 쌍 (00, 01, 10, 11)이 결정됩니다.

3. **2^k-PAM (k-등급 진폭 변조)**:

   - 2^k-PAM 변조의 복조는 수신된 진폭 레벨을 기반으로 데이터를 복원합니다. 두 개의 진폭 레벨이 0과 1과 매핑되며, k-등급 진폭 변조에서 k개의 레벨이 있을 때 k개의 비트가 한 번에 복조됩니다.

4. **8PSK (8-등급 위상 변조)**:

   - 8PSK의 복조는 3비트 데이터를 복원합니다. 수신된 위상을 분석하여 3비트 데이터를 복원합니다.

5. **16QAM (16-등급 진폭 변조)**:

   - 16QAM 변조의 복조는 수신된 진폭과 위상을 분석하여 4비트 데이터를 복원합니다. 이진 진법으로 각 차원에 대해 2비트씩 복조됩니다.

6. **64QAM (64-등급 진폭 변조)**:

   - 64QAM의 복조는 수신된 진폭과 위상을 분석하여 6비트 데이터를 복원합니다. 이진 진법으로 각 차원에 대해 3비트씩 복조됩니다.

각 변조 방식은 데이터가 아날로그 신호로 변조되고 수신되었으며, 수신기에서 데이터를 디지털 비트로 복원하기 위한 특정 알고리즘 및 방법을 사용합니다. 수신기는 수신된 신호의 품질과 복잡성에 따라 신호를 복원하고 데이터를 해독합니다.

#### Pros and Cons of them ... example 16 QAM vs. QPSK

> 각 방식의 장단점은 어떻게 되는가?

디지털 변조 방식인 BPSK, QPSK, 2^k-PAM, 8PSK, 16QAM 및 64QAM은 각각 고유한 특징과 장단점을 가지고 있습니다. 이러한 방식의 일반적인 장단점은 다음과 같습니다:

**BPSK (Binary Phase Shift Keying):**

- 장점:
  - 간단한 구현과 복조가 가능하다.
  - 높은 신호-대잡음 비율 (SNR)에서 좋은 성능을 제공한다.
- 단점:
  - 데이터 전송률이 다른 방식에 비해 낮다.
  - 노이즈에 민감하다.

**QPSK (Quadrature Phase Shift Keying):**

- 장점:
  - BPSK에 비해 더 높은 데이터 전송률을 제공한다.
  - 공간적 효율성이 높다.
- 단점:
  - BPSK에 비해 노이즈에 민감할 수 있다.

**2^k-PAM (k-등급 진폭 변조):**

- 장점:
  - 데이터 전송률과 스펙트럼 효율성을 조절할 수 있다.
- 단점:
  - 고등급 PAM은 노이즈에 민감하고 복잡해진다.

**8PSK (8-등급 위상 변조):**

- 장점:
  - 데이터 전송률이 높고 공간적 효율성이 높다.
- 단점:
  - 16QAM 및 64QAM과 비교했을 때 노이즈에 상대적으로 민감하다.

**16QAM (16-등급 진폭 변조):**

- 장점:
  - 높은 데이터 전송률과 공간적 효율성을 제공한다.
- 단점:
  - 64QAM에 비해 노이즈에 상대적으로 민감하다.

**64QAM (64-등급 진폭 변조):**

- 장점:
  - 매우 높은 데이터 전송률을 제공한다.
- 단점:
  - 노이즈와 간섭에 매우 민감하며, 고려해야 할 복잡성이 높다.

각 방식은 사용 사례와 통신 환경에 따라 선택되며, 신호-대잡음 비율 (SNR), 스펙트럼 사용, 데이터 전송률 및 성능을 고려하여 적절한 변조 방식을 선택하는 것이 중요합니다.

### Why do we discuss about complex symbol (or a complex number) in wireless communication?

> 무선 통신에서 복소 심볼(또는 복소수)을 논하는 이유가 무엇인가?

무선 통신에서 복소 심볼(또는 복소수)을 사용하는 이유는 다양합니다. 주요 이유는 다음과 같습니다:

1. **효율적인 표현**: 복소 수는 진폭과 위상 정보를 동시에 포함하므로 신호를 효과적으로 표현할 수 있습니다. 복소수를 사용하면 신호의 세부 정보를 놓치지 않고 표현할 수 있습니다.

2. **다중 차원 표현**: 복소수는 실수 축과 허수 축을 결합하여 복소 평면을 형성하므로, 다양한 신호 파라미터를 다중 차원으로 표현할 수 있습니다. 이것은 다양한 변조 방식, 위상 및 진폭 조절에 유용합니다.

3. **코훼이겐스 및 복조 용이성**: 복소수는 채널 효과와 노이즈와의 상호 작용을 나타내는데 사용되며, 복소 도메인에서는 코훼이겐스 및 복조가 간단해집니다.

4. **복소 변조와 복소 복조**: 복소 심볼은 복소 변조 방식 (예: QAM)과 복소 복조를 사용하여 데이터를 전송하고 복원하는 데 효과적입니다.

5. **고속 데이터 전송**: 무선 통신에서 고속 데이터 전송을 위해서는 다양한 변조 방식과 고려해야 할 매개 변수가 있으며, 복소수를 사용하면 다양한 데이터 속도와 스펙트럼 효율성을 동시에 고려할 수 있습니다.

복소 심볼은 무선 통신 시스템에서 다양한 응용 분야에서 중요한 역할을 하며, 다양한 통신 표준과 기술에서 사용됩니다.

### Where is the digital modulation in wireless communication system

> 무선 통신 시스템에서 디지털 변조는 어디서 이루어지는가?

- Answer is between channel encoding/decoding and DAC/ADC
  - 정답: 채널 인코딩/디코딩과 DAC/ADC 사이에서 일어남

<img width="970" alt="스크린샷 2023-10-22 오후 9 59 34" src="https://user-images.githubusercontent.com/138586629/277166221-292d83e1-4b15-408e-a5ad-abd93e526dea.png">

> 데이터 <-> 소스 코딩 <-> 채널 코딩 <-> **변복조** <-> DAC/ADC <-> RF 회로 <-> 안테나
