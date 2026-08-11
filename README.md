# 2026-git-start

*시퀀스 다이어그램
    두 작업자(A, B)가 동일한 파일의 같은 줄을 수정했을 때 발생하는 Git 충돌 과정과 해결 절차 나타냄

*흐름
-동일 문서 시작: 작업자 A, B가 같은 내용의 README.md를 가지고 시작

-작업자 A 푸시: A가 먼저 문서를 수정하여 GitHub 원격 저장소에 Push 성공

-작업자 B 거절: B가 같은 줄을 수정 후 Push 시도하나, 최신 상태가 아니므로 거절 발생

-충돌 및 해결: B가 원격 내역을 가져와 병합 시도 중 충돌(Conflict) 발생, 수동 수정 후 커밋

-최종 반영: 충돌을 해결한 B가 GitHub에 Push 완료

-상태 동기화: A가 병합된 최신 내역을 가져와 동기화함으로써 두 작업자 모두 동일한 상태 완료

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
