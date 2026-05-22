# Gemini CLI - 업무 말투 변환기 프로젝트 지침

이 파일은 **업무 말투 변환기** 프로젝트를 위한 Gemini CLI 전용 개발 및 협업 지침입니다. 프로젝트의 아키텍처, 기술 스택, 개발 원칙 및 워크플로우를 정의합니다.

---

## 1. 프로젝트 개요 (Project Overview)

- **목적**: 사용자의 일상적인 말투를 수신 대상(상사, 동료, 고객 등)에 적합한 비즈니스 언어로 변환하는 AI 서비스.
- **철학**: "바이브 코딩(Vibe Coding)" 원칙에 기반하여, AI를 활용해 빠르게 작동하는 프로토타입을 제작하고 배포하는 것을 목표로 합니다.
- **핵심 아키텍처**:
  - **Frontend**: Vanilla HTML/CSS/JS (프레임워크 없음)
  - **Backend**: Python FastAPI
  - **AI Model**: Upstage Solar-Pro2 (via LangChain)

---

## 2. 기술 스택 (Tech Stack)

### 2.1. Backend
- **Language**: Python 3.11+
- **Framework**: FastAPI
- **Library**: 
  - `langchain`, `langchain-upstage` (AI 연동)
  - `python-dotenv` (환경 변수 관리)
  - `pydantic` (데이터 스키마)
  - `uvicorn` (ASGI 서버)

### 2.2. Frontend
- **HTML5 / CSS3 / JavaScript (ES6+)**
- 별도의 프론트엔드 프레임워크나 번들러 없이 브라우저 네이티브 기술 사용.

### 2.3. DevOps & Tooling
- **Package Manager**: `uv` (가상환경은 `.venv` 사용)
- **Deployment**: Vercel (Front + Back 통합 배포)
- **Version Control**: Git / GitHub

---

## 3. 개발 원칙 (Development Principles)

이 프로젝트는 **PRD**에 명시된 "바이브 코딩 3원칙"을 엄격히 준수합니다.

### 원칙 1. 완료 기준을 먼저 정의하라
- 모든 기능 구현 전, 무엇이 완성인지 체크리스트를 먼저 확인하거나 작성합니다.
- 불필요한 기능 확장을 지양합니다.

### 원칙 2. 조사 먼저, 구현 나중
- 외부 API(Upstage 등) 연동이나 새로운 라이브러리 도입 시, 구현 코드를 작성하기 전에 최신 문서와 연동 방식을 먼저 확인합니다.

### 원칙 3. 버그는 분석 먼저, 수정 나중
- 에러 발생 시 즉각적인 코드 수정 대신, 에러의 근본 원인을 먼저 분석하고 사용자에게 설명합니다.

---

## 4. 핵심 디렉토리 구조 (Directory Structure)

```
/
├── backend/                # FastAPI 서버 코드
│   ├── main.py             # 앱 진입점 및 CORS 설정
│   ├── routers/            # API 라우터 (convert.py 등)
│   ├── services/           # 비즈니스 로직 (tone_converter.py)
│   ├── prompts/            # 대상별 프롬프트 템플릿 (templates.py)
│   ├── models/             # Pydantic 스키마 (schemas.py)
│   └── requirements.txt    # 의존성 목록
├── frontend/               # 정적 파일
│   ├── index.html          # 메인 화면
│   ├── css/                # 스타일시트
│   └── js/                 # 클라이언트 로직 (app.js)
├── .env                    # 민감 정보 (UPSTAGE_API_KEY 등) - GIT 제외
├── .gitignore              # Git 무시 목록
├── PRD_업무말투변환기.md   # 상세 기획 및 요구사항
└── 개요서_업무말투변환기.md # 프로그램 개요
```

---

## 5. 실행 및 테스트 (Running & Testing)

### 5.1. 환경 설정
```bash
# uv를 사용한 가상환경 생성 및 의존성 설치
uv venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r backend/requirements.txt
```

### 5.2. 백엔드 실행
```bash
cd backend
uvicorn main:app --reload --port 8000
```

### 5.3. 프론트엔드 확인
- `frontend/index.html`은 `http://localhost:8000` 으로 확인합니다. 
---

## 6. 보안 및 금지 사항 (Security & Restrictions)

- **API 키 보호**: `.env` 파일에 저장된 `UPSTAGE_API_KEY` 등이 코드에 노출되거나 커밋되지 않도록 주의합니다.
- **Git 조작**: `my-rules.md`에 명시된 Git 관련 금지 작업(강제 푸시, 히스토리 파괴 등)을 절대 수행하지 않습니다.
- **응답 언어**: 모든 설명과 주석은 **한국어**로 작성합니다.

---
### @PRD_업무말투변환기.md 문서와 GEMINI.md 문서 항상 최신화 하기
* 모든 변경사항이 발생하면 (예를 들어 Source Code가 변경 되거나 라이브러리 버전이 변경되면) md 문서도 반드시 업데이트 합니다. 
* 구현이 완료된 사항들은 `2. 완료 체크리스트`에 모두 체크표시를 해서 완료 되었음을 반드시 표시하세요.
* `8. 단계별 구현 순서` 에서도 STEP별로 구현이 완료되면 체크표시를 해서 완료 되었음을 반드시 표시하세요.



> 📌 **참고**: 상세한 기능 요구사항 및 프롬프트 전략은 `PRD_업무말투변환기.md` 문서를 최우선으로 참고하십시오.
