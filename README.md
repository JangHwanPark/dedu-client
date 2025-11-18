## D`Edu 프로젝트 소개
2025년 9월 3일 팀에 중간 합류하여 학습 플랫폼 프론트엔드를 도메인 중심 구조(FSD/DDD-lite)로 재정비하고 BFF 기반 통신 구조를 구축, 스터디룸/노트 등 핵심 기능 플로우를 설계 및 구현한 프로젝트입니다.

기존 산재된 코드베이스를 재구조화하면서 퍼포먼스, 유지보수성, 협업 효율을 모두 개선하는 방향으로 아키텍처 전반을 다듬는 역할을 수행했습니다.

<br/>

## 참고
이 저장소는 원본 프로젝트를 기반으로 재정리한 코드로 일부 구조나 플로우가 실제 서비스 리포(Main Repo)와 다를 수 있습니다.

또한 도메인 구조, BFF 핸들러, 플로우 연결, 컴포넌트 구성 등은 ongoing 작업으로 지속적으로 업데이트될 예정입니다.

현재는 제가 작업을 진행하는 동안에 한해 업데이트가 이루어지며 프로젝트 종료 또는 제가 더 이상 참여하지 않는 경우 업데이트가 중단될 수 있습니다.

<br/>

## 기여 내용(Contribution Overview)
본 프로젝트에서 프론트엔드 영역 전반을 담당하며 다음과 같은 기능 개선 및 구현 작업을 진행했습니다.

### FSD(Folder-Slice-Domain) 구조 재정립
- 기존 산재된 파일/코드를 도메인 단위로 재정렬하고,
- api / hooks / components / types / constants 구조를 재정리
- 유지보수성 향상 및 신규 기능 추가 시 개발 속도 향상

### BFF(Route Handler) 기반 API 통신 구조 구축
- Next.js Route Handler를 이용한 BFF 계층 구성
- 클라이언트 직통 API 호출을 제거하고, 인증/에러 처리 로직을 중앙집중화
- API 응답 스키마 통일 및 안정성 강화

### StudyRoom / StudyNote 플로우 개발
- 대시보드 → 스터디룸 선택 → 상세 뷰 → 노트 흐름 전체 구현
- 검색, 필터, 정렬, 페이징 등 UI/데이터 연동 작업
- 도메인 단위 컴포넌트 정립 및 재사용성 개선

### 권한 기반 UI 설계(Role-Based UI)
- 보호자 / 학생 / 선생님 / 관리자 케이스에 따라 접근 가능한 화면과 액션을 분리
- UI 레벨에서의 접근 제한 + 서버 검증 이중 구조 정립

### 컴포넌트/패턴 정립
- 공통 UI 컴포넌트 정리 및 컴포즈 패턴 일부 적용
- 복잡한 페이지는 Container/Presenter 구조 확립
- 정렬/필터/SearchBar 등 기능성 컴포넌트 모듈화

### 팀 협업 템플릿화
- Git 브랜치 전략, PR 템플릿, 커밋 컨벤션 정리
- 스터디룸/노트 기획 플로우를 문서화하여 디자이너, 백엔드와의 협업 효율 개선

<br/>

## 기술 스택(Tech Stack)
- Framework: Next.js 14 (App Router)
- Language: TypeScript
- Styling: TailwindCSS
- Data Fetching: React Query
- State Management: Context + Reducer (도메인 단위 적용)
- API Layer: Next.js Route Handler 기반 BFF
- Validation: Zod
- Build/Deploy: Vercel

<br/>

## 폴더 구조 예시(Folder Structure)
```text
src/
├── app/                      # Next.js App Router
│   └── api/v1/<domain>/      # BFF(Route Handler)
│
├── entities/                 # Domain Layer
│   └── <domain>/
│       ├── core/             # Domain 핵심 로직
│       │   ├── <domain>.domain.schema.ts
│       │   ├── <domain>.factory.ts
│       │   └── index.ts
│       │
│       └── infrastructure/   # Domain ↔ 외부계층 연결
│           ├── <domain>.dto.schema.ts
│           ├── <domain>.api.repository.ts
│           ├── <domain>.adapters.ts
│           ├── <domain>.keys.ts
│           ├── types/
│           │   ├── <domain>.types.ts
│           │   └── index.ts
│           └── index.ts
│
├── features/                 # 기능 구현(UI + 비즈니스 로직)
│   └── <domain>/
│       ├── api/              # queryFn, queryKeys, options
│       ├── components/       # Domain UI
│       ├── hooks/            # useQuery/useMutation 래퍼
│       └── services/         # Feature-level 비즈니스 로직(선택)
│
├── shared/                   # 공통 모듈
│   ├── ui/
│   ├── lib/
│   ├── hooks/
│   └── store/
│
└── styles/
```