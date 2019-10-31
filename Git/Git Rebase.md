# Git Rebase

## Rebase 정의
한 branch에서 다른 branch로 합쳐지는 방법 
  1) **Merge** 
  - History가 남아 있음  
  ![git Merge](./practiceCapture/gitMerge)
  
  2) **Rebase**
  - History는 단순 but 정확한 history 필요시 사용 금지, fast-forward 개념 사용  
  ![git Rebase](./practiceCapture/gitRebase)  

  - `git checkout [branch명]` 해당 브랜치로 바꾸기
  - 파일 수정 실행 
  - `git add .`
  - `git commit -m "message"`
  - `git rebase master test2` test2 branch 수정사항을 master branch에 적용
  - `git checkout master` `master로 다시 돌아오기
  - `git merge test2` master branch를 Fast-Forward진행
  - `git branch -d test2` test2 branch 삭제  
   
  * 이미 공개 저장소에 push 한 commit은 rebase 하지 말 것. 다른 사람과 branch가 엉키게 되기 때문에 문제 발생. 
  * 위 문제 같은 경우 rebase한 것을 다시 rebase 한다
  * `git pull --rebase` 명령어를 사용 (나중에 책 참고)
  
## Rebase vs Merge
* 정리를 위해서 local에서 사용하는 것은 그냥 rebase해도 되지만 push로 remote에 내보낸 commit에 대해서는 rebase를 하지 말아야한다.
* merge와 rebase는 history관점에서 다르기 때문에 상황을 보고 어떤 것을 사용할지 결정

