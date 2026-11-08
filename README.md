# beryllium Metal 플러그인 빌드 (GitHub Actions)

POCO F1(beryllium, Adreno 630)에 올린 iPadOS 17.7.11용 `NativeAdrenoMetal.bundle`(AdrenoMetal + Turnip)을 GitHub의 macOS 머신에서 빌드한다.

- 이 저장소에는 워크플로와 우리 패치만 있다. 소스는 모두 공개 저장소를 고정 커밋으로 받는다(`.github/workflows/build.yml` 위쪽 주석).
  - `patches/adrenometal/`: 플러그인 패치(이름 순서로 적용).
  - `patches/mesa/`: Turnip 패치. 코어의 기록된 Mesa 패치 목록 뒤에 붙어 같은 검사를 받는다. 수동 실행에서 `mesa_patches=off`로 뺄 수 있다.
  - 폰에서 다시 빌드하지 않고 켜고 끄는 파일(`NativeAdrenoMetal.env` 등)은 `unixnu/drivers-wip/gpu/PLUGIN-PERF-s34.md`에 정리했다.
- 기기 고유 정보, 펌웨어, 트러스트 캐시는 넣지 않는다.
- 실행: Actions 탭 → build-metal-plugin → Run workflow. `main`에 push해도 돈다.
- 결과: 실행 페이지의 Artifacts → `native-adreno-metal` (번들, `trust.json`, 빌드 로그).

받은 번들은 PC의 `unixnu/drivers-wip/gpu/integration/apply.sh`에 `GPU=12 PLUGIN=<번들>`로 넣고, `trust.json`의 CDHash 두 개를 트러스트 캐시에 추가한다(`drivers-wip/gpu/PLAN.md` 8–11절).
