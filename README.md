
# 🎨 AI 브랜드 아이덴티티 생성기

> 브랜드 브리프(JSON) 하나로 **네이밍·슬로건·스토리·컬러 팔레트·로고 시안**까지 자동 생성하는 CLI 프로그램

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Groq](https://img.shields.io/badge/LLM-Groq-orange)
![HuggingFace](https://img.shields.io/badge/Image-HuggingFace-yellow)

---

## 1. 🎯 미션 소개

브랜드 디자인은 네이밍, 슬로건, 스토리, 컬러, 로고 등 다양한 요소를 종합적으로 기획해야 하는 전문 작업입니다. 외주 비용이 수백만 원에서 시작하는 이유도 시간과 전문성을 요구하기 때문입니다.

이 프로젝트는 **브랜드 브리프(업종, 타겟, 키워드 등)를 입력하면 AI가 브랜드 요소를 자동 생성**하는 CLI 프로그램입니다.

- **LLM API(Groq)** → 텍스트 브랜드 요소 생성 (네이밍, 슬로건, 스토리, 컬러)
- **이미지 생성 API(HuggingFace)** → 로고 시안 생성
- 모든 결과물을 폴더에 저장

---

## 2. 📦 최종 결과물

CLI 기반 Python 프로그램 1개로 아래 기능을 모두 구현했습니다.

| 기능 | 구현 내용 |
|------|-----------|
| **브랜드 브리프** | JSON 파일로 브랜드 정보 입력 |
| **브랜드 요소 생성** | 네이밍 3개(+의미), 슬로건 3개, 스토리(300자), 컬러 팔레트 |
| **로고 시안 생성** | 이미지 생성 API로 로고 2~3개 PNG 저장 |
| **결과 저장** | 텍스트 → JSON, 컬러 팔레트 → PNG, 로고 → PNG |

---

## 3. 🖼️ 결과물 예시

**입력 브랜드**: 인스타 감성 카페 `코지그램` ☕

컬러 팔레트

<img width="921" height="331" alt="image" src="https://github.com/user-attachments/assets/78aa4ddf-573f-4c58-b499-1552d1264b0c" />

로고 시안

<img width="338" height="294" alt="image" src="https://github.com/user-attachments/assets/23b8ec46-459b-4274-9267-f8b77a4447c8" />
<img width="241" height="208" alt="image" src="https://github.com/user-attachments/assets/4956810b-3820-4e67-bfd1-0eea299f6ebe" />


* 로고를 3개 만들도록 프롬프트를 설개했으나 완성하는 도중 무료토큰의 소진으로 두 개 밖에 만들지 못했습니다.
* 로고 생성 중 만들었던 네이밍과 다른 글자가 로고에 첨부되는 일이 발생하여 프롬프트에 no word를 추가했습니다.


- **메인 컬러**: `#F7D2C4`
- **서브 컬러**: `#964B00`, `#C9E4CA`, `#FFC5C5`

---

## 4. ⚙️ 개발 환경

- **Python 3.10+**
- **Groq API** – 텍스트 생성 (LLM)
- **HuggingFace InferenceClient** – 이미지 생성 (FLUX 모델)

---

## 5. 📂 폴더 구조

```
brand_generator/
├── brand_generator.py     # 메인 프로그램
├── brief.json             # 브랜드 브리프 입력 파일
├── check_models.py        # 사용 가능 모델 확인용
├── requirements.txt       # 의존성 목록
├── .env                   # API 키 (git 미포함)
├── .gitignore             # 제외 파일 목록
└── output/                # 결과물 저장 폴더
    ├── brand_result.json  # 전체 텍스트 결과
    ├── color_palette.png  # 컬러 팔레트 시각화
    ├── logo_1.png         # 로고 시안 1
    └── logo_2.png         # 로고 시안 2
    
```

---

## 6. 🚀 설치 및 실행

### 1) 저장소
```bash
[brand_generator](https://github.com/SonJH0/brand_generator)
```

### 2) 의존성 설치
```bash
pip install -r requirements.txt
```

### 3) API 키 설정 (`.env` 파일 생성)
```env
GROQ_API_KEY=your_groq_api_key
HF_TOKEN=your_huggingface_token
```

### 4) 실행
```bash
python brand_generator.py
```

---

## 7. 📥 입력 예시 (`brief.json`)

```json
{
  "industry": "카페",
  "target": "20-30대 인스타 감성 고객",
  "keywords": ["따뜻함", "세련됨", "트렌디", "편안함"],
  "tone": "감성적이고 세련된",
  "competitors": ["스타벅스", "투썸플레이스"],
  "notes": "인스타그램에 어울리는 미니멀한 브랜드"
}
```

| 구분 | 필드 |
|------|------|
| **필수** | `industry`(업종), `target`(타겟), `keywords`(키워드) |
| **선택** | `tone`(톤앤매너), `competitors`(경쟁사), `notes`(추가 요청) |

---

## 8. 💻 실행 예시

<img width="774" height="805" alt="image" src="https://github.com/user-attachments/assets/e43bbaa4-bba7-4b5e-a83c-b187dfc489ad" />


---

## 9. 🔄 처리 파이프라인

```
[1] brief.json 로드
      ↓
[2] 브랜드 네이밍 생성 (Groq LLM)
      ↓
[3] 슬로건 생성 (Groq LLM)
      ↓
[4] 브랜드 스토리 생성 (Groq LLM)
      ↓
[5] 컬러 팔레트 생성 (Groq LLM) → matplotlib 시각화
      ↓
[6] 로고 시안 생성 (HuggingFace) → PNG 저장
      ↓
[7] brand_result.json 저장
```

---

## 10. ✅ 요구사항 대비 완료 현황

| 요구사항 | 완료 | 설명 |
|----------|:----:|------|
| 사용자 입력 (print/input 대화형) | ✅ | 브리프 경로 필수, 출력 폴더 선택(기본 `./output`) |
| 브랜드 브리프 입력 (JSON) | ✅ | 필수/선택 필드 파싱 |
| 브랜드 네이밍 생성 (3~5개+의미) | ✅ | 4개 생성 |
| 슬로건 생성 (3개) | ✅ | 톤앤매너 반영 |
| 브랜드 스토리 (300자) | ✅ | 탄생 배경·철학·비전 포함 |
| 컬러 팔레트 (메인1+서브2~3) | ✅ | HEX 코드로 생성 |
| 컬러 팔레트 시각화 (PNG) | ✅ | matplotlib 저장 |
| 로고 시안 생성 (2~3개 PNG) | ✅ | HuggingFace로 2개 생성 |
| 결과 저장 (JSON+PNG) | ✅ | `brand_result.json` + 개별 PNG |
| 에러 처리 | ✅ | API 실패 시 다음 단계 계속 진행 |
| API 키 관리 | ✅ | `.env` 환경변수 사용 |
| **[보너스]** 경쟁사 분석 | ✅ | 차별화 포인트 제안 |

---

## 11. ⚠️ 에러 처리 전략

| 상황 | 대응 방법 |
|------|-----------|
| API 키 없음 | 명확한 안내 메시지 출력 후 종료 |
| API 호출 실패 | 에러 메시지 출력 후 **다음 단계 계속 진행** |
| 이미지 크레딧 소진(402) | 경고 출력, 이미 생성된 로고는 정상 저장 |

---

## 12. 📝 배운 점 (과제 목표 달성)

- ✅ 브랜드 브리프를 입력받아 AI로 브랜드 요소를 생성하는 **파이프라인**을 설계했다.
- ✅ **LLM API + 이미지 생성 API를 조합**하여 텍스트 + 이미지 결과물을 생성하는 방법을 익혔다.
- ✅ LLM이 추천한 HEX 코드를 **matplotlib로 시각화**하여 이미지로 저장하는 방법을 익혔다.
- ✅ API 호출 시 발생하는 **오류 상황과 대응 방법**(예외 처리, 키 관리)을 이해했다.
