# Git을 활용한 버전 관리 (1): Git 기초 개념 이해
버전 관리의 필요성과 Git의 핵심 개념에 대한 서술

## 1. 버전 관리의 필요성
1. 동시 작업으로 인한 충돌 방지
2. 과거 버전으로의 손쉬운 복원
3. 여러 실험(시도) 간 이력 유지
4. 변경 이력 추적 및 책임 소재 파악
## 2. Git의 핵심 개념
Git은 분산형 버전 관리 시스템이다. Git에서 중요한 개념은 크게 3가지 작업 영역(워킹 디렉토리, 스테이징 영역, 저장소), 그리고 그안에서 이뤄지는 커밋(Commit)과 HEAD이다.
### 2.1 Git의 3가지 작업 영역
1. Working Directory (워킹 디렉토리)
- 실제 코드 작성 작성·편집·삭제 등을 수행하는 디렉토리
- 코드 변경 후, 아직 커밋하지 않은 수정 사항은 이 워킹 디렉토리에만 반영
2. Staging Area (스테이징 영역)
- 커밋하기 전에, "이번 커밋에 포함도리 변경 사항"을 임시로 모아두는 공간
- 여러 파일 중 선택적으로 스테이징할 수 있어, 논리적으로 하나의 작업 단위가 되도록 커밋을 구성 가능
3. Repository (저장소)
- 커밋이 최종적으로 저장되는 영역, .git 내부 디렉토리 내부에서 모든 버전 이력이 관리
- 여기에서 더 나아가 로컬 저장소(Local Repository)는 내 컴퓨터에 있는 저장소를 말하고, 원격 저장소(Remote Repository)는 팀원들이 함께 접근할 수 있는 서버(예:GitHub, GitLab 등)에 위치한 저장소
- 즉, 로컬 저장소는 개인 개발 환경에서의 변경 이력을 담당. 원격 저장소는 협업을 위한 코드 공유와 통해 이력을 담당
### 2.2 Commit과 버전
Git에서 커밋(Commit)은 특정 시점의 변경 내용을 사진 찍듯이 스냅샷 형태로 저장하는 작업
각각의 커밋은 고유한 해시(hash)로 식별되며, 이 해시 값과 함께 작성자, 날짜, 커밋 메시지 등이 기록된다.
### 2.3 HEAD
Git에서 HEAD는 "현재 작업 중인 버전(커밋)"을 가르키는 특별한 포인터(pointer)다. 즉, HEAD가 어느 커밋을 향하고 있느냐에 따라 워킹 디렉토리가 해당 커밋의 상태를 반영한다.
## 3. Git 설치 확인 및 초기 설정
### 3.1 Git 설치 확인
```bash
$ git --version
```
- 정상적으로 설치되었다면 git version 2.x.x 등 버전 정보가 표시
### 3.2 Git 사용자 정보 설정
1. 전역(Global) 사용자 정보 설정
```bash
$ git config --global user.name "사랑"
$ git config --global user.email "love@example.com"
```
2. 설정 확인
```bash
$ git config --list
```

# Git을 활용한 버전 관리 (2): Git 기본 명령어 실습
## 1. 레포지토리 설정 및 초기화
### 1.1 사용자 정보 설정 (git config)
git은 각 커밋에 작성한 정보를 기록, 올바른 사용자 이름과 이메일을 설정.
```bash
$ git config --global user.name "사랑"
$ git config --global user.email "love@example.com"
```
### 1.2 로컬 저장소 초기화 (git init)
프로젝트용 디렉토리에서 git init을 하여 로컬 저장소로 만든다.
```bash
$ git init
```
- git init : .git 디렉토리가 생성되며, 해당 폴더가 Git 로컬 저장소로 등록
## 2. 변경 파일 다루기
### 2.1 새 파일 생성
```bash
$ touch README.md
```
### 2.2 스테이징 (git add)
```bash
$ git add README.md
```
- 특정 파일만 올릴 때: git add <파일명>, <파일명>
- 현재 디렉토리 내 모든 수정도니 파일을 한꺼번에 올릴 때 : git add .
### 2.3 변경 취소 (git restore)
아직 커밋하지 않은 변경을 되돌리고 싶다면, git restore 명령어를 사용
```bash
# 워킹 디렉토리에서 변경된 내용 취소
$ git restore README.md
# 이미 스테이징된 파일을 스테이징 해제
$ git rm --cached README.md
```
## 3. 정보 확인하기
### 3.1 저장소 상태 확인 (git status)
```bash
$ git status
```
- 새로 생성된 파일, 수정된 파일, 스테이징된 파일 등을 항목별로 표시
- 커밋 준비가 안 된 파일과 준비된 파일을 구분해 보여주므로, 현재 저장소 상태를 파악하기에 유용한 명령어
### 3.2 커밋 이력 확인 (git log)
```bash
git log
```
- 작성자, 커밋 메시지, 커밋 시각, 해시 등을 확인
- git log --oneline 은 해시 메시지만 간략히 표시, git log --graph 는 브랜치 구조를 시각화
### 3.3 변경 사항 비교 (git diff)
```bash
# 워킹 디렉토리 vs 스테이징 영역
$ git diff
# 스테이징 영역 vs 마지막 커밋
$ git diff -staged
```
- 과거 커밋과 현재 커밋 간 차이를 비교하려면 git diff <커밋해시> <커밋해시> 등의 형식으로 사용 가능
## 4. 버전 관리하기
### 4.1 커밋 생성 (git commit)
```bash
$ git commit -m "Add README.md as initial project description"
```
- git log 로 해당 커밋이 추가된 것을 확인
### 4.2 추가 수정 및 커밋
1. 파일 수정(README.md)
```md
<!-- READM.md 에 들어간 내용 -->
이 저장소는 Git 명령어 실습을 위한 예제 프로젝트입니다.
현재 버전: v0.1
```
2. 스테이징 및 커밋
```bash
$ git add README.md
$ git commit -m "Update project version in README"
```
### 4.3 이전 버전으로 되돌리기 (git reset)
```bash
# 가장 최근 커밋만 삭제하고, 변경 사항은 워킹 디렉토리에 남긴다.
git reset --soft HEAD^

# 변경 사항을 스테이징 영역에서 해제하고 워킹 디렉토리에만 남긴다.
git reset --mixed HEAD^

# 워킹 디렉토리 자체도 이전 버전으로 되돌려버린다.
git reset --hard HEAD^ 
```
- HEAD^는 "바로 이전 커밋"을 의미, HEAD~2는 "이전의 이전 커밋" 등으로 표현
## 5. .gitignore 파일 활용
프로젝트 작업 시, 빌드 결과물이나 임시 파일, 민감 정보 등을 Git 이력에 포함시키지 않고 무시하고 싶을때 .gitignore 파일을 활용
1. .gitignore 파일 생성
- 프로젝트 루트 폴더(~/git_project/git_1)에 .gitignore 이름의 파일을 생성
2. 무시 패턴 작성 예시
```md
# 빌드 결과물 무시
/build

# 운영체제별 임시 파일
*.log
*.tmp

# 민감 정보 파일
.env
secret.key
```
- /build : 프로젝트 루트의 build 디렉토리를 무시
- .log : 확장자가 .log 인 모든 파일 무시
- .env : 특정 파일명을 무시
3. 적용 확인
- .gitignore 파일에 추가도니 패턴에 해당되는 파일들은 git add . 를 해도 자동으로 무시되어 스테이징되지 않는다.
- 이미 추적 중이던 파일을 .gitignore 에 추가만 해서는 제외되지 않으므로, 필요하다면 git rm --cached <파을> 등을 통해 한 번 추적을 중지해야 한다.
## 6. 종합 시나리오 예제
1. 디렉토리 생성 및 이동
```bash
$ mkdir git_2
$ cd git_2
```
2. Git 초기 설정 확인
```bash
$ git config --list
```
- 필요시 git config --global user.name, git config --global user.email 설정
3. 저장소 초기화
```bash
$ git init
```
4. 파일 생성
```bash
$ touch README.md
```
5. 스테이징 및 커밋
```bash
$ git add README.md
$ git commit -m "test commit"
```
6. 파일 수정 후 재커밋
```bash
$ git add README.md
$ git coomit -m "Update README version 2.0"
```
7. 상태 확인
```bash
$ git status
$ git log --oneline
```
8. 원격 저장소 Push
```bash
$ git push origin master
```
- master 는 브랜치이다.
9. .gitignore 생성
- .gitignore 파일 작성 후, 무시 목록을 추가
10. 변경 취소 및 되돌리기
- git restore 로 수정 사항을 되돌리거나, git reset 을 통해 커밋을 취소해 이전 버전으로 돌아갈 수 있음.
## 7. 정리
- git config: 사용자 정보 설정 및 확인
- git init: 새로운 Git 로컬 저장소 생성
- git add: 변경 사항을 스테이징 영역에 추가
- git commit: 변경 내용을 확정하여 버전(커밋)으로 기록
- git status: 현재 스테이징/비스테이징 상태 확인
- git log: 커밋 이력 확인
- git diff: 수정된 부분 차이 비교
- git restore: 변경 사항 혹은 스테이징을 취소
- git reset: 특정 시점으로 버전을 되돌림
- .gitignore: 추적에서 제외할 파일(또는 패턴) 지정
# .git 디렉토리의 역할
Git 저장소를 초기화할 때 생성되는 .git 디렉토리는 Git이 버전 관리를 수행하는 데 필요한 모든 정보를 저장하는 "내부 데이터베이스" 역할을 한다.
1. objects
- Git이 관리하는 모든 커밋, 트리(tree), 블롭(blob) 객체가 해시 값(sha-1)을 키로 하여 저장 되는 곳이다.
```md
트리(tree) :
- 트리는 Git에서 디렉토리 구조를 나타내는 객체. 트리는 파일과 다른 트리(하위 디렉토리)를 포함할 수 있다.
- 각 트리는 그 안에 포함된 블롭과 트리의 목록을 가지고 있으며, 각 항목의 이름과 해당 객체의 SHA-1 해시로 식별
- 트리는 Git의 커밋 객체와 연결되어 있으며, 커밋은 특정 시점의 트리 상태를 참조
- 예를 들어, 특정 커밋이 있을 때, 그 커밋은 해당 시점의 파일과 디렉토리 구조를 나타내는 트리를 가리킴.

블롭(blob) :
- 블롭은 "Binary Large Object"의 약자로, Git에서 파일의 내용을 저장하는 단위
- 블롭은 파일의 실제 데이터만 포함하고 있으며, 파일 이름이나 메타데이터(예: 파일의 권한, 수정 시간 등)는 포함하지 않음
- 각 블롭은 SHA-1 해시를 사용하여 고유하게 식별. 이 해시는 블롭의 내용에 기반하여 생성
- 예를 들어, 텍스트 파일이 내용이 "Hello, World!"라면, 이 내용에 대한 블롭이 생성되고, 그 블롭은 해당 내용의 SHA-1 해시로 식별

SHA-1(Secure Hash Algorithm 1) :
- 출력 크기 : 160bit (20bite)
- 특징 : SHA-1은 MD5보다 더 강력한 보안성을 제공하지만, 여전히 충돌 저항성이 약해지는 문제가 발견. 보안이 중요한 분야에서는 더 이상 사용이 권장 되지 않음.
- 문자열 : 16진수 40자리로 표현(16진수 한자리에 4bit 사용)

```
2. Refs
- 브랜치(branch), 태그(tag) 등이 어떤 커밋을 가리키는지 참조 정보를 저장
- 예 : refs/heads/main 파일은 현재 main 브랜치가 어떤 커밋 해시를 가리키는지를 명시
3. HEAD
- 현재 작업 중인 브랜치 혹은 특정 커밋(Detached HEAD 상태일 경우)의 참조 정보를 담고 있음
- HEAD를 이동(checkout)하면 이 파일 내용이 바뀜
4. Config
- 현재 저장소에만 적용되는 Git 설정(사용자명, 이메일, ignore 옵션 등)이 기록
- 글로벌 설정(~/.gitconfig)보다 우선순위가 높아, 특정 프로젝트에서만 다른 설정을 적용할 수 있음
5. Index
- 스테이징 영역에 어떤 파일과 변경 사항이 포함되어 있는지 관리
- git add 를 실행하면, 이 파일이 갱신되어 다음 커밋에 포함될 내용이 기록

즉, .git 디렉토리는 Git의 모든 버전 관리 동작을 가능하게 해주는 핵심 데이터 저장소다. 개발자는 .git 디렉토리를 직접 수정할 일이 거의 없으며, Git 명령어를 통해 안전하게 조작하는 것이 일반적이다. 만약 .git 디렉토리가 삭제되거나 손상되면 해당 저장소의 버전 이력 전체가 사라지거나 복구가 어려워지므로, 주의해서 다루어야 함.
