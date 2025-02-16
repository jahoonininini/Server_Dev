# CLI 기초 명령어 학습 및 실습

- Markdown(.md)에서 코드 예제를 강조하고 싶다면 ```(백틱)을 사용하면 된다. `는 숫자 1 왼쪽에 위치한다.<br>
- \- 를 쓰고 싶다면 특수기호 앞에 백슬래시(\\)를 추가하면 된다.
```bash
# 여기에 코드 예제를 작성하세요
$ echo "Hello, World!"
```

## 1. CLI 기초 명령어 합습 및 실습
### 1.1 디렉토리 탐색 및 관리 
#### 1.1.1 pwd
pwd(print working directory)는 현재 작업 디렉토리의 절대 경로를 출력
```bash
$ pwd
```
#### 1.1.2 ls
ls 는 현재 디렉토리의 파일 및 하위 디렉토리 목록 표시
```bash
$ ls
```
#### 1.1.3 cd
cd(changed directory)는 현재 작업 디렉토리를 변경
```bash
$ cd [디렉토리 경로]
```
- ~ 홈 디렉토리를 의미함
- .. 상위 디렉토리를 의미함
- \- 이전 디렉토리로 이동
### 1.2 파일 및 디렉토리 관리
#### 1.2.1 mkdir
mkdir 는 새로운 디렉토리를 생성
```bash
$ mkdir 직박구리
```
#### 1.2.2 touch
touch는 새로운 빈 파일을 생성하거나, 이미 존재하는 파일의 수정 시간을 갱신
```bash
$ touch README.md
```
#### 1.2.3 mv
mv 는 파일이나 디렉토리를 이동하거나 이름을 변경할 때 사용
```bash
$ mkdir mv
$ mv README.md mv/ 
$ cd mv
$ mv README.md ..
```
```bash
$ mv README.md README_trans.md
$ mv README_trans.md README.md
```
#### 1.2.4 cp
cp는 파일이나 디렉토리 복사
```bash
$ cp README.md mv/
$ rm mv/README.md
```
### 1.3 기본출력
#### 1.3.1 echo
echo 는 뒤따르는 문자열을 출력
```bash
$ echo "Hello, World!"
```
#### 1.3.2 cat
cat 은 텍스트 파일의 내용을 화면에 출력
```bash
$ cat README.md
```
## 2. 개발 상황에서 자주 사용하는 명령어
### 2.1 프르세스 확인 및 종료
#### 2.1.1 ps
ps 명령어는 현재 실행 중인 프로세스 정보를 확인. 보통 ps aux 나 ps -ef 와 같이 옵션을 조합해 사용.
```bash
# 실행중인 프로세스 중 java 라는 단어가 포함된 프로세스만 출력
$ ps aux | grep java
```
- -e 또는 -A : 모든 프로세스 표시
- -f : 프로세스의 전체 형식 확인.(부모 프로세스 ID, 사용자, 시작 시간 등)
- -u [사용자] : 특정 사용자가 실행한 프로세스를 확인
- -p [PID] : 특정 프로세스 ID(PID)에 대한 정보 표시
- aux : 모든 프로세스를 자세히 표시. a는 다른 사용자의 프로세스도 포함, u는 사용자 정보, x는 터미널에 연결되지 않은 프로세스도 포함
#### 2.1.2 kill
kill 명령어는 지정한 PID(Process ID)를 가진 프로세스를 종료
### 2.2 특정 포트 사용 프로세스 확인 및 종료
서버를 구동하거나 외부 API를 연동할 때 특정 포트를 사용 중인 프로세스를 확인, 필요에 따라 종료
#### 2.2.1 lsof(windows는 제공 X)
```bash
# 8080 포트를 점유하고 있는 PID 관련 정보를 출력
$ lsof -i :8080
```
```bash
# 필여 시 해당 PID를 이용해 프로세스 강제 종료
$ kill -9 <PID>
```
#### 2.2.2 netstat
netstat 명령어는 포트별 연결 상태를 확인할 때 사용
```bash
# 현재 LISTEN 상태에 있는 모든 포트 목록을 확인
$ netstat -an | grep LISTEN
```
### 2.3 현재 열려 있는 포트 확인
```bash
$ netstat -an | grep LISTEN
```
- a : 모든 소켓(서버 소켓, 클라이언트 소켓 등)을 표시
- n : IP 주소와 포트 번호를 숫자 형태로 바로 표시
### 2.4 그 외 유용한 명령어
#### 2.4.1 tail -f
로그 파일이나 서버 콘솔 출력이 담긴 파일을 실시간으로 모니터링할 때 사용
```bash
$ tail -f /var/log/syslog
```
#### 2.4.2 curl
외부 API나 웹 서비스에 대한 요청,응답을 테스트할 때 간단히 사용
```bash
# 로컬의 8080 포트에서 동작 중인 애플리케이션 /api/health endpoint 상태를 확인
$ curl -X get "<http://localhost:8080/api/health>"
```
