# 2026-git-start

로컬 저장소에서 수정한 내용입니다. Github 웹에서 수정한 내용입니다.

오늘의 학습 목표: 작업자 A의 Git 협업 실습
오늘의 학습 목표: 작업자 B의 Merge 충돌 실습


```mermaid
sequenceDiagram
    autonumber

    participant A as 🧑‍💻 작업자 A<br>(로컬 저장소)
    participant G as ☁️ GitHub<br>(원격 저장소)
    participant B as 🧑‍💻 작업자 B<br>(로컬 저장소)

    Note over A, B: 💡 사전 준비: 두 작업자가 동일한 README.md 문장을 가지고 시작

    rect rgb(238, 242, 255)
        Note right of A: Phase 1. 작업자 A의 정상 반영
        A->>A: 📝 README.md 수정 및 커밋
        A->>G: 🚀 git push (A의 변경 사항 반영)
    end

    rect rgb(254, 242, 242)
        Note left of B: Phase 2. 작업자 B의 Push 거절
        B->>B: 📝 README.md '동일한 줄' 수정 및 커밋
        B->>G: 🚀 git push 시도
        G-->>B: ❌ Push 거절 (rejected - fetch first)
    end

    rect rgb(255, 251, 235)
        Note left of B: Phase 3. 작업자 B의 충돌 확인 및 해결
        B->>G: 🔍 git fetch origin (원격 내역 몰래 가져오기)
        B->>B: 🔀 git merge origin/main (내 로컬에 병합 시도)
        
        Note over B: ⚠️ README.md 파일 충돌(Conflict) 발생!
        
        B->>B: ✂️ 충돌 내용 수정(최종 코드 결정) 후 git add
        B->>B: 📦 git commit (Merge Commit 생성)
        B->>G: ✅ git push (충돌 해결 완료된 결과 최종 반영)
    end

    rect rgb(240, 253, 244)
        Note right of A: Phase 4. 작업자 A의 최신화 동기화
        A->>G: 🔍 git fetch origin (병합된 최신 내역 가져오기)
        A->>A: 🔀 git merge origin/main (로컬 동기화 완료)
    end

    Note over A, B: 🎉 완료: 두 로컬 저장소와 GitHub 원격 저장소의 상태가 모두 일치함
