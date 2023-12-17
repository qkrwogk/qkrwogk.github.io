# 5G Core Network

## 요약

진정한 5G, 5G Core Network! (5G NR말고 기지국 뒷단)

- 1~8(중간)까지는 5G NR까지의 설명. PHY Layer
- 10~12까지는 MAC Layer + 알파
- 13은 5GC를 100% 쓰진않고 같이 쓰는 EN-DC
  - EPC(Evolved Packer Core, 4GC) + NR(5G NR)
- 14~15는 앞으로 펼쳐질.. 5GC

5G는 다양한 application을 염두해두고 설계됨(IoT 등)

## EPC to 5GC

공통점 : CP과 UP의 분리

분리가 된 가장 큰 포인트는 scalability

EPC -> 5GC의 가장 큰 포인트는 `virtualization`

뭔소리냐면 EPC에선 하나하나의 요소가 하드웨어였다면
5G에선 하나하나가 모두 SW로 가상화된 개념임
그래서 UP도 UPF으로 기능들로만 구조를 표현함

"Core"가 기지국에서 Internet가는 역할인데, 이게 5G에선
모든 것을 Function으로 정의했단 게 가장 큰 차이점.

두번째는 Service GW와 PDN GW가 UPF로 합쳐짐

eNB -> gNB (next Generation Node B)
=> 5G 기지국. mobility때문에 RAN이 있어야 하구요
RAN = Radio Access Network

radio protocol을 보면 하이라키 구조를 가져야 하기때문에
PHY, MAC, ... 이런 Layer Structure로 표현되었다.

근데 뭐 5GC는 Layered Architecture는 아니래

5G에선 Control Plane이 하는 역할이 그리 많지않다
SMF(Session Management Function)
AMF와 SMF가 가장 핵심적인 Functions고, 4G의 MME 역할

## What is the "Core Network"

아무튼 UE <-> gNB <-> ... <-> DN(인터넷)

여기서 gNB끼리 네트워크를 RAN(Radio Access Network)
gNB와 DN을 연결해주는 ...을 Core Network(CPF+UPF)
라고 함!

- RAN/gNB & DN은 유저 데이터 전송을 위해 "물리적인" 연결이 필요함
  - -> 이것이 "User Plane Function"에 의해 달성됨
- 모든 다른 RAN/gNB & DN 관련 이슈들은 Core Network Functions에 의해 제어된다.

## Session이란? (뜬금) / Connection

Session이라는 개념은 Connection(연결)과 달라

컴퓨터 과학, 특히 네트워크 분야에서
반 영구적이고 상호 작용적인 정보 교환을 전제하는 연결상태.

세션은 연결상태의 유지보다 연결상태의 안정성을 더 중요시.
그니까 언제든지 통신(연결)이 가능하도록 셋업된 상태.

IP연결에서 세션이 형성된다는 건 UE와 DN이 연결될 준비가 완료되었다는 것.

## PDU(Packet Data Unit) Session in 5G

- end-to-end User Plane connectivity(= a series of connections). UE와 DN 사이의 UPF를 통한 연결들(UE<->gNB<->...<->DN)!

## PDU sessions are established

- ISP <- Internet Service Provider
  - 일반 인터넷
- IMS <- Internet Multimedia Server
  - 음성, 화상 통화, ...

UE <-> gNB <-> UPF <-> external IP flows <-> DNN-1,2

"5G Quality of Service Identifier(5QI)"에 의해
QoS를 결정해줘야 한다. 모든 애들을 좋게 해줄순 없으니까!

## 5G/NR Standardized 5QI Characteristics (1/3)

리소스 타입 : GBR(Guaranteed Bit Rate)

5QI는 1, 2, 3, 4, 65, 66, 67, 75, ... 이런식인데

- Default Priority Level : 1에 가까울수록 높음 우선순위
- Packet Delay Budget : 패킷 딜레이. 짧을수록 좋음
- Packet Error Rate : 에러 레이트. 낮을수록 좋음(에러율 낮음)
- Default Averaging Window : 뭐시기

이게 상황에 따라 저 parameter값이 세트로 옵션으로 정해져있는 거랄까?
YouTube면 5QI 몇번, 라이브 스트리밍이면 5QI 몇번, 긴급통화면 5QI 몇번 이런식

## 5G/NR Standardized 5QI Characteristics (2/3)

리소스 타입 : Non-GBR(Non-Guaranteed Bit Rate)

## 5G/NR Standardized 5QI Characteristics (3/3)

리소스 타입 : Delay Critical Guaranteed Bit Rate(GBR)

이건 말 그대로 Packet Delay Budget이 많이 짧아야 하는 서비스.
대체로 Priority Level 높음

- Default Max Data Burst : 대충 한번에 많은 데이터는 안보내나봄. 그래서 데이터 사이즈 상한

예를 들면 V2X 메시지(자율주행), 공장 자동화, 송전관 컨트롤, AR/VR 서비스 등
이런 거에 대한 옵션들을 미리 다 만들어놨단게 포인트지용~

5G는 다~ 계획이 있다 이말씀

생각보다 스마트폰이 얼마없고 IoT디바이스, 자동차 등 다양한 목적을 커버함.

## PDU sessions revisited

다시 PDU 세션에 대해 설명해보자면

- UPF는 external IP flow와 QoS flow간의 대화를 수행!
- gNB는 QoS flow와 DRB 간의 대화를 수행!
- QoS flow는 a stream of packets with the same 5QI 그 자체!
  - 5QI 같다 = 같은 QoS Requirements

## 5GC Simplified View

AMF = Access & Mobility Functions
SMF = Session Management Functions

UE -> gNB -> AMF로 먼저 요청이 가고, 요금 잘 냈는지 뭐 잘 인증됐는지 확인하고
(처음 세션 수립 전에 Authentication Server, Unified Data Mgmt 등)
이상 없으면 AMF -> SMF로 세션 만들어주세요~~~하고 요청을 함!

그러고 나면 이제 UE -> gNB -> UP -> DN으로 연결이 되고,
AMF, SMF는 이제 다 빠져주는거죠(CP는 이제 큰 역할없음. 필요할 때나 함)

## 5G Core Network is very different from EPC (1/3)

- Native Virtualization
  - 4G에선 MMF/HSS 등으로 하드웨어로 구현되었으나
  - 5G에선 Network Function Virtualization(NFV)로 가상화, Cloud에서 Implementation(구현)됨!!
- Service-based Architecture
  - 하드웨어 기반이 아닌, 서비스 기반으로 역할이 분리된 아키텍처

## 5G Core Network is very different from EPC (2/3)

- Network Exposure
  - Network Exposure Function(NEF)에 의해, 5GC를 컨트롤 할 수 있는 써드파티 어플리케이션이 가능해졌다!
- Enhanced Security Framwork
  - 또 그런걸 안전하게 가능하게 보안적으로도 우수하다!
  - Concealed Subscriber Identity라는 개념이 있는데 이동통신보안 수업들으면 가르쳐주신대! 하지만 난 졸업 ㅋ ㅅㄱ

## 5G Core Network is very different from EPC (3/3)

- **Network Slicing** (중요, 다음 주에 다룸)
  - 다음 여러가지 네트워크, ISP, IMS, 자동차, 공장 자동화 등 다양한 네트워크들을 하나의 physical 네트워크에서 구성하되 logically구분하는 기술!!
- Control and User Plane Separation
  - CP와 UP의 분리!

## Why Standalone?

스킵 ㅋ 위에서 했던 얘기들이 다 답임 ㅇㅇ

## 5G Core Network & 5G Radio Access Network

UE <-> gNB <-> UPF <-> DN
UE에서 바로 User Plane으로 Wifi 등으로 연결도 가능.

## Control of UPF and RAN-UE

가장 기본적인 두 네트워크 Functions

- SMF : Session Management Function
  - Use Plane을 관리하는!
  - UP와 직접적인 통신을 한다.
- AMF : (Initial) Core Network Access and Mobility Management Function
  - gNB와 직접적인 통신을 한다.

왜 Control Function이 필요하냐. UE가 UP와 연결되게 하기 위해.

Random Access를 배웠잖아

UE는 나도 껴줘~ 하고 RACH 채널을 통해서 gNB에 요청을 해야겠죠
그러면 gNB는 스윽 형님(AMF)한테 가서 이친구한테 빈자리 내줘도 되나 하고 물어봐줌.
AMF는 신원조사 한번 스윽 하고 SMF한테 요청해서 UP에 세션 만들도록 해줌.

그 AMF는 신원조사중에 Authentication Server를 통해 Unified Data Mgmt..

- authentication

## 5G Core Network SBA(Service-Based Architecture)

- In addition to UPF/SMF and AMF
  - 다른 많~은 functions가 필요함
  - 다양한 방식으로 구현될 수 있으며, gNB, UP는 그걸 알 필요가 없음.
    - single physical node, distributed multiple nodes, cloud platform 등 다양한 방식으로 구현될 수 있다 이말씀!

<img width="1102" alt="스크린샷 2023-12-14 오전 1 01 10" src="https://gist.github.com/assets/138586629/03d66c71-8a7b-4698-80a8-2f5cc4b43514">

재밌는 게 이 나머지 수많은 서비스들이 그래서 다 API 콜로 정의되어 있음
교수님도 다 알지는 못함 AF, AMF, AUSF, BSF, CHF, ... UDSF, SPF

Non-3GPP access, N3IWF도 있음 -> WiFi, Bluetooth등
꼭 단말 5GC 표준을 따를 필요 없이 5GC UP Functions도 가능하다!

기억해둘만한 것

- AF: Application Function
- AMF: Access and Mobility Management Function
- AUSF: Authentication Server Function
- **NRF : Network Repository Function**
- N3IWF : N3 Interworking Function
- **NSSF : Network Slice Selection Function**
- PCF : Policy Control Function
- SEPP : Security Edge Protection Proxy
- SMF : Session Management Function
- UDM : Unified Data Management
- UPF : User Plane Function

## 5GC is a Service Based Architecture

...

## Network Repository Function (NRF)

<img width="665" alt="스크린샷 2023-12-14 오후 11 39 38" src="https://gist.github.com/assets/138586629/0b9b474e-01e0-4d54-9331-d22b15b117a2">

NRF는 가용한 NF 인스턴스와 그 서비스에 대한 정보를 관리함.

NRF의 주 역할은 다른 NF의 서비스를 제공하거나, 이거를 사용하도록 접근 인가를 하거나 그런 역할을 함

# Network Functions

## Access and Mobility Management Function (AMF)

RAN Signaling의 목적지

## Session Management Function (SMF)

UPF를 제어하고 선택함

## Unified Data Repository (UDR)

subscription 데이터, policy 데이터 이런 유저에 대한 데이터가 직접 저장되어 있는 DB임.

## Unified Data Management (UDM)

이 데이터베이스 UDR을 관리해주는 친구임. DBMS라고 생각하셈

우리 단말의 전화번호, 국가번호 이런게 다 암호화돼서 보관되어 있는데, 이걸 암복호화해주는 게 UDM이라고 보면됨.

## Network Repository Function (NRF)

SMF같은것들이 접근할 수 있게 어떠한 NF들이 있는지, 이런 정보를 가지고 NF들을 관리하는 친구

## Network Exposure Function (NEF)

써드파티 AF(Application Function)s들이 들어갈 수 있는 친구들.

예를 들면 자동차라면 자동차 교통 정보든 뭐든..

## Network Data Analytics Function (NWDAF)

AI나 ML 테크닉을 위한..! 아니면 보안과 관련된!!
Network의 자동화된 데이터 분석이 가능한 뭐시기!

## Policy Control Function

PCF..

## User Plane Function (UPF)

패킷 라우팅 & 포워딩 - 메인 function임.

## 5GC Enhanced Security Framework

Subscriber Permanent ID(SCPI)
Concealed ID(SUCI) 등등

전화번호같은 단말 정보를 암복호화해야 하거든. 거기에 관련된거. 불행히도 아직 잘 안씀

무선통신네트워크보안 수업에서 좀 하신대 ㅋ

## Three main features of 5GCN

<img width="658" alt="스크린샷 2023-12-14 오후 11 53 53" src="https://gist.github.com/assets/138586629/0d34d781-29e1-4887-97e9-b0229e1f764a">

이게 메인 그림이고.

가장 중요한 메시지는 이것이 모두 `software-defined network(SDN)`로 정의되어 있다.

여기서 CP, UP를 분할하는 것은 "scalablity"를 위함임.

"Network Slicing" 지원은? => 이거 다음시간에!

## Questions

- Explain PDU session and QoS flow
- Explain 5GC service-based architecture
- Explain UPF/AMF/SMF
- Explain other 5GC’s control functions

## Explain PDU session and QoS flow

> PDU 세션과 QoS 플로우에 대해 설명하라

## Explain 5GC service-based architecture

> 5GC 서비스 기반 아키텍처를 설명하라

## Explain UPF/AMF/SMF

> UPF/AMF/SMF에 대해 설명하라

## Explain other 5GC’s control functions

> 다른 5GC의 control functions에 대해 설명하라
