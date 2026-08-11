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
---

# 자사몰 픽셀 연동

아래 가이드는 직접 구축한 자사몰에 토스 픽셀을 설치하는 방법을 안내해요.

[카페24](24.md), [메이크샵](makeshop.md) 등 쇼핑몰 솔루션을 사용 중이라면 플랫폼별 설치 가이드를 참고해 주세요.

***

## 토스 픽셀 설치하기

토스 픽셀을 설치하려면 전환 코드가 필요해요.

전환 코드는 토스애즈 대시보드에서 발급할 수 있고, 광고계정마다 고유하게 부여돼요.

전환 코드 발급 방법은 [전환 코드 발급](../tag/code_generation.md) 가이드를 참고해 주세요.

{% stepper %}
{% step %}
**SDK 스크립트 설치**

모든 페이지에 공통으로 적용되는 레이아웃 파일의 \<head>태그 안에 아래 스크립트를 추가해 주세요.

{% code overflow="wrap" %}
```javascript
<head>
    <!-- 기존 태그들 -->
    <script src="https://static.toss.im/lex/v1.js"></script>
</head>
```
{% endcode %}

* SDK 스크립트는 사이트 전체에서 한 번만 로딩하면 돼요. 각 이벤트 코드마다 다시 넣을 필요는 없어요.
* SDK 스크립트에는 async 또는 defer 속성을 사용하지 마세요. 이벤트 코드보다 먼저 로딩되어야 해요.
* SDK 로딩에 실패하더라도 쇼핑몰의 기본 동작에는 영향을 주지 않아요.
{% endstep %}

{% step %}
**이벤트 스크립트 삽입**

전환이 발생하는 지점에 아래 이벤트 스크립트를 추가해 주세요.

토스 픽셀이 지원하는 이벤트와 파라미터는 아래와 같아요.

**이벤트**

| 리포트 내 이벤트명 | 메서드명               | 설명                |
| ---------- | ------------------ | ----------------- |
| 구매         | purchase()         | 결제 및 주문 완료(매출 발생) |
| 회원가입       | signUp()           | 회원가입 완료           |
| 잠재 고객      | lead()             | 상담 신청, 양식 제출      |
| 상세페이지 조회   | productView()      | 상품/콘텐츠 상세 페이지 조회  |
| 장바구니 담기    | addToCart()        | 장바구니 상품 추가        |
| 결제 시작      | initiateCheckout() | 결제/주문 페이지 진입      |
| 검색         | search()           | 서비스 내 검색 결과 조회    |
| 로그인        | signIn()           | 로그인 완료            |
| 페이지 조회     | pageView()         | 페이지 방문            |
| 홈 조회       | viewHome()         | 홈 화면 방문           |
| 첫 구매       | firstPurchase()    | 첫 구매 완료           |
| 쿠폰 다운로드    | getOffer()         | 쿠폰 다운로드 / 혜택 수령   |
| 위시리스트 추가   | addToWishlist()    | 상품 위시리스트 추가       |
| 구독         | subscribe()        | 알림 신청 / 구독 시작     |
| 사전 예약      | preRegister()      | 사전 예약 / 런칭 전 등록   |
| 한도 조회      | viewLimit()        | 대출/보험료 한도 조회      |
| 가심사 조회     | applyScreening()   | 가심사 조회 / 적격 확인    |
| 커스텀 이벤트    | custom()           | 자유롭게 정의 가능        |

**파라미터**

| 파라미터명           | 타입     | 설명                          | 예시                                                |
| --------------- | ------ | --------------------------- | ------------------------------------------------- |
| event\_id       | String | 전환 이벤트를 고유하게 식별하는 값         | "ORD-20260722-001"                                |
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

{% hint style="info" %}
모든 이벤트의 파라미터는 선택사항이에요.

파라미터 없이 메서드만 호출해도 정상 수집돼요.

다만, 파라미터를 함께 전달하면 광고 성과를 더 정확하게 분석할 수 있어요.
{% endhint %}
{% endstep %}
{% endstepper %}

***

### event\_id로 전환 이벤트 식별하기

event\_id는 수집된 전환 이벤트 하나하나를 구분하는 고유 값이에요. 모든 이벤트에 함께 보낼 수 있어요.

**기본 규칙**

* 같은 전환을 가리키는 이벤트에는 **같은 의미를 가진 값**을 넣어주세요.
* 발생한 전환 이벤트에는 **서로 다른 값**을 넣어주세요.
* 같은 전환추적코드로 보내는 이벤트끼리 겹치지 않으면 돼요. 다른 광고주와 값이 겹치는 건 괜찮아요.
* 다른 파라미터와 마찬가지로 선택사항이에요. 값 없이 보내도 이벤트는 정상적으로 수집돼요.

**어떤 값을 쓰면 되나요**

이미 서비스에 존재하는 유일 값을 그대로 쓰는 걸 가장 권장해요.

| 이벤트 성격   | 권장 값             | 예시                        |
| -------- | ---------------- | ------------------------- |
| 구매·결제    | 주문번호, 결제 트랜잭션 ID | "ORD-20260722-001"        |
| 리드·양식 제출 | 폼 제출 ID          | "LEAD-20260722-0031"      |
| 회원가입·로그인 | 가입/세션 처리 ID      | "SIGNUP-20260722-0142"    |
| 조회·클릭 등  | 서비스에서 직접 만든 유일 값 | "PV-20260722-093245-4c1b" |

**어떻게 보내나요**

다른 파라미터와 동일하게 파라미터 객체 안에 event\_id를 넣어주세요.

```html
<script>
  TossPixel('전환 코드').purchase({
    event_id: "ORD-20260722-001",
    order_id: "ORD-20260722-001",
    revenue: 78000,
    total_quantity: 2,
    currency: "KRW"
  });
</script>
```

{% hint style="info" %}
order\_id는 리포트에서 주문을 확인하기 위한 파라미터이고, event\_id는 이벤트 자체를 식별하는 값이에요.&#x20;

구매 이벤트라면 두 값에 같은 주문번호를 넣어도 괜찮아요.
{% endhint %}

### 이벤트 스크립트 예시

아래 예시는 표준 이벤트 / 표준 파라미터 활용 방식을 이해하기 위한 샘플이에요.

실제 연동 시에는 자사 서비스 구조와 수집 가능한 데이터에 맞게 필요한 파라미터만 선택해서 적용해 주세요.

#### 구매 purchase()

결제 및 주문이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').purchase({
    event_id: "ORD-20260722-001",
    order_id: "ORDER_20260423_0001",
    revenue: 78000,
    total_quantity: 2,
    currency: "KRW",
    purchase_type: "CARD",
    products: [ /* ... 기존과 동일 ... */ ],
    custom_param1: "member_purchase",
    custom_param2: "spring_campaign"
  });
</script>
```

#### 회원가입 signUp()

회원가입이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').signUp({
    event_id: "SIGNUP-20260722-0142",
    custom_param1: "email",
    custom_param2: "normal_signup"
  });
</script>
```

#### 잠재 고객 lead()

상담 신청, 양식 제출 등 리드 수집이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').lead({
    event_id: "LEAD-20260722-0031",
    lead_type: "Consultation",
    custom_param1: "insurance",
    custom_param2: "landing_form"
  });
</script>
```

**lead\_type**

* lead\_type 원하는 문자열을 자유롭게 입력할 수 있어요. 아래는 업종별 권장 값이에요.

| 리드 유형   | 권장 값         |
| ------- | ------------ |
| 이벤트 참여  | Event        |
| 상담 신청   | Consultation |
| 시승 신청   | TestDrive    |
| 무료체험 신청 | FreeTrial    |
| 사전예약    | Preorder     |
| 보험료 조회  | QuoteCheck   |
| 대출한도 조회 | LoanCheck    |

#### 상세페이지 조회 productView()

상품 또는 콘텐츠 상세 페이지를 조회한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').productView({
    event_id: "PV-20260722-093245-4c1b",
    product_id: "P12345",
    product_name: "오가닉 코튼 티셔츠",
    category_id: "C100",
    category_name: "상의",
    price: 39000,
    currency: "KRW"
  });
</script>
```

#### 장바구니 담기 addToCart()

상품을 장바구니에 추가한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').addToCart({
    event_id: "CART-20260722-093512-7a2e",
    revenue: 78000,
    total_quantity: 2,
    currency: "KRW",
    products: [ /* ... 기존과 동일 ... */ ],
    custom_param1: "cart_button"
  });
</script>
```

#### 결제 시작 initiateCheckout()

결제/주문 페이지에 진입한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').initiateCheckout({
    event_id: "CHK-20260722-0087",
    order_id: "ORDER_20260423_0001",
    revenue: 78000,
    total_quantity: 2,
    currency: "KRW",
    products: [ /* ... 기존과 동일 ... */ ],
    custom_param1: "checkout_page"
  });
</script>
```

#### 검색 search()

서비스 내 검색 결과를 조회한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').search({
    event_id: "SRCH-20260722-093820-9e5f",
    category_id: "C100",
    category_name: "상의",
    custom_param1: "오가닉 코튼 티셔츠",
    custom_param2: "search_result"
  });
</script>
```

#### 로그인 signIn()

로그인이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').signIn({
    event_id: "SIGNIN-20260722-093412-8f3a",
    custom_param1: "email",
    custom_param2: "existing_user"
  });
</script>
```

#### 페이지 조회 pageView()

페이지를 방문한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').pageView({
    event_id: "PAGE-20260722-093010-1a7c",
    custom_param1: "all_page",
    custom_param2: "web"
  });
</script>
```

#### 홈 조회 viewHome()

홈 화면을 방문한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').viewHome({
    event_id: "HOME-20260722-092955-3d8e",
    custom_param1: "main_home",
    custom_param2: "logged_in"
  });
</script>
```

#### 첫 구매 firstPurchase()

첫 구매가 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').firstPurchase({
    event_id: "ORD-20260722-002",
    order_id: "ORDER_20260423_0002",
    revenue: 39000,
    total_quantity: 1,
    currency: "KRW",
    purchase_type: "CARD",
    products: [ /* ... 기존과 동일 ... */ ],
    custom_param1: "new_buyer"
  });
</script>
```

#### 쿠폰 다운로드 getOffer()

쿠폰 다운로드 또는 혜택 수령 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').getOffer({
    event_id: "OFFER-20260722-0221",
    custom_param1: "WELCOME10",
    custom_param2: "download_coupon"
  });
</script>
```

#### 위시리스트 추가 addToWishlist()

상품을 위시리스트에 추가한 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').addToWishlist({
    event_id: "WISH-20260722-094010-2b9d",
    product_id: "P12345",
    product_name: "오가닉 코튼 티셔츠",
    category_id: "C100",
    category_name: "상의",
    price: 39000,
    quantity: 1,
    currency: "KRW"
  });
</script>
```

#### 구독 subscribe()

알림 신청 또는 구독이 시작된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').subscribe({
    event_id: "SUB-20260722-0455",
    lead_type: "Newsletter",
    custom_param1: "push_opt_in",
    custom_param2: "app"
  });
</script>
```

#### 사전 예약 preRegister()

사전 예약 또는 런칭 전 등록이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').preRegister({
    event_id: "PRE-20260722-0113",
    product_id: "PRD_PRE_001",
    product_name: "신규 멤버십",
    lead_type: "Preorder",
    custom_param1: "launch_campaign"
  });
</script>
```

#### 한도 조회 viewLimit()

대출/보험료 한도 조회가 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').viewLimit({
    event_id: "LIMIT-20260722-0762",
    lead_type: "LoanCheck",
    custom_param1: "credit_loan",
    custom_param2: "mobile_web"
  });
</script>
```

#### 가심사 조회 applyScreening()

가심사 조회 또는 적격 확인이 완료된 시점에 호출해 주세요.

```html
<script>
  TossPixel('전환 코드').applyScreening({
    event_id: "SCR-20260722-0338",
    lead_type: "PreScreening",
    custom_param1: "mortgage",
    custom_param2: "qualified_check"
  });
</script>
```

***

#### 커스텀 이벤트 (custom)

* 표준 이벤트에 해당하지 않는 전환을 추적할 때 사용해요.
* 이벤트명은 직접 지정할 수 있고, 표준 이벤트와 같은 파라미터를 사용할 수 있어요.

{% code overflow="wrap" %}
```html
<script>
  TossPixel('전환 코드').custom('BUTTON_CLICK', {
    event_id: "BTN-20260722-095012-6f4a",
    product_id: "P12345",
    product_name: "오가닉 코튼 티셔츠",
    category_id: "C100",
    price: 39000,
    currency: "KRW"
  });
</script>
```
{% endcode %}

**파라미터**

| 파라미터                | 타입     | 필수 | 설명                                         |
| ------------------- | ------ | -- | ------------------------------------------ |
| eventName (첫 번째 인자) | string | 필수 | 이벤트명 (예: "BUTTON\_CLICK", "WISHLIST\_ADD") |
| params (두 번째 인자)    | object | 선택 | 이벤트에 포함할 추가 데이터                            |

* 두 번째 인자에는 product\_id, price, currency 등 표준 이벤트에서 사용하는 파라미터를 전달할 수 있어요.
* 추적하려는 전환에 맞는 값을 선택해 포함해 주세요.

{% hint style="info" %}
**표준 이벤트와의 차이**

* 표준 이벤트는 메서드명이 곧 이벤트명이에요.
* 커스텀 이벤트는 첫 번째 인자에 이벤트명을 직접 입력해요
  * **그 외 파라미터 사용 방식은 동일해요.**
{% endhint %}

***

#### 커스텀 프로퍼티

* 모든 이벤트(표준 이벤트, 커스텀 이벤트)에 custom\_param1 \~ custom\_param5를 추가할 수 있어요.
* product\_id, price 같은 표준 파라미터로 표현하기 어려운 추가 정보를 전달할 때 사용해요.
  * 예를 들어, 캠페인 구분값, 프로모션 코드, A/B 테스트 그룹, 유입 경로 등 필요에 따라 정의한 값을 담을 수 있어요.

```html
<!-- 표준 이벤트에 커스텀 프로퍼티 추가 -->
<script>
    TossPixel('전환 코드').purchase({
        event_id: "ORD-20260722-003",
        revenue: 78000,
        currency: "KRW",
        custom_param1: "summer_sale",
        custom_param2: "landing_A"
    });
</script>

<!-- 커스텀 이벤트에 커스텀 프로퍼티 추가 -->
<script>
    TossPixel('전환 코드').custom('BUTTON_CLICK', {
        event_id: "BTN-20260722-095430-3c8b",
        product_id: "P12345",
        custom_param1: "cta_top",
        custom_param2: "variant_B"
    });
</script>
```

* 커스텀 프로퍼티는 최대 5개까지 사용할 수 있고, 표준 파라미터와 함께 하나의 객체로 전달해 주세요.

| 프로퍼티           | 타입     | 설명         |
| -------------- | ------ | ---------- |
| custom\_param1 | string | 커스텀 프로퍼티 1 |
| custom\_param2 | string | 커스텀 프로퍼티 2 |
| custom\_param3 | string | 커스텀 프로퍼티 3 |
| custom\_param4 | string | 커스텀 프로퍼티 4 |
| custom\_param5 | string | 커스텀 프로퍼티 5 |

***

#### SPA(Single Page Application) 환경

*   React, Next.js, Vue 등 SPA 프레임워크를 사용하는 경우,페이지 이동 시 HTML이 새로 로딩되지 않아요.

    따라서 라우트가 변경되는 시점에 이벤트를 직접 호출해 주세요.

- [x] React 예시

{% code overflow="wrap" %}
```javascript
import { useEffect } from 'react';
import { useLocation } from 'react-router-dom';

function usePageView() {
    const location = useLocation();

    useEffect(() => {
        TossPixel('전환 코드').pageView({
            event_id: "PAGE-20260722-093010-1a7c"
        });
    }, [location.pathname]);
}
```
{% endcode %}

* TossPixel 객체는 1단계에서 추가한 SDK 스크립트(v1.js)가 window에 등록해요. SPA 환경에서도 SDK 스크립트는 index.html의 \<head>에 한 번만 추가하면 돼요.

***

## 설치 확인

토스 픽셀이 정상적으로 설치되었는지 아래 방법으로 확인할 수 있어요.

1. Toss Pixel Helper 크롬 확장프로그램

[Toss Pixel Helper](https://chromewebstore.google.com/detail/toss-pixel-helper/kbbggbgnfmbpjpaieklnbbjfkjkkpcbi?hl=ko\&gl=US\&pli=1)를 설치하면, 현재 페이지에서 수집된 토스 픽셀 이벤트를 실시간으로 확인할 수 있어요.

자세한 사용 방법은 [픽셀 이벤트 수집 확인하기](pixel_event.md) 페이지를 참고해주세요.

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

***

## 자주 묻는 질문

**Q. SDK 스크립트 로딩이 실패하면 쇼핑몰에 영향이 있나요?**

A. 영향은 없어요. SDK 로딩이 실패하면 TossPixel 호출만 무시되고, 쇼핑몰의 정상 동작에는 영향을 주지 않아요.

**Q. 구매 완료 페이지에서 새로고침하면 이벤트가 중복 전송되나요?**

A. 중복 전송될 수 있어요. 주문 완료 여부를 서버에서 한 번 더 확인하거나, 주문 ID 기준으로 중복 호출을 막는 처리가 필요해요.

**Q. 파라미터를 보내지 않아도 되나요?**

A. 가능해요. 모든 파라미터는 선택사항이에요. 메서드만 호출해도 정상 수집돼요.

다만, 파라미터를 함께 전달하면 광고 성과를 더 정확하게 분석할 수 있어요.

**Q. event\_id는 꼭 보내야 하나요?**

A. 필수는 아니에요. 다른 파라미터와 마찬가지로 선택사항이라 값 없이 보내도 이벤트는 정상적으로 수집돼요. 다만 광고주 시스템의 주문·리드 데이터와 수집된 이벤트를 대조하려면 채워서 보내는 걸 권장해요.

**Q. event\_id는 어떤 값으로 만들어야 하나요?**

A. 같은 전환추적코드로 보내는 이벤트끼리 겹치지 않는 값이면 돼요. 주문번호, 결제 트랜잭션 ID, 리드 폼 제출 ID처럼 이미 서비스에 있는 유일 값을 그대로 쓰는 걸 권장해요. 다른 광고주와 값이 겹치는 건 괜찮아요.

**Q. 조회 이벤트처럼 고유 ID가 없는 경우에는요?**

A. 서비스에서 겹치지 않는 값을 직접 만들어 넣어주세요. 값을 만들기 어렵다면 `event_id` 없이 보내도 이벤트는 정상적으로 수집돼요.

**Q. order\_id가 있는데 event\_id를 또 보내야 하나요?**

A. `order_id`는 리포트에서 주문을 확인하기 위한 파라미터이고, `event_id`는 이벤트 자체를 식별하는 값이라 역할이 달라요. 구매 이벤트라면 두 값에 같은 주문번호를 넣어도 괜찮아요.
