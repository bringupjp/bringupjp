
# Decap CMS로 GitHub Pages에서 쉽고 안전하게 수정하기

이 설정은 **Decap CMS(구 Netlify CMS)**를 이용해 `buj-data.json`을 웹 UI로 수정하고, 수정 사항을 **깃허브 커밋**으로 반영합니다.  
사이트는 **GitHub Pages**로 계속 호스팅할 수 있습니다.

## 1) 파일 배치
- `admin/index.html`
- `admin/config.yml`  ← 여기서 `repo`, `site_url`, `base_url` 수정
- `buj-data.json`
- `index.html` (이미 JSON 로더 포함)

## 2) 인증(선택지 A: GitHub OAuth 프록시)
GitHub Pages만 쓰는 경우, **GitHub OAuth 프록시**가 필요합니다. (무료 배포 가능)
- 예: https://github.com/daresaydigital/decap-cms-oauth  (Vercel/Render에 원클릭 배포)
- 배포 후 발급된 URL을 `admin/config.yml`의 `base_url`로 넣고, `auth_endpoint: /auth` 유지
- GitHub에서 OAuth App 생성:
  - Authorization callback URL: `https://<배포한-oauth-app-도메인>/callback`
  - Client ID/Secret을 OAuth 앱에 설정

## 3) 인증(선택지 B: Netlify + Identity/Git Gateway)
만약 Netlify로 배포한다면 OAuth 프록시 없이 **Netlify Identity**를 켜고 `backend.name: git-gateway`로 설정 가능합니다.
(이번에는 GitHub Pages를 선택하셨으므로 A 권장)

## 4) config.yml 채우기
```yml
backend:
  name: github
  repo: <깃허브아이디>/<저장소명>
  branch: main
  base_url: https://<배포한-oauth-app-도메인>
  auth_endpoint: /auth
site_url: "https://<깃허브아이디>.github.io/<저장소명>/"
```

## 5) /admin 접속
- 배포 후 `https://<깃허브아이디>.github.io/<저장소명>/admin/` 로 접속
- GitHub 로그인 → 승인
- “サイトデータ (buj-data.json)” 항목에서 **News/Activities** 등 수정 → **Publish** → 자동 커밋

## 주의
- `buj-data.json`은 이미 **index.html**에서 읽도록 구현돼 있으니, CMS로 수정하면 바로 사이트에 반영됩니다.
- 미디어 업로드 경로는 `media/`를 사용합니다. 필요하면 Git LFS를 고려하세요.
- 보안상, OAuth 프록시의 도메인은 **HTTPS**가 필요합니다.
