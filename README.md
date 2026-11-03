# AsterCache shared profiles

Load-order profiles for [AsterCache](https://github.com/DO0OG/AsterCache). The service downloads
`profiles.zip` from the latest release here once a week (`auto.shared_profiles`, on by default) and uses a
profile only for a game whose installed files match the recorded sizes and sample hashes. Nothing here is
required: without a matching profile AsterCache records the first run itself.

## Contents

- `index.json`: which game each profile belongs to (`steam`, `epic`, or `exe` key), see the
  [index format](https://github.com/DO0OG/AsterCache/blob/main/csharp/README.md#shared-profile-index-for-contributors).
- `p/<game>.json`: the profile made with `aster profile export`. It holds relative paths, file sizes, sample
  hashes, and read offsets. No account data, no save data, no file contents.

## Contributing a profile

1. Let AsterCache record one normal start of the game, then run `aster profile export --game <name> --out p/<name>.json`.
2. Add an `index.json` entry. For Epic games the `app_name` and `version` come from the launcher manifest
   (`%ProgramData%\Epic\EpicGamesLauncher\Data\Manifests\*.item`); for Steam, the app ID and depot manifest
   gids from `appmanifest_<appid>.acf`; for everything else the `exe` size and sample SHA-256 that `aster`
   prints in `profile export`.
3. Open a pull request. The release zip is rebuilt from `index.json` and `p/`.

## Profiles

| Game | Key | Recorded on |
|---|---|---|
| Frostpunk (Epic) | epic `0.0.10`, exe fingerprint | HDD, 2026-11-02 |
| Call of Duty HQ (Steam 1938090) | steam depots 1938091/1938092, exe fingerprint | HDD, 2026-11-02 |

---

# AsterCache 공유 프로필 (한국어)

[AsterCache](https://github.com/DO0OG/AsterCache) 의 읽기 순서 프로필 모음입니다. 서비스는 이 저장소의 최신
릴리스에서 `profiles.zip` 을 주 1 회 내려받고(`auto.shared_profiles`, 기본 켜짐), 설치된 파일의 크기·표본 해시가
기록과 일치하는 게임에만 프로필을 씁니다. 일치하는 프로필이 없으면 첫 실행을 직접 기록하므로 필수가 아닙니다.

- `index.json`: 프로필이 어느 게임의 것인지(`steam`·`epic`·`exe` 중 하나).
- `p/<게임>.json`: `aster profile export` 로 만든 프로필. 상대 경로·파일 크기·표본 해시·읽기 오프셋만 담고,
  계정·세이브·파일 내용은 들어가지 않습니다.

기여: 게임을 한 번 평소처럼 실행해 기록을 만든 뒤 `aster profile export --game <이름> --out p/<이름>.json` 으로
내보내고, `index.json` 에 항목을 더해 풀 리퀘스트를 보내 주십시오.
