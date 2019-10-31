# Branch

## Basic Branch
* **branch** : lightweight movable pointer to one of commits
* **default branch = master** : 매번 commit 할 때마다 master 브랜치가 앞으로 이동한다.
* **HEAD** : special pointer로 최근에 사용하는 branch를 알려준다.  

- `git branch [브랜치명]` 새로운 브랜치 생성
- `git log --oneline --decorate` --oneline은 한 줄로 표현, --decorate는 브랜치 포인터가 어디를 가리키고 있는지 나타냄
- `git checkout [브랜치명]` 브랜치명으로 포인터 바꾸기 (HEAD가 바꾼 [브랜치명]을 가리킴)
-  파일 수정 후
- `git commit -a -m "메시지"` 수정한 파일 커밋하기
- `git checkout master` master 브랜치로 다시 바꾸기
- `vim [수정했던 파일 명]` 아까 수정했던 파일명을 다시 들어가보면 수정이 안됨을 확인
- `git checkout -b [새 브랜치명]` 브랜치를 생성하고 동시에 새 브랜치로 포인터 바꿈
- `git merge [브랜치명]` 브랜치에서 작업한 내용을 합치기
- `git branch -d [브랜치명]` 브랜치 삭제하기
- `git branch` 브랜치가 무엇이 있는지 알 수 있음
- `git branch -v` 브랜치와 마지막 commit을 알 수 있음
- `git branch --merged` merge된 브랜치를 알 수 있음
- `git branch --no-merged` merge되지 않은 브랜치를 알 수 있음  

merge가 되지 않았을 때 `$git branch -d [브랜치명]`은 실행 되지 않는다.  
강제로 merge하지 않고 지우기 위해서는 `$git branch -D [브랜치명]`을 실행한다.

## Remote Branch
* **remote references**는 브랜치, 태그 , 등을 포함한 remote 저장소의 포인터  

- `git ls-remote` remote reference의 리스트를 조회
- `git remote show` remote reference 리스트 조회 (간단하게 표현)  

* remote-tracking branch : remote branch를 추적하는 branch
  - remote 서버에 연결할 때 자동으로remote branch에 따라 움직임 
  - remote repository에 마지막으로 연결했던 순간에 branch가 어떤 commit을 가리키고 있었는지 나타냄 
* remote branch 이름 : (remote)/(branch) 형식으로 나타냄  

## Push and Pull Branch
* local branch를 서버로 전송하기 위해 쓰기 권한이 있는 remote저장소에 push
- `git push [remote저장소] [branch명]` 
  - 예: `git push origin testing`
  - 나중에 다른 사람이 저장소를 fetch 하고 나서 서버에 있는 push 한 branch(예: testing)에 접근할 때 origin/branch명(예: origin/testing)으로 접근이 가능
  - branch가 새로 생기는 것이 아니라 fetch한 branch 포인터가 생김
* `$git checkout -b [new branch 명] [fetch 한 branch]` 새 branch를 만들기 위한 명령어 
  - 예: `git checkout -b testing origin/testing`
* **pull** : fetch 하고 merge를 수행하는 것으로 서버로부터 데이터를 가져와 현재 local branch와 서버의 추적 branch를 merge한다.

## Tracking Branch
* Remote tracking branch를 local로 checkout하면 자동으로 tracking branch(=upstream branch)가 만들어짐
* Tracking Branch: remote branch와 직접적인 연결고리 존재하는 local branch  
* Tracking Branch에서 git pull하면 remote 저장소에서 데이터를 내려 받아 자동으로 merge 진행  

- `git checkout --track [remote명]/[branch명]` local branch 이름을 자동으로 생성
- `git checkout -b [바꿀 branch명] [remote명]/[branch명]` 다른 이름으로 branch 생성
- `git branch -u [remote명]/[branch명]` 이미 존재하는 branch가 특정 branch 추적
- `git branch --set-upstream-to [remote명]/[branch명]` git branch -u 와 동일
- `git branch -vv` 추적 branch 설정 확인

## Remote Branch 삭제
- `git push origin --delete [삭제할 브랜치명]` 
  - 예: `git push origin --delete testing`
