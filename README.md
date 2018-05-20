Test 
------------------
Test line  


HelloHello

나중에는
add commit push 만 하면 됨. 처음 설정할 때는 init하고 등등 해야함

build된 파일은 commit하지 말자. 이런걸 git이 알아서 해주도록 하는 게 gitignore

a.exe	a.exe 예외처리
*.exe	모든 exe 파일을 예외처리(숨김파일 .*.exe도 포함)
/a.exe	최상위 디렉토리만의 a.exe 예외처리
!a.exe	이미 예외처리된 규칙을 무시하고 a.exe 추가
!a/**	이미 예외처리된 규칙을 무시하고 a 디렉토리에 있는 모든 파일/디렉토리 추가

(/: root, !: not)


normal rool같은 경우에는 torvalds/linux/.gitignore에서 확인할 수 있는데, 컴파일 중간에 생기는 파일같은것들이 주로 들어가 있는 것 같다

binary같은거 예외처리할 때 컴파일 잘 안되거나 그럴 수도 있으므로, gitignore를 처음부터 제대로 정해놓아야 한다.

각 commit에는 commit hash값이 있다.

git show
git log
git diff
git reset	git add 전으로 되돌리기. git add된 것을 git add하기 전으로 바꿀 뿐 파일 자체가 바뀌는 것은 아님
		특정 커밋으로 jump할 수 있다. 
		- git을 시간여행 시킨다
		- 실제 파일들까지 시간여행시킨다
		보통 commit 실수했을 때 많이 사용

		git reset		초록색->빨간색
		git reset --hard	실제 파일들까지 reset. commit된 시점으로 원상복구
		git reset --soft	git만 reset

		* 커밋을 잘못했을 때*
		git reset --soft @^	파일 냅두고 한단계 위로 이동하기
		(수정)
		git add .
		git commit
		git push origin master -f	-f means force. git revert는 되돌리는 커밋을 만드는건데(revert했다는 기록이 남을 것), 이거는 예전에 한 커밋을 없던 셈치는 것. 
						지금은 서버보다 내 로컬이 더 옛날과정이다보니 -f 안하면 에러뜰 것. 다만 다른 사람과 같이 할때는 조심해야..
						동료가 내 커밋을 사용해서 개발하고 있을 때 reset해서 커밋을 없던셈쳐버리면 merge할 때 문제가 생긴다.
						즉, reset은 10초 이전에 바로 수정해야 할 정도로 바로바로 해야할 때, 그 사이에 누가 내 커밋을 가져갈 일 없을 경우에만 사용하기.

		git revert @		
		git revert a^..b

		git reflog		실제 시간순으로 log. 내 기준으로. reset/revert 사용 전의 시점이 어느 커밋인지 찾아낼 수 있음. reset/revert 잘못했을 때 찾아낼 수 있음.
					서버에는 저장 안되고 로컬에만 저장된다.
		

git revert
git cherry-pick		다른 branch에 있는 commit 몇개를 가져오고 싶을 때
git merge

git status


git은 commit과 그 hash 중심으로 구성된다.

..	~같은 의미. 1..3 는 1~3 같은

2018.1.23


commit 예쁘게 하기
1. 커밋 제목의 첫 글자는 대문자로
2. 과거형이 아니라 현재형
3. 제목엔 맞침표 없이
4. 자세하게 작성
5. 두번째 줄은 항상 비워둠(커밋 메시지는 여러줄 가능함)	-m "asfd" 하고 엔터 눌러서 쓰면 그게 body가 된다. 그러나 두번째 줄은 '반드시' 항상 바꿔두어야 한다. title과 body를 구분하는 기준이 됨
6. 첫 줄은 50자 내로, 나머지 줄은 70자 이내로 작성
7. 대형 프로젝트의 경우 앞에 소분류 적기(여기선 소문자로 시작해도 됨)	좀 대형 프로젝트인 경우.
8. 분할해서 커밋하기(중요)	나중에 revert하거나 할 때 힘들어짐	gitignore

Signed-off 본인서명	CC 참조

주석: 코드를 처음 보는 사람을 이해시키기 위한 목적
커밋 메시지: 코드가 왜 이렇게 바뀌었는지 알리는 목적

git grep
	소스 코드 중 특정 키워드 검색
	$ git grep abcd		// abcd라는 키워드를 모두 하이라이트

git checkout
	브랜치를 이동할 수 있음
	git checkout branch_name	branch_name으로 이동
	git checkout -b branch_name	branch_name 새로 생성
	git push origin branch_name	branch_name에 업로드

	특정 파일(디렉토리) 가져오기 가능. 다른 브랜치의 특정 파일만 빼올 수도 있음
	git checkout branch_name -- Makefile	branch_name에 있는 Makefile을 가져옴	git을 통해 가져왔으므로 git add는 바로 되어있는 상태
	-- Makefile block.c 	이러면 Makefile과 block.c 를 가져온다는 의미

git merge
	branch 병합하기
	특정 branch의 3번째 commit을 병합하려고 하면, 1번째~3번째까지 같이 병합됨(history까지)

git branch
	이름만 거창하고 브랜치 지울 때만 사용되는 명령어
	git banch -d branch_name	local에서 branch_name을 지우는 명령어. github에서는 안 지워진다. 서버에서도 지우려면 git push origin :master	이러면 master branch가 서버에서 삭제된다
	모든 브랜치를 보고 싶을 때도 사용된다고 합니다
	git branch -a

git fetch & git pull
	remote 업데이트 받아올 때 사용하는 명령어
	git fetch라고 하면 origin만 업데이트
	git fetch --all 이라고 하면 following된 것들까지

git pull
	git fetch와 git merge의 단축키같은 것. git fetch 한 다음 git merge하는 걸 한번에 하는 것
	노트북과 데스크탑의 로컬 파일이 다른 경우에 git pull을 쓰면 꼬일 수도 있음. 
	git fetch를 한 다음 git status 등을 하면서 문제가 있는지 확인하고 git merge하는 게 좋음.

	서버에 1, 2, 3이 있고 로컬에 1이 있을때 git pull 치면 로컬이 1, 2, 3을 바뀔 것

git cherry-pick
	cherry-pick: (최고를) 선별하다. 농장에서 선별하는 그런 것
	특정 branch의 특정 commit만 가져오고 싶을 때도 사용
	마음에 드는 커밋만 따로 git merge(브랜치 병합) 없이 적용
		그러면 commit의 hash값은? 	cherry-pick 전후로 바뀔까?	merge는 같다(안 바뀐다)
						달라야 할 것. 같으면 안 된다. git log 등만 생각해봐도 그 이전의 hash값에 dependency가 있어서.. merge는 다같이 가져오는거니까 괜찮은데
						cherry-pick은 뜬금없이 특정 commit만 가져오니까 바뀌어야 한다.

git log --oneline
	너무 길 때 한줄로 축약해서 log 보여주기(세부적인 내용은 생략됨)

git log --format="%H %ae %ce" 	// H는 hash값, ae는 arthor email, ce는 commiter email
git log --format="%H %ae %ce" > a.txt	//이러면 a.txt에 저장된다. > 말고  | grep 으로 필터링 등을 할 수도
git diff --stat

Type of commit
	git commit	그냥 커밋(자기 커밋)
	git revert	커밋 되돌리기
	git cherr-ypick	특정 커밋 적용
	git merge	병합

git commit --amend
	제일 마지막 커밋을 다시 수정
	커밋 메시지를 수정하고 싶거나, 새로 바뀐 파일까지 반영하고 싶을 때
	git add main.cpp
	git commit -m "Initial commit"
	git add test.cpp
	git commit --amend -m "Initial commit"
	
	hash값은 어떻게 될까? 파일이 바뀌었으니..

git reflog
	commit을 바꿨는지 아닌지 보여줌. 여기서 볼 수 있듯이 커밋 hash값은 다 다르다

	git commit --amend 라고만 치면 -m을 다시 입력하는 창이 뜬다
	
git revert --no-edit
	기본 리벗 커밋 메시지만 유지
	git commit --amend --no-edit 도 된다
	no edit은 텍스트 에디터를 안띄우겠다는 의미이기도 함
	git commit만 쓰면 텍스트 에디터가 뜰 것

git revert --continue	중단된 revert 재개
git revert --quit	revert를 중단
git revert --abort	revert를 중단하고 이전 시점으로 되돌아가기

conflicts - 충돌
	revert할 수 없다 등... 종종 뜬다
	
	git mergetool	로 해결

	a..b	a< <=b
	a^..b 	a<= <=b
	
	c로부터 앞으로 2개까지 pick하기
	c^^^..c
