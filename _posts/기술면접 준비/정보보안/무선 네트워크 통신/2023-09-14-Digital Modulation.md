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

### BPSK 변복조시스템 고려사항

### Digital Circuit vs. RF Analog Circuit

### DAC and ADC

### BPSK 복조 알고리즘 - 문제

### BPSK 복조 Key Idea

### BPSK 변복조 시스템 – 설명

### 무선 변복조 모뎀 (BPSK시스템) 구현

### 다른 고려 사항

### BPSK performance

## 다양한 변복조 방법 / 송수신기 설계 및 수신기 성능

- BPSK, On-Off Keying, PAM
- QPSK
- 8PSK, 16 QAM, 64 QAM
- 변조 방식 비교

### BPSK, On-Off Keying, PAM

#### BPSK의 다른 관점

#### On-Off Keying (OOK)

#### Pulse Amplitude Modulation (PAM), 예시 4-PAM

#### BER Performance of PAMs

### QPSK

#### Quadrature Phase Shift Keying (QPSK)

#### BPSK 과 QPSK

#### Complex Numbers

#### QPSK = 2개의 BPSK

#### QPSK Signal Constellation

### 8PSK, 16 QAM, 64 QAM

#### 8PSK Signal Constellation

#### PSK + PAM = QAM System

#### 16-QAM & 64-QAM Constellation

#### 64-QAM Constellation 및 복조과정

#### Symbol Error Rate (SER) Curve

### 변조 방식 비교

#### Radio Frequency and Baseband - Summary

#### Communication System and BPSK

#### Communication System and QPSK

#### Communication System and QAM

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

### What is the channel coding and why is it needed?

> 채널 코딩이란 무엇이며 왜 필요한가?

`채널 코딩(Channel Coding)`은 데이터 전송 중에 발생할 수 있는 오류에 대비하여 데이터를 보호하고 오류 검출 및 수정을 위한 과정입니다. 필요한 이유는 데이터 전송의 신뢰성을 유지하기 위해 오류에 대비하고 품질을 향상시키기 위함입니다.

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
