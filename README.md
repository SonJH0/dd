# 🍽️ 오늘뭐먹지 (Oneul-Mwt-Mukji)

> AI가 당신의 기분과 상황에 맞는 메뉴를 추천해주는 웹 서비스

매일 반복되는 **"오늘 뭐 먹지?"** 고민!  
기분, 음식 종류, 인원만 선택하면  
AI가 딱 맞는 메뉴를 추천해드립니다. 🤖

<div align="center">

**🔗 배포 URL**

### [https://oneul-mwt-mukji.vercel.app](https://oneul-mwt-mukji.vercel.app)

전 세계 누구나 접속 가능합니다!

</div>

---

## 📋 목차

1. [서비스 기획](#-1-서비스-기획)
2. [주요 기능](#-2-주요-기능)
3. [기술 스택](#️-3-기술-스택)
4. [프로젝트 구조](#-4-프로젝트-구조)
5. [실행 방법](#-5-실행-방법)
6. [환경 변수 설정](#-6-환경-변수-설정)
7. [배포 방법](#-7-배포-방법)
8. [AI 기능 테스트](#-8-ai-기능-테스트)
9. [스크린샷](#-9-스크린샷)
10. [배운 점](#-10-배운-점)

---

## 🎯 1. 서비스 기획

### 서비스 개요
| 항목 | 내용 |
|------|------|
| **서비스명** | 오늘뭐먹지 |
| **타겟 사용자** | 매일 메뉴 고민이 귀찮은 직장인 및 학생 |
| **목표** | 간단한 선택만으로 AI 맞춤 메뉴 추천 제공 |

### 페이지 구성 (3개 이상)
🏠 메인 (index.html) → 서비스 소개 + Hero
🍽️ AI 추천 (recommend.html) → 핵심 AI 기능
❓ FAQ (faq.html) → 자주 묻는 질문

code
📋 복사
> 상단 네비게이션으로 모든 페이지 이동 가능

### AI 기능 설계
| 구분 | 내용 |
|------|------|
| **입력** | 기분 / 음식 종류 / 인원수 / 직접 입력 |
| **출력** | AI 분석 기반 맞춤 메뉴 추천 + 안내 문구 |
| **제공 가치** | 메뉴 선택 시간 절약 + 새로운 메뉴 발견 |

### 실패 처리 기준
| 상황 | 안내 메시지 |
|------|------------|
| **API 오류 (4xx/5xx)** | "😥 오류가 생겼어요. 다시 시도해주세요!" |
| **로딩 지연** | "😋 AI가 메뉴를 고민하는 중..." |

---

## ✨ 2. 주요 기능

| 기능 | 설명 |
|------|------|
| 🤖 **AI 메뉴 추천** | 기분/음식/인원 기반 맞춤 추천 (핵심 기능) |
| 🌙 **다크 모드** | 눈이 편한 야간 모드 (localStorage 저장) |
| 📱 **반응형 디자인** | 모바일/태블릿/PC 모두 최적화 |
| ❓ **FAQ** | 자주 묻는 질문 안내 |
| 🧭 **네비게이션** | 3개 페이지 자유 이동 |

---

## 🛠️ 3. 기술 스택

### Frontend (순수 바닐라)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JS](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

- **HTML5** : 페이지 구조 및 콘텐츠 마크업
- **CSS3** : 스타일링 + 반응형 (미디어쿼리) + 다크모드
- **JavaScript** : 사용자 입력 처리 + fetch 통신 + DOM 조작

> ⚠️ React/Vue 등 프레임워크 미사용 (순수 바닐라)

### Backend
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white)

- **Python** : Vercel Serverless Functions
- **Google Gemini API** : AI 메뉴 추천 (`gemini-2.0-flash`)

### 배포 & 협업
- **GitHub** : 코드 저장소 및 버전 관리
- **Vercel** : GitHub 연동 자동 배포

---

## 📁 4. 프로젝트 구조
oneul-mwt-mukji/
├── api/
│ └── recommend.py # AI 추천 백엔드 (Serverless Function)
├── public/
│ ├── css/
│ │ └── style.css # 전체 스타일 + 반응형 + 다크모드
│ ├── js/
│ │ ├── main.js # 다크모드 토글 기능
│ │ └── recommend.js # AI 요청 처리 (fetch)
│ ├── index.html # 메인 페이지
│ ├── recommend.html # AI 추천 페이지
│ └── faq.html # FAQ 페이지
├── .gitignore # 보안 파일 제외 (.env 등)
├── requirements.txt # Python 패키지 정의
├── vercel.json # Vercel 배포 설정
└── README.md # 프로젝트 문서



---

## 🚀 5. 실행 방법

### 1️⃣ 저장소 복제
```bash
git clone https://github.com/SonJH0/oneul-mwt-mukji.git
cd oneul-mwt-mukji
```

2️⃣ 패키지 설치
bash
📋 복사
pip install -r requirements.txt
3️⃣ 로컬 실행 (Vercel CLI)
bash
📋 복사
vercel dev
브라우저에서 http://localhost:3000 접속

🔐 6. 환경 변수 설정
⚠️ API 키는 절대 코드에 직접 입력하지 않습니다!
보안을 위해 반드시 환경 변수로 관리합니다.

필요한 환경 변수
변수명	설명
GEMINI_API_KEY	Google Gemini API 키
로컬 개발 시
프로젝트 루트에 .env 파일 생성:

GEMINI_API_KEY=여기에_본인_API_키_입력
Vercel 배포 시
Vercel 프로젝트 → Settings
Environment Variables 메뉴
GEMINI_API_KEY 추가 후 저장

🌐 7. 배포 방법
GitHub에 코드 push
Vercel과 GitHub 저장소 연동
Framework Preset: Other 선택
환경 변수 GEMINI_API_KEY 등록
Deploy 클릭 → 자동 배포 완료!
GitHub에 push할 때마다 Vercel이 자동으로 재배포합니다.

데이터 흐름 구조
code
📋 복사
[사용자 입력]
      ↓ (JavaScript)
[fetch("/api/recommend")]
      ↓ (POST 요청)
[Vercel Serverless Function - Python]
      ↓ (Gemini API 호출)
[AI 추천 결과 반환]
      ↓ (JSON 응답)
[화면에 결과 표시]
🧪 8. AI 기능 테스트
테스트 케이스	입력	결과
정상 입력	우울함 / 한식 / 2명	✅ 추천 결과 화면에 표시
로딩 중	요청 처리 대기	"😋 AI가 고민하는 중..." 표시
API 오류	서버 오류 발생 시	"😥 오류가 생겼어요" 안내 표시
📸 9. 스크린샷
💻 데스크톱 화면


📱 모바일 화면


🤖 AI 기능 동작 장면
