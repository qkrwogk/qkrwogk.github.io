# 5G Call Flow and Network Slicing

## 15장

- 5G Call Flow
  - => 결국 어떤 흐름으로 UE가 통화(또는 인터넷 통신)가 가능하게 되는 것인지
- Network Slicing

# 5G Call Flow

## UE Registration Call Flow (1/2) Authentication and Key Agreement (AKA)

<img width="1121" alt="스크린샷 2023-12-15 오전 12 17 14" src="https://gist.github.com/assets/138586629/fcedbfef-8caf-4fa1-a5d0-65df637925c8">

AUSF가 관여를 함. 인증을 해야겠지요?
UE가 RAN 통해서 AMF에 접근을 하면,
AMF는 NRF에 AUSF 어딨냐고 물어봄.
AUSF는 UDM과 통신해서 가입한 사용자인지 확인함
AUSF가 굳굳 하면 그때 SMF에 요청해서 세션 만들겠지
그럼 그때부터 UPF와 통신을 하겠지요~

## RM-NAS Registration Request (step 1/2/3)

1. UE -> RAN, RM-NAS Registration Request
2. RAN -> AMF, RM-NAS Registration Request
3. AMF -> UE, Identity Request / UE -> AMF, Identity Response

## AMF starts registration procedure by asking NRF (step 4)

4. AMF <-> NRF, AUSF Discovery

## AUSF generates Q&A for the requested SUCI (step 5/6/7)

5. AMF -> AUSF, Authenticate Request
6. AUSF <-> NRF, UDM Discovery
7. AUSF <-> UDM, Authentication Request/Response

## AMF's Authentication and AUSF's check (step 8/9/10)

8. AUSF -> AMF, Authentication Response (challenge)
9. AMF <-> UE, Auth Request/Response (challenge)
10. AMF -> AUSF, Authentication Request (challenge)

USIM이 있으면 응답할 수 있는 AKA Challenge를 주고, EAP Req/Res 진행

## Authentication is done (step 10/11)

10. AUSF -> AMF, Authentication Response
11. AMF -> UE, EAP-SUCCESS

성공한 경우 UE에 알림

## Now, Authentication is done. Then,

UE is "legitimate" now
이제 인증 완료됨!

AMF는 단말의 subscription & policy data 사본을 보관함

- UDM에 subscription data가 있고
- PCF에 policy data가 있음

## UE Registration Call Flow (2/2) (step 12-20)

<img width="1160" alt="스크린샷 2023-12-15 오전 12 24 35" src="https://gist.github.com/assets/138586629/1d8492f1-741c-40f6-8770-40b07a93ce61">

12. AMF <-> NRF, UDM Discovery
13. AMF <-> UDM, UECM registration
14. AMF <-> UDM, SDM Get
15. AMF <-> UDM, SDM Subscribe
16. AMF <-> NRF, PCF Discovery
17. AMF <-> PCF, AM Policy Control Get
18. AMF <-> PCF, Event Exposure Subscribe
19. AMF -> UE, Registration Accept
20. AMF -> UE, Registration Complete

## As a result of registration, UE gets

- 다음을 포함하는 Registration Accept Message
  - 5G-GUTI
  - Registration Area
  - Mobility restriction
  - Allowed NSSAI
  - IMS voice over PS indication

## PDU Session Establishment Call Flow (1/2)

1. UE -> AMF, NAS Message
2. AMF <-> NRF, SMF Discovery
3. AMF -> SMF, Create SM Context Request
4. SMF <-> NRF, UDM Discovery
5. SMF <-> UDM, UECM registration
6. SMF <-> UDM, SDM Get
7. SMF <-> UDM, SDM Subscribe
8. SMF -> AMF, PDU Session Create SM Context Response

## PDU Session Establishment Call Flow (2/2) Policy Control and User Plane Setup

<img width="1156" alt="스크린샷 2023-12-15 오전 12 27 15" src="https://gist.github.com/assets/138586629/2faaef7b-9f50-41f2-b6f4-8504cfb35989">

9. SMF <-> NRF, PCF Discovery
10. SMF <-> PCF, SM Policy Control Get
11. SMF <-> PCF, Event Exposure Subscribe
12. SMF <-> NRF, UPF Discovery
13. SMF <-> PCF, Event Exposure Notify
14. SMF <-> UPF, N4 Session Establishment
15. SMF -> AMF, Communication N1 N2 Message Transfer
16. AMF -> RAN, N2 PDU Session Request, NAS
17. RAN -> UE, RRC Connection Reconfiguration, NAS
18. RAN -> AMF, N2 PDU Session Response
19. AMF -> SMF, PDU Session Update SM Context Request
20. SMF <-> UPF, N4 Session Modification
21. SMF -> AMF, PDU Session Update SM Context Response
22. UE <-> RAN <-> UPF <-> DNN, User Plane

# Network Slicing

## Network Slicing Overview

이통사업자들이 일반사용자 말고 헬스케어, 자동차 등등 B2B로 네트워크를 특정 조직에게 할당해주는 그런 B2B에 대한 내용

<img width="1257" alt="스크린샷 2023-12-15 오전 12 31 59" src="https://gist.github.com/assets/138586629/6994055b-8e33-49ac-bcc1-51c949b87f5b">

물리적으론 그대로 있고, 가상적으로 완전히 다른 네트워크로 분리시키는 기술

E2E orchestration functionality는 AN/CN/TN 자원의 관리가 요구됨 ㅇㅇ

## Network Slice Requirements

SLA(Service Level Agreement), 예를 들면 현대자동차가 자동차 통신을 위한 네트워크를 이통사업자인 SK 등에게 협약을 한다.

Generic Network Slice Template(GST). 일종의 계약서를 쓰는거임. 현대차는 이러이러한 (품질 등에 대한) 요구사항을 쓰고, 이통사업자는 그걸 준수해야 하고 ㅇㅇ 그정도의 리소스를 할당해줘야 하겠죠.

## Important GST atrributes

모니터링, 레이턴시, 네트워크 패킷 사이즈 등 여러가지 네트워크의 특징들을 정의할 수 있다.

## Network Slice Instances and Subnets

Slice Instances and Subnets..!

아주 다양한 게 가능하다

## Slicing in the RAN and the CN(Core Network)

RAN과 CN을 슬라이싱해서 할당해준다!

- RAN Slicing
  - Slice-aware Scheduling
  - Radio Resrouce Partitioning
  - Slice-aware User Plane Routing
- CN Slicing
  - Slice-aware Virtualized Network Function(NVF) 할당
  - Slice-aware User Plane Routing

## Slice Identifier

5G/NR Stand Alone에서는, Network Slicing이 새로운 속성으로 제공됨

- S-NSSAI(Session-Network Slice Service Assistance Information)

  - SST(Slice Service Type)
  - SD(Slice Differentiator)

- 하여간 하나 단말이 꼭 하나의 네트워크에만 접속할 수 있는 게 아니고, 표준에서 하나의 단말이 8개까지의 S-NSSAI를 가질 수 있음.
  - 물론 아직은 `voice` & `data`. 2 개의 sliced된 네트워크를 사용한다 ㅋ

## 5GS is natively slice-aware (How 5G is designed to support Network Slicing)

**NSSF(Network Slice Selection Function)**!!

바로 이 친구를 기본적으로 참고해서. 접속을 할 때 어떤 Network Slice를 사용할 지를 구분한다.

## Network Slicing - Allocation of Functions

아직은 안됐지만 EN-DC가 아니라 Stand Alone 5G를 우리가 사용하게 된다면,

가장 쉬운 예제가 voice & data가 다른 logical 네트워크로 구성된다고 볼 수 있음.

<img width="872" alt="스크린샷 2023-12-15 오전 12 48 04" src="https://gist.github.com/assets/138586629/2cb0aea5-0e24-4fba-abe1-778aa6374ca4">

- ISP(Internet Service Provider) = 인터넷
- IMS(IP Multimedia Subsystem) = 음성통화

대부분은 공통으로 사용하게 되고, UPF만 나눠진다고 보면 되시겠다.

## Allocation of Functions - others

이건 조금 더 먼 미래의 얘기.

<img width="1381" alt="스크린샷 2023-12-15 오전 12 51 37" src="https://gist.github.com/assets/138586629/33601f6c-f33d-4d6f-bf61-283c8ecfe8ce">

Network Slicing이 더 잘 도입이 된다면

요런식으로 Network Slice마다 서로 다른 DN

그리고 CN단에서도 여러 NF들이 공유되기도 하고, 따로 할당되기도 하고~~

## AMF selection During UE Registration

...

## SMF and UPF selection example

...
뭐 위에서 다 설명한거 ㅇㅇ

## RAN Slicing - Slice-aware Scheduling

## RAN Slicing - Radio Resource Partitioning

마지막 페이진데, 결국 하고싶은말은

Radio Resource를 효율적으로 잘 분할해주는 게 목적이다 이거다!

## RAN Slicing - Slice-aware User Plane Routing

같은얘기

## 뭐 이제 또 샤샥 넘어감

## Core Network Slicing Examples

여러 다른 네트워크들이 다른 DN까지 가는 데 뭐 이러저러하다.

## 정리

Network Slicing에서 가장 중요한 개념은

Network Resource(주파수 자원, 유선 자원 등)를
B2B 개념으로 특정한 vertical application을 위해
가상적으로 특성화된 네트워크를 제공하는 그런 것이다!

여기까지!!!!

## 무선통신네트워크특론 총정리

Physics부터 쭉~ 이동통신 Network 전반에 대해 가르쳐줌

이런 기본적인 내용을 기반으로 이동통신 보안에 대해서도 공부해보세요~ 끝!

## Questions

- Explain how CP functions (AMF/NRF/AUSF/UDM/...) are involved in the 5G call flow
- Explain Network Slice
  - why is it needed, what it is and how it works
- Explain Service Level Agreement

## Explain how CP functions (AMF/NRF/AUSF/UDM/...) are involved in the 5G call flow

> CP function들(AMF/NRF/AUSF/UDM/...)이 어떻게 5G call flow에 사용되는지 설명하라

## Explain Network Slice

> 네트워크 슬라이스에 대해 설명하라

### why is it needed, what it is and how it works

> 이게 뭔지, 왜 필요하고 어떻게 동작하는지

## Explain Service Level Agreement

서비스 레벨 승인이 무엇인지 설명하라
