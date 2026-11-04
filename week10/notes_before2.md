# week09 tools.py 함수 설명

`week09/tools.py`는 영화진흥위원회(KOBIS) 오픈 API에서 박스오피스 정보를 가져오는 도구 모음이다.
들어 있는 함수는 `get_boxoffice_rank_1` 1개다.

## 함수 목록

| 함수 | 받는 것 | 돌려주는 것 |
| --- | --- | --- |
| `get_boxoffice_rank_1(date)` | 8자리 날짜 문자열. 예: `"20260824"` | 그 날짜 1위 영화 제목 문자열. 예: `"오디세이"` |

## `get_boxoffice_rank_1(date)`

지정한 날짜의 일별 박스오피스에서 1위 영화 제목을 찾아 돌려준다.

1. `secret.py`의 `API_KEY`와 `date`로 요청 파라미터(`key`, `targetDt`)를 만든다.
2. `BASE_URL`(일별 박스오피스 조회 API)에 `requests.get`으로 요청한다. 제한 시간은 10초다.
3. 응답을 JSON으로 바꾸고 `boxOfficeResult` → `dailyBoxOfficeList`에서 영화 목록을 꺼낸다.
4. 목록 첫 번째 영화의 `movieNm`을 돌려준다.

## 알아둘 점

- 실행하려면 `API_KEY`가 들어 있는 `secret.py`가 있어야 한다.
- docstring에는 매개변수가 `data`로 적혀 있지만 실제 이름은 `date`다.
- 오류 처리가 없다. 응답에 예상한 키가 없으면 `KeyError`, 영화 목록이 비어 있으면 `IndexError`가 난다.
