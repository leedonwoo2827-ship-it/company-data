# Company Data Manager - 전사 지식 활용 스킬

회사의 기존 자료(워드, 엑셀, PDF, SRT 등)에서 제안서 작성을 위한 소스 데이터를 관리하고 추출하는 Claude Desktop 스킬입니다.

## 주요 기능

- **지식 베이스 구축**: 다양한 포맷(HWPX, PDF, Excel, SRT)에서 핵심 내용을 분리하여 AI가 참조하기 쉬운 형태로 구조화
- **컨텍스트 매핑**: RFP의 요구사항마다 가장 적합한 과거의 성공 사례(Reference)와 현재의 기술 팩트(Raw Data)를 자동으로 매칭
- **참조 문서 관리**: 과거 합격 제안서, 우수 제안서의 톤앤매너, 논리 전개 방식 학습
- **원본 소스 추출**: 이력서, 기술 설명서, 실적 증명서, 회의록에서 구체적인 수치와 팩트 추출

## 데이터 분류

### 1. Reference Documents (참조 제안서)
- **대상**: 전년도 타사 합격 제안서, 우리 회사가 타 기관에 제출했던 우수 제안서
- **활용**: 업계 표준 톤앤매너, 논리 전개 방식, 디자인 레이아웃 및 설득 포인트 참조

### 2. Raw Data Resources (원본 소스)
- **대상**: 이번 사업에 직접 투입될 인력 이력서, 기술 설명서, 실적 증명서, 회의록(SRT)
- **활용**: 제안서에 포함될 구체적인 수치, 팩트, 최신 기술 스펙 등 '실측 데이터' 추출

## 설치 방법

### 방법 1: 드래그 앤 드롭 (권장)

1. 이 레포지토리를 클론하거나 ZIP으로 다운로드합니다:
   ```bash
   git clone https://github.com/leedonwoo2827-ship-it/company-data-manager.git
   ```

2. Claude Desktop을 실행합니다.

3. `company-data-manager` 폴더를 Claude Desktop 창에 드래그 앤 드롭합니다.

4. 스킬이 자동으로 설치되며, Claude가 사용 가능하다고 알려줍니다.

### 방법 2: 수동 설치

Claude Desktop의 Skills 디렉토리에 직접 복사:

**Windows:**
```bash
xcopy /E /I company-data-manager "%APPDATA%\Claude\skills\company-data-manager"
```

**macOS/Linux:**
```bash
cp -r company-data-manager ~/.config/Claude/skills/
```

## 사용 방법

### 기본 사용

Claude Desktop에서 자연스럽게 요청하세요:

```
"이 폴더에 있는 과거 제안서들을 분석해서 좋은 표현들을 정리해줘"
```

```
"이력서 파일에서 핵심 경력을 추출해줘"
```

```
"회의록 SRT 파일에서 주요 결정 사항을 뽑아줘"
```

### Claude Desktop 프로젝트에서 사용

`claude_desktop_config.json` 또는 프로젝트 지침에 다음을 추가:

```json
{
  "instructions": "회사 자료 분석이 필요할 때는 company_data 스킬을 사용하세요. Reference 데이터는 제안서의 '뼈대와 흐름'을, Raw 데이터는 '내용과 전문성'을 채우는 데 활용하세요."
}
```

### 통합 제안서 자동화 프로젝트에서 사용

이 스킬은 다음 워크플로우에서 2단계에 해당합니다:

1. **rfp-analyzer** - RFP 분석 및 구조 추출
2. **company-data-manager** (이 스킬) - 회사 자료 분석 및 매칭
3. **proposal-writer** - 제안서 초안 작성
4. **hwpx-writer** - HWPX 파일 생성
5. **text2img-mcp** - 이미지 생성

## 예제

### Reference 제안서 분석

```
사용자: 이 폴더에 있는 과거 합격 제안서들을 분석해줘
        [/references 폴더 공유]

Claude: Reference 제안서 분석을 시작합니다.

1단계: 파일 목록 확인 중...
- 2024_A기관_AI교육_합격본.pdf
- 2023_B기관_데이터분석_우수사례.hwpx

2단계: 핵심 표현 추출 중...
✓ 논리 전개 방식 학습 완료
✓ 설득 포인트 패턴 분석 완료

다음과 같은 효과적인 표현들을 발견했습니다:
- "실무 중심의 hands-on 교육..."
- "검증된 전문 강사진 구성..."
```

### Raw Data 추출

```
사용자: 회의록 SRT 파일에서 교육 내용을 추출해줘
        [meeting-notes.srt 업로드]

Claude: SRT 파일을 분석하여 교육 내용을 추출합니다.

추출된 핵심 내용:
- 1차시: AI 기초 개념 (2시간)
- 2차시: 머신러닝 실습 (3시간)
- 강사: 김OO 교수 (15년 경력)
- 실습 비율: 60%
```

## 활용 팁

### 1. 파일 조직화
- Reference와 Raw Data를 별도 폴더로 구분하면 더 효율적입니다
- 파일명에 날짜나 버전을 포함하면 관리가 쉽습니다

### 2. 데이터 품질
- 최신 자료일수록 참조 가치가 높습니다
- 합격한 제안서나 우수 평가를 받은 문서를 우선 활용하세요

### 3. 통합 활용
- RFP 분석 결과와 함께 사용하면 더 정확한 매칭이 가능합니다
- 추출된 데이터를 `proposal-writer`에 전달하여 자동 작성

## 지원 파일 형식

- **문서**: PDF, HWPX, DOCX, TXT
- **표**: XLSX, CSV
- **자막**: SRT
- **기타**: 대부분의 텍스트 기반 포맷

## 주의 사항

- Reference 데이터는 제안서의 '뼈대와 흐름'을 잡는 데 우선 활용합니다
- Raw 데이터는 제안서의 '내용과 전문성'을 채우는 데 집중적으로 활용합니다
- 개인정보나 민감한 정보가 포함된 파일은 사전에 검토가 필요합니다

## 라이선스

MIT License

## 기여

이슈나 개선 제안은 GitHub Issues를 통해 제출해주세요.

## 관련 프로젝트

- [rfp-analyzer](https://github.com/leedonwoo2827-ship-it/rfp-analyzer) - RFP 분석 스킬
- [proposal-writer](https://github.com/leedonwoo2827-ship-it/proposal-writer) - 제안서 작성 스킬
- [hwpx-writer](https://github.com/leedonwoo2827-ship-it/hwpx-writer) - HWPX 생성 스킬
- [text2img-mcp](https://github.com/leedonwoo2827-ship-it/text2img-mcp) - 이미지 생성 MCP
