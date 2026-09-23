# 네이버 구독관 연동 규격서

네이버 구독관의 매입 및 연체 내역 연동에 필요한 응답 규격을 정의합니다.

> ⚠️ **필수옵션:** `M` = 필수, `O` = 선택, `X` = 불필요, `M/O` = 응답 시 필수

---

## 1. 네이버 구독관 매입

### 1.1 Master Info

| 요청/결과 구분 | Parameter | 한글 파라미터명 | 필수 | Type | Max Size | 설명 |
|---|---|---|:---:|---|---:|---|
| 응답 | `sttl` | 정산내역 결과 |  |  |  |  |
| 응답 | `itrkDt` | 연동일자 | M | String | 8 | 기본 형태: `YYYYMMDD`<br>청구일자·결제일자 |
| 응답 | `itrkFlNm` | 연동파일명 | M | String | 60 |  |
| 응답 | `var` | Naver |  |  |  |  |
| 응답 | `slctDt` | 조회일자 | M | String | 10 | 정산 매출일 기준일 (`YYYYMMDD`) |
| 응답 | `totCnt` | 연동총건수 | M/O | String | 8 |  |

> Request List 개별 리스트 : 응답에만 존재하는 매입 리스트입니다.

| 요청/결과 구분 | Parameter | 한글 파라미터명 | 필수 | Type | Max Size | 설명 |
|---|---|---|:---:|---|---:|---|
| 응답 | `sttlList` | 매입리스트 |  |  |  |  |
| 응답 | `sno` | 처리순번 | M/O | String | 8 | DATA의 처리순번<br>토스의 청구 SNO와 불일치 |
| 응답 | `var` | sttlInfo |  |  |  |  |
| 응답 | `mId` | 상점아이디(MID) | M/O | String | 14 |  |
| 응답 | `pmtKey` | 결제의 키 값 | M/O | String | 200 | PG 거래번호 |
| 응답 | `contractNo` | 계약번호 | M/O | String | 64 | 계약번호 |
| 응답 | `amount` | 결제한 금액 | M/O | String | 10 | 결제 금액 |
| 응답 | `sellingInterlockCommissionAmount` | 수수료 금액 | M/O | String | 10 | 매출 연동 수수료<br>솔루션사용료 + 판매수수료 |
| 응답 | `totalPayCommissionAmount` | 수수료 금액 | M/O | String | 10 | 네이버페이 관련 수수료<br>주문관리 수수료 |
| 응답 | `payOutAmount` | 지급 금액 | M/O | String | 10 | `payOutAmount = amount - sellingInterlockCommissionAmount - totalPayCommissionAmount` |
| 응답 | `approvedAt` | 거래가 승인된 일시 | M/O | String | 30 | 승인일 (`YYYYMMDD`) |
| 응답 | `paidOutDate` | 정산 지급일 | M/O | String | 10 | 정산 지급일 (`YYYYMMDD`) |

---

## 2. 네이버 구독관 연체

### 2.1 Master Info

| 요청/결과 구분 | Parameter | 한글 파라미터명 | 필수 | Type | Max Size | 설명 |
|---|---|---|:---:|---|---:|---|
| 응답 | `sttl` | 정산내역 결과 |  |  |  |  |
| 응답 | `paymentRequestYmdFrom` | 연동일자 | M | String | 8 | 기본 형태: `YYYYMMDD`<br>결제 시작일<br>각월의 시작일 |
| 응답 | `paymentRequestYmdTo` | 연동일자 | M | String | 8 | 기본 형태: `YYYYMMDD`<br>결제 종료일<br>각월의 종료일 |
| 응답 | `itrkFlNm` | 연동파일명 | M | String | 60 |  |
| 응답 | `var` | Naver |  |  |  |  |

## 2. 네이버 구독관 연체

> ⚠️ **필수옵션:** `M` = 필수, `O` = 선택, `X` = 불필요, `M/O` = 응답 시 필수

### 2.1 Master Info

| 요청/결과 구분 | Parameter | 한글 파라미터명 | 필수 | Type | Max Size | 설명 |
|---|---|---|:---:|---|---:|---|
| 응답 | `sttl` | 정산내역 결과 |  |  |  |  |
| 응답 | `startDate` | 데이터 시작일<br>(결제 예정일 기준) | M | String | 8 | 기본 형태: `YYYYMMDD`<br>특정 구간(`startDate`~`endDate`)의 연체·미납 데이터 전달<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentRequestYmdFrom` |
| 응답 | `endDate` | 데이터 종료일<br>(결제 예정일 기준) | M | String | 8 | 기본 형태: `YYYYMMDD`<br>특정 구간(`startDate`~`endDate`)의 연체·미납 데이터 전달<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentRequestYmdTo` |
| 응답 | `itrkFNm` | 연동파일명 | M | String | 60 | `NAVER_SUB_UNPAID_시작일_종료일`<br>(`NAVER_SUB_UNPAID_YYMMDD_YYMMDD`) |
| 응답 | `var` | Naver |  |  |  |  |
| 응답 | `slctDt` | 조회일자 | M | String | 14 | EBP에서 네이버 데이터 조회 일자<br>(`YYYYMMDDHHMMSS`) |
| 응답 | `totCnt` | 연동총건수 | M | String | 8 |  |

### 2.2 Request List 개별 리스트

> 응답에만 존재하는 연체·미납 리스트입니다.

| 요청/결과 구분 | Parameter | 한글 파라미터명 | 필수 | Type | Max Size | 설명 |
|---|---|---|:---:|---|---:|---|
| 응답 | `sttlLst` | 매입리스트 |  |  |  |  |
| 응답 | `sno` | 처리순번 | M/O | String | 8 | DATA의 처리순번<br>청구의 SNO와 불일치 |
| 응답 | `var` | sttlInfo |  |  |  |  |
| 응답 | `mId` | 상점아이디(MID) | M/O | String | 14 |  |
| 응답 | `pmtKey` | 결제의 키 값 | M/O | String | 200 | PG 거래번호<br>네이버 API 월 렌탈료 수납 내역 조회의 `orderId` |
| 응답 | `contractNo` | 계약번호 | M/O | String | 64 | 계약번호 |
| 응답 | `recurrenceNumber` | 결제 회차 | M/O | String | 8 | 결제 회차(N회차 결제)<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentDegreeCount` |
| 응답 | `RequestAmount` | 결제 요청 금액 | M/O | String | 10 | 결제 요청 금액<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentRequestAmount` |
| 응답 | `StatusCode` | 결제 상태 코드 | M/O | String | 10 | 네이버 결제 상태 코드<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentStatusCode` |
| 응답 | `paymentRequestAt` | 결제 요청 일자 | M/O | String | 10 | 결제 요청 일자<br>네이버 API 월 렌탈료 수납 내역 조회의 `paymentRequestYmd` |

> 월별 수납 내역에서 미납 내역( unpaidYn  : true)만 전달
