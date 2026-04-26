# macOS에서 한글 파일명이 ?로 깨질 때

> Windows에서 받은 zip을 풀거나 외장하드에서 파일을 옮길 때, 파일명이 `??_???.txt`처럼 보이는 문제.

## 상황

- 동료가 보낸 zip을 macOS에서 풀었더니 한글 파일명이 다 깨짐
- 외장하드(NTFS·FAT32)의 한글 파일명이 ?로 보임
- 압축할 때 멀쩡했는데 풀면 깨짐

원인은 인코딩. macOS는 UTF-8, Windows의 옛 zip은 CP949(EUC-KR)로 파일명을 저장합니다.

## 그루밍

### 압축 풀 때만 문제라면 — `unar` 사용

```bash
# Homebrew로 한 번만 설치
brew install unar

# 그 다음부터는 이걸로 풀기
unar 받은파일.zip
```

`unar`은 자동으로 인코딩 감지. macOS 기본 압축 풀기보다 거의 항상 더 잘 풉니다.

### CLI에서 강제로 인코딩 지정

```bash
# Python 내장으로 (별도 설치 불필요)
python3 -c "
import zipfile, os
with zipfile.ZipFile('받은파일.zip') as z:
    for info in z.infolist():
        try:
            name = info.filename.encode('cp437').decode('cp949')
        except:
            name = info.filename
        z.extract(info, '.')
        os.rename(info.filename, name)
"
```

### 외장하드의 파일명이 깨진 경우 — `convmv`

```bash
brew install convmv

# 미리보기 (실제 변경 X)
convmv -f cp949 -t utf8 -r ./폴더

# 실제 변경
convmv -f cp949 -t utf8 -r --notest ./폴더
```

> `--notest` 빼고 한 번 돌려서 결과 보고, 괜찮으면 붙여서 다시.

### 보낼 때 미리 막으려면

- **압축 형식을 zip 대신 7z 또는 tar.gz**로 보내달라고 부탁. 이 둘은 UTF-8 기본.
- 본인이 보낼 때:
  ```bash
  # macOS에서 한글 파일명 안전한 zip 만들기
  zip -r 보낼파일.zip 폴더 -x "*.DS_Store"
  ```

## 출처/참고

- [unar 공식](https://theunarchiver.com/command-line)
- 본인 외장하드 한 번 통째로 깨먹고 복구한 경험

---
**발견자**: @GoGoComputer · 2026-04-27
