# 전환 이벤트

토스애즈에서 지원하는 표준 전환 이벤트는 아래와 같아요.

| Toss Ads 이벤트 라벨     | 리포트 내 이벤트명 | 설명                |
| ------------------- | ---------- | ----------------- |
| PURCHASE            | 구매         | 결제 및 주문 완료(매출 발생) |
| SIGNUP              | 회원가입       | 회원가입 완료           |
| LEAD\_COLLECTION    | 잠재 고객      | 상담 신청, 양식 제출      |
| PRODUCT\_VIEW       | 상세페이지 조회   | 상품/콘텐츠 상세 페이지 조회  |
| ADD\_TO\_CART       | 장바구니 담기    | 장바구니 상품 추가        |
| INITIATE\_CHECKOUT  | 결제 시작      | 결제/주문 페이지 진입      |
| INSTALL             | 앱 설치       | 앱 설치 완료           |
| APP\_OPEN           | 앱 열기       | 앱 실행              |
| SEARCH              | 검색         | 서비스 내 검색 결과 조회    |
| SIGNIN              | 로그인        | 로그인 완료            |
| PAGE\_VIEW          | 페이지 조회     | 페이지 방문            |
| VIEW\_HOME          | 홈 조회       | 홈 화면 방문           |
| FIRST\_PURCHASE     | 첫 구매       | 첫 구매 완료           |
| GET\_OFFER          | 쿠폰 다운로드    | 쿠폰 다운로드 / 혜택 수령   |
| ADD\_TO\_WISHLIST   | 위시리스트 추가   | 상품 위시리스트 추가       |
| SUBSCRIBE           | 구독         | 알림 신청 / 구독 시작     |
| APP\_DEEPLINK\_OPEN | 딥링크 열기     | 딥링크를 통한 앱 실행      |
| PRE\_REGISTER       | 사전 예약      | 사전 예약 / 런칭 전 등록   |
| VIEW\_LIMIT         | 한도 조회      | 대출/보험료 한도 조회      |
| APPLY\_SCREENING    | 가심사 조회     | 가심사 조회 / 적격 확인    |
| AD\_IMPRESSION      | 인앱 광고 노출   | 광고 노출 (매출 발생)     |

* 이벤트별 상세 연동 예시와 파라미터 설명은 각 연동 문서에서 확인할 수 있어요.
  * 웹 전용 이벤트의 상세 구현 방법은 [토스 픽셀 연동 가이드](https://toss-ads.gitbook.io/guide/resources/tosspixel)를 참고해 주세요.
  * 앱 전용 이벤트의 상세 구현 방법은 [MMP 연동 가이드](https://toss-ads.gitbook.io/guide/resources/mat)를 참고해 주세요.
