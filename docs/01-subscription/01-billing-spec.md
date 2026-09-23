# 01. 청구 연동규격서

> ⚠️ **필수옵션:** `M` 필수 | `O` 선택 | `X` 불필요 | `M/O` 응답 시 필수

## 1. 청구

적용 기관: **금결원 / 쿠콘 / 코밴 / 토스 / 네이버**

---

## 1.1 Master Info
> PG 요청 전문의 **Header와 Tail을 합친 항목**입니다.

| 구분 | Parameter | 한글명 | 금결원 | 쿠콘 | 코밴 | 토스 | 네이버 | Type | Max Size | 설명 | 비고 |
|---|---|---|:---:|:---:|:---:|:---:|:---:|---|---:|---|---|
| 요청 | `payment` | 정기청구 |  |  |  |  |  |  |  |  |
| 요청/응답 | `itrkDt` | 청구일자 | M | M | M | M | M | String | 8 | 기본 형태: `YYYYMMDD` | 금결원: `YYMMDD`, 코밴: `YYMMDD`, 쿠콘: `YYYYMMDD` |
| 요청/응답 | `itrkFlNm` | 연동파일명 | M | M | M | M | M | String | 60 | 연동파일명 | 연동파일명 Sheet 참조 |
| 응답 | `rsltFileCd` | 파일처리결과코드 | O | O | O | O | O | String | 2 | `TS`: 전체 성공, `PS`: 일부 성공, `TF`: 전체 실패, `IS`: PG 연동 성공 | EBP 제공 |
| 요청 | `var` | kftc/coocon<br>/kovan/toss<br>/naver |
| 요청/응답 | `totCnt` | 총건수 | M | M | M | M | M | String | 8 | 요청 파일의 총건수 | 숫자만 허용 |
| 요청/응답 | `totAmt` | 총금액 | M | M | M | M | M | String | 15 | 요청 파일의 금액 | 숫자만 허용 |
| 요청/응답 | `insttCd` | 기관코드 | M | M | X | X | X | String | 10 | 이용기관 식별코드 | 금결원/쿠콘 기관코드 |
| 요청/응답 | `bspnNo` | 가맹점 사업자번호 | X | X | M | X | M | String | 10 | 가맹점 사업자번호 | 네이버는 MID 사용 |
| 요청/응답 | `bnkCd` | 은행코드 | M | O | X | X | X | String | 7 | 은행 또는 주거래은행코드 | 금결원 7자리, 쿠콘 3자리 |
| 요청/응답 | `dpstAccntNo` | 입금계좌번호 | M | X | X | X | X | String | 16 | 기관의 수납모계좌번호 |  |
| 요청/응답 | `trsmDiv` | 송수신구분 | X | M | X | X | X | String | 2 | 출금: `B2`, 지급: `C2` |  |
| 요청/응답 | `debpEndDt` | 이체종료일자 | X | O | X | X | X | String | 8 | `YYYYMMDD` | Master Info의 `itrkDt` 대체 |
| 요청/응답 | `prntAccntNo` | 모계좌번호 | X | M | X | X | X | String | 16 | 쿠콘 5대 은행별 설정 |  |
| 요청/응답 | `dcrpSmbl` | 복기부호 | X | O | X | X | X | String | 10 | 이체 거래 인증 정보 |  |
| 요청/응답 | `replInsttCd` | 대표기관코드 | X | O | X | X | X | String | 10 | 대표기관 식별코드 |  |

> 응답 결과

| 구분 | Parameter | 한글명 | 금결원 | 쿠콘 | 코밴 | 토스 | 네이버 | Type | Max Size | 설명 | 비고 |
|---|---|---|:---:|:---:|:---:|:---:|:---:|---|---:|---|---|
| 응답 | `ebpErrCnt` | EBP 검증 오류 건수 | M/O | M/O | M/O | M/O | M/O | String | 8 | EBP 검증 오류 건수 | EBP 제공 |
| 응답 | `ebpErrAmt` | EBP 검증 오류 금액 | M/O | M/O | M/O | M/O | M/O | String | 15 | EBP 검증 오류 금액 | 금액 없을 시 `0` |
| 응답 | `aprvCnt` | 승인건수 | X | X | M/O | M/O | M/O | String | 8 | 승인 건수 | PG사 제공 |
| 응답 | `aprvAmt` | 승인금액 | X | X | M/O | M/O | M/O | String | 15 | 승인 금액 | PG사 제공 |
| 응답 | `rejCnt` | 거절건수 | X | X | M/O | M/O | M/O | String | 8 | 거절 건수 | PG사 제공 |
| 응답 | `rejAmt` | 거절금액 | X | X | M/O | M/O | M/O | String | 15 | 거절 금액 | PG사 제공 |
| 응답 | `wtdrCnt` | 전액출금(건수) | M/O | M/O | X | X | X | String | 8 | 전액출금 건수 | PG사 제공 |
| 응답 | `wtdrAmt` | 전액출금(금액) | M/O | M/O | X | X | X | String | 15 | 전액출금 금액 | PG사 제공 |
| 응답 | `partCnt` | 부분출금(건수) | X | M/O | X | X | X | String | 8 | 부분출금 건수 | PG사 제공 |
| 응답 | `partAmt` | 부분출금(금액) | X | M/O | X | X | X | String | 15 | 부분출금 처리 금액 | PG사 제공 |
| 응답 | `ipsbCnt` | 전액출금불능(건수) | M/O | M/O | X | X | X | String | 8 | 전액출금 불능 건수 | PG사 제공 |
| 응답 | `ipsbAmt` | 전액출금불능(금액) | M/O | M/O | X | X | X | String | 15 | 전액출금 불능 금액 | PG사 제공 |
| 응답 | `partIpsbCnt` | 부분출금불능(건수) | O | X | X | X | X | String | 8 | 부분출금 불능 건수 | PG사 제공 |
| 응답 | `partIpsbAmt` | 부분출금불능(금액) | O | X | X | X | X | String | 15 | 의뢰금액에서 실출금액을 차감한 합계 | PG사 제공 |
| 응답 | `cntrCnt` | 센터검증오류건수 | O | X | X | X | X | String | 8 | PG 검증 오류 건수 | PG사 제공 |
| 응답 | `wtdrBnkFee` | 출금 참가기관(은행) 수수료 | O | X | X | X | X | String | 11 | 출금 참가입행 수수료 | PG사 제공 |
| 응답 | `dpstBnkFee` | 입금 참가기관(은행) 수수료 | O | X | X | X | X | String | 11 | 입금 참가입행 수수료 | PG사 제공 |

---

## 2.1. Request List :개별 처리 요청 건 리스트

> Payment List

| 구분 | Parameter | 한글명 | 금결원 | 쿠콘 | 코밴 | 토스 | 네이버 | Type | Max Size | 설명 | 비고 |
|---|---|---|:---:|:---:|:---:|:---:|:---:|---|---:|---|---|
| 요청 | `payment` | 정기청구 |  |  |  |  |  |  |  |  |
| 응답 | `reqVrifyCd` | 요청검증결과코드 | M/O | M/O | M/O | M/O | M/O | String | 2 | 요청 개별 처리 결과 값<br>`PY`: 정상처리 완료<br>`PP`: 부분출금 처리<br>`PN`: PG처리오류, `rspsCd` 및 `rspsFailCd` 상세 확인 가능<br>`VE`: EBP 검증 오류 | 요청 개별 처리 결과 값<br>`PY`: 정상처리 완료<br>`PP`: 부분출금 처리<br>`PN`: PG처리오류, `rspsCd` 및 `rspsFailCd` 상세 확인 가능<br>`VE`: EBP 검증 오류 |
| 요청 | `var` | kftc/coocon<br>/kovan/toss<br>/naver |
| 요청/응답 | `eno` | 일련번호 | M | M | M | M | M | String | 8 | 요청 리스트의 키값 | 일련번호는 중복 허용하지 않음<br>중복 일련번호의 경우 전체 청구 요청 불가<br>Max Size: 금결원 8자리, 쿠콘 7자리 |
| 요청 | `pmtAmt` | 금액 | M | M | M | M | M | String | 13 | 출금의뢰금액 | 숫자만 허용<br>Max Size: 금결원 13자리, 쿠콘 13자리, 코밴 10자리 |
| 요청 | `trdDivCd` | 거래구분코드 | X | X | M | X | X | String | 1 | 신용승인: `A`, 체크승인: `C` | 코밴 AS-IS: `A` |
| 요청 | `cardNo` | 카드번호 | X | X | M | M | M | String | 16 | 네이버: 토큰 ID, 사용자가 결제수단 종류(카드/계좌)와 무관하게 `cardNo` 사용 | 숫자만 허용 |
| 요청 | `cardNo` | 카드번호 | X | X | M | M | X | String | 16 | 네이버: 토큰 ID, 사용자가 결제수단 종류(카드/계좌)와 무관하게 `cardNo` 사용 | 숫자만 허용 |
| 요청 | `paymentMethodId` | Token ID | X | X | X | X | M | String | 50 | 네이버: EBP에서 발행한 토큰 ID |  |
| 요청 | `vldTerm` | 유효기간 | X | X | M | M | X | String | 4 | `YYMM` | 숫자만 허용<br>코밴: 4자리 |
| 요청 | `istlMn` | 할부개월 | X | X | M | M | X | String | 2 | 카드결제 할부개월<br>토스: 2~12 사이의 값을 사용 가능<br>`0`: 일시불 결제, 결제 금액이 5만원 이상일 때만 할부 적용 | 코밴 AS-IS: `00`(일시불), 2자리<br>토스 AS-IS: `0`, 일시불<br>AS-IS: 코밴, 토스 일시불만 업무 존재 |
| 요청 | `crcdPass` | 카드비밀번호 | X | X | X | O | X | String | 2 | 카드비밀번호 2자리 |  |
| 요청 | `bnkCd` | 출금 참가기관(은행) 코드 | M | M | X | X | X | String | 7 | 은행코드: 전문수신 은행코드<br>쿠콘: 거래은행코드 | 금결원 최대 7자리<br>금결원 연동 규격: 전표 관리 불가능 시 은행코드 3자리만 SET, 나머지 4자리는 `0`으로 SET<br>쿠콘 최대 3자리<br>Max Size: 금결원 7자리, 쿠콘 3자리 |
| 요청 | `accntNo` | 출금계좌번호 | M | M | X | X | X | String | 16 |  | 하이픈(`-`) 입력, 숫자만 허용 |
| 요청 | `payerNo` | 납부자번호 | M | M | X | M | M | String | 20 | 출금이체 신청등록 시 납부자번호를 정확히 기재<br>토스: `usNo`(사용자번호)와 `payerNo` 일치<br>네이버: `usrNo`(사용자번호) | 쿠콘: 20자리<br>금결원: 20자리 |
| 요청 | `persNo` | 예금주 생년월일 또는 사업자등록번호 | M | X | X | M | X | String | 13 | 개인: 생년월일(`YYMMDD`)<br>사업자: 사업자번호 |  |
| 요청 | `fundKnd` | 자금종류 | O | X | X | X | X | String | 2 | 출금자금의 종류, 미사용 시 Space 처리 | 금결원 규격서: 미사용 시 SPACE<br>AS-IS: 공백으로 연동 |
| 요청 | `insttEtc` | 이용기관 사용영역 | O | X | X | X | X | String | 5 |  | PG사 제공 문구, 미사용 시 SPACE 처리<br>AS-IS: 공백으로 연동 |
| 요청 | `wtdrKnd` | 출금형태 | M | X | X | X | X | String | 1 | `0`: 부분출금 가능<br>`1`: ONLY 전액출금 | 금결원 AS-IS: `0`<br>TO-BE: 변동사항을 고려하여 필수값으로 반영 |
| 요청 | `telNo` | 전화번호(핸드폰) | O | X | X | X | X | String | 12 |  | 숫자만 허용, 하이픈(`-`) 생략 |
| 요청 | `kbkkCd` | 통장기장항목코드 | X | O | X | X | X | String | 4 | 통장기장항목코드 사용은행 | AS-IS: 공백으로 연동 |
| 요청 | `kbkkCtnt` | 통장기장내역 | O | O | X | X | X | String | 16 | 통장기장 사용은행, 은행에 따라 최대 길이가 다름 | 쿠콘 AS-IS: 14자리, 원지전자구독료, EUC-KR<br>금결원 AS-IS: 16자리, 원지전자구독료, EUC-KR<br>Max Size: 금결원 16자리, 쿠콘 14자리 |
| 요청 | `userId` | 사용자아이디 | X | X | X | O | X | String | 50 | 사용자(고객)를 관리하는 번호 | 공백으로 연동 가능 |
| 요청 | `prdtNm` | 상품명 | X | X | X | M | M | String | 200 | 상품명 연동, 정산기관비<br>네이버: 결제수단 등록 시 사용된 상품 코드와 정확히 일치해야 함 |  |
| 요청 | `emailId` | 이메일 아이디 | X | X | X | O | X | String | 100 |  | 공백으로 연동 가능<br>토스 연동 규격: 결제 상태가 바뀌면 이메일 주소로 결제내역 전송 |
| 요청 | `custNm` | 고객명 | X | X | X | M | X | String | 200 | 고객명 |  |

> 2.3 응답 정보

| 구분 | Parameter | 한글명 | 금결원 | 쿠콘 | 코밴 | 토스 | 네이버 | Type | Max Size | 설명 | 비고 |
|---|---|---|:---:|:---:|:---:|:---:|:---:|---|---:|---|---|
| 응답 | `rspsCd` | 응답코드 | X | X | M/O | M/O | M/O | String | 200 | 토스: `resultCode` | PG사 제공<br>코밴: 정상 `00`,<br>상세내용은 코밴 결과 확인 가능<br>토스: 정상 `00`,<br>상세내용은 토스 결과 확인 가능 |
| 응답 | `aprvNo` | 승인번호 | X | X | M/O | M/O | M/O | String | 200 | 인증/승인 키값<br>`billing`<br>`.pmtAddInfo`<br>`.cardAprvNo`또는 `pgAprvNo <->`<br>`lastTransactionKey`,<br>인증/승인 키값은<br>정상건은 2개 들어옴<br>토스:`cardAprvNo`<br>🔴 **네이버: `cardAuthNo`<br>(신용카드 결제가 포함된 경우)** | PG사 제공 |
| 응답 | `mrcntNo` | 가맹점번호 | X | X | M/O | X | M/O | String | 13 |  | PG사 제공 |
| 응답 | `aprvDt` | 승인일시 | X | X | M/O | X | M/O | String | 8 | `YYYYMMDD`<br>코밴: `HHMMSS` | PG사 제공 |
| 응답 | `wtdrRslt` | 출금결과<br>(출금여부) | M/O | M/O | X | X | X | String | 1 | 금결원: 성공 `Y`,<br>`N`/출금불능,<br>`P`/부분출금<br>쿠콘: 성공 `Y`,<br>`N`/ 출금불능,<br>`Z`/ 부분출금 | PG사 제공 |
| 응답 | `wtdrRsn` | 출금결과<br>(불능코드) | M/O | M/O | X | X | X | String | 4 | 출금불능 시 코드,<br>상세내용은 금결원 결과<br>또는 쿠콘 결과 확인 가능 | PG사 제공 |
| 응답 | `utrdAmt` | 미처리금액 | O | O | X | X | X | String | 13 | 의뢰금액-실출금액<br>쿠콘: `PP` 부분출금되지 않은 금액<br>금결원: `PP` 부분출금된 금액 | PG사 제공 |
| 응답 | `pmtKey` | PG거래번호 | X | X | X | M/O | M/O | String | 50 | PG거래번호<br>토스: `paymentKey`<br>네이버: `pgTrdNo` | PG사 제공 |
| 응답 | `ordId` | EBP주문번호 | X | X | X | M/O | M/O | String | 50 | EBP 처리번호(거래번호):`ordNo`<br>토스:`ordNo` |  |
| 응답 | `primaryAmount` | 주결제수단<br>결제금액 | X | X | X | X | M | String | 50 | 주결제수단 결제금액,<br>신용카드/계좌이체 | 네이버 결제전용 |
| 응답 | `npointAmount` | 네이버 포인트<br>결제금액 | X | X | X | X | M/O | String | 50 | 네이버 포인트 결제금액 | 네이버 결제전용 |
| 응답 | `cardNo` | 카드번호(masked) | X | X | X | X | M/O | String | 50 | 사용자가<br>주 결제수단으로<br>등록한 카드번호 | 네이버 결제전용 |
| 응답 | `cardCorpCode` | 카드회사코드 | X | X | X | X | M/O | String | 50 | 사용자가<br>주 결제수단으로<br>신용카드 회사코드를 등록 | 네이버 결제 전용<br><br>[주 결제수단 카드사](https://docs.pay.naver.com/docs/more-information/card-code/)<br>링크를 참고 바랍니다 |
| 응답 | `accountNo` | 계좌번호<br>(masked) | X | X | X | X | M/O | String | 50 | 사용자가<br>주 결제수단으로<br>등록한 계좌번호 | 네이버 결제전용 |
| 응답 | `bankcode` | 은행코드 | X | X | X | X | M/O | String | 50 | 사용자가<br>주 결제수단으로<br>등록한 계좌의 은행코드 | 네이버 결제 전용<br><br>[주 결제수단 은행](https://docs.pay.naver.com/docs/more-information/bank-code/)<br>링크를 참고 바랍니다 |

---
## 변경 이력

| 버전 | 변경일 | 변경 내용 | 작성자 |
|---|---|---|---|
| `v0.1.91` |26.09.23  | 최초 작성 | 이승용 |
