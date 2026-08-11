# 2026-git-start

in addition to local git, contents from git hub web

오늘의 학습 목표: 작업자 B의 Merge 충돌 실습

오늘의 학습 목표: 작업자 A의 Git 협업 실습


sequenceDiagram
    participant A as 작업자 A (로컬 저장소)
    participant GitHub as GitHub (원격 저장소)
    participant B as 작업자 B (로컬 저장소)

    Note over A, GitHub, B: 두 작업자가 동일한 README.md 문장을 가지고 시작
    
    A->>A: README.md 같은 문장 수정 및 커밋
    A->>GitHub: git push (작업자 A의 변경 사항 반영)
    
    B->>B: README.md 같은 문장 수정 및 커밋
    B->>GitHub: git push 시도
    GitHub-->>B: Push 거절 (rejected - fetch first)
    
    B->>GitHub: git fetch origin (원격 변경 내역 확인)
    B->>B: git merge origin/main (병합 시도)
    
    Note over B: README.md 파일에서 충돌(Merge conflict) 발생[cite: 1]
    
    B->>B: 충돌 표시 삭제 및 최종 내용 결정 후 git add[cite: 1]
    B->>B: git commit (Merge Commit 생성)[cite: 1]
    B->>GitHub: git push (충돌 해결 결과 반영)[cite: 1]
    
    A->>GitHub: git fetch origin (원격의 최신 결과 가져오기)[cite: 1]
    A->>A: git merge origin/main (최종 결과 로컬 동기화)[cite: 1]
