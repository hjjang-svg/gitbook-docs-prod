---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# MMP로 광고 성과 측정하기

사용 중인 모바일 측정 파트너(MMP)를 토스애즈와 연동하면 광고를 통해 발생한 전환을 MMP에서 확인할 수 있어요. 토스애즈는 애드저스트, 앱스플라이어, 에어브릿지, 디파이너리, 브랜치, 싱귤러와 연동할 수 있어요.

MMP는 앱뿐 아니라 웹 측정도 지원할 수 있지만, 지원 범위와 설정 방법은 MMP마다 달라요. 사용 중인 MMP를 아래에서 선택하고 가이드에 따라 연동해 주세요.&#x20;

{% hint style="info" %}
**웹 광고 성과를 측정하려고 하나요?**

사용 중인 MMP가 웹 측정을 지원한다면 해당 MMP로 연동할 수 있어요. MMP 대신 토스 픽셀을 사용하려면 [토스 픽셀로 웹 광고 성과 측정하기](../tosspixel/)를 확인해 주세요.
{% endhint %}

## 이벤트

토스애즈에서 지원하는 표준 전환 이벤트는 아래와 같아요. 사용 중인 MMP에 따라 이벤트 설정과 매핑 방법이 다르므로, 각 [MMP의 연동 가이드](./#mmp)를 확인해 주세요.

| 토스애즈 이벤트 라벨         | 리포트 내 이벤트명 | 설명                |
| ------------------- | ---------- | ----------------- |
| AD\_IMPRESSION      | 인앱 광고 노출   | 광고 노출 (매출 발생)     |
| ADD\_TO\_CART       | 장바구니 담기    | 장바구니 상품 추가        |
| ADD\_TO\_WISHLIST   | 위시리스트 추가   | 상품 위시리스트 추가       |
| APP\_DEEPLINK\_OPEN | 딥링크 열기     | 딥링크를 통한 앱 실행      |
| APP\_OPEN           | 앱 열기       | 앱 실행              |
| FIRST\_PURCHASE     | 첫 구매       | 첫 구매 완료           |
| INITIATE\_CHECKOUT  | 결제 시작      | 결제/주문 페이지 진입      |
| INSTALL             | 앱 설치       | 앱 설치 완료           |
| LEAD\_COLLECTION    | 잠재 고객      | 상담 신청, 양식 제출      |
| LEVEL\_ACHIEVED     | 레벨 달성      | 특정 레벨 도달          |
| PRODUCT\_VIEW       | 상세페이지 조회   | 상품/콘텐츠 상세 페이지 조회  |
| PURCHASE            | 구매         | 결제 및 주문 완료(매출 발생) |
| SEARCH              | 검색         | 서비스 내 검색 결과 조회    |
| SIGNIN              | 로그인        | 로그인 완료            |
| SIGNUP              | 회원가입       | 회원가입 완료           |
| SUBSCRIBE           | 구독         | 알림 신청 / 구독 시작     |
| TUTORIAL            | 튜토리얼       | 튜토리얼 수행 결과        |
| VIEW\_HOME          | 홈 조회       | 홈 화면 방문           |

{% hint style="info" %}
**Adjust, Singular를 사용한다면 카탈로그 광고를 운영하기 전에 토스애즈에 요청해 주세요.**

카탈로그를 연동한 [구매 유도하기](../../a-d/purchase/) 광고는 사용자가 어떤 상품을 보고, 담고, 구매했는지 토스애즈가 알아야 운영할 수 있어요. Adjust, Singular는 이 상품 정보를 토스애즈에 기본으로 보내지 않아서, 토스애즈에서 추가 작업이 필요해요. 담당 AM에게 요청해 주세요.
{% endhint %}

{% hint style="warning" %}
**TUTORIAL, LEVEL\_ACHIEVED는 토스애즈에 별도로 요청해 주세요.**

Adjust, Branch, Singular를 사용하는 광고주가 게임 이벤트 중 TUTORIAL, LEVEL\_ACHIEVED를 연동하려면, MMP 설정과 별개로 토스애즈에서 추가 작업이 필요해요. 담당 AM에게 요청해 주세요.
{% endhint %}



## 파라미터

전환 이벤트와 함께 수집하는 파라미터는 아래와 같아요. 원본 파라미터명, 타입, 전달할 수 있는 항목은 MMP마다 다를 수 있으니 사용 중인 MMP의 연동 설정을 확인해 주세요.

| 파라미터명            | 타입     | 설명                          | 예시                                               |
| ---------------- | ------ | --------------------------- | ------------------------------------------------ |
| `category_id`    | String | 상품 카테고리 ID                  | `"C100"`                                         |
| `category_name`  | String | 상품 카테고리명                    | `"상의"`                                           |
| `currency`       | String | 통화 (ISO 4217 Currency Code) | `"KRW"`                                          |
| `custom_param1`  | String | Custom Parameter 1          | `"summer_sale"`                                  |
| `custom_param2`  | String | Custom Parameter 2          | `"landing_A"`                                    |
| `custom_param3`  | String | Custom Parameter 3          | `"variant_B"`                                    |
| `custom_param4`  | String | Custom Parameter 4          | `"member"`                                       |
| `custom_param5`  | String | Custom Parameter 5          | `"campaign_01"`                                  |
| `event_id`       | String | 전환 이벤트를 고유하게 식별하는 값         | `"ORD-20260722-001"`                             |
| `lead_type`      | String | 리드 유형                       | `"Consultation"`                                 |
| `level`          | String | `LEVEL_ACHIEVED` 이벤트의 달성 레벨 | `"10"`                                           |
| `order_id`       | String | 주문 ID                       | `"ORDER_20260423_0001"`                          |
| `price`          | Number | 상품 가격                       | `39000`                                          |
| `product_id`     | String | 상품 ID                       | `"P12345"`                                       |
| `product_name`   | String | 상품명                         | `"오가닉 코튼 티셔츠"`                                   |
| `products`       | Array  | 상품 목록                       | `[{ product_id: "P12345", category_id: "C100"}]` |
| `purchase_type`  | String | 결제 수단                       | `"naverpay"`                                     |
| `quantity`       | Number | 상품 개수                       | `2`                                              |
| `revenue`        | Number | 전체 상품 가격                    | `78000`                                          |
| `score`          | String | `LEVEL_ACHIEVED` 이벤트의 달성 점수 | `"1500"`                                         |
| `total_quantity` | Number | 전체 상품 개수                    | `2`                                              |



## MMP 연동 가이드

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>애드저스트</strong></td><td>전환 추적 코드를 만들고 애드저스트와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="adjust.md">adjust.md</a></td></tr><tr><td><strong>앱스플라이어</strong></td><td>전환 추적 코드를 만들고 앱스플라이어와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="appsflyer.md">appsflyer.md</a></td></tr><tr><td><strong>에어브릿지</strong></td><td>전환 추적 코드를 만들고 에어브릿지와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="airbridge.md">airbridge.md</a></td></tr><tr><td><strong>디파이너리</strong></td><td>전환 추적 코드를 만들고 디파이너리와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="dfinery.md">dfinery.md</a></td></tr><tr><td><strong>브랜치</strong></td><td>전환 추적 코드를 만들고 브랜치와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="branch.md">branch.md</a></td></tr><tr><td><strong>싱귤러</strong></td><td>전환 추적 코드를 만들고 싱귤러와 토스애즈를 연동하는 방법을 확인해요.</td><td><a href="singular.md">singular.md</a></td></tr></tbody></table>
