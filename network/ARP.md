# ARP에 대해서 ✅

# ARP(Address Resolution Protocol)가 필요한 이유

- 단말기 간 통신을 위해서는 통신을 수행하는 물리적 매개체(UTP 케이블)와 해당 매개체가 연결돼 장치를 식별하기 위한 물리적 주소가 필요함.
- LAN Card에 부착된 고유한 물리적 주소를 MAC 주소라고 할 수 있음.
- 즉 최종적인 **단말 간 통신을 위해서는 IP 주소뿐만 아니라 상대방 단말기의 MAC 주소도 알아야 함**
→ ARP

![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image.png)

# ARP의 동작 원리

![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%201.png)

1. **LAN 환경에서 A PC가 B PC로 Packet을 전송합니다.**
2. **A PC는 B PC의 IP 주소와 매핑되는 MAC 주소를 가지고 있는지 ARP Table를 확인합니다.**
3. **없다면, ARP Request 를 Broadcasting 합니다.**
4. **LAN 환경 내 모든 단말기는 ARP Request 를 전달받아 자신의 IP 주소와 비교하고, 맞다면 ARP Reply 를 Unicasting 합니다.
다른 경우, ARP Broadcast Frame 이 폐기됩니다.**
5. **B PC의 MAC 주소를 알게된 A PC는 ARP Table를 생성하고, Packet을 전송합니다.**
    - 참고용
    
    ![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%202.png)
    

### 어떤 취약점이 발생할 수 있을까?

- **기술명 : ARP Spoofing**
- **핵심 : ARP Response 변조**

![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%203.png)

- **어떻게 내가 해결했을까? → Port Security**
    - 스위치에서 port security mode 활성화 → port와 mac 주소 1:1 매핑
    
    ![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%204.png)
    
    ![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%205.png)
    

## 더 나아가서, ARP Ethernet Frame Structure에 대해

**ARP 을 전송하기 위해 이더넷 프레임의 Payload 에 ARP Header 를 구성함.**

![image.png](ARP%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%20%E2%9C%85%2020318fdf38ed80159672c1d190643d44/image%206.png)

- Hardware Type: 네트워크 하드웨어 종류 → 이더넷(1) 을 표현할 때 사용
- Protocol Type: 상위 프로토콜 → 예시) IP 0x0800
- Hardware Length: MAC 주소 길이 → 이더넷(6)
- Protocol Length: IP 주소 길이 → IPv4(4)
- Operation: 작업 방식(요청, 응답) → 요청(1) 또는 응답(2)
- Sender/Target Hardware Address: 송신자/목적지 MAC 주소
- Sender/Target Protocol Address: 송신자/목적지 IP 주소

# 면접 예상 질문

ARP란 무엇인가요? 어떤 역할을 하나요?
ARP의 동작 과정을 설명해주세요.
ARP Request와 ARP Reply의 차이와 동작 방식은?
ARP 캐시(테이블)은 무엇이며, 왜 필요한가요?
ARP 스푸핑(ARP Spoofing)이란 무엇이고, 어떻게 방어할 수 있나요?
ARP와 RARP의 차이점은 무엇인가요?