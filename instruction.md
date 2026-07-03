# 개발 진행 과정 (Instruction)

이 문서는 `Calc` 계산기 프로젝트가 어떻게 만들어지고 발전해왔는지, 주요 흐름을 시간 순서대로 정리한 기록입니다.

## 1. 계산기 최초 제작
- 사칙연산(+, −, ×, ÷)과 메모리 기능(MC/MR/M+/M-)을 갖춘 계산기를 단일 HTML 파일(`index.html`)로 제작
- 부호 전환(±), 백분율(%) 등 보조 기능 포함
- 키보드 기본 입력(숫자, 연산자, Enter, Backspace, Escape) 반영

## 2. 메모리 내역 기능 개선
- 요청: "메모리 기능에 있어, 처음부터 입력했던 사항이 다 보일 수 있도록 수정"
- M+/M- 조작 시점의 값과 누적 합계를 기록하는 `memoryLog` 배열 추가
- 계산기 상단에 "메모리 내역 ▾" 토글을 두어 클릭하면 지금까지의 모든 메모리 변경 내역을 리스트로 확인 가능하도록 구현
- MC(메모리 초기화) 시 내역도 함께 초기화

## 3. GitHub 저장소 생성 및 업로드
- GitHub 계정 `hakim00`으로 public 저장소 [`Calc`](https://github.com/hakim00/Calc) 생성
- 로컬에 git이 설치되어 있지 않아, GitHub REST API(Contents API)를 통해 `index.html`을 직접 업로드

## 4. 키보드 지원 강화 - Issue → PR → Merge
1. **Issue #1** 생성: "키보드 입력으로 계산기 동작 지원"
   - 마우스 없이 모든 기능(사칙연산 + 메모리)을 키보드만으로 조작할 수 있어야 한다는 요구사항을 체크리스트로 정리
   - 담당자로 `hakim00`과 `Copilot`을 assign
2. **Copilot이 Issue #1을 처리**하여 **PR #2** 생성
   - 신규 키보드 단축키 추가: `%`(백분율), `Ctrl+M`(M+), `Ctrl+Shift+M`(M-), `Ctrl+R`(MR), `Alt+M`(MC)
   - 키 입력 시 해당 버튼에 시각적 플래시 피드백(`key-active` 클래스) 추가
   - 버튼에 `title` 속성으로 단축키 툴팁 안내
3. PR #2를 draft → ready 전환 후 **squash merge**, 브랜치 삭제
   - merge와 동시에 연결된 Issue #1 자동 종료(closed)

## 5. 라이트/다크 테마 토글 추가
- 요청: "밝은톤과 흑백톤을 변경할 수 있는 토글 버튼 추가"
- 새 브랜치 `feature/theme-toggle`에서 작업
  - 계산기 헤더에 `☀️ 라이트` / `🌙 다크` 토글 버튼 추가
  - 클릭 시 `data-theme` 속성을 즉시 전환하고 `localStorage`에 저장하여 다음 방문 시에도 선택한 테마 유지
  - 기존 시스템 다크모드 자동 감지보다 사용자가 직접 선택한 테마를 우선 적용
- **PR #3** 생성 후 **squash merge**로 `main`에 반영, 브랜치 삭제

## 6. README 작성
- 계산기의 주요 기능(사칙연산, 메모리, 키보드 단축키, 테마 전환)을 정리한 `README.md`를 작성해 `main`에 반영

## 전체 흐름 요약

```
계산기 제작 (사칙연산 + 메모리)
        │
메모리 내역 조회 기능 개선
        │
GitHub 저장소(Calc) 생성 및 최초 업로드
        │
Issue #1 등록 (키보드 지원 요구사항 정리, Copilot assign)
        │
Copilot이 PR #2 생성 (키보드 단축키 구현)
        │
PR #2 merge → Issue #1 자동 종료
        │
테마 토글 기능 개발 (브랜치: feature/theme-toggle)
        │
PR #3 생성 → merge → 브랜치 삭제
        │
README.md 작성 및 반영
        │
instruction.md 작성 (본 문서)
```

## 관련 링크
- 저장소: https://github.com/hakim00/Calc
- Issue #1: https://github.com/hakim00/Calc/issues/1
- PR #2 (키보드 지원): https://github.com/hakim00/Calc/pull/2
- PR #3 (테마 토글): https://github.com/hakim00/Calc/pull/3
