# Git 공부
[출처: 내블로그](https://chanspark.github.io/2017/08/29/Git을-배워보자.html)

팀원들과 협업할때 가장 중요한 버전관리툴로 Git을 뽑을 수 있겠습니다. 버전관리 툴로는 Mercurial, SVN, Git등 다양한 종류가 있습니다. 

## Git 명령어
Git은 기본적으로 CLI를 통해서 제어할수 있습니다.물론 아직 CLI가 익숙하지 않으신 분들은 Source Tree 같은 GUI프로그램을 이용해서 좀더 편리한 Git질?을 힐 수 있습니다. 아래는 제가 '자주 사용하겠다' 싶은 명령어들입니다.

### 기본적으로 알아야하는 명령어
1. git add `file` / git add .  
	수정된 파일을 git이 track할 수 있도록 설정하는 명령어. 파일들이 staging된다. '.' 은 '모든 파일'을 뜻함.
2. git commit -m '`message here`'  
	staging된 파일을 커밋하는 명령어. 
3. git push origin `branch` / git push
4. git pull origin `branch` / git pull
5. git init
6. git clone `url`
7. git status
8. git merge
9. .gitignore file
10. git log   
    - git log `--oneline` 

### 언젠가는 필요하게될? 명령어
1. git stash  
 	현재 수정중이던 상태를 로컬에 저장하는 명령어. 깃으로 관리하다보면 커밋을 쏴주지 않을경우 아무것도 못하는 경우가 종종 생기는데, 이럴때 현재 작업을  stash하고  필요한 명령어를 수행한다.
2. git stash pop  
   stash 명령어로 로컬에 저장되어있던 수정사항을 불러온다. 저장되어 있던 stash는 삭제됨.
3. git stash apply  
   stash 명령어로 저장되어있던 수정사항을 현재 브랜치에 '적용'함. 이 과정에서 머지가 일어날 수도 있음. 재밌는거는 `stash`로 저장된 사항들은 아직 유효한 상태임. 따라서 몇개의 브랜치를 이동하며 apply할 수 있는 명령어임.
4. git branch `new branch name`  
   브랜치를 생성하는 명령어
   - git branch -r  
     브랜치 리스트를 알려주는 명령어
5. git checkout `branch || commit` / git checkout `commit` `file`  
   checkout 명령어는 특정 브랜치나 커밋으로 이동하게 되는 명령임. 현재 파일 상태(untracked or tracked)는 새로운 커밋으로 저장을 한 후 이동할 수 있다. 재밌는점은 '이동'한다는 개념이기 때문에 로컬 파일의 내용들도 다 바뀌게 된다. 이전 커밋으로 이동을 하게 되면, 다른 브랜치에 영향을 미치지 않고 독립적인 `HEAD`로 존재하게 된다. 만약 '이전 커밋'에서 생긴 변동사항을 저장하고 싶으면, 브랜치를 새로 생성한 후 체크아웃하면 된다. `git checkout -b <new branch name>`를 입력하면 새로운 브랜치가 생겨나고 기존 커밋은 변경사항이 생기기 전 상태로 돌아가게 된다. 유용하게 사용할 수 있는 기능 중 하나인듯 하다.  
   반면에 특정 파일로 체크아웃 하고, 수정된 파일을 커밋할경우 가장 최근 커밋과 merge가 일어나게된다.
6. git fetch  
   원격 저장소에 있는 커밋들을 로컬 저장소에 저장하는 명령어. 원격 저장소에서 가져온 커밋들은 원격 브랜치에 저장되며, 이 브랜치들은 아직 로컬에 적용되지 않은 상태임. `fetch`를 해서 커밋들을 불러온 후, `merge`를 해서 합쳐야함.
7. git fetch `remote` / git fetch `remote` `branch` 
   특정 저장소 또는 브랜치에 있는 커밋을 가져(`fetch`)오는 명령어.
8. git remote  
   다른 저장소와의 통신을 생성하고, 삭제할 수 있는 명령어. 실시간으로 정보를 주고 받는 개념보다는 사이트 '즐겨찾기' 개념으로 이해를 하는편이 좋을 듯하다. 매번 원격저장소의 URL을 가지고 접속을 하기보다는 특정 값(이름?)으로 저장해놓고 사용한다. 
   - git remote -v
   - git remote add `name` `url`
   - git remote rm `name`
   - git remote rename `old name` `new name`

### git 마스터가 되어보자
1. git revert  
	주로  `git reset`명령어와 자주 헷갈리게 된다. 유의해야할점은 `reset`은 현재 상태에서 바로 전 커밋으로 돌아가는것이고, `revert`는 전 커밋을 앞으로 당겨와서 새로운 커밋을 생성하는 명령어이다. 커밋 4번에서 `revert` 할 경우, 커밋 3번을 당겨와서 커밋 5번으로 생성하게 되는것이다. 이럴 경우 커밋 4번에서 어떤 일이 있었는지 'history'가 남게 되기때문에 단순 롤백하는 경우보다 더 효과적이라고 볼 수 있다.
2. git reset  
   `revert`가 안전하게 뒤로 돌아가는 명령어라면, `reset`은 '매우 위험한' 명령어라고 한다. 굉장히 파워풀한 명령어이며, 지금 당장은 알 필요가 없으므로 패스.
3. git clean  
   untracked 파일들을 삭제. 
4. git rebase, git commit --ammend, git reflog
5. Workflow 비교하는 방법
6. 다른 버전관리툴에서 migrate하는 방법
7. 등등... 
   

*위의 명령어들은 소스트리와 같은 프로그램을 사용하면 쓸일이 없습니다 ㅇㅅㅇ 단지 소스트리 사용법을 익혀야겠죠!*
 
 
참고: [Bitbucket Git Tutorial](https://www.atlassian.com/git/tutorials)





