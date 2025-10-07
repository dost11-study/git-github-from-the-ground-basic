# git-github-from-the-ground-basic
인프런의 [Git & GitHub, 원리부터 차근차근 - 근본깃 [기초편]](https://www.inflearn.com/course/git-github-%EC%9B%90%EB%A6%AC%EB%B6%80%ED%84%B0-%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EA%B7%BC%EB%B3%B8%EA%B9%83%EB%AC%B4%EB%A3%8C)를 정리한 내용입니다.

## Git 구조
- working directory
	- 실제 파일을 편집하고 변경하는 내 로컬 작업 공간
- staging area
	- 커밋하기 전에 변경 내용을 임시로 저장하고 선택하는 준비 구역
- repository
	- 커밋 이력과 버전을 모두 보관하는 Git의 데이터베이스

## Github
Repository(버전)을 보관하는 클라우드 시스템

## Git 설치

### **1. Homebrew로 Git을 설치해주세요.**

먼저, Homebrew를 사용하여 Git을 설치하는 방법을 소개하겠습니다. Homebrew는 Mac에서 패키지 관리를 쉽게 해주는 툴입니다.

1. **터미널(Terminal) 열기**:
    - `⌘ Command` + `Space`를 누르고, **터미널**을 검색하여 실행합니다.

2. **Homebrew 설치 확인**
	- Homebrew가 이미 설치되어 있는지 확인하려면 터미널에 다음 명령어를 입력하세요.
        ```bash
        brew --version
        ```
      
	-  설치되어 있지 않다면, 아래 명령어를 터미널에 복사하여 실행하세요.
        ```bash
        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
        ```
        
2. **Git 설치**:
    - Homebrew가 설치된 상태라면, 터미널에 다음 명령어를 입력하여 Git을 설치합니다.
        ```bash
        brew install git
        ```
        
    - 설치가 완료되면, Git 버전을 확인하여 제대로 설치되었는지 확인할 수 있습니다.
        ```css
        git --version
        ```

### **2. 유저 네임과 이메일 설정하기**

Git을 처음 사용할 때, 유저 네임과 이메일을 설정해 두어야 커밋할 때마다 누가 작업했는지 기록됩니다.  

1. **Git Bash 실행**:
    - 시작 메뉴에서 **"Git Bash"**를 찾아 실행합니다. Git Bash는 Linux 명령어를 사용할 수 있는 환경을 제공합니다.  
        
2. **유저 네임 설정**:
    - 다음 명령어를 입력하여 전역(global)으로 유저 네임을 설정합니다:
        ```bash
        git config --global user.name "Your Name"
        ```
        
3. **유저 이메일 설정**:
    - 다음 명령어를 입력하여 전역으로 유저 이메일을 설정합니다:
        ```bash
        git config --global user.email "your.email@example.com"
        ```
        
    
4. **설정 확인**:
    - 아래 명령어로 유저 네임과 이메일 설정이 제대로 되었는지 확인할 수 있습니다:
        ```bash
        git config --global --get user.name 
        git config --global --get user.email
        ```

### **3. Git 언어를 영어로 변경해주세요.**

Git은 설치 시 기본 언어로 Mac의 시스템 언어를 따릅니다.  
아래 링크를 참고하여 기본 언어를 영어로 바꿔주세요.

[https://velog.io/@rxdryd/git-출력-언어변경](https://velog.io/@rxdryd/git-%EC%B6%9C%EB%A0%A5-%EC%96%B8%EC%96%B4%EB%B3%80%EA%B2%BD)  
[출처 - [](https://velog.io/@rxdryd/posts)**rxdryd.log**]

## 시작하기

1. .git 폴더에 staging area와 repository 생성하기 (깃이 프로젝트 관리하게 만들기)
	- `git init`
	- 여기에 있는 파일들은 untracked 상태 즉 버전 관리 대상이 아님
2.  working directory의 파일을 staging area에 복사하거나 덮어쓴다 (tracked 상태, 즉 버전 관리 대상으로 추가하기)
	- `git add`
3. staging area에 모아둔 파일들을 하나의 버전(commit)으로 만든다
	- `git commit`


## 저장소 상태 보기

working directory의 파일 상태와 staging area의 파일 상태가 서로 다를 때 커밋할 경우 staging area 기준으로 커밋이 생성됨. 그렇기 때문에 저장소의 상태를 보여주는 명령어를 통해 주기적으로 확인해야함

`git status` 의 기능

	1. staging area와 최신 커밋 간의 차이점
	2. tracked 상태와 staging area 간의 차이점
	3. untracked 상태에 있는 파일


![image](./images/Pasted%20image%2020251006174505.png)

## 저장소 비교
- working directory의 tracked 상태와 repository의 commit 간의 상태를 비교하고 싶을 때
	- `git diff [커밋ID]`
- working directory의 tracked 상태와 staging area를 비교하고 싶을 때
	- `git diff`
- staging area와 repository의 commit과 비교하고 싶을 때
	- `git diff --cached`

![image](./images/Pasted%20image%2020251006202908.png)

커밋 간의 차이점을 알고 싶을 땐 `git diff [커밋ID 1] [커밋ID 2]` 를 사용한다.  
더 쉬운 커밋ID 실행 방법은 `git diff HEAD^ HEAD` 를 써도 최신과 그 이전 커밋 기준으로 동작한다.
![image](./images/Pasted%20image%2020251006203405.png)

## HEAD

1. `HEAD`
	- working directory와 staging area가 어떤 커밋의 상태인지 보여주는 표기이다
2. `git checkout [커밋ID]` 
   - `HEAD` 가 명령어에서 지정한 커밋을 가리키게 만든다.
   - 이때, working directory와 staging area는 HEAD가 새롭게 가리키는 커밋의 상태로 바뀐다
![image](./images/Pasted%20image%2020251006210038.png)

### HEAD의 상대적 위치 (부모 커밋)

`HEAD ^` 는 `HEAD`가 가리키고 있는 커밋(상대적인 위치)에서 과거로 한 칸 떨어져 있는 커밋을 나타낸다.
(이때 ^는 캐럿이라고 부름)

캐럿 대신에 ~를 사용할 수도 있다. 
- 예) HEAD~3은 HEAD로부터 3번 과거의 커밋이다. = HEAD^^^
![image](./images/Pasted%20image%2020251006210846.png)

부모 커밋은 커밋이 화살표로 가리키는 커밋이다.
- 즉, 1~3번 커밋 중 가장 최근에 만들어진 3번 커밋이 HEAD일때 3번 커밋의 부모 커밋은 2번 커밋이다.

## 브랜치

- 브랜치를 통해 독립적인 공간에서 코드를 실험적으로 짤 수 있다
- 다른 브랜치에서 개발한 애용을 단 한줄의 명령어로 가져올 수 있다
- 브랜치를 아무리 많이 만들어도 용량을 거의 차지하지 않는다 (각각의 새로 추가한 커밋들만 가지고 있기 때문)

보통 브랜치 그래프를 보면 아래와 같이 선모양으로 되어 있는데, test 브랜치는 main 브랜치가 가지고 있는 두개의 커밋도 포함하고 있다는걸 기억해야 한다.
![image](./images/Pasted%20image%2020251006224231.png)

아래와 같은 사진의 박스 구조로 이해하면 편하다
![image](./images/Pasted%20image%2020251006224335.png)

### 브랜치 생성하고 이동하기

- HEAD가 브랜치를 가리키면, 해당 브랜치에서 작업하고 있는 상태로 간주한다 (HEAD -> main)
- HEAD가 커밋을 가리키면, 분리된 HEAD 상태이다
	- Detached HEAD가 이 경우인데 어떠한 브랜치도 가리키지 않고 있어서, 새로운 커밋은 생기지만 다른 브랜치로 이동하면 그 커밋은 고아 상태가 되어 사라질 수 있음
- 브랜치가 변경되면 working directory(tracked)와 staging area의 데이터가 해당 브랜치의 HEAD가 가리키는 커밋 상태로 변경된다

HEAD의 실제 모양은 포인터가 포인터를 가리키는 구조이다
![image](./images/Pasted%20image%2020251006232707.png)

## 머지 (3-way merge)

커밋 히스토리에서 

###  충돌 (Conflict)
1. base로부터 main과 test 브랜치에 새로운 head commit이 있는 경우 동일한 파일의 같은 위치를 수정하려고해서 어느 쪽 diff를 적용해야할지 모
![image](./images/Pasted%20image%2020251007153138.png)