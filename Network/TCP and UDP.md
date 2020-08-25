# TCP and UDP

### UDP (User Datagram Protocol)

- IP 상에서 동작하는 **신뢰성이 없는** 메세지 지향 통신을 제공하는 비연결형 프로토콜
  - 받았겠지 라는 가정
- 신뢰성을 지원하지 않아 단순하고 고속 통신이 가능
- 브로드캐스트가 가능
- SNMP (네트워크 진단), SYSLOG( 로그 수집) 등 서비스에서 사용
- 실시간 서비스가 요구되는 영상 및 음성 스트리밍과 IP 전화에 사용
- UDP 헤더에는 순서 번호가 없음



### TCP(Transmission Control Protocol)

- IP 상에서 동작하는 **신뢰성이 있는** 메세지 지향 통신을 위한 프로토콜
- 바이트 스트림을 전송
- 순차적인 전달
- FTP( 파일 전송), SMTP(메일 송신) , POP3(메일 수신), HTTP(웹페이지 열람) 등의 서비스 프로토콜에서 사용
- 전이중 (full-duplex), 점 대점 (point to point) 연결 방식
  - 전이중 : 전송이 양방향으로 동시에 일어날 수 있음
  - 점 대점 : 각 연결이 정확히 2개의 종단점을 가지고 있음
- 3 way hand shake를 통해 연결을 설정하고 4 way handshaking을 통해 해제 한다. 



#### TCP 기능

- 연결 설정 
  - 네트워크 통신을 위한 가상적인 통신로를 설정
- 확인 응답
  - 통신 내용에 이상이 없으면 긍정 확인 응답 신호 전송 (ACK)
  - 통신 내용에 이상이 있으면 부정 확인 응답 신호 전송 (NACK)
- 중복 제어
  - TCP 헤더에 순서번호를 실어 보내서 순서를 복원하고 중복 제어
- 재전송 타이머
  - 송신 쪽에서 패킷을 송신 할 때 타이머를 가동하여 ACK이 일정 시간 동안 오지 않으면 테이터 재전송
- 연결 관리
  - TCP 헤더의 제어 플래그를 이용하여 연결 설정 및 해제 관리
- 윈도우 제어
  - 한번에 수신할 수 있는 데이터 크기 제어
- 흐름 제어
  - 중간처리 속도로 인하여 수신 호스트가 데이터 처리 하는데 있어서 지연이 발생하면 송신 호스트에 대해데이터 전송 중지 및 재재 지시
- 혼잡 제어
  - 통신 상황에 따라 통신 가능한 데이터 조절
  - 보낼 메세지를 잘게 쪼개서 흩뿌린다.
- 검사합
  - 데이터에 오류를 검출하는 check sum을 헤더에 넣어서 확인 
- 재전송 제어
  - ACK이 올 때까지 송신 측은 송신용 소켓 버퍼에 데이터를 저장 및 관리
  - ACK 받으면 삭제





#### Reference

-  [https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Network#tcp%EC%99%80-udp%EC%9D%98-%EB%B9%84%EA%B5%90](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Network#tcp와-udp의-비교) 
-  https://mangkyu.tistory.com/15 
-  https://asfirstalways.tistory.com/327 