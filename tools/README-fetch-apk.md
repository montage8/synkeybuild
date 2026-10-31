# APK 가져오기 (최초 1회 수동 설정)

에이전트 샌드박스에서는 GitHub Actions 아티팩트 저장소(Azure Blob)로의
직접 다운로드가 차단되고, 에이전트 토큰으로는 `.github/workflows/` 파일을
푸시할 수 없어서(`workflows` 권한 필요), 최초 1회만 아래 작업을 해주세요.

## 설정 방법 (GitHub 웹)

1. 이 저장소(`montage8/synkeybuild`)에서 브랜치를
   `arena/94294d67-synkeybuild` 로 선택합니다.
2. `Add file` → `Create new file` 을 누르고, 파일 이름을 정확히
   `.github/workflows/fetch-apk.yml` 로 입력합니다.
3. `tools/fetch-apk-workflow.yml` 파일의 내용 전체를 복사해 붙여넣습니다.
4. `Commit changes` 로 이 브랜치(`arena/94294d67-synkeybuild`)에 직접 커밋합니다.
5. 채팅에서 "추가 완료"라고 알려주세요.

## 설정 후 (재빌드 때마다 반복)

에이전트가 아래만 실행하면 기존 APK가 새 APK로 교체되어
이 워크스페이스에 올라옵니다. 사용자는 채팅에서 파일을 다운로드하면 됩니다.

```bash
gh workflow run fetch-apk.yml --ref arena/94294d67-synkeybuild   # 최신 성공 빌드 자동 선택
gh run watch <fetch-run-id>
git pull origin arena/94294d67-synkeybuild   # synkey-nevi-debug.apk 교체됨
```

- APK 고정 파일명: `synkey-nevi-debug.apk` (재빌드 시 같은 이름으로 교체)
- 빌드 정보(run id, 소스 브랜치/sha, sha256, 크기): `apk-info.json`
