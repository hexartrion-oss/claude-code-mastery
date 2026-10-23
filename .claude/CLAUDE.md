# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

이 프로젝트는 **초보자 대상의 프론트엔드 학습 프로젝트**입니다. 순수 HTML, CSS, JavaScript를 사용하여 계산기를 만드는 과정을 통해 웹 개발의 기초를 학습합니다.

### 핵심 특징
- **언어**: 한국어 (모든 설명, 주석, 커뮤니케이션은 한국어로)
- **출력 스타일**: "Beginner Friendly" (자세한 설명과 한글 주석)
- **설계**: 모던 다크 테마 + 네온 그린 액센트 (#CAFF00)
- **타겟**: 프론트엔드 초보자

## 프로젝트 구조

```
.
├── calculator.html          # 계산기 메인 파일 (HTML + CSS + JavaScript 통합)
├── .claude/
│   ├── settings.json        # Claude Code 설정 (출력 스타일, 권한)
│   ├── md/                  # 문서/가이드
│   └── output-styles/       # 커스텀 출력 스타일 정의
└── .git/                    # Git 저장소
```

## 파일별 설명

### calculator.html
계산기 프로젝트의 전체 구현 파일입니다.

**HTML 부분** (라인 1-150)
- `<div class="calculator">`: 계산기 전체 컨테이너
- `<div class="display">`: 숫자 표시 영역
- `<div class="buttons">`: 버튼 그리드 (4열 레이아웃)

**CSS 부분** (라인 7-149)
- **색상 체계**: 
  - 배경: 짙은 파란색 (#1a1f3a)
  - 액센트: 네온 그린 (#CAFF00)
  - 에러: 레드 (#d32f2f)
- **반응형 설계**: `grid-template-columns: repeat(4, 1fr)` 사용
- **호버 효과**: 모든 버튼에 `box-shadow`와 `transform` 애니메이션

**JavaScript 부분** (라인 182-213)
- **변수**:
  - `currentInput`: 현재 입력된 숫자
  - `previousInput`: 이전 숫자
  - `operator`: 선택된 연산자 (+, -, *, /)

- **구현 필요 함수** (TODO):
  - `appendNumber(num)`: 숫자 버튼 클릭 처리
  - `appendOperator(op)`: 연산자 버튼 클릭 처리
  - `calculate()`: 계산 실행

- **구현 완료 함수**:
  - `clearDisplay()`: 전체 초기화 (라인 203-207)
  - `deleteLast()`: 마지막 숫자 삭제 (라인 210-212)

## 개발 가이드

### 계산기 로직 구현 시 고려사항

#### `appendNumber(num)` 함수
- **역할**: 숫자 또는 소수점 입력 처리
- **고려사항**:
  - 소수점 중복 방지 (한 번만 입력 가능)
  - 0 앞에 0 방지 (단, 0.5 같은 형식은 가능)
  - display 업데이트
  
#### `appendOperator(op)` 함수
- **역할**: 연산자(+, -, ×, ÷) 처리
- **고려사항**:
  - 이전 계산이 있으면 먼저 실행
  - 새로운 연산자 설정
  - currentInput을 previousInput으로 이동

#### `calculate()` 함수
- **역할**: 최종 계산 실행
- **고려사항**:
  - 나누기 0 방지
  - 연산자가 없는 경우 처리
  - 결과를 currentInput에 저장

### 디자인 시스템

**색상 팔레트** (수정 금지 - 프로젝트 정체성)
- 주 배경: `#1a1f3a` (짙은 파란)
- 보조 배경: `#0a0e27` (더 어두운 파란)
- 액센트: `#CAFF00` (네온 그린)
- 버튼 배경: `#2a2f4a` (중간 파란)
- 호버 시: `#3a3f5a` (밝은 파란)
- 에러/초기화: `#d32f2f` (레드)

**버튼 스타일링**
- 모든 버튼: `border-radius: 10px`, `padding: 15px`
- 숫자/소수점 버튼: 테두리 있음, 호버 시 글로우 효과
- 연산자 버튼: 네온 그린, 호버 시 확대
- 등호 버튼: 네온 그린, 2칸 너비
- 초기화 버튼: 레드, 2칸 너비

### 기본 작업 흐름

#### 계산기 테스트
```
브라우저에서 calculator.html 열기 → 숫자와 연산자 입력 → 결과 확인
```

#### 버그 수정 시
1. 어떤 기능이 제대로 작동하지 않는지 확인
2. JavaScript 로직 검토 (appendNumber, appendOperator, calculate)
3. CSS 스타일 확인 (필요시)
4. 테스트 후 커밋

#### 새 기능 추가 시
예시: 제곱근, 백분율 등
1. HTML에 새 버튼 추가
2. CSS에 스타일 추가
3. JavaScript에 처리 로직 추가
4. 테스트

## 커뮤니케이션 스타일

### 출력 스타일: "Beginner Friendly"
- 모든 설명은 **한국어**로 작성
- 코드는 **한줄씩 자세히** 설명
- 어려운 용어는 **쉽게 풀어서** 설명
- **비유**를 많이 사용하여 이해하기 쉽게
- 예제 코드에는 **한글 주석을 충분히** 추가
- **HTML 구조부터** 설명한 후 JavaScript 로직 설명

### 주석 작성 규칙
```javascript
// ✓ 좋은 예: 왜 이렇게 하는지 명확
// 소수점이 이미 있으면 추가하지 않음
if (currentInput.includes('.')) return;

// ✗ 나쁜 예: 뻔한 설명
// 점을 추가
currentInput += '.';
```

## 권한 설정

현재 활성화된 권한:
- ✅ Bash (쉘 명령 실행)

필요시 요청하여 추가 권한 활성화 가능

## 관련 메모리

- `user_profile.md`: 사용자 프로필 (한국어 커뮤니케이션, 프론트엔드 학습 중)
- `design_direction.md`: 디자인 방향 (모던 다크 + 네온 그린 #CAFF00)

## Git 규칙

- **커밋 메시지**: 한국어로 작성하되, 간결하게
- **브랜치**: main 브랜치에서 작업
- **예시**:
  ```
  계산기 appendNumber 함수 구현
  계산기 버그 수정: 소수점 중복 입력 방지
  ```


## 코드 스타일
- 들여쓰기 : 스페이스 2칸
- 세미콜론 사용하지 않음
- 작은 따옴표 사용('')

# Git 규칙
- 커밋 메시지는 한글로 사용
- 브렌치 명 : feature/기능명, fix/버그명
- 커밋은 작은 단위로 나눠서

# 작업 방식
- 파일 수정 전 변경 계획을 먼저 설명
- 한번에 너무 많은 파일을 수정하지 말 것

# 내 개발 환경
- OS : windows 11
---

**마지막 업데이트**: 2026-10-23
