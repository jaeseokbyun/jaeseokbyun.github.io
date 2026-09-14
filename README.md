# jaeseokbyun.github.io

개인 홈페이지. **내용은 전부 `_data/` 안의 YAML 파일에만 있습니다.** HTML/CSS를 건드릴 일은 거의 없습니다.

```
_config.yml              사이트 제목, 주소, 자동 볼드 처리할 이름
_data/profile.yml        이름, 소속, 이메일, 프로필 링크, 소개글
_data/publications.yml   논문 목록 (preprint 포함)
_data/cv.yml             학력 / 경력 / 수상 / 리뷰어 / 활동
_data/nav.yml            상단 탭 목록
_includes/topbar.html    상단 고정 탭 바
_layouts/default.html    공통 <head>, 푸터, 탭 활성화 스크립트
index.html               섹션 배치 (순서 바꿀 때만 수정)
assets/css/style.css     디자인 (색·폰트는 파일 맨 위 토큰만 고치면 됨)
assets/img/profile.jpg   프로필 사진 ← 본인 사진으로 교체
assets/files/            CV PDF 등 첨부 파일
```

## 1. 처음 배포하기

1. GitHub에서 **`jaeseokbyun.github.io`** 라는 이름으로 새 레포를 만듭니다.
   (이 이름이어야 `https://jaeseokbyun.github.io` 주소를 씁니다.)
2. 이 폴더의 파일을 전부 올립니다.

   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/jaeseokbyun/jaeseokbyun.github.io.git
   git push -u origin main
   ```

3. 레포 **Settings → Pages → Build and deployment**에서
   Source를 `Deploy from a branch`, Branch를 `main` / `/ (root)`로 설정합니다.
4. 1~2분 뒤 사이트가 뜹니다. 이후로는 **push만 하면 자동으로 다시 빌드**됩니다.
   별도 빌드 도구나 CI 설정이 필요 없습니다.

## 2. 논문 추가하기

`_data/publications.yml` 맨 위에 블록 하나를 추가하고 commit/push 하면 끝입니다.

```yaml
- title: 논문 제목
  authors: "Jaeseok Byun, Someone Else, and Taesup Moon"
  venue: NeurIPS
  year: 2026
  note: "Spotlight"            # 선택
  links:                        # 선택
    - { name: arXiv, url: https://arxiv.org/abs/0000.00000 }
    - { name: Code,  url: https://github.com/jaeseokbyun/... }
```

- 파일에 적힌 **순서 그대로** 화면에 나옵니다. (최신 논문을 맨 위에)
- 저자 목록의 `Jaeseok Byun`은 자동으로 굵게 표시됩니다.
  (`_config.yml`의 `author_name`으로 바꿀 수 있음)
- `preprint: true`를 넣으면 Publications가 아니라 Preprints 섹션으로 갑니다.
  논문이 accept되면 이 줄만 지우고 `venue`/`year`만 고치면 됩니다.

## 3. 상단 탭 수정하기

`_data/nav.yml`에서 순서를 바꾸거나 항목을 빼면 그대로 반영됩니다.
새 섹션을 만들어 탭에 넣으려면 `index.html`의 `<section>`에
`class="section anchor" id="원하는이름"`을 주고, `nav.yml`에 `href: "#원하는이름"`을 추가하면 됩니다.

## 4. 프로필 사진 / CV

- `assets/img/profile.jpg`를 본인 사진으로 덮어쓰세요. 세로 4:5 비율 권장 (예: 528×660).
- CV PDF는 `assets/files/cv.pdf`로 올린 뒤, `_data/profile.yml`의 `links`에서
  CV 항목 주석(`#`)을 지우면 상단 링크에 나타납니다.

## 5. 로컬에서 미리 보기 (선택)

안 해도 됩니다. push 후 GitHub에서 바로 확인해도 충분합니다.
굳이 로컬에서 보려면 Ruby 설치 후:

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

## 6. 커스텀 도메인을 붙이고 싶다면

1. 레포 루트에 `CNAME` 파일을 만들고 도메인만 한 줄 적습니다. (예: `jaeseokbyun.com`)
2. 도메인 DNS에서 `A` 레코드를 GitHub Pages IP(185.199.108–111.153)로,
   또는 `www` 서브도메인이면 `CNAME`을 `jaeseokbyun.github.io`로 설정합니다.
3. `_config.yml`의 `url` 값도 새 도메인으로 바꿉니다.

## 7. 디자인 손보기

`assets/css/style.css` 맨 위 `:root` 블록의 색/폰트 변수만 바꿔도 인상이 크게 달라집니다.
다크 모드는 OS 설정을 따라 자동으로 전환됩니다.
