# 230907

## 목차


- Preview
- Wireless Communication
- Questions

## Preview

- 주파수 (frequency)
  - Propagation(전파)
  - Modulation(변조)
  - Radio Frequency and Baseband (무선 주파수(radio=wireless)와 기저대역)

- 대역폭 (bandwidth)

- Spectrum of 5G
  - Spectrum for Mobile Systems (모바일 시스템을 위한 스펙트럼)
  - Frequency Bands for NR (NR(New Radio)을 위한 주파수 대역)
  - RF Exposure Above 6GHz (6GHz를 초과한 무선 노출)

## Wireless Communication

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


## Questions

###  What is the Maxwell equation and how is it related to the wireless communication?

> Maxwell equation은 무엇이고, 무선 통신과 어떤 관련성이 있는가?

<img width="498" alt="스크린샷 2023-10-05 오후 9 47 46" src="https://user-images.githubusercontent.com/138586629/272906916-d02cd16f-102d-44db-aa2b-8e9fbcc17779.png">

<img width="468" alt="스크린샷 2023-10-05 오후 9 49 11" src="https://user-images.githubusercontent.com/138586629/272907286-ba7d357b-4600-4cff-abea-8adf072a7b21.png">

학습메모 1 참고. 맥스웰 방정식은 결국 전자기파의 존재를 증명했다. <br /><br />

이로 인해 전력이 발생하면 신호가 전파되고 무선 통신이 가능한 것이다.


- Explain a wave’s frequency and wavelength (=파장).
  -  파동의 주파수와 파장에 대해 설명하시오.
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