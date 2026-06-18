# DMU 반도체부트캠프사업단 리뉴얼 프로젝트

본 프로젝트는 Vite + React + Tailwind CSS v3를 기반으로 제작된 모던 원페이지 웹사이트입니다.

## 🚀 실행 및 배포 방법

### 1. 필수 요구사항
- **Node.js**: v18 이상 권장
- **npm**: 패키지 관리자

### 2. 로컬 개발 환경 실행
```bash
# 1. 의존성 패키지 설치
npm install

# 2. 로컬 개발 서버 실행
npm run dev
```
위 명령어를 실행한 후 터미널에 나타나는 주소(예: `http://localhost:5173`)로 접속하세요.
*※ `index.html` 파일을 브라우저로 직접 열면(file://) React 모듈 시스템이 작동하지 않아 화면이 나오지 않습니다.*

### 3. Vercel 배포 방법
1. 본 폴더의 내용을 GitHub에 업로드합니다.
2. Vercel에서 `New Project`를 선택하고 해당 저장소를 연결합니다.
3. Framework Preset이 `Vite`로 자동 인식됩니다. 그대로 `Deploy` 버튼을 누르면 배포가 완료됩니다.
   - 프로젝트 설정에 `vercel.json`이 포함되어 있어 SPA 라우팅이 정상 작동합니다.

## ✨ 기술 스택 및 특징
- **Framework**: Vite + React (JavaScript)
- **Styling**: Tailwind CSS v3 (Custom Dark Theme)
- **Features**: 
  - D-Day 실시간 계산 로직
  - IntersectionObserver 활용 스크롤 애니메이션
  - 탭 기반 공지사항 가변 섹션
  - 외부 의존성 없는 인라인 SVG 그래픽 및 패턴

## 🛠 수정 및 최적화 내역
- **이미지/글자 깨짐 방지**: UTF-8 메타 태그 적용 및 시스템 폰트 프리셋(system-ui) 추가로 폰트 로드 실패 시에도 레이아웃 유지.
- **SVG 보안**: `aria-hidden` 및 `color-current` 방식을 활용해 깨짐 없는 그래픽 출력 보장.
- **SPA 라우팅**: Vercel 배포 시 발생할 수 있는 404 오류 방지를 위해 `vercel.json` 추가.
