# GIT, GITHUB

* GITHUB GUI로 형상관리는 해보았으나 GIT으로 정리한 적이 없어 정리하고자함.

**GIT**

## Git 사용 add, commit

* Git이라는 버전관리 소프트웨어를 통한 형상관리 가능
* Git을 통해 작업한 코드들 기록, 보관가능, 과거 작업내용, 과거로 revert, pull, push 등등

**코드짤 작업용 폴더 생성**

* 터미널에서 작업할 작업용 폴더를 생성하여 아래와 같은 명령어 입력.
* 버전이 아무거나 뜨면 git 설치성공

```git
git --version
```

**git 유저 이름 셋팅**

```git
git config --global user.email "홍길동@naver.com"
git config --global user.name "홍길동"
```

* 컴퓨터에서 git을 처음 사용할 시에 터미널에 입력
* 누가 지금 git을 쓰고있는지 구분하기 위한 아이디 등록과 같은 것

**작업 폴더내 git 이용**

* 파일의 경로로 이동하여 git init 부터 입력하고 시작.
* 입력하면 git이 파일생성하는거, 코드작성하는걸 추적하게 해줌.
* 아래와 같이 사용.

```git
git init       
git add 파일명  
git commit -m '메세지내용'  
```

* git init 을 통해 git 생성
* text.txt 파일 생성 후 git add text.txt 명령어 입력
* git commit -m 'text.txt파일 생성 commit'

**용어 정리 staging area & repository**

![Alt text](image.png)

* 버전 만들 때 git add, git commit 입니다.
* git add 하면 staging area로 이동.
* git commit 하면 repository 이동.
* 아래는 추가 명령어

```git
git add 파일명1 파일명2    // 여러 파일 동시 스테이징
git add .   // 전체 스테이징
git status
git restore     // 스테이징 파일 취소
git commit -m '메세지'
git log     // vim 에디터 j,k 위아래 스크롤, q로 종료
```

> 간단한 기능(회원가입 폼 레이아웃 같은) 추가 시 commit 주기가 제일 좋다.

## Git diff 사용

* commit 하기 전과 현재 코드의 차이를 보여주는 명령어 git diff

```git
git diff 커밋id     // 과거의 특정 commit과 비교
git difftool    // diff 보다 비주얼적으로 더 보기 좋게 보여준다.
```

* git diff 별로면 git graph 부가 기능을 통해 볼 수도 있습니다.

## Git branch 사용

* Git branch 왜 쓰는지에 대해 먼저 알아보고자한다.
* 커밋하면서 계속 코드 짜다보면 새로운 기능 추가하고, 수정한다. 원본파일에 바로 작업해도 되겠지만 혹시나 코드가 꼬이거나 망가지거나 할 경우 프로젝트의 복사본을 만들어 개발해야한다.
* 이를 위해 git 안에서 branch 기능을 사용해 복사본을 만들어 작업한다.(아래 그림과 같이)

![Alt text](image-1.png)

```git
git branch 브랜치이름   // 프로젝트 사본 생성
git switch 브랜치이름   // 만든 브랜치로 이동 (checkout과 같음)
```

* 어떤 브랜치인지 확인할 떄는 git status를 자주 사용하자.

![Alt text](image-2.png)

* coupon branch를 만들었다고 가정했을 떄 그림은 위와 같습니다.
* coupon branch에서 작업한 내용은 main branch와 아무런 영향이 없습니다.
* coupon branch에서 작업한 내용이 완벽하다할 때 원본코드가 있는 main 브랜치에 합치면 됩니다. 이 때 사용하는 것이 merge

![Alt text](image-3.png)

```git
git switch main
git merge 브랜치명
```

* main 브랜치로 이동 후에 get merge coupon 하면 코드들이 main으로 합쳐진다.
* 충돌이 나는 경우에는 어떤 코드를 남길지 결정 후에(==== << >> // 이런거 지우고) 원하는 코드만 남기고 아래 명령어 사용

```git
git add 파일명
git commit -m '메세지
```

> 브랜치 생성 git branch 브랜치명, 이동 git switch 브랜치명, 합치기(main 이동 후) git merge 브랜치명, commit 내역 확인 git log --graph --oneline --all, 브랜치 합칠 때 충돌 발생 시 파일 열어서 수정 후 git add, git commit 하기