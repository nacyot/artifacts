# artifacts

공개해도 되는 작업 산출물 모음. 실측 정리·리서치·시각화를 정적 HTML로 담고 GitHub Pages로 서빙한다.

개인 식별 정보(시리얼·자격증명·집 네트워크 주소·호스트명)는 제거한 것만 올린다.

- 사이트: https://nacyot.github.io/artifacts/
- RSS: https://nacyot.github.io/artifacts/feed.xml

## 목록 (최신순)

| 날짜 | 산출물 | 설명 |
|---|---|---|
| 2026-07-25 | [claude-code-install-pitfalls](./claude-code-install-pitfalls/) | `claude update`가 "최신"이라는데 최신이 아닌 이유: 릴리스 채널(stable/latest), PATH 순서로 갈리는 중복 설치, mise shim 잔재, Agent SDK가 번들한 CLI (docker 컨테이너 실측) |
| 2026-07-15 | [asahi-macbook-speaker-crackle](./asahi-macbook-speaker-crackle/) | 맥북 내장 스피커 크래클: 세 원인(DSP, 효율코어 스케줄링, 스트림 전환)과 처방, macOS가 멀쩡한 이유 (PipeWire, d3 인터랙티브) |
| 2026-07-15 | [tailscale-per-app-exit-node](./tailscale-per-app-exit-node/) | Tailscale exit node를 앱 단위로: 브라우저 하나만 다른 리전으로 (유저스페이스 SOCKS5, fail-closed, d3 인터랙티브) |
| 2026-07-10 | [displaylink-asahi-m1](./displaylink-asahi-m1/) | Asahi M1 Max 외장 2대 — 막힌 지점과 접은 이유 (DP 드라이버 · DisplayLink CPU · HDMI) |
| 2026-07-05 | [bambu-p1s-scripting](./bambu-p1s-scripting/) | Bambu Lab P1S를 앱 없이 MQTT·FTPS 프로토콜만으로 제어한 실측 정리 + d3.js 시각화 |

## 구조

```
├── index.html                    랜딩(산출물 목록, 최신순)
├── feed.xml                      RSS 2.0
├── vendor/d3.v7.min.js           공용 d3 (상대경로로 참조)
└── <slug>/index.html             각 산출물
```

정적 파일뿐이라 빌드 단계는 없다. `main` 브랜치 루트를 그대로 Pages가 서빙한다.
새 글을 올리면 `index.html` 목록 맨 위와 `feed.xml` `<item>` 맨 위에 같은 순서로 추가한다.
