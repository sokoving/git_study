# 명령어(git bash)
pwd : 현재 경로 출력(지금 내가 있는 위치(폴더))
ls : 현재 디렉토리 내부 파일 목록 출력(지금 위치에 있는 파일 모두 보여줘)
clear : 화면 깨끗이

cd ** : 디렉토리 변경 (** 폴더로 이동)
	cd Desktop/ :바탕화면으로 이동 [~/Desktop]
	cd .. : 뒤로 이동
	cd ../.. : 뒤로 두번 이동
	cd ~ : 사용자 폴더로 가기
	cd e: : e드라이브로 이동

** [Tab] : **로 시작하는 폴더 이름 완성
** [Tab][Tab] : **로 시작하는 폴더 이름 목록

mkdir ** : **이름의 폴더 만들기
	mkdir a b c : a, b, c 폴더 한 번에 만들기
rmdir ** : **이름의 폴더 삭제
	rmdir a b c : a, b, c 폴더 삭제
touch *.txt : *이름의 텍스트 파일 만들기
notepad *.txt : *이름의 텍스트 파일 열기
code *.txt : *이름의 텍스트 파일을 vscode로 열기


#하위 폴더 만들기
 만든 하위 폴더와 그 하위 파일을 add, commit은
 .git 폴더가 있는 상위 폴더에서 명령


#	    add          commit
working tree - staging area - repository

git status : working tree의 정보를 보여줌
git diff : working tree의 변경사항을 보여줌
	git diff ** : **파일의 변경 사항을 보여줌

git log : commit된 버전 정보를 보여줌
	git log --oneline : 버전 정보를 한 줄로 보여줌
	git log --stat : 버전 정보를 자세히 보여줌
	git log -p : 버전 정보를 더 자세히 보여줌
  *q로 빠져나오기



####버전 관리####

0. 사용자 정보 등록 [컴퓨터당 한 번]
   $ git config --global user.email "mail"
   $ git config --global user.name "name"
  
1. 로컬저장소(내 컴퓨터) 프로젝트 폴더 생성

2. $ git init
 초기화(Initialization) [프로젝트/폴더당 한 번]
 해당 폴더로 이동해서 (cd 명령어 사용) 
 깃 초기화 명령을 하면 (버전관리 시작)
 해당 폴더에 .git 이라는 숨김폴더 생성
 로컬 저장소가 됨
 (master)가 붙음

3. $ git add 파일명
   $ git add .
working tree에 있는 작업물을 add를 통해 staging area에 올린다

4. $ git commit -m "커밋 메시지"
staging area에 있던 작업물을 유의미한 버전으로 저장함.

   $ git commit -am "커밋 메시지"
이미 add한 파일을 수정했을 때 add 건너뛰고 커밋 가능


   $ git tag 
수많은 커밋 중 유의미한 변화가 있는 커밋에 버전 넘버링을 해 관리에 편의성을 줌
 ex) git tag v1.0.0 -m "First Release version" 68c1b63
	    넘버링은 회사마다 다름		git log에서 확인
			-m는 선택 사항

5. 원격 저장소 생성 (깃허브 저장소)

  깃허브 사이트 로그인 한 후 
  + 버튼 누르고 New Repository 선택
  해당 repository의 code(url) 복사

6. 로컬 저장소와 원격 저장소 연동 [프로젝트/폴더당 한 번]

  $ git remote add origin https://~~~
		  저장소 이름 origin 말고 딴 거 써도 되는데 보통 origin 씀
		  나중에 헷갈리니까 origin 쓰기


7. 로컬 버전관리작업내용 원격에 업로드

  $ git push origin master


*주의
로컬저장소 내부에서는 커밋을 취소 가능
푸시(업로드) 이후에는 커밋 취소가 불가능
 >커밋 취소의 흔적이 남음



####클론(clone)####
0. 1번째 로컬저장소에서 원격저장소에 푸시.
1. 원격저장소(깃허브)의 프로젝트를 복제한다.(클론 생성)
	$ git clone https://저장소URL

2. 2번째 로컬저장소에서 커밋을 해 새로운 버전을 생성한다.
	$ git commit -m "커밋 메시지"

3. 새로운 버전을 원격저장소로 푸시한다.
	$ git push origin master

4. 1번째 로컬저장소에서 풀을 통해 2번째 저장소의 작업물을 업데이트한다.
	$ git pull origin master

*주의
 **집컴과 회사컴 사이에 버전 차이가 있는 상태에서 푸시할 경우 에러남.
 **클론 작업할 때는 pull을 미리 하자
 **팀 작업 때는 push했을 경우 고지(주로 팀장급이 함)
푸시는 신중히!!



####버전 간 이동 (git checkout)####

현재 작업물 add, commit 후 이동

$ git log --oneline
	목록에서 이동하고 싶은 커밋 아이디 복사

$ git checkout **
	** 버전 커밋으로 돌아감

$ git log --oneline --all 
	master 버전 로그 보여줌
	head가 현재 checkout한 버전(포인터라고 생각)

$ git checkout master 	로컬의 최신버전으로 돌아가기
$ git checkout origin/master 깃허브의 최신버전으로 돌아가기
$ git checkout v1.0.0 	이전에 넘버링했던 태그로 돌아가기


-이전 버전에서 수정을 하여 새로운 branch 만들 수 있음
 이전 버전을 확인하는 용도이지 수정이 아님


####reset####

$ git reset --hard 33ef7b8
	33ef7b8 버전 이후 파일 완전 삭제
$ git reset --soft 33ef7b8
	파일 삭제하진 않고 unstaged 상태로 내림
	수정 파일을 지우진 않는다

#reset --hard로 파일을 날려버렸다 해도 이전 버전 주소를 가지고 있다면 복구 가능
reset하기 전에 log --oneline으로 주소 저장하기

#push 이전 commit만 기록 완전 삭제 가능
push를 했다면 그 이후에는 기록은 남는다.
push는 신중하게!!

#checkout	 reset --softf		reset --hard
head만 움직임		master와 head 둘 다 이동
커밋 남아있음	커밋 삭제		커밋 삭제
파일 남아있음	파일 남아있음		파일 삭제



####branch###
master 버전은 놔두고 독립적(개별적)으로 작업해
새 작업 후 있을 충돌, 에러를 방지한다.
팀 작업할 때 좋음

$ git branch : 현재 만들어져 있는 branch 목록을 확인
$ git log --oneline --all --graph 

1. $ git branch **
	** branch를 만든다

2. $ git checkout **
	** branch로 이동 (head가 **로 이동한다)

3. ** branch에서 작업후 add, commit을 한다.
	(master) > (**)

4. $ git checkout master
	head를 **에서 master로 이동

5. $ git merge **
	** branch에서 작업한 내용을 master에 통합
	다른 branch에서 작업한 내용도 마찬가지로 통합

6. 같은 이름의 파일을 작업해서 merge하면 conflict(충돌)이 남
  >자동병합에 실패, 수동으로 합쳐야 함.

7. $ git commit -am "****"
  병합 끝~
  (이미 add 되어있는 파일이기 때문에 add 건너뛰고 -am 함)

8. $ git branch -d ** **
	만들었던 ** branch 삭제

*주의
 각 branch에서 오류가 없는지 수정할 부분 없는지 확인하고 
 최종적으로 merge해야 함
 merge하고 branch 수정하면 소용 없음~
 다시 해야 함