# 오늘의 운세 — 배포 가이드

## 파일 구성
- `오늘의운세.html` (배포 시 `index.html`로 이름 변경)
- `og-image.png` (1200×630, 카카오톡·페이스북·X 미리보기용)

## GitHub Pages 배포 (가장 간단)

1. GitHub에서 새 리포지토리 생성 (예: `fortune` 또는 `username.github.io/fortune`)
2. 두 파일을 업로드:
   - `오늘의운세.html` → 이름을 **`index.html`**로 변경 후 업로드
   - `og-image.png` → 그대로 업로드 (같은 폴더)
3. 리포지토리 → **Settings → Pages** → Source를 **`main` 브랜치 / `/(root)`** 로 설정
4. 1~2분 후 `https://[username].github.io/[repo-name]/` 에서 접속 가능

## ⚠️ 배포 후 꼭 해야 할 일 — OG 미리보기 활성화

`index.html` 상단의 메타태그에서 `https://YOUR-DOMAIN.com` 부분을 **실제 호스팅 주소로 교체**해야 카카오톡 미리보기가 뜹니다.

예를 들어 `https://username.github.io/fortune/` 에 배포했다면, 다음 4곳을 바꿔주세요:

```html
<meta property="og:image" content="https://username.github.io/fortune/og-image.png">
<meta property="og:url" content="https://username.github.io/fortune/">
<meta name="twitter:image" content="https://username.github.io/fortune/og-image.png">
```

상대 경로(`/og-image.png`)도 일부 크롤러는 해석하지만, **카카오톡은 절대 URL을 요구**하므로 풀 주소로 적어주세요.

## 카카오톡 미리보기 캐시 갱신

카카오톡은 한 번 본 링크의 미리보기를 캐싱합니다. OG 태그를 수정한 뒤 미리보기가 안 바뀌면:
- 카카오톡 채팅창에서 링크 끝에 `?v=2` 같은 쿼리스트링을 붙여서 다시 보내면 새로 가져옵니다 (예: `https://username.github.io/fortune/?v=2`)
- 또는 페이스북 공유 디버거에서 URL을 다시 스크래핑해도 도움이 됩니다: `https://developers.facebook.com/tools/debug/`

## 작동 확인

배포 후 미리보기가 잘 뜨는지 확인하려면:
- **카카오톡 미리보기**: 나에게 보내기 (혼자 채팅) 에 링크를 붙여서 테스트
- **페이스북/X 미리보기**: 위 페이스북 디버거 또는 X(Twitter) Card Validator
- **OG 메타태그 점검**: `https://www.opengraph.xyz/` 에 URL 입력

## 공유 버튼 동작 방식

- **공유** 버튼: 모바일에서는 `navigator.share()`로 OS 공유 시트가 열려 카카오톡·메시지·메일 등이 한 번에 뜹니다. PC에서는 자동으로 링크 복사로 대체됩니다.
- **링크 복사**: 클립보드에 운세 결과 + 링크가 함께 복사됩니다.
- **X에 공유**: 트위터 공유 인텐트 창이 열립니다.

카카오톡 자체 SDK(공식 공유 버튼)는 카카오 개발자 센터 앱 등록·도메인 등록이 필요하기 때문에 빼두었습니다. 위 3가지로도 충분히 잘 동작합니다.

## 콘텐츠 커스터마이즈

`index.html` 안의 `CARDS` 객체에서:
- 각 카드(天/地/人/日/月/風/水/火)의 `pool` 배열에 운세 문구 추가/수정
- `proverbs` 배열에 한 줄 명언 추가
- 카드의 `range`로 해당 카드의 점수 분포 조정

`COLORS_POOL`, `DIRS_POOL` 도 자유롭게 늘리실 수 있어요.
