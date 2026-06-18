# DMU 반도체부트캠프사업단 리뉴얼 프로젝트

본 프로젝트는 **단일 `index.html` 정적 웹사이트**입니다. Tailwind CSS(CDN)와 순수 JavaScript(해시 기반 라우팅)로 동작하며, 별도의 빌드 과정이 필요 없습니다.

## 🚀 실행 및 배포 방법

### 1. 로컬에서 보기
별도 설치 없이 정적 서버로 열면 됩니다.
```bash
# 예시 1) Node가 있는 경우
npx serve .

# 예시 2) Python이 있는 경우
python -m http.server 3000
```
브라우저에서 표시되는 주소(예: `http://localhost:3000`)로 접속하세요.
*※ 해시 라우팅(`#/about` 등)을 사용하므로 `index.html`을 직접 열어도 동작하지만, 정적 서버로 여는 것을 권장합니다.*

### 2. Vercel 배포 방법
1. 본 폴더의 내용을 GitHub에 업로드합니다.
2. Vercel에서 `New Project`를 선택하고 해당 저장소를 연결합니다.
3. 빌드 과정이 없으므로 **Framework Preset은 `Other`(정적)** 로 두고 그대로 `Deploy` 합니다.
   - `vercel.json`에 SPA rewrite가 포함되어 있어 모든 경로가 `index.html`로 연결됩니다.

## ✨ 기술 스택 및 특징
- **Styling**: Tailwind CSS v3 (CDN, Light Theme)
- **Routing**: 순수 JavaScript 해시 라우터 (빌드 도구 불필요)
- **Features**:
  - 탭 기반 가변 섹션(사업단 소개 / 교육과정 / 교육 인프라 / 커뮤니티 / 취업지원)
  - 마이크로디그리 초급·중급·고급 커리큘럼 표
  - 커뮤니티 게시글 작성/조회 (Firebase Firestore 연동, 미설정 시 localStorage로 동작)
  - 외부 이미지 로드 실패 시 자동 대체(placeholder) 처리

## 🔥 Firebase(게시판) 설정 방법
커뮤니티의 게시글 작성/조회는 Firebase Firestore에 저장됩니다. 연결하려면:

1. [Firebase 콘솔](https://console.firebase.google.com)에서 프로젝트를 만들고 **Firestore Database**를 생성합니다.
2. `프로젝트 설정 > 일반 > 내 앱(웹)`에서 `firebaseConfig` 값을 복사합니다.
3. `index.html` 하단의 `<script type="module">` 안에 있는 `firebaseConfig` 객체에 값을 붙여넣습니다.
4. Firestore 보안 규칙에서 `posts` 컬렉션에 대한 읽기/쓰기를 허용합니다. (테스트용 예시)
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /posts/{doc} { allow read, write: if true; }
     }
   }
   ```
   *※ 위 규칙은 누구나 읽기/쓰기가 가능하므로, 운영 시에는 인증/검증 규칙을 추가하세요.*

> 설정값을 입력하기 전에도 게시글 작성은 동작하며, 이 경우 글이 해당 브라우저(localStorage)에만 저장됩니다.

## 🛠 수정 및 최적화 내역
- **배포 오류 제거**: 존재하지 않는 `/src/main.jsx`를 불러오던 React 잔재 및 미사용 빌드 설정(Vite/PostCSS/Tailwind config, package.json)을 제거하여 Vercel 빌드 실패를 해결.
- **이미지 깨짐 방지**: 누락된 로컬 `./assets/*.png` 참조를 안정적인 외부 이미지로 교체하고, 로드 실패 시 대체 UI가 표시되도록 처리.
- **가독성 개선**: 루트 글꼴 크기 상향 및 내비게이션·탭·표·푸터 등 작은 텍스트 크기 확대.
- **콘텐츠 보강**: 비어 있던 `교육 인프라`, `취업지원` 페이지에 내용을 채우고 `오시는 길`에 지도를 임베드.
