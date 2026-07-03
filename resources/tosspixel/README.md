---
icon: pixelfed
---

# 토스 픽셀 연동하기

웹 캠페인을 운영한다면 웹사이트에 토스 픽셀을 설치하여, 전환 이벤트를 수집할 수 있어요.

토스 픽셀에서 지원하는 이벤트와 파라미터는 아래와 같아요.

{% hint style="warning" %}
* 현재 토스애즈 픽셀은 **자사몰**과 **카페24,메이크샵**을 지원해요.
* 브라우저 API 기반 SDK로, 네이티브 앱 환경에서는 동작하지 않아요.
{% endhint %}

***

#### 이벤트

| Toss Ads 이벤트 라벨     | 리포트 내 이벤트명 | 메서드명               | 설명                |
| ------------------- | ---------- | ------------------ | ----------------- |
| PURCHASE            | 구매         | purchase()         | 결제 및 주문 완료(매출 발생) |
| SIGNUP              | 회원가입       | signUp()           | 회원가입 완료           |
| LEAD\_COLLECTION    | 잠재 고객      | lead()             | 상담 신청, 양식 제출      |
| PRODUCT\_VIEW       | 상세페이지 조회   | productView()      | 상품/콘텐츠 상세 페이지 조회  |
| ADD\_TO\_CART       | 장바구니 담기    | addToCart()        | 장바구니 상품 추가        |
| INITIATE\_CHECKOUT  | 결제 시작      | initiateCheckout() | 결제/주문 페이지 진입      |
| INSTALL             | 앱 설치       | install()          | 앱 설치 완료           |
| APP\_OPEN           | 앱 열기       | appOpen()          | 앱 실행              |
| SEARCH              | 검색         | search()           | 서비스 내 검색 결과 조회    |
| SIGNIN              | 로그인        | signIn()           | 로그인 완료            |
| PAGE\_VIEW          | 페이지 조회     | pageView()         | 페이지 방문            |
| VIEW\_HOME          | 홈 조회       | viewHome()         | 홈 화면 방문           |
| FIRST\_PURCHASE     | 첫 구매       | firstPurchase()    | 첫 구매 완료           |
| GET\_OFFER          | 쿠폰 다운로드    | getOffer()         | 쿠폰 다운로드 / 혜택 수령   |
| ADD\_TO\_WISHLIST   | 위시리스트 추가   | addToWishlist()    | 상품 위시리스트 추가       |
| SUBSCRIBE           | 구독         | subscribe()        | 알림 신청 / 구독 시작     |
| APP\_DEEPLINK\_OPEN | 딥링크 열기     | appDeeplinkOpen()  | 딥링크를 통한 앱 실행      |
| PRE\_REGISTER       | 사전 예약      | preRegister()      | 사전 예약 / 런칭 전 등록   |
| VIEW\_LIMIT         | 한도 조회      | viewLimit()        | 대출/보험료 한도 조회      |
| APPLY\_SCREENING    | 가심사 조회     | applyScreening()   | 가심사 조회 / 적격 확인    |
| AD\_IMPRESSION      | 인앱 광고 노출   | adImpression()     | 광고 노출 (매출 발생)     |
| -                   | 커스텀 이벤트    | custom()           | 자유롭게 정의 가능        |

#### 파라미터

* 스크립트의 파라미터 placeholder 값은 실제 데이터로 치환해요.
* 존재하지 않는 파라미터는 제외해서 전달할 수 있어요.
* 지원 파라미터를 함께 보내지 않아도 픽셀 이벤트 자체는 정상 발동해요.
* currency는 ISO 4217 Currency Code 형식으로 전달해야 (예: KRW, USD)

| 파라미터명           | 타입     | 설명                          | 예시                                                |
| --------------- | ------ | --------------------------- | ------------------------------------------------- |
| order\_id       | String | 주문 ID                       | "ORDER\_20260423\_0001"                           |
| product\_id     | String | 상품 ID                       | "P12345"                                          |
| product\_name   | String | 상품명                         | "오가닉 코튼 티셔츠"                                      |
| category\_id    | String | 상품 카테고리 ID                  | "C100"                                            |
| category\_name  | String | 상품 카테고리명                    | "상의"                                              |
| price           | Number | 상품 가격                       | 39000                                             |
| quantity        | Number | 상품 개수                       | 2                                                 |
| revenue         | Number | 전체 상품 가격                    | 78000                                             |
| total\_quantity | Number | 전체 상품 개수                    | 2                                                 |
| currency        | String | 통화 (ISO 4217 Currency Code) | "KRW"                                             |
| purchase\_type  | String | 결제 수단                       | "naverpay"                                        |
| lead\_type      | String | 리드 유형                       | "Consultation"                                    |
| products        | Array  | 상품 목록                       | \[{ product\_id: "P12345", category\_id: "C100"}] |
| custom\_param1  | String | Custom Parameter 1          | "summer\_sale"                                    |
| custom\_param2  | String | Custom Parameter 2          | "landing\_A"                                      |
| custom\_param3  | String | Custom Parameter 3          | "variant\_B"                                      |
| custom\_param4  | String | Custom Parameter 4          | "member"                                          |
| custom\_param5  | String | Custom Parameter 5          | "campaign\_01"                                    |

{% hint style="success" %}
참고 사항

모든 파라미터는 선택사항이므로, 파라미터 없이 메서드만 호출해도 이벤트는 정상적으로 수집되지만,

파라미터를 충실히 전달할수록 광고 성과 분석의 정밀도가 높아지므로 가능한 한 포함하는 것을 권장해요.
{% endhint %}

{% content-ref url="self-hosted.md" %}
[self-hosted.md](self-hosted.md)
{% endcontent-ref %}

{% content-ref url="24.md" %}
[24.md](24.md)
{% endcontent-ref %}

{% content-ref url="makeshop.md" %}
[makeshop.md](makeshop.md)
{% endcontent-ref %}
