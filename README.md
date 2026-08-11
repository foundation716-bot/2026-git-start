# 2026-git-start

로컬 저장소에서 수정한 내용입니다. Github 웹에서 수정한 내용입니다.

오늘의 학습 목표: 작업자 A의 Git 협업 실습
오늘의 학습 목표: 작업자 B의 Merge 충돌 실습



```mermaid
sequenceDiagram
    participant A as 작업자 A (로컬 저장소)
    participant GitHub as GitHub (원격 저장소)
    participant B as 작업자 B (로컬 저장소)

    Note over A, B: 두 작업자가 동일한 README.md 문장을 가지고 시작
    
    A->>A: README.md 같은 문장 수정 및 커밋
    A->>GitHub: git push (작업자 A의 변경 반영)
    
    B->>B: README.md 같은 문장 수정 및 커밋
    B->>GitHub: git push 시도
    GitHub-->>B: Push 거절 (rejected - fetch first)
    
    B->>GitHub: git fetch origin (원격 변경 확인)
    B->>B: git merge origin/main (병합 시도)
    
    Note over B: README.md 파일에서 충돌(Merge conflict) 발생
    
    B->>B: 충돌 표시 삭제 및 최종 내용 결정 후 git add
    B->>B: git commit (Merge Commit 생성)
    B->>GitHub: git push (충돌 해결 결과 반영)
    
    A->>GitHub: git fetch origin (최신 결과 가져오기)
    A->>A: git merge origin/main (최종 결과 동기화)
