# study-v1

깃 정리

git bash -> cd 로 문서 이동

ls –al 해당 폴더 안에 있는 전체 리스트 보기

git init 해당 폴더에서 버전관리 시작 

mkdir << 폴더 생성하기

vim << 편집기

vim 안에서 I 누르면 insert 가능 esc 누르고 :wq 하면 나오기

git status 상태보기

git add 파일명 << 얘를 추적해라

git config --global user.name jang-dh
git config --global user.email jangdh0428@gmail.com <<깃 시작하고 한번만 쓰는 것임 
git commit 후 vim 으로 들어가서 message 입력 가능 << 최초 버전 생성

git log 역사 확인

cp 파일1 파일2   <<파일2명으로 복사

git log –p 전 후 버전 비교
git diff 비슷함

reset vs revert

$ git reset c49aaba954588dbcac2196e62d00b257fff0792f —hard 
c49aaba954588dbcac2196e62d00b257fff0792f  commit 상태로 돌아감

git branch < 브랜치 확인

git branch 브랜치이름  < 브랜치 만들기

git checkout 브랜치이름 << 브랜치 이름 으로 들어가기

git log --branches --decorate --graph --oneline 브랜치 썻을 때 전체적인 상황 보기 

git merge 브랜치이름  << 마스터에 브랜치이름 머지

git banch -d 브랜치이름 << 브랜치 삭제

git stash << 현재 작업한것을 숨길때 ( 커밋하기도 싫고 다른 브랜치로 가야할때)

git stash list << stash 리스트 보기

git stash apply << 숨긴것을 다시 꺼낼때

git stash drop << 가장 최신 stash 삭제

git stash pop << apply되면서 drop 까지 한방에

git clone 깃허브주소 프로젝트명 << 깃허브꺼 가져오기

git remote add origin 깃허브주소 <<현재 로컬저장소에 원격 저장소를 연결시킨다 (주소는 origin으로 명명)

gi remote -v << 목록확인

git push origin master << 현재 체크아웃되어있는 로컬저장소 브랜치를 push한다

주소에 . 들어가면 현재 디렉토리

git pull origin master << 원격저장소에있는걸 로컬저장소에 가져오기

git rm --cached –r target/  깃배쉬내에서 타겟폴더 삭제
