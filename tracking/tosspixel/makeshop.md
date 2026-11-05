---
hidden: true
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

# 메이크샵 픽셀 연동

메이크샵 쇼핑몰에 토스 픽셀을 설치하는 방법을 안내해요.

직접 구축한 자사몰은 [자사몰 픽셀 연동](https://toss-ads.gitbook.io/guide/tracking/tosspixel/preservationguide-1), 카페24는 [카페24 픽셀 연동](https://toss-ads.gitbook.io/guide/tracking/tosspixel/24)을 참고해 주세요.

## 토스 픽셀 설치하기

{% hint style="info" %}
#### **전환 추적 코드 생성하기**

* **토스 픽셀**은 [전환 추적 코드 생성하기 가이드](https://toss-ads.gitbook.io/guide/tracking/tag/code_generation)에 따라 **전환 추적 코드를 생성한 후에 사용**할 수 있어요. 생성한 전환 추적 코드는 반드시 따옴표(`' '` 또는 `" "`)로 감싸서 이벤트 스크립트에 입력해 주세요.
* 예시의 `"전환 코드"` 부분을 생성한 실제 값으로 바꾸고, 따옴표는 그대로 유지해 주세요.
{% endhint %}

### 이벤트별 스크립트

토스 픽셀이 지원하는 이벤트 목록은 아래와 같아요.

이벤트 중에서 추적하고 싶은 이벤트만 메이크샵 코드 편집기에 삽입해 주세요.

| 이벤트      | 메서드명          | 삽입 위치           |
| -------- | ------------- | --------------- |
| 페이지 방문   | pageView()    | 모든 페이지          |
| 회원가입     | signUp()      | 회원가입 완료 페이지     |
| 상품 상세 조회 | productView() | 상품 상세 페이지       |
| 장바구니 담기  | addToCart()   | 장바구니 추가 버튼 클릭 시 |
| 구매       | purchase()    | 구매 완료 페이지       |
| 커스텀 이벤트  | custom()      | 자유롭게 정의         |

이벤트 스크립트 코드는 전환이 실제로 일어나는 시점에 맞춰 넣어야 해요. 그래야 전환 데이터를 정확하게 모을 수 있어요.

예를 들어 사용자가 상품 상세 페이지를 본 뒤 장바구니에 담는 과정을 추적하려면 아래처럼 넣으면 돼요.

1.  상품 상세 페이지에

    “상품/콘텐츠 상세페이지 조회” 이벤트 스크립트를 넣어요.
2.  장바구니 담기 버튼을 클릭할 때

    “장바구니 담기” 이벤트 스크립트를 실행되게 넣어요.

이렇게 하면 두 이벤트를 모두 추적할 수 있어요.

***

### event\_id로 전환 이벤트 식별하기

`event_id`는 **같은 이벤트가 여러 번 전송됐을 때 이를 중복으로 판단하기 위한 값**이에요. 예를 들어 한 번의 구매에 대한 이벤트가 여러 번 전송되더라도 같은 `event_id`를 사용하면 중복 집계를 방지할 수 있어요.

**기본 규칙**

* **같은 이벤트를 다시 보낼 때는 정확히 같은 값을 사용해 주세요.** 같은 이벤트를 다시 전송한다면 처음 사용한 `event_id`를 그대로 전달해 주세요.
* **별도로 발생한 이벤트에는 서로 다른 값을 사용해 주세요.** 같은 고객이 같은 상품을 다시 구매해도 별개의 구매 이벤트이므로 새로운 값이 필요해요. 고객 ID나 상품 ID만으로는 이를 구분할 수 없어요.
* **이벤트가 발생할 때 값을 한 번 정하고, 다시 전송할 때도 유지해 주세요.** 구매라면 `purchase-주문번호`처럼 구성할 수 있어요. 임의의 고유 값을 생성하는 경우에도 전송할 때마다 새로 만들지 말고 그 이벤트와 함께 저장해 재사용해 주세요.
* **`event_id`는 광고주가 직접 설정해야 해요.** 픽셀이 자동으로 생성하거나 주문번호를 대신 넣어주지는 않아요.
* **선택 사항이므로 생략해도 이벤트를 보낼 수 있어요.** 다만 `event_id`를 이용해 중복을 제거하려면 같은 이벤트를 전송할 때마다 동일한 값을 전달해야 해요.

**어떤 값을 쓰면 되나요**

이미 서비스에 있는 고유 값을 그대로 쓰는 걸 가장 권장해요.

| 이벤트 성격   | 권장 값             | 예시                        |
| -------- | ---------------- | ------------------------- |
| 구매·결제    | 주문번호, 결제 트랜잭션 ID | "ORD-20260722-001"        |
| 리드·양식 제출 | 폼 제출 ID          | "LEAD-20260722-0031"      |
| 회원가입·로그인 | 가입/세션 처리 ID      | "SIGNUP-20260722-0142"    |
| 조회·클릭 등  | 서비스에서 직접 만든 고유 값 | "PV-20260722-093245-4c1b" |

**어떻게 보내나요**

다른 파라미터와 동일하게 파라미터 객체 안에 event\_id를 넣어 주세요.

```html
<script>
  // "이벤트 고유 값" 대신 이벤트마다 겹치지 않는 값을 넣어 주세요
  TossPixel("전환 코드").purchase({
    event_id: "이벤트 고유 값",
    order_id: "ORD-20260722-001",
    revenue: 78000,
    total_quantity: 2,
    currency: "KRW"
  });
</script>
```

{% hint style="info" %}
* **별도로 발생한 이벤트에 같은 `event_id`를 사용하면 중복으로 처리되어 실제 발생 횟수보다 적게 집계될 수 있어요.** 새로 발생한 이벤트에는 다른 값을 사용하고, 같은 이벤트를 다시 보낼 때는 기존 값을 유지해 주세요.
* **이 기준에 맞게 값을 생성하고 관리하기 어렵다면 `event_id`를 생략해 주세요.** 생략해도 이벤트를 보낼 수 있지만, `event_id`를 이용한 중복 제거는 적용되지 않아요.
{% endhint %}

***

### 메이크샵 어드민에서 설치하기

{% stepper %}
{% step %}
**메이크샵 웹페이지 코드 수정**

<figure><img src="../../.gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>

메이크샵 관리자 센터 → 상단 네비게이션 바 \[디자인] 버튼을 클릭해 주세요.
{% endstep %}

{% step %}
**디자인 스킨 관리**

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

* \[디자인 스킨 관리] 페이지에서 PC, 모바일, 반응형 중 토스 픽셀을 추가하려는 디자인을 선택하고 \[디자인 편집] 버튼을 클릭해 주세요.
  * PC/모바일 두 디자인 모두 운영 중이라면 두 곳 모두 픽셀을 설치해야 해요.
  * 스크립트 내용은 PC, 모바일, 반응형 모두 같아요.
{% endstep %}

{% step %}
**정상 설치 여부 확인**

<figure><img src="../../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

* 좌측 상단 \[디자인 환경설정] 메뉴에서 예시 화면과 같은 내용이 보인다면 정상적으로 설치되었어요.

이제 아래 4가지 설치 단계를 마무리해주세요.
{% endstep %}
{% endstepper %}

***

#### 1. 전체 페이지 공통 설치

<figure><img src="../../.gitbook/assets/image (255).png" alt=""><figcaption></figcaption></figure>

```html
<script>
!function(t){try{if("function"==typeof t.TossPixel)return;if("function"!=typeof Proxy)return
;!function(t){function n(n){var r=new Proxy({},{get:function(e,i){
if("string"==typeof i&&"then"!==i&&"toJSON"!==i){if(!(i in e))e[i]=function(){try{
t._tpq.push([n,i,Array.prototype.slice.call(arguments)])}catch(t){}return r};return e[i]}}})
;return r}n(),t._tpq=Array.isArray(t._tpq)?t._tpq:[],t.TossPixel=n}(t)
;var n=t.document,r=n.createElement("script");r.type="text/javascript",r.async=!0,
r.src="https://static.toss.im/lex/v1.js",(n.head||n.documentElement).appendChild(r)}catch(t){return}
}(window);
</script>
```

* \[디자인 환경설정] → \[HEAD 입력]란에 위 스크립트를 복사해서 넣어 주세요.
  * 수정한 뒤에는 항상 \[HEAD 입력]란 아래 \[저장] 버튼을 눌러 적용해야 해요.

***

#### 2. 상품 상세 조회 (productView)

<figure><img src="../../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

```html
<script>  
  // Toss Pixel 상품 상세 조회 이벤트 수집
  var priceElement = "<!--/price_sell/-->";
  var tempDiv = document.createElement("div");
  tempDiv.innerHTML = priceElement;
  var priceText = tempDiv.textContent || tempDiv.innerText || priceElement;
  var priceValue = parseInt(priceText.replace(/[^0-9]/g, ""), 10) || 0;
  // "전환 코드" 대신 생성한 전환코드 값을 넣어주세요
  TossPixel("전환 코드").productView({
    products: [
      {
        product_id: "<!--/number/-->",
        product_name: "<!--/name/-->",
        price: priceValue,
      }
    ],
    currency: "<!--/currency_name/-->"
  });
</script>
```

* 상품 상세 페이지 조회 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[상품관련]** → **\[상품 상세 페이지]** → **\[상품 상세 페이지 파일]**&#xC5D0;서 추가해야 해요.
  * 상품 상세 페이지 조회 이벤트 수집 스크립트는 반드시 기존 코드 아래에 추가해야 해요.
    * 위 이미지 예시에서 기존 코드 최하단 태그 `</div><!-- #wrap -->` 아래 토스 픽셀 스크립트가 있어요.
  * 수정한 뒤에는 항상 \[저장] 버튼을 눌러 적용해야 해요.
* 이벤트 수집 스크립트 안에 있는 `"<!--/name/-->"` 같은 값은 메이크샵에서 각 모듈에 맞게 자동으로 변수로 바꿔줘요.
  * 자세한 설정 방법은 [메이크샵 가이드](https://www.makeshop.co.kr/newmakeshop/home/faq_tip_list.html)를 참고해 주세요.

#### 3. 장바구니 담기 (addToCart)

<figure><img src="../../.gitbook/assets/image (257).png" alt=""><figcaption></figcaption></figure>

```html
<a href="<!--/link_basket/-->" class="btn_cart fe" id="product_detail_top::add_to_cart_btn">CART</a>

<script>
// Toss Pixel 장바구니 추가 이벤트 수집
document
  .getElementById("product_detail_top::add_to_cart_btn")
  .addEventListener("click", function () {
    var priceElement = "<!--/price_sell/-->";
    var tempDiv = document.createElement("div");
    tempDiv.innerHTML = priceElement;
    var priceText = tempDiv.textContent || tempDiv.innerText || priceElement;
    var priceValue = parseInt(priceText.replace(/[^0-9]/g, "")) || 0;
    // "전환 코드" 대신 생성한 전환코드 값을 넣어주세요
    TossPixel("전환 코드").addToCart({
      products: [
        {
          product_id: "<!--/number/-->",
          product_name: "<!--/name/-->",
          price: priceValue,
        },
      ],
      currency: "<!--/currency_name/-->",
    });
  });
</script>
```

* 장바구니 추가 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[상품관련]** → **\[상품 상세 페이지]** → **\[상품 상세 페이지** **파일**]에서 추가해야 해요.

자세한 설정 방법은 다음과 같아요.

1. 상품 상세 페이지 html 파일 내에서 \[**장바구니 버튼]**&#xC5D0; 해당하는 html tag 찾기

* 장바구니 버튼에 해당하는 html tag 는 **‘장바구니’** 또는 **‘CART’** 텍스트를 노출해요
  * 장바구니 버튼은 `href="<!--/link_wishlist/-->"` 또는 `href="<!--/link_basket/-->"` 이라는 속성이 들어가있어요. (위 이미지 예시 안에 \<a> \</a> 태그에는 해당 속성이 들어가있어요)

2. 장바구니 버튼에 해당하는 html tag 에 id 속성 부여

* 해당 html tag에 이미 id 값이 있다면, 그 값을 그대로 복사해서 사용하고 아래 설정 내용은 건너뛰어도 돼요.
* 위 이미지 예시 안에 장바구니 버튼에 `id=”product_detail_top::add_to_cart_btn”` 라는 코드는 장바구니 버튼에 `product_detail_top::add_to_cart_btn` 라는 이름의 식별자를 붙인 것이에요.
* 장바구니 버튼을 클릭할 때 토스 픽셀 장바구니 이벤트 수집 스크립트를 실행하도록 해요.
  * 이 때 `<script> </script>` 태그는 반드시 **장바구니 버튼 html tag 아래**에 작성해주세요.

***

#### 4. 구매(주문) 완료 (purchase)

<figure><img src="../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

```html
<script>
  // Toss Pixel 구매 완료 이벤트 수집
  var lex_order_products_data = [];
  <!--/loop_order_product/-->
  var optionElement = "<!--/order_product@option/-->";
  var tempDiv = document.createElement("div");
  tempDiv.innerHTML = optionElement;
  var optionText = tempDiv.textContent || tempDiv.innerText || optionElement;
  var priceText = "<!--/order_product@price/-->";
  var priceValue = priceText.replace(/[^0-9]/g, "");
  var quantityText = "<!--/order_product@amount/-->";
  var quantityValue = parseInt(quantityText, 10);
  lex_order_products_data.push({
    product_id: "<!--/order_product@product_id/-->",
    product_name: "<!--/order_product@name/-->",
    quantity: quantityValue,
    price: priceValue,
    options: [optionText.trim()],
  })
  <!--/end_loop/-->
</script>
<script>
  // Toss Pixel 구매 완료 이벤트 수집
  var priceElement = document.getElementById("mk_totalprice")
  var priceText = priceElement.textContent || priceElement.innerText;
  var priceValue = priceText.replace(/[^0-9]/g, "");
  // "전환 코드" 대신 생성한 전환코드 값을 넣어주세요
  TossPixel("전환 코드").purchase({
    order_id: "<!--/order_num/-->",
    products: lex_order_products_data,
    revenue: priceValue,
    total_quantity: lex_order_products_data.reduce((acc, cur) => acc + cur.quantity, 0),
  });
</script>
```

* 구매(주문) 완료 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[주문관련]** → **\[주문 완료** **파일**]에서 추가해야 해요.
* 구매(주문) 완료 이벤트 수집 스크립트는 반드시 기존 코드 아래에 추가해야 해요.
  * 위 예시 이미지에서 기존 코드 최하단 태그 `</div><!-- #wrap -->` 아래 토스 픽셀 스크립트가 있는 것을 볼 수 있어요.

***

#### 5. 커스텀 이벤트

*   표준 이벤트에 해당하지 않는 전환을 추적할 때 사용해요.

    이벤트명은 직접 지정할 수 있고, 표준 이벤트와 동일한 파라미터를 사용할 수 있어요.

    * 추적하려는 전환이 발생하는 페이지의 HTML 파일에 아래 스크립트를 추가해 주세요.

```html
<script>
  TossPixel("전환 코드").custom("BUTTON_CLICK", {
    product_id: "P12345",
    product_name: "오가닉 코튼 티셔츠",
    category_id: "C100",
    price: 39000,
    currency: "KRW"
  });
</script>
```

| 파라미터                | 타입     | 필수 | 설명                                         |
| ------------------- | ------ | -- | ------------------------------------------ |
| eventName (첫 번째 인자) | String | 필수 | 이벤트명 (예: "BUTTON\_CLICK", "WISHLIST\_ADD") |
| params (두 번째 인자)    | Object | 선택 | 이벤트에 포함할 추가 데이터                            |

*   두 번째 인자에는 product\_id, price, currency 등 표준 이벤트에서 사용하는 파라미터를 전달할 수 있어요.

    전환 성격에 맞는 값을 선택해 포함해 주세요.

{% hint style="info" %}
**표준 이벤트와의 차이**

* 표준 이벤트는 메서드명이 곧 이벤트명이에요.
* 커스텀 이벤트는 첫 번째 인자에 이벤트명을 직접 입력해요.

**그 외 파라미터 사용 방식은 동일해요.**
{% endhint %}

***

#### 6. 커스텀 프로퍼티

* 모든 이벤트(표준 이벤트, 커스텀 이벤트)에 custom\_param1 \~ custom\_param5를 추가할 수 있어요.
* 표준 파라미터(product\_id, price 등)로 표현하기 어려운 추가 정보를 전달할 때 사용해요.
  * 예를 들어 캠페인 구분값, 프로모션 코드, A/B 테스트 그룹, 유입 경로 등 필요에 따라 정의한 값을 담을 수 있어요.

```html
<!-- 표준 이벤트에 커스텀 프로퍼티 추가 -->
<script>
  TossPixel("전환 코드").pageView({
    custom_param1: "summer_sale",
    custom_param2: "landing_A"
  });
</script>
```

```html
<!-- 커스텀 이벤트에 커스텀 프로퍼티 추가 -->
<script>
  TossPixel("전환 코드").custom("BUTTON_CLICK", {
    custom_param1: "cta_top",
    custom_param2: "variant_B"
  });
</script>
```

* 커스텀 프로퍼티는 최대 5개까지 사용할 수 있고, 표준 파라미터와 함께 하나의 객체로 전달해 주세요.

| 프로퍼티           | 타입     | 설명         |
| -------------- | ------ | ---------- |
| custom\_param1 | String | 커스텀 프로퍼티 1 |
| custom\_param2 | String | 커스텀 프로퍼티 2 |
| custom\_param3 | String | 커스텀 프로퍼티 3 |
| custom\_param4 | String | 커스텀 프로퍼티 4 |
| custom\_param5 | String | 커스텀 프로퍼티 5 |

## 설치 확인

토스 픽셀이 정상적으로 설치되었는지 아래 방법으로 확인할 수 있어요.

**Toss Pixel Helper 크롬 확장 프로그램**

[Toss Pixel Helper](https://chromewebstore.google.com/detail/toss-pixel-helper/kbbggbgnfmbpjpaieklnbbjfkjkkpcbi?hl=ko\&gl=US\&pli=1)를 설치하면 현재 페이지에서 수집된 토스 픽셀 이벤트를 실시간으로 확인할 수 있어요.

자세한 사용 방법은 [픽셀 이벤트 수집 확인하기](pixel_event.md) 페이지를 참고해 주세요.

<figure><img src="../../.gitbook/assets/image (9) (3).png" alt=""><figcaption></figcaption></figure>
