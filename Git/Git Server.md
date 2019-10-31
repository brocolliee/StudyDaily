# Git Server
* **bare repository**
  - general remote repository without working directory, only for collaboration so no need to checkout
  - 일반 프로젝트에서 .git 디렉토리만 있는 저장소

## Protocols
* 4가지 프로토콜: **Local , HTTP , SSH , Git**

### Local Protocol
* 가장 기본 적인 프로토콜로 리모트 저장소가 단순히 디스크의 다른 디렉토리에 있을 때 사용
* collaborator 모두 한 시스템에 로그인 하여 개발 or NFS 같은 것으로 파일 시스템 공유 할 때 사용
* 모든 저장소가 한 시스템에 있기 때문에 문제 발생시 모두 다 없어지게 된다.
* git clone 예시
  - `git clone [파일 경로]` 필요한 파일을 직접 복사 혹은 하드 링크 사용
  - `git clone [file://파일 경로]` 네트워크를 통해 프로세스를 별도로 생성 후 처리, 효율성은 떨어짐.
* file://사용 이유 : 복사본을 깨끗한 상태로 남겨두기 위해 사용  

* 장점
  - 간단함. 기존에 있던 네트워크나 파일의 권한을 그대로 사용하기 때문에 설정에 용이  
* 단점
  - 다양한 상황에서 접근할 수 있도록 디렉토리를 공유하는 것 자체가 어렵다.
  - 속도 빠르지 않음
  - 모든 사용자가 쉘에서 remote저장소에 접근이 가능하므로 쉽게 침범하여 내용 수정 가능

### HTTP Protocol
* HTTP Protocol modes: Smart HTTP(version 1.6.6 이후 사용가능), Dumb HTTP
* Smart HTTP
- SSH or Git Protocol처럼 통신 but HTTP,HTTPS 포트를 사용하여 통신하며 HTTP 인증방식을 사용 (사용자 이름, 비밀번호 방식 사용)
- Git에서 가장 많이 사용하는 Protocol
* Dumb HTTP
   - smart HTTP 요청에 Git Server가 응답하지 않을 때 Git Client는 차선책으로 Dumb HTTP로 시도
   - remote 저장소를 그냥 파일 전달하는 웹 서버로 취급
   - HTTP Document root 밑에 bare repository를 두고 post-update hook을 설정
   
* 장점(Smart HTTP)
  - 읽기와 쓰기 모두 하나의 URL을 사용, 아이디와 비밀번호 방식의 인증 사용
  - SSH보다 간단하고 빠르고 효율적, SSL인증서 요구 가능 
  - 모든 회사 방화벽 통과하도록 구성  
* 단점(Smart HTTP)
  - SSH설정보다 HTTP, HTTPS를 사용이 복잡할 때 존재
  - Push 할 때 HTTP 인증 사용이 좀 더 복잡 (but smart HTTP는 그렇게 단점이 별로 없다.)

### SSH Protocol
* Git의 대표 프로토콜로 SSH 사용시 대부분 서버에서 SSH로 접근이 가능하도록 설정이 되어있다. 
* SSH는 인증기능이 있어 어디든지 쉽게 사용할 수 있다.
* SSH 예시
  - `git clone [ssh://URL]`
  - `git clone [user@]server:project.git`
  
* 장점
   - SSH daemon은 흔하고 다뤄본 경험들이 있고 , SSH daemon과 관리도구들이 OS배포판에 포함되어 있기 때문에 상대적으로 설정하기 쉽다. 
   - 모든 데이터는 암호화 되어 인증된 상태로 전송되어 보안에 안전하다.
   - SSH는 전송시 데이터를 가능한 압축하여 효율적이다.   
* 단점
   - 익명으로 접근할 수 없어 읽기 전용도 익명으로 시스템에 접근할 수 없다. 그래서 오픈소스 프로젝트로는 SSH만으로는 부족하다. 

### Git Protocol
* Git protocol은 git에 포함된 daemon을 사용하는 것으로 port는 9418이다.
* SSH와 비슷한 서비스를 제공하지만 인증 메커니즘이 존재하지 않는다. 
* 잘 사용하지 않는 프로토콜로 존재만 알아 두기

* 장점
  - 전송속도가 제일 빠르다. 별도의 인증이 필요 없고 읽기만 허용하는 프로젝트에 적합
* 단점
  - 인증 메커니즘이 없어서 Git 프로토콜로만 접근하는 프로젝트는 좋지 않다. 
  - 대규모 회사의 방화벽에서는 이 포트를 막아 놓는다. 설치가 제일 어려운 방법이며 별도의 daemon이 필요하다.
