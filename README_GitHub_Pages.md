
# Bring Up Japan — GitHub Pages 배포 패키지

이 패키지는 정적 사이트를 GitHub Pages로 배포하기 위한 최소 파일로 구성되어 있습니다.

## 포함 파일
- `index.html` : 홈페이지 (JSON 로더 포함)
- `buj-data.json` : 콘텐츠 데이터 (뉴스/활동)
- `admin/buj-admin.html` : 관리자 JSON 편집 페이지 (서버 공개 비권장, 로컬에서만 사용 권장)
- `README_GitHub_Pages.md` : 이 안내 문서

## 배포 방법 (GitHub Pages)
1. GitHub에서 새 저장소(예: `bring-up-japan-site`) 생성
2. 이 폴더의 모든 파일을 저장소 루트에 업로드/커밋
3. **Settings → Pages** 이동
   - Source: `Deploy from a branch`
   - Branch: `main` (또는 기본 브랜치) / Folder: `/ (root)`
   - **Save** 클릭
4. 잠시 후 `https://<사용자명>.github.io/<저장소명>/` 주소로 접속

> `index.html`가 자동 홈으로 열립니다. `buj-data.json`은 같은 폴더에서 로드됩니다.

## 콘텐츠 수정(관리)
- `admin/buj-admin.html`을 **로컬에서** 열고, 상단의 **"サンプル読込"** 버튼으로 `buj-data.json`을 불러온 뒤 수정하세요.
- **"JSONをダウンロード"**로 저장한 파일을 레포의 `buj-data.json`에 덮어써서 커밋하면 사이트가 갱신됩니다.

### 보안 주의
- `admin/buj-admin.html`은 편집 도구일 뿐 **보안 인증이 없습니다.**  
  공개 저장소에 포함하면 누구나 접근할 수 있으니, **로컬 전용 사용**을 권장합니다.
  - 공개 배포 시에는 `admin` 폴더를 레포에서 제외하거나, 별도 비공개 레포로 분리하세요.

## 커스텀 도메인(선택)
- Settings → Pages → **Custom domain**에서 도메인 입력
- 레지스트라에서 `CNAME`을 `username.github.io`로 설정
- GitHub 레포 루트에 자동 생성되는 `CNAME` 파일 확인

## 이미지 연동(선택)
- `buj-data.json`의 `activities[i].images`는 현재 `div#img-001` 같은 자리 표시자만 렌더합니다.
- 실제 이미지를 쓰려면 `images/` 폴더에 파일을 넣고, 스크립트를 `<img src="...">` 삽입 형태로 확장하세요.
  원하시면 해당 스크립트도 제공해 드립니다.
