# 키프리스 플러스 API 사용 가이드

> **작성일:** 2026-05-27  
> **출처:** [키프리스 플러스](https://plus.kipris.or.kr)
> **GitHub Repo:** https://github.com/ojc1234/kipris-api-list

---

## 1. API란?

키프리스 플러스 API는 **특허·실용·상표·디자인·심판** 등 지식재산 관련 데이터를 프로그래밍 방식으로 조회할 수 있는 REST API 서비스입니다.

---

## 2. 신청 방법 (이용 절차)

### Step 1 — 회원가입
- https://plus.kipris.or.kr/portal/member/joinView.do?menuNo=200028

### Step 2 — 로그인
- https://plus.kipris.or.kr/portal/member/login.do?menuNo=200027

### Step 3 — 서비스 선택
- https://plus.kipris.or.kr/portal/data/service/List.do?menuNo=200100 (서비스 유형별 → API)
- 원하는 API 서비스 클릭 → 상세보기

### Step 4 — 서비스 신청
- https://plus.kipris.or.kr/portal/data/request/apiFsmtmList.do?menuNo=290005
-，申请할 API 선택 → 이용약관 동의 → 신청

### Step 5 — 키(KIPRIS API KEY) 발급
- 신청 완료 후 마이페이지 또는 서비스 상세에서 **API 키** 확인
- 요청 시 HTTP Header에 `Authorization: KIPRIS_API_KEY` 또는 `appKey` 파라미터로 전달

---

## 3. API 호출 기본 구조

### 기본 정보

| 항목 | 내용 |
|---|---|
| **엔드포인트** | `https://plus.kipris.or.kr/` 로 시작 |
| **통신 방식** | REST (HTTP GET/POST) |
| **응답 형식** | JSON (`dataType=JSON` 파라미터) |
| **인코딩** | UTF-8 |

### 기본 요청 예시

```
GET https://plus.kipris.or.kr/portal/openInfo/getAdvancedSearch?
  appKey=발급받은_APP_KEY&
  patentNumber=1020200012345&
  dataType=JSON
```

### 공통 헤더

```
Authorization: KIPRIS_API_KEY [발급받은 키]
Content-Type: application/json
```

---

## 4. 대분류별 서비스 목록

### 국내 IP데이터 (45개 서비스)

| 중분류 | 서비스 수 | 대표 서비스 |
|---|---|---|
| **공보** | 다수 | 특허·실용 공개·등록공보, 디자인 공보, 상표 출원 속보, 정정공보 |
| **행정** | 다수 | 특허·실용 행정처리 이력, 디자인 행정처리 이력, 상표 행정처리 이력 |
| **부가** | 다수 | 분류코드, 출원인 명칭 변동 이력, 대표 출원인, 권리자 변동 이력 |
| **AI학습데이터** | 다수 | 특허 중한 코퍼스, 시소러스 |

### 해외 IP데이터

| 중분류 | 서비스 수 | 대표 서비스 |
|---|---|---|
| **해외공통** | 다수 | 해외특허, 해외디자인, 해외상표 |
| **일본** | 다수 | 일본 특허 합금조성비 |

---

## 5. 주요 API 오퍼레이션 (특허·실용 공개·등록공보 기준)

| # | 오퍼레이션명 | 분류 | 설명 |
|---|---|---|---|
| 1 | `getWordSearch` | 일반검색 | **단어 검색** (폐기예정, 비권장) |
| 2 | `getNumberSearch` | 일반검색 | **번호 검색** (폐기예정, 비권장) |
| 3 | `getAdvancedSearch` | 항목별검색 | **전체검색** — 복수 조건 조합 |
| 4 | `freeSearchInfo` | 항목별검색 | **자유검색** —テキスト自由形式 |
| 5 | `applicationNumberSearchInfo` | 항목별검색 | **출원번호 검색** |
| 6 | `cpcSearchInfo` | 항목별검색 | **CPC 분류 검색** |
| 7 | `itemTLSearchInfo` | 항목별검색 | **발명의 명칭 검색** |
| 8 | `itemABSearchInfo` | 항목별검색 | **초록 검색** |
| 9 | `itemCLSearchInfo` | 항목별검색 | **청구범위 검색** |
| 10 | `ipcSearchInfo` | 항목별검색 | **IPC 국제특허분류 검색** |
| 11 | `openNumberSearchInfo` | 항목별검색 | **공개번호 검색** |

---

## 6. 분류 유형 (API 분류 코드)

| 분류 코드 | 설명 |
|---|---|
| A | API 서비스 (실시간) |
| B | BULK 데이터 (기간제/선택형 일괄 제공) |

**중분류:**
- `공보` — 공개·등록 공보 관련
- `행정` — 행정처리 이력 관련
- `부가` — 부가 정보 (분류코드, 인명 등)
- `AI학습데이터` — AI 학습용 코퍼스
- `해외공통` — 해외 IP 데이터
- `일본` — 일본 특익 데이터

---

## 7. 유용한 링크 모음

### 데이터
- [↑ API 목록 처음부터 보기](https://plus.kipris.or.kr/portal/data/service/List.do?menuNo=200100&searchCondition=&clasKeyword=&orderTp=&subTab=SC001&entYn=N&pageIndex=1)
- [API 서비스 신청](https://plus.kipris.or.kr/portal/data/request/apiFsmtmList.do?menuNo=290005)
- [API 서비스 맵 (Beta)](https://plus.kipris.or.kr/portal/main/contents.do?menuNo=210167)
- [IP-BIZ 맵 (Beta)](https://plus.kipris.or.kr/portal/main/contents.do?menuNo=210166)

### 개발문서
- [API 통합설명서 (전체 오퍼레이션 카탈로그)](https://plus.kipris.or.kr/portal/main/contents.do?menuNo=210165)
- [API 상태 확인](https://plus.kipris.or.kr/portal/main/apiStatus.do?menuNo=210157)
- [활용사례집 PDF](https://plus.kipris.or.kr/sampledata/KIPRISPlus%20Service%20Use%20Samlpe.pdf)
- [IP정보 활용 길라잡이 PDF](https://plus.kipris.or.kr/sampledata/KIPRISPlus%20IP%20Information%20Guide.pdf)

### 회원/안내
- [로그인](https://plus.kipris.or.kr/portal/member/login.do?menuNo=200027)
- [회원가입](https://plus.kipris.or.kr/portal/member/joinView.do?menuNo=200028)
- [서비스 수수료 안내](https://plus.kipris.or.kr/portal/use/paymentMmg.do?menuNo=210112)
- [이용안내 — 가입 및 신청](https://plus.kipris.or.kr/portal/main/contents.do?menuNo=210104)
- [FAQ](https://plus.kipris.or.kr/portal/bbs/Faq_info.do?bbsId=B0000019&menuNo=210190)

### 공유/문의
- [공식 네이버 카페](http://cafe.naver.com/kipris)
- [카카오톡 채널](http://pf.kakao.com/_bhreG)
- [유튜브](https://www.youtube.com/watch?v=tucX7gD8MzM)
- [데이터 기프트 제도](https://plus.kipris.or.kr/portal/bbs/list.do?bbsId=B0000007&menuNo=200023)

### 연락처
- **기술문의:** 02-6915-1553 (평일 09:00~12:00, 13:00~18:00)
- **특허고객상담센터:** 1544-8080
- **주소:** 대전광역시 서구 청사로 136, 10층 (월평동, 대전무역회관)

---

## 8. Quick Reference — 가장 많이 쓰는 검색 예시

### 발명의 명칭으로 특허 검색
```http
GET /portal/openInfo/itemTLSearchInfo?
  appKey=YOUR_APP_KEY&
  patentNumber=1020200012345
```

### IPC 분류로 검색
```http
GET /portal/openInfo/ipcSearchInfo?
  appKey=YOUR_APP_KEY&
  ipcCode=H01L&
  dataType=JSON
```

### 출원번호로 검색
```http
GET /portal/openInfo/applicationNumberSearchInfo?
  appKey=YOUR_APP_KEY&
  applicationNumber=1020190123456
```

---

## 9. 참고 사항

- **무료 데이터Gift 제도:** 특정 조건 충족 시 무료로 데이터 제공 (사전 신청 필요)
- **BULK:** 대량 데이터가 필요하면 API 대신 벌크 데이터 서비스 이용 권장
- **갱신/비갱신:** 갱신 BULK은 주기적 업데이트, 비갱신은 스냅샷 형태
- **폐기예정 오퍼레이션:** `getWordSearch`, `getNumberSearch` 등 폐기 예정이므로 `getAdvancedSearch` 또는 `freeSearchInfo` 사용 권장
