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
  
  
 ## 파일의 세가지 상태와 세가지 단계
 ### 상태
 - **Committed** : 데이터가 로컬 데이터베이스에 안전하게 저장됨
 - **Modified** : 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않음
 - **Staged** : 현재 수정한 파일을 곧 커밋할 예정
 
 ### 단계
 - **Working Directory** : **Working directory**에서 파일 수정
 - **Staging Area** : **Staging area**에 파일을 stage 해서 커밋할 스냅샷을 만듦.
 - **.git directory (repository)** : Staging Area에 있는 파일들을 커밋해서 **Git directory**에 영구적인 스냅샷으로 저장
 
 ## git status : 수정하고 저장소에 저장하기
 워킹 디렉토리의 파일들은 Tracked/Untracked 로 나뉜다. Tracked는 관리 대상으로 이미 스냅샷에 포함한 파일을 의미하고 Unmodified, Modified, Staged중 하나의 상태로 나타난다. 그 외 나머지는 Untracked 파일이라고 지칭한다. 
  - **Untracked** : 관리 대상이 아님.
  - **Unmodified** : 수정되지 않은 상태
  - **Modified** : 수정된 상태
  - **Staged** : 커밋으로 저장소에 기록할 상태  
  
- `cd [깃 경로]` .git 저장소 경로로 이동
- `git status` 파일의 상태 확인하기, 아무것도 안 하면 clean으로 뜸 , -s 옵션은 짧게 보여주기.
- `touch [파일 명]` 파일명 파일 만들기
- `git status` 새로 만든 파일이 untracked file로 올라가 있음. 
- `git add [파일명]` git add 명령어로 파일 새로 추적
- `git status` 새로 만든 파일이 tracked되어 commit 되길 기다리고 있음. 
- `git commit -m “메시지”`
- `git status` commit을 완료한 상태로 clean , 로컬에 저장됨. 
- `git push origin master` git hub에 올리기 (origin repository 연결 되어있음)

- `git status -s` or `git status --short` status를 짤막하게 보여줌
### 실습

![git status 실습](./practiceCapture/gitstatus-s.jpg)
- ??: untracked 파일
- M: modified file
- A: add한 파일 
- status_s_1.txt는 새로 생성 후 add 한 파일
- status_s_2.txt는 새로 생성 후 add 하고 나서 수정한 파일
- status_test.txt는 전에 있던 파일 수정.
- status_s_3.txt는 새로 생성 후 add하지 않은 파일

## Github fork
fork : 다른 원격 저장소에 있는 히스토리를 그대로 나의 GitHub원격 저장소에 복사하는 것

## Github : private and collaborator

### Github private 
git hub는 개인 계정에서 private을 무료로 제공하기 시작함. 단, 3명의 collaborator만 가질 수 있다. (2019.10 기준)

### Github collaborator
- repository의 setting에 들어가면 collaborator 추가 가능
- collaborator를 추가하면 이메일이 가고 그 링크(invitation)를 타고 들어가야 invite가 accept됨.
- collaborator가 my repositories 리스트로 보고 싶으면 fork를 해야함. 


