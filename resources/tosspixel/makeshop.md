# 메이크샵 픽셀 연동

> 토스 픽셀은 [전환 추적 코드 생성하기 가이드](../tag/code_generation.md)에 따라 전환 추적 코드를 생성한 후에 사용할 수 있어요.&#x20;

### 이벤트 별 스크립트

토스 픽셀이 지원하는 이벤트 목록은 아래와 같아요.

이벤트 중에서 추적하고 싶은 이벤트만 메이크샵 코드 편집기에 삽입해 주세요.&#x20;

<table><thead><tr><th width="354.76953125">이벤트명</th><th>이벤트 라벨</th></tr></thead><tbody><tr><td>페이지 방문</td><td>pageView</td></tr><tr><td>상품 상세페이지 조회</td><td>productView</td></tr><tr><td>장바구니 추가</td><td>addToCart</td></tr><tr><td>구매(주문)</td><td>purchase</td></tr></tbody></table>

이벤트 스크립트 코드는 전환이 실제로 일어나는 시점에 맞춰 넣어야 해요 그래야 전환 데이터를 정확하게 모을 수 있어요.

예를 들어, 사용자가 **상품 상세 페이지를 보고** → **장바구니에 담는 과정을 추적**하고 싶다면 아래처럼 넣으면 돼요.

1.  상품 상세 페이지에

    “상품/콘텐츠 상세페이지 조회” 이벤트 스크립트를 넣어요.
2.  장바구니 담기 버튼을 클릭할 때

    “장바구니 담기” 이벤트 스크립트를 실행되게 넣어요.

이렇게 하면 두 가지 이벤트를 문제 없이 깔끔하게 추적할 수 있어요.

***

### 토스 픽셀 설치하기

{% stepper %}
{% step %}
#### 메이크샵 웹페이지 코드 수정

<figure><img src="../../.gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>

메이크샵 관리자 센터 → 상단 네비게이션 바 \[디자인] 버튼 클릭
{% endstep %}

{% step %}
#### 디자인 스킨 관리

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

* \[디자인 스킨 관리] 페이지에서  PC, 모바일, 반응형 중 토스 픽셀을 추가하려는 디자인을 선택하고 \[디자인 편집] 버튼 클릭해주세요.
  * PC/모바일 두 디자인 모두 운영 중이라면 두 곳 모두 픽셀을 설치해야 해요
  * 스크립트 내용은 PC/모바일/반응형 동일해요.
{% endstep %}

{% step %}
#### 정상 설치 여부 확인

<figure><img src="../../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

* 좌측 상단 \[디자인 환경설정] 메뉴에서 예시 화면과 같은 내용이 보인다면 정상적으로 설치되었어요.

이제 아래 4가지 설치 단계를 마무리해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

#### 1. 전체 페이지 공통 설치 + 페이지 방문 (pageView)

<figure><img src="../../.gitbook/assets/image (255).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```html
<!-- Toss Pixel 스크립트 로드 -->
<script src="https://static.toss.im/lex/v1.js"></script>

<!-- Toss Pixel PageView 이벤트 -->
<script>
    document.addEventListener('DOMContentLoaded', function() {
        // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
        TossPixel('전환 코드').pageView(); 
    });
</script>
```
{% endcode %}

* \[디자인 환경설정] →  \[HEAD 입력]란에 에 위 스크립트를 복사하여 넣어주세요.
  * 수정 변경 후에는 항상 \[HEAD 입력]란 아래 \[저장] 버튼을 눌러 적용해야해요.

***

#### 2. 상품 상세 페이지 조회 (product View)

<figure><img src="../../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```html
<script>
    // Toss Pixel 상품 상세 조회 이벤트 수집
    var priceElement = '<!--/price_sell/-->';
    var tempDiv = document.createElement('div');
    tempDiv.innerHTML = priceElement;
    var priceText = tempDiv.textContent || tempDiv.innerText || priceElement;
    var priceValue = parseInt(priceText.replace(/[^0-9]/g, ''), 10) || 0;
    // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
    TossPixel('전환 코드').productView({
        product_id: "<!--/number/-->",
        product_name: "<!--/name/-->",
        price: priceValue,
        currency: "<!--/currency_name/-->"
    });
</script>
```
{% endcode %}

* 상품 상세 페이지 조회 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[상품관련]**  → **\[상품 상세 페이지]** → **\[상품 상세 페이지 파일]**&#xC5D0;서 추가해야 해요.
  * 상품 상세 페이지 조회 이벤트 수집 스크립트는 반드시 기존 코드 아래에 추가해야 해요&#x20;
    * 위 이미지 예시에서 기존 코드 최하단 태그 `</div><!-- #wrap -→` 아래 토스 픽셀 스크립트가 있어요.
  * 수정 변경 후에는 항상 \[HEAD 입력]란 아래 \[저장] 버튼을 눌러 적용해야해요.
* 이벤트 수집 스크립트 안에 있는 `"<!--/name/-->”` 과 같은 값들은 메이크샵에서 각 모듈에 맞게 자동으로 변수로 바꿔줘요.
  * 자세한 설정 방법은 [메이크샵 가이드](https://www.makeshop.co.kr/newmakeshop/home/faq_tip_list.html)를 참고해 주세요.

#### 3. **장바구니 추가 (**&#x61;ddToCar&#x74;**)**

<figure><img src="../../.gitbook/assets/image (257).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```html
<a href="<!--/link_wishlist/-->" class="btn_cart fe" id="product_detail_top::add_to_cart_btn">CART</a>
<script>
     // Toss Pixel 장바구니 추가 이벤트 수집
     document.getElementById("product_detail_top::add_to_cart_btn").addEventListener('click', function () {
     var priceElement = '<!--/price_sell/-->';
     var tempDiv = document.createElement('div');
     tempDiv.innerHTML = priceElement;
     var priceText = tempDiv.textContent || tempDiv.innerText || priceElement;
     var priceValue = parseInt(priceText.replace(/[^0-9]/g, '')) || 0;
     // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
     TossPixel('전환 코드').addToCart({
          product_id: "<!--/number/-->",
          product_name: "<!--/name/-->",
          price: priceValue,
          currency: "<!--/currency_name/-->"
        });
     });
</script>
```
{% endcode %}



* 장바구니 추가 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[상품관련]** → **\[상품 상세 페이지]** → **\[상품 상세 페이지** **파일**]에서 추가해야 해요.&#x20;

자세한 설정 방법은 다음과 같아요.

1. 상품 상세 페이지 html 파일 내에서 \[**장바구니 버튼]**&#xC5D0; 해당하는 html tag 찾기&#x20;

* 장바구니 버튼에 해당하는 html tag 는 **‘장바구니’** 또는 **‘CART’**  텍스트를 노출해요&#x20;
  * 장바구니 버튼은 `href="<!--/link_wishlist/-->"` 또는 `href="<!--/link_basket/-->"` 이라는 속성이 들어가있어요. (위 이미지 예시 안에 \<a> \</a> 태그에는 해당 속성이 들어가있어요)

2. 장바구니 버튼에 해당하는 html tag 에 id 속성 부여

* 해당 html tag에 이미 id 값이 있다면, 그 값을 그대로 복사해서 사용하고 아래 설정 내용은 건너뛰어도 돼요.
* 위 이미지 예시 안에 장바구니 버튼에 `id=”product_detail_top::add_to_cart_btn”` 라는 코드는 장바구니 버튼에 `product_detail_top::add_to_cart_btn` 라는 이름의 식별자를 붙인 것이에요.
* 장바구니 버튼 클릭 할 때 토스 픽셀 장바구니 이벤트 수집 스크립트를 실행하도록 해요.
  * 이 때 `<script> </script>` 태그는 반드시 **장바구니 버튼 html tag 아래**에 작성해주세요.

***

#### 4. 구매(주문) 완료 (purchase)

<figure><img src="../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```html
<script>
    // Toss Pixel 구매 완료 이벤트 수집
    var lex_order_products_data = [];
    <!--/loop_order_product/-->
    var optionElement = "<!--/order_product@option/-->";
    var tempDiv = document.createElement('div');
    tempDiv.innerHTML = optionElement;
    var optionText = tempDiv.textContent || tempDiv.innerText || optionElement;
    var priceText = '<!--/order_product@price/-->';
    var priceValue = priceText.replace(/[^0-9]/g, '');
    var quantityText = '<!--/order_product@amount/-->';
    var quantityValue = parseInt(quantityText, 10);
    lex_order_products_data.push({
        product_id: '<!--/order_product@product_id/-->',
        product_name:'<!--/order_product@name/-->',
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
    var priceValue = priceText.replace(/[^0-9]/g, '');
    // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
    TossPixel('전환 코드').purchase({
        order_id:"<!--/order_num/-->",
        products: lex_order_products_data,
        total_price: priceValue,
        total_quantity: lex_order_products_data.reduce((acc, cur) => acc + cur.quantity, 0),
    });
</script>
```
{% endcode %}

* 구매(주문) 완료 이벤트 수집 스크립트는 \[**중앙 디자인]** → **\[주문관련]** → **\[주문 완료** **파일**]에서 추가해야 해요.
* 구매(주문) 완료 이벤트 수집 스크립트는 반드시 기존 코드 아래에 추가해야 해요
  * 위 예시 이미지에서 기존 코드 최하단 태그 `</div><!-- #wrap -→` 아래 토스 픽셀 스크립트가 있는 것을 볼 수 있어요.

***

#### 5. 커스텀 이벤트

*   표준 이벤트에 해당하지 않는 전환을 추적할 때 사용해요.

    이벤트 이름은 직접 지정할 수 있고, 표준 이벤트와 동일한 파라미터를 사용할 수 있어요.

    * 추적하려는 전환이 발생하는 페이지의 HTML 파일에 아래 스크립트를 추가해 주세요.

{% code overflow="wrap" %}
```html
<!-- Toss Pixel 커스텀 이벤트 -->
<script>
    // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
    TossPixel('전환 코드').custom('BUTTON_CLICK', {
        product_id: "{$product_no}",
        product_name: "{$name}",
        price: "{$product_sale_price}",
        currency: "{$price_unit_tail}"
    });
</script>
```
{% endcode %}

| 파라미터                | 타입     | 필수 | 설명                                           |
| ------------------- | ------ | -- | -------------------------------------------- |
| eventName (첫 번째 인자) | string | 필수 | 이벤트 이름 (예: "BUTTON\_CLICK", "WISHLIST\_ADD") |
| params (두 번째 인자)    | object | 선택 | 이벤트에 포함할 추가 데이터                              |

*   두 번째 인자에는 product\_id, price, currency 등 표준 이벤트에서 사용하는 파라미터를 전달할 수 있어요.

    전환 성격에 맞는 값을 선택해 포함해 주세요.

{% hint style="info" %}
**표준 이벤트와의 차이**

* 표준 이벤트는 메서드명이 곧 이벤트 이름이에요.
* 커스텀 이벤트는 첫 번째 인자에 이벤트 이름을 직접 입력해요.

&#x20;       **그 외 파라미터 사용 방식은 동일해요.**
{% endhint %}

***

#### 6.커스텀 프로퍼티

* 모든 이벤트(표준 이벤트, 커스텀 이벤트)에 custom\_param\_1 \~ custom\_param\_5를 추가할 수 있어요.
* 표준 파라미터(product\_id, price 등)로 표현하기 어려운 추가 정보를 전달할 때 사용해요.
  * 예를 들어, 캠페인 구분값, 프로모션 코드, A/B 테스트 그룹, 유입 경로 등 필요에 따라 정의한 값을 담을 수 있어요.

{% code overflow="wrap" %}
```html
<!-- 표준 이벤트에 커스텀 프로퍼티 추가 -->
<script>
    // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
    TossPixel('전환 코드').purchase({
        total_price: "{$total_order_price_original}",
        currency: "{$product_total_price_ref}",
        custom_param_1: "summer_sale",
        custom_param_2: "landing_A"
    });
</script>
```
{% endcode %}

{% code overflow="wrap" %}
```html
<!-- 커스텀 이벤트에 커스텀 프로퍼티 추가 -->
<script>
    // '전환 코드' 대신 생성한 전환코드 값을 넣어주세요
    TossPixel('전환 코드').custom('BUTTON_CLICK', {
        product_id: "{$product_no}",
        custom_param_1: "cta_top",
        custom_param_2: "variant_B"
    });
</script>
```
{% endcode %}

* 커스텀 프로퍼티는 최대 5개까지 사용할 수 있고, 표준 파라미터와 함께 하나의 객체로 전달해 주세요.

| 프로퍼티             | 타입     | 설명         |
| ---------------- | ------ | ---------- |
| custom\_param\_1 | string | 커스텀 프로퍼티 1 |
| custom\_param\_2 | string | 커스텀 프로퍼티 2 |
| custom\_param\_3 | string | 커스텀 프로퍼티 3 |
| custom\_param\_4 | string | 커스텀 프로퍼티 4 |
| custom\_param\_5 | string | 커스텀 프로퍼티 5 |
