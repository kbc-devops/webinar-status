# webinar-status — 웨비나 긴급 안내 페이지

`kbc-devops/webinar` 플랫폼(https://watch.cuemed.co.kr)이 **통째로 죽었을 때** 참석자가
볼 수 있는 정적 안내 페이지다. 앱의 `EMERGENCY_STATUS_URL` 환경변수에 이 주소를 넣는다.

- 공개 주소: https://kbc-devops.github.io/webinar-status/
- 서빙: **GitHub Pages** (우리 서버·우리 도메인·우리 DB 를 하나도 타지 않는다)

## 왜 별도 저장소인가

우리 저장소·우리 서버에 두면 우리가 죽을 때 같이 죽는다.
이 페이지는 epic01 · Cloudflare 터널 · PostgreSQL 어느 것도 경유하지 않는다.

## 고치는 법

`index.html` 하나만 고쳐 `main` 에 push 하면 1~2분 뒤 반영된다.

```bash
git clone git@github.com:kbc-devops/webinar-status.git
# index.html 수정 (행사명·일시·마지막 갱신 시각)
git commit -am "안내 문구 갱신" && git push
```

## 규칙 (깨면 페이지의 존재 이유가 사라진다)

- ⛔ 자바스크립트·외부 폰트·외부 이미지·외부 CSS 금지. 인라인 CSS 만.
  하나라도 바깥을 부르면 그것이 이 페이지의 장애점이 된다.
- ⛔ 우리 앱의 API·DB 호출 금지.
- ⛔ 커스텀 도메인(`*.cuemed.co.kr`) 붙이지 말 것.
  와일드카드 DNS 가 걸려 있어 큐메드 운영이 망가지고, 우리 도메인에 의존하면 의미가 없다.
- 행사가 끝나면 행사명·일시·마지막 갱신 시각을 다음 행사로 갱신한다.
