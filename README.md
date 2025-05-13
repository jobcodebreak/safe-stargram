# Safe-Stargram

Safe-Stargram 프로젝트의 컨벤션 및 기획을 정리한 문서입니다.

## 개발 방향

- 폴더구조:

  MVP를 만들고 그 후 기능 확장을 하는 방식이라, 어떤 기능이 필요할지 알 수 없습니다. FSD를 간단하게 도입하였습니다.

- 이슈 [많은 데이터를 처리하면서 사용자 경험 높이기]

## Stack

- FrontEnd
  - React, JS+SWC, Vite 를 사용하여 개발환경 세팅
  - Routing : React-router v6 이상
  - style : Styled-components
- BackEnd
  - Serverless (Firebase)
  - PWA와 Service Worker를 통해 사용자 친화적 UX개선과 Web Push 기능 구현

## 폴더 구조

본 프로젝트는 MVP 개발과 이후 확장성을 고려하여 **Feature-Sliced Design (FSD)** 개념을 조합하였습니다.

### 기본 폴더 설명
- `/app`

  프로젝트 초기 세팅 파일을 관리합니다.

- `/features`  
  **기능 단위로** 코드(컴포넌트 등)를 그룹핑합니다. 재사용하는 **기본 컴포넌트**를 관리합니다.
  - 예) 유저정보변경 기능: `/features/EditProfile.jsx`
  - 예) 상품 기능: `/features/Product.jsx`
  - 예) 특정 도메인 또는 기능에 관련된 hook `/features/auth/useAuth.jsx

- `/pages`  
  **라우팅 단위** 화면을 구성합니다.  

- `/shared`
  전역적으로 재상용 되는 것들 (예: 범용 hook, API, 버튼, 테마, 헬퍼 함수 등)을 정의합니다.
  - 버튼 : `/ui/Button/

- `/store`  
  **스토어**를 관리합니다.

```text
// 프로젝트 예시 FSD파일구조
src/
├── app/                       # 앱 초기화 및 전역 설정
│   ├── App.tsx
│   ├── index.tsx
│   ├── providers/             # context, store provider 등
│   ├── router/                # react-router-dom 설정
│   └── config/                # 전역 설정 (API baseURL, feature flags 등)
│
├── pages/                     # 라우트 기준 화면
│   ├── HomePage/
│   │   ├── ui/                # 페이지 UI 구성
│   │   └── model/             # 페이지 내부 상태
│   └── ProfilePage/
│
├── features/                  # 사용자 중심의 기능 단위
│   ├── editProfile/
│   └── likePost/
│
├── shared/                    # 범용 컴포넌트, 유틸 등
│   ├── ui/                    # 버튼, 모달 등 디자인 시스템
│   │   ├── Button/
│   │   ├── Input/
│   │   └── Modal/
│   ├── lib/                   # 범용 훅, 함수 등
│   │   ├── hooks/
│   ├── api/                   # axios 인스턴스, 공통 API 설정
│   └── config/                # 글로벌 상수, 환경 설정
│
└── store/                     # 스토어 관리
```

### 설계 원칙

- **공통은 shared**, **기능별은 features**에 위치합니다.
- **컴포넌트는 작은 단위로 만들고** 필요한 경우 조합하여 사용합니다.
- **API 통신**은 Shard 디렉토리 안에 함께 관리합니다.
- **상태관리**는 Store에 따로 관리합니다.
- **Custom Hook**은 **전역적**으로 사용되는 것인지, 특정 **기능**에 관련된 것인지 용도에 따라 shared와 features에 관리합니다.


### 인수인계 참고사항

- 기능 개발 시, **features 하위에 디렉토리를 새로 만들고** 그 안에 컴포넌트, 모델, 훅 등을 작성합니다.
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
