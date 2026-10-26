# 알파시그널AI — 종목별 페이지 자동 생성 사이트

코스피·코스닥 전 종목마다 무료 AI 주가예측(5거래일 상승 확률·예상 범위)과 시세·차트 페이지를 만들고, 평일 장 마감 후(16:40) 매일 자동으로 갱신합니다.
모든 페이지 하단에 상담 신청 양식·카카오톡·전화 버튼이 붙어 있고, 신청 내용은 구글 시트에 쌓입니다.

## 폴더 구성
| 파일 | 역할 |
|---|---|
| `config.json` | **사이트 설정 (여기만 고치면 됨)** — 주소, 구글시트 URL, 카톡, 전화, 사업자 정보 |
| `build.py` | 데이터 수집 + 페이지 생성 프로그램 |
| `templates/` | 페이지 디자인 (메인, 종목, 목록, 개인정보처리방침) |
| `static/` | 공통 디자인(css)과 기능(js) |
| `.github/workflows/daily.yml` | 매일 자동 실행 설정 |
| `google-sheet/apps_script.gs` | 구글 시트에 붙여넣을 접수 코드 |

## config.json 항목
- `site_url`: 사이트 주소 (예: `https://아이디.github.io`). 도메인을 사면 그 주소로 변경
- `base_path`: 저장소 이름이 `아이디.github.io` 가 아니면 `/저장소이름` (예: `/stock-site`). 도메인 연결 후에는 `""`
- `sheet_url`: 구글 Apps Script 웹 앱 URL (…/exec)
- `kakao_url`, `phone`, `phone_hours`, `biz_info`: 연락처와 사업자 정보
- `privacy_*`: 개인정보처리방침에 들어갈 정보
- `google_site_verification`, `naver_site_verification`: 구글 서치콘솔·네이버 서치어드바이저 소유확인 코드

## 내 컴퓨터에서 미리보기 (선택)
```
pip install -r requirements.txt
python build.py --limit 30      # 시가총액 상위 30종목만 빠르게
python -m http.server 8000 --directory site
```
브라우저에서 http://localhost:8000 접속.

## 자주 생기는 문제
- **Actions가 빨간 X로 실패**: Actions 탭 → 실패한 실행 → 로그 마지막 줄 캡처해서 Claude에게 보내기.
  실패하면 기존 사이트는 그대로 유지됩니다.
- **양식이 "접수 연결이 설정되지 않았습니다"**: `config.json`의 `sheet_url`이 비어 있음.
