# Personal Portfolio

전북대학교 컴퓨터인공지능학부 재학생 여경용의 개인 포트폴리오입니다.
관심 분야와 학습 경험, 개인 프로젝트의 개발 과정을 소개합니다.

**[사이트 보기](https://zichana1598.github.io/portfolio-assignment/)**

## 주요 페이지

| 페이지 | 내용 |
|---|---|
| Home | 자기소개와 대표 프로젝트 |
| About Me | 관심 분야, 기술 스택, 학습 목표 |
| Projects | 개인 프로젝트 목록 |
| Notice Monitor | 전북대학교 공지 모니터링 프로젝트 상세 소개 |

## 기술 스택

- Hugo Extended 0.167.0 · Blowfish
- Markdown · TOML · HTML
- GitHub Actions · GitHub Pages

## 로컬 실행

Git과 [Hugo Extended 0.167.0](https://github.com/gohugoio/hugo/releases/tag/v0.167.0)을 설치합니다.
설치 방법은 [Hugo 공식 문서](https://gohugo.io/installation/)를 참고하세요.

```bash
git clone https://github.com/zichana1598/portfolio-assignment.git
cd portfolio-assignment/site
hugo server --config pages.json --environment development --baseURL http://localhost:1313/
```

브라우저에서 http://localhost:1313/ 에 접속합니다.
`pages.json`에 테마 설정이 있으므로 실행할 때 `--config pages.json`을 함께 지정합니다.

### 프로덕션 빌드

`site/` 디렉터리에서 실행합니다.

```bash
hugo --config pages.json --environment production --minify --enableGitInfo=false --baseURL https://zichana1598.github.io/portfolio-assignment/
```

결과물은 `site/public/`에 생성됩니다.

## 프로젝트 구조

실제 사이트는 `site/`에 있습니다. 루트의 테마 파일과 `exampleSite/`는 배포 대상으로 사용하지 않습니다.

```text
.
├── .github/
│   ├── workflows/hugo-pages.yml  # 자동 배포
│   └── pages_build.py           # 배포 빌드 및 경로 보정
├── site/
│   ├── config/_default/        # 사이트 설정과 메뉴
│   ├── content/
│   │   ├── _index.md           # Home
│   │   ├── about/              # About Me
│   │   └── projects/           # 프로젝트 목록과 상세 페이지
│   ├── assets/                 # 이미지 등 정적 자산
│   ├── layouts/                # 사이트 전용 템플릿
│   ├── pages.json              # 배포 주소와 테마 설정
│   └── themes/template/        # Blowfish 테마
├── .github-pages.json           # 배포 스크립트 설정
├── README.md
└── LICENSE
```

페이지 내용은 `site/content/`, 메뉴는 `site/config/_default/menus.ko.toml`,
프로필은 `languages.ko.toml`, 화면 옵션은 `params.toml`에서 수정합니다.
테마 템플릿을 변경할 때는 원본 대신 `site/layouts/`의 같은 경로에 파일을 두어 재정의합니다.

## 배포

GitHub 저장소의 **Settings → Pages → Source**를 **GitHub Actions**로 설정합니다.
`main`에 푸시하면 `.github/workflows/hugo-pages.yml`이 빌드와 배포를 실행합니다.

저장소 루트에서 변경 파일을 커밋하고 푸시합니다. 아래는 홈페이지 수정 예시입니다.

```bash
git add site/content/_index.md
git commit -m "content: update homepage introduction"
git push origin main
```

[Actions](https://github.com/zichana1598/portfolio-assignment/actions)에서 해당 커밋의
`build`와 `deploy` 성공 여부를 확인한 뒤 공개 사이트에서 변경 내용을 확인합니다.

CI는 Hugo Extended 0.167.0을 사용하며, Pages 주소에 맞게 경로를 보정한 결과물을
루트 `public/`에 생성해 배포합니다. 로컬 빌드의 `site/public/`과는 출력 위치가 다릅니다.
배포에 필요한 Python, Node.js, Go, Sass는 워크플로에서 설치합니다.

## 출처 및 라이선스

- 정적 사이트 생성기: [Hugo](https://gohugo.io/)
- 테마: [Blowfish](https://github.com/nunocoracao/blowfish) — MIT License, © 2022 Nuno Coração
- 배경과 아이콘: Blowfish에 포함된 자산 사용. 아이콘 출처는 [Font Awesome](https://fontawesome.com/), 이용 조건은 [공식 라이선스 안내](https://fontawesome.com/license/free) 참고
- 배포 준비 및 빌드 스크립트: 수업 제공 자료 사용

Blowfish의 저작권 및 라이선스 고지를 [LICENSE](LICENSE)와
[테마 LICENSE](site/themes/template/LICENSE)에 유지합니다.
개인 소개와 프로젝트 설명은 직접 작성했으며, 일부 설정과 템플릿 수정에는 AI 도구의 도움을 받았습니다.
