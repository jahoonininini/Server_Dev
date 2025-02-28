# Git 을 이용해 협업하기 (3): GitHub 협업 기능 활용하기

GitHub 협업 기능 중심으로 학습.   
특히, 브랜치 기반 작업 뒤 Pull Request를 통해 코드 리뷰 진행, 팀원들과 효율적 협업 프로세스를 중점.    
외부 프로젝트나 오픈소스 기여 시 Fork 활용법 확인

## 1. Pull Request 이해하기

### 1.1 PR의 개념과 필요성
- 브랜치 기반 작업<br>
브랜치를 이용해 독립적으로 기능 개발, 완성된 코드를 합치는 방식이 협업의 기본
- 코드 리뷰의 중요성<br>
개발 과정에서 발생할 수 있는 오류, 개선 사항 등을 미리 점검하여, 코드 품질과 유지보수성을 높일 수 있음.
- PR을 통한 품질 관리<br>
작성된 코드를 병합하기 전, 다른 팀원들이 PR 화면을 통해 변경 사항을 검토하고 피드백을 제공함.<br>
이를 통해 무분별한 코드 반영을 방지, 프로젝트의 안정성과 일관성 보장.
### 1.2 PR 활용하기
#### 1.2.1 PR 생성과 관리
1. 브랜치 푸시
- 독립된 기능(브랜치)에서 작업을 마친 뒤, 해당 브랜치를 원격 저장소에 푸시