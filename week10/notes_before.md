# week09 tools.py 함수 정리

`week09/tools.py`는 영화진흥위원회(KOBIS) 오픈 API로 박스오피스 정보를 가져오는 도구 모음이다.
현재 함수는 1개뿐이다.

## 모듈 구성

- `requests`: API 호출에 사용
- `secret.API_KEY`: `secret.py`에서 가져오는 KOBIS API 키
- `BASE_URL`: 일별 박스오피스 조회 API(`searchDailyBoxOfficeList.json`) 주소

## 함수

### `get_boxoffice_rank_1(date)`

그 날짜의 박스오피스 1위 영화 제목을 알려준다.

- 받는 것: `date` (문자열) - 8자리 날짜. 예: `"20260824"`
- 돌려주는 것: (문자열) 1위 영화 제목. 예: `"오디세이"`

동작 순서:

1. `key`와 `targetDt`를 파라미터로 묶는다.
2. `requests.get`으로 API를 호출한다. (timeout 10초)
3. 응답을 JSON으로 변환한다.
4. `boxOfficeResult` → `dailyBoxOfficeList`에서 영화 목록을 꺼낸다.
5. 첫 번째 영화의 `movieNm`(영화 제목)을 돌려준다.

## 참고할 점

- docstring에는 매개변수 이름이 `data`로 적혀 있지만 실제 이름은 `date`다.
- 오류 처리가 없다. 잘못된 날짜나 API 키 오류로 응답 형식이 다르거나 목록이 비어 있으면 `KeyError`나 `IndexError`가 날 수 있다.
