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
