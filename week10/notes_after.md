작성: Claude Code / 확인: (지승오)

# week09 tools.py 함수 정리

- 대상 파일: `week09/tools.py`
- 역할: 영화진흥위원회(KOBIS) 오픈 API로 박스오피스 정보를 가져오는 도구 모음임
- 함수 개수: 1개

## 모듈 구성

- `requests`: API 호출에 사용함
- `secret.API_KEY`: `secret.py`에서 가져오는 KOBIS API 키임
- `BASE_URL`: 일별 박스오피스 조회 API(`searchDailyBoxOfficeList.json`) 주소임

## 함수

### `get_boxoffice_rank_1(date)`

- 기능: 지정한 날짜의 박스오피스 1위 영화 제목을 돌려줌
- 입력: `date` (문자열) - 8자리 날짜. 예: `"20260824"`
- 출력: (문자열) 1위 영화 제목. 예: `"오디세이"`
- 동작 순서
  1. `key`, `targetDt`를 파라미터로 묶음
  2. `requests.get`으로 API를 호출함 (timeout 10초)
  3. 응답을 JSON으로 변환함
  4. `boxOfficeResult` → `dailyBoxOfficeList`에서 영화 목록을 꺼냄
  5. 첫 번째 영화의 `movieNm`(영화 제목)을 돌려줌

## 참고 사항

- docstring의 매개변수 이름은 `data`이나 실제 이름은 `date`임
- 오류 처리가 없음
  - 잘못된 날짜나 API 키 오류로 응답 형식이 다르면 `KeyError` 발생 가능함
  - 영화 목록이 비어 있으면 `IndexError` 발생 가능함
  - 네트워크 오류나 시간 초과 시 `requests` 예외가 그대로 전달됨
