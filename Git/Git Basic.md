# Git Basic

- Git Bash 사용
## git 설치 및 버전 확인
1. [Git 설치](https://git-scm.com/)
2. 버전 확인  
`$ git --version`

## 환경 설정
처음에 1회 실행
- `$ git config --global user.name "이름"` 이름 등록
- `$ git config --global user.email "이메일@이메일"` 이메일 등록  
- `$ git config --list` 설정 확인

## Git과 Github 원격 저장소에 연동

- `$ mkdir [file명]` 폴더 생성
- `$ cd [폴더명]` 폴더로 이동
- `$ git init` 현재 폴더를 git 로컬 저장소로 등록 , (master)가 나타난다.
- `$ git add [폴더명 혹은 파일명]` git add . 은 현재 폴더의 모든 파일
- `$ git commit -m "commit message"` commit message를 기록 하며 commit하기
- `$ git remote` 연결 된 저장소가 있음 이름이 나오고 없으면 아무것도 안나온다.
- git hub에서 new repository 생성
- `$ git remote [단축 이름] [URL]` URL에 github repository 주소 입력하면 연결
- `$ git push origin master` 데이터 전송 창이 뜨면서 github에 잘 올라감 (로그인 창이 뜨기도)

## .ignore로 git에서 제외시키기
.ignore파일 열어서 원하는 파일 입력 ,  * 과 같은 것으로 확장자 및 공통된 파일들을 ignore 대상으로 넣을 수 있다. Ex) *.pdf
- `$ vim .ignore`
- `$ git add .`
- `$ git status` git 상태 확인 – ignore 에 넣은 파일은 제외 됨을 알 수 있음
- `$ git commit -m "testing ignore"`
- `$ git push origin master` github에 push

## git clone
- `$ git clone [원격 저장소]` github에서 주소를 받아와서 clone하기

## git pull 
- `$ git pull origin master` origin의 내용이 master로 복사

## git clone, pull, fetch 차이
* **git clone**
  - 원격에서는 소스를 수정할 수 없으므로 이 저장소로 작업할 로컬에 내려 받는 과정, 새로운 프로젝트 투입 상황
* **git pull**
  - github에 있는 파일들을 local로 가지고 오지만 pull은 local repository에 저장(add)되며 현재 local repository와 비교
  - git pull = git fetch + git merge
* **git fetch**
  - local에 연결된 remote repository를 업데이트 하는 명령어
