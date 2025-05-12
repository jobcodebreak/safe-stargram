# Safe-Stargram

Safe-Stargram 프로젝트의 컨벤션 및 기획을 정리한 문서입니다.

## 개발 방향

- 폴더구조:

  MVP를 만들고 그 후 기능 확장을 하는 방식이라, 어떤 기능이 필요할지 알 수 없습니다. FSD를 간단하게 도입하였습니다.

- 이슈 [많은 데이터를 처리하면서 사용자 경험 높이기]

## Stack

- FrontEnd
  - React, JS+SWC, Vite 를 사용하여 개발환경 세팅
  - style : Styled-components
- BackEnd
  - Serverless (Firebase)

## 폴더 구조

본 프로젝트는 MVP 개발과 이후 확장성을 고려하여 **Feature-Sliced Design (FSD)** 개념을 조합하였습니다.

### 기본 폴더 설명

- `/shared`  
  프로젝트 전체에서 재사용하는 **기본 컴포넌트, 훅, 유틸리티**를 관리합니다.

  - `ui`: 공통 UI 컴포넌트
  - `hooks`: 공통 Custom Hook
  - `utils`: 공통 함수
  - `lib`: 기타 라이브러리 로직
  - `config`: 설정 파일
  - `types`: 공통 타입 정의

- `/features`  
  **기능 단위로** 코드(컴포넌트, API, 상태관리 등)를 그룹핑합니다.

  - 예) 로그인 기능: `/features/auth`
  - 예) 상품 기능: `/features/product`

- `/pages`  
  **라우팅 단위** 화면을 구성합니다.  

- `/app`  
  프로젝트 **초기 세팅** 파일을 관리합니다.  
  (ex. 글로벌 상태 프로바이더, 라우터 설정 등)

### 설계 원칙

- **공통은 shared**, **기능별은 features**에 위치합니다.
- **컴포넌트는 작은 단위로 만들고** 필요한 경우 조합하여 사용합니다.
- **API 통신, 상태관리, 타입**은 기능별 디렉토리 안에 함께 관리합니다.
- **필요할 때만** entities, widgets, processes 구조를 추가하여 확장할 수 있습니다.

### 인수인계 참고사항

- 기능 개발 시, **features 하위에 디렉토리를 새로 만들고** 그 안에 컴포넌트, 모델, API를 작성합니다.
- 공통적으로 재사용되는 요소는 shared에 추가합니다.
- pages 폴더는 라우팅 전용입니다. UI 로직은 features나 shared에서 관리합니다.

## Convention

프로젝트 참여 방식은 언제 누구든 와서 자신이 기여할 수 있는 부분에 대해 참여할 수 있다는 것입니다. 그래서 초기 컨벤션 설정이 중요하다고 생각했습니다.

### 커밋

- prefix [add, update, fix, remove, docs]를 붙여 한글로 커밋합니다.
  - add: 세팅 추가, 코드 추가 등
  - update: 기존 함수 내부 로직 변경 등
  - fix: 이슈 해결
  - remove: 폴더, 파일, 코드 제거
  - docs: 주석 혹은 문서 추가
  - ex) `add: 개발환경 세팅`

### 코드

- 변수명, 함수명은 카멜케이스 사용
- 이름만 읽고 어떤 값을 가지는지, 어떻게 변경되는지, 무엇을 하는지 등을 알 수 있어야 함.
  ex) isOpen -> isOpenMainList, handleClickButton -> handleClickButtonToSwitchCurrentSensor
- prefix
  - bool: is-, has-
  - event handler: handle{Event}-
  - function() => bool: check-

### changelog

- 각 폴더 하위에 변경기록을 확인하여 개발 진행도를 바로 알 수 있도록 하려 합니다.
- 개발 시작 전 예상 커밋 메세지들을 투두리스트로 적어놓고 시작합니다.
- **짧고 명확하게 한 줄**로 작성합니다.

1. 매일 작업 시작 시

- 오늘 작업할 계획을 체크박스 형식으로 작성합니다.

  예시:

  - [ ] add: 로그인 폼 컴포넌트 추가
  - [ ] update: 로그인 폼 유효성 검사 수정
  - [ ] fix: 로그인 버튼 클릭 시 오류 수정

2. 작업 중 이슈 발생 시

- 계획에 없던 작업은 아래 "추가 작업" 섹션에 `[ISSUE]`, `[HOTFIX]`를 붙여 작성합니다.

  예시:

  - [ ] [ISSUE] 로그인 리다이렉트 실패 수정
  - [ ] [HOTFIX] 긴급: 로그인 실패 시 에러 메시지 표시

3. 작업 완료 시

- 완료된 항목은 `[ ]` → `[x]`로 체크합니다.

  예시:

  - [x] add: 로그인 폼 컴포넌트 추가

#### changelog 템플릿

```md
# 2025-05-10

## 작업 목록

- [ ] add: 로그인 폼 컴포넌트 추가
- [ ] update: 로그인 폼 유효성 검사 수정
- [ ] fix: 로그인 버튼 클릭 오류 수정

## 추가 작업 (이슈 발생 시 기록)

- [ ] [ISSUE] fix: 로그인 완료 후 상태 초기화 문제 수정
- [ ] [HOTFIX] fix: 로그인 실패 에러메시지 표시 오류 수정
```
