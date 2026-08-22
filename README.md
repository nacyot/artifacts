# artifacts

공개해도 되는 작업 산출물 모음. 실측 정리, 리서치, 시각화를 정적 HTML로 담는다.
서빙은 홈랩 k8s의 nginx가 하고, Cloudflare Tunnel로 나가 Cloudflare가 CDN 역할을 한다.

개인 식별 정보(시리얼·자격증명·집 네트워크 주소·호스트명)는 제거한 것만 올린다.

- 사이트: https://artifacts.nacyot.com/
- RSS: https://artifacts.nacyot.com/feed.xml

## 목록 (최신순)

| 날짜 | 산출물 | 설명 |
|---|---|---|
| 2026-08-22 | [dgx-spark-node-setup](./dgx-spark-node-setup/) | ASUS Ascent GX10(DGX Spark) 한 대를 추론 서버로: 필수(서버 모드, 드라이버 595, PD FW, 보안) / 추천(GPU와 CPU 클럭 상한 스윕 그래프, vLLM 스핀 패치) / 트러블슈팅 / 직접 검증한 레시피(ollama Qwen3.8-27B, DeepSeek V4 Flash EXL3) |
| 2026-08-22 | [dgx-spark-node-setup-en](./dgx-spark-node-setup-en/) | 위 글의 영어판 (English) |
| 2026-08-22 | [dgx-spark-node-setup-ja](./dgx-spark-node-setup-ja/) | 위 글의 일본어판 (日本語) |
| 2026-08-11 | [deepseek-v4-flash-2x-dgx-spark](./deepseek-v4-flash-2x-dgx-spark/) | DGX Spark 2노드에 DeepSeek V4 Flash 0731 원본 FP8(166.9GB)을 vLLM TP=2로 서빙한 실측: 컨텍스트·클럭 무관한 디코드, 전성비 최적점, 95케이스 벤치 |
| 2026-08-10 | [10gbe-transfer-bottlenecks](./10gbe-transfer-bottlenecks/) | 디스크는 800MB/s인데 rsync는 230: 사라진 70%를 ssh 암호화·직렬 처리·커널 소켓 버퍼·readahead 힌트로 분해 (단독 A/B 검증) |
| 2026-08-10 | [gb10-gpu-clock-cap](./gb10-gpu-clock-cap/) | GB10 전력 상한: -pl 없음, nvidia-smi -lgc 클럭 캡으로 70W→40W 실측 + systemd 영속 + PD 고착 버그 구분 |
| 2026-07-28 | [dvorak-dubeolsik](./dvorak-dubeolsik/) | Dvorak에서 두벌식이 깨지는 이유: Windows·macOS에 없는 조합을 libhangul·fcitx5-hangul 소스 패치로 근본 해결 (우회 실패·부작용 타임라인, 키보드 배열 시각화) |
| 2026-07-25 | [claude-code-install-pitfalls](./claude-code-install-pitfalls/) | Opus 5가 나왔는데 "최신" 클로드 코드엔 4.8만: stable 채널 고착이 범인. 필요한 버전(2.1.220 · latest 채널)과 점검 레시피 (docker 컨테이너 실측) |
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

정적 파일뿐이라 빌드 단계는 없다. `main` 브랜치 루트를 그대로 서빙한다.
푸시하면 홈랩의 git-sync 사이드카가 30초 안에 당겨 간다. 배포 파이프라인은 homelab 리포
`k8s/apps/artifacts/` 에 있고, 갱신을 바로 보이게 하려면 Cloudflare 캐시를 퍼지한다.
새 글을 올리면 `index.html` 목록 맨 위와 `feed.xml` `<item>` 맨 위에 같은 순서로 추가한다.
