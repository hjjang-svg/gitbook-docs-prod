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

#### 이벤트&#x20;

| **이벤트명** | **이벤트 라벨**  | **설명**          |
| -------- | ----------- | --------------- |
| 페이지 방문   | pageView    | 모든 페이지 방문 시     |
| 회원가입     | signUp      | 회원가입 완료 시       |
| 상세페이지 조회 | productView | 상품 상세 페이지 조회 시  |
| 장바구니 담기  | addToCart   | 장바구니 추가 버튼 클릭 시 |
| 구매 완료    | purchase    | 구매 완료 페이지 도달 시  |
| 잠재고객 수   | lead        | 리드 제출 완료 시      |
| 커스텀 이벤트  | customevent | 자유롭게 정의 가능      |

#### 파라미터

* 스크립트의 파라미터 placeholder 값은 실제 데이터로 치환해요.
* 존재하지 않는 파라미터는 제외해서 전달할 수 있어요.
* 지원 파라미터를 함께 보내지 않아도 픽셀 이벤트 자체는 정상 발동해요.
* currency는 ISO 4217 Currency Code 형식으로 전달해야 (예: KRW, USD)

| **파라미터명**       | **타입** | **설명**                                              |
| --------------- | ------ | --------------------------------------------------- |
| order\_id       | String | 주문 ID                                               |
| product\_id     | String | 상품 ID                                               |
| product\_name   | String | 상품명                                                 |
| category\_id    | String | 상품 카테고리 ID                                          |
| category\_name  | String | 상품 카테고리명                                            |
| price           | Number | 상품 가격                                               |
| quantity        | Number | 상품 개수                                               |
| revenue         | Number | 전체 상품 가격                                            |
| total\_quantity | Number | 전체 상품 개수                                            |
| currency        | String | 통화 (ISO 4217 Currency Code 형식으로 전달 필요, 예: KRW, USD) |
| purchase\_type  | String | 결제 수단                                               |
| lead\_type      | String | 리드 유형                                               |
| products        | Array  | 상품 목록                                               |
| custom\_param1  | String | Custom Parameter 1                                  |
| custom\_param2  | String | Custom Parameter 2                                  |
| custom\_param3  | String | Custom Parameter 3                                  |
| custom\_param4  | String | Custom Parameter 4                                  |
| custom\_param5  | String | Custom Parameter 5                                  |

{% hint style="success" %}
&#x20;참고 사항

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
