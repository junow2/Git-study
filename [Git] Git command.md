# **자주 사용하는 Git 명령어를 기억하기 위해 정리한 문서**

- Github에 이미 저장소가 있을 경우 

        git clone [Repo_url]

- 로컬 저장소와 연결하는 경우 

        git init 
        git remote add origin [Repo_url]
- 다른 컴퓨터에서 작업해 로컬 저장소 업데이트가 필요한 경우

        git pull origin [branch name]

- 작업한 파일을 원격 저장소에 업로드하기 

        git add . || git add [dir]          // Working directory -> Staging Area 
        git commit -m "[commit message]"    // Staging Area -> repository(.git) 
        git push -u origin [branch name]    // remote repository upload 

- [branch] 목록 확인하기 

        git branch 

- 파일 상태 확인하기 

        git status 


- [branch]로 이동하기 

        git checkout [branch name]

- [branch] 합치기

        git merge [branch name] // main에서 해당 코멘드 실행시 [branch name] 작업물이 메인에 생성됨 
        

 # Git에는 세 가지 영역이 존재한다. 

        Working Directory   Staging Area    Git Directory

        Git     -> Working: Checkout
        Working -> Staging: Stage 
        Staging -> Git    : Commit

- Working Directory 

        프로젝트를 진행하는 실제 작업 공간으로 개발한 소스 및 자원이 존재하며 이곳에서 파일을 수정 및 추가합니다.

- Staging Area 

        워킹 디렉터리에서 작업한 내역을 Git 디렉터리로 커밋 하기 위해 커밋 대상 목록으로 담아두는 장바구니 목록 같은 영역입니다.

- Git 디렉터리 

        실제로는 .git 이라는 이름의 디렉터리이며, 여러가지 버전의 커밋 데이터들과 Git 프로젝트에 대한 모든 정보를 담고 있는 핵심 데이터베이스 디렉터리입니다.

