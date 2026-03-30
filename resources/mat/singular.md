# 싱귤러

### 전환 추적 코드 생성하기

{% stepper %}
{% step %}
#### 전환 및 추적 연동

<figure><img src="../../.gitbook/assets/Group 335 (2).png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
#### 전환 추적 코드 생성

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-3.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 생성한 전환 추적 코드 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 싱귤러 연동하기

{% stepper %}
{% step %}
#### 싱귤러 연동 경로&#x20;

싱귤러 연동 링크 생성은 아래 경로에서 가능해요.

Attribution → Partner Management 메뉴 선택 → \[Add a Partner] 버튼 클릭
{% endstep %}

{% step %}
#### 연동 앱 검색&#x20;

\[Toss]앱 검색 하여 추가하고 발급 받은 전환 추적 ID값을 전환 추적 코드 입력 란에 등록해주세요.&#x20;
{% endstep %}

{% step %}
#### 추가 설정&#x20;

Attribution → Manage Links 메뉴를 접속 \[Create Link] 버튼 클릭 → Link Type 항목을 \[Partner] 선택 → Source Name 항목에서 \[Toss]앱 검색 후 선택 → Tracking Link Name 항목에 링크 명칭을 입력  → \[Generate] 버튼 클릭
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="127">이벤트 이름</th><th width="204.6953125">Toss Ads 이벤트 라벨</th><th width="231.7734375">Singular 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>sng_start_trial</td></tr><tr><td>딥링크 앱 오픈</td><td>APP_DEEPLINK_OPEN</td><td>sng_attr_deep_link</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>sng_complete_registration</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>sng_login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>sng_ecommerce_purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>sng_content_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>sng_add_to_cart</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 안내

토스애즈에서 싱귤러를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 들어가야 해요.

필수 항목이 누락되는 경우 **어떤 광고에서 전환이 일어났는지 알 수 없고** **에어브릿지 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

<table><thead><tr><th width="173.35546875">항목</th><th>값</th><th>설명</th></tr></thead><tbody><tr><td>cl</td><td><strong>{TOSS_TK_CLICK_ID}</strong></td><td>클릭 발생 시 부여되는 고유 클릭 ID</td></tr><tr><td>pcid</td><td><strong>{TOSS_CID}</strong></td><td>캠페인 ID</td></tr><tr><td>ad_id</td><td><strong>{USER_ADID}</strong></td><td>유저의 ADID (광고 식별자)</td></tr></tbody></table>

#### 권장 항목

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재별 전환 데이터를 정확하게 추적하기 어려워지고 싱귤러 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목       | 값                    | 설명    |
| -------- | -------------------- | ----- |
| pcrid    | {TOSS\_CREATIVE\_ID} | 소재 ID |
| site\_id | {SITE\_ID}           | 매체 ID |

#### &#x20;링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://sample.sng.link/sample/sample?<mark style="color:red;">**cl={TOSS\_TK\_CLICK\_ID}\&pcid={TOSS\_CID}\&ad\_id={USER\_ADID}**</mark>&<mark style="color:blue;">**pcrid={TOSS\_CREATIVE\_ID}\&pcrid={TOSS\_CREATIVE\_ID}**</mark>

{% hint style="success" %}
#### **링크 설정 Tip**

* 싱귤러 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * Tracking Link Name 항목에 링크 명칭을 입력한 후 Generate 버튼을 클릭해서 생성된 링크를 활용해주세요.
* 토스애즈 가이드에 있는 표준 이벤트와 파라미터가 들어 있는 링크 템플릿을 사용하는 걸 권장해요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
{% endhint %}
