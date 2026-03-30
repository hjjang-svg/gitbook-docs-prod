# 앱스플라이어

### 전환 추적 코드 생성하기

{% stepper %}
{% step %}
#### 전환 및 추적 연동&#x20;

<figure><img src="../../.gitbook/assets/Group 335 (1).png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
#### 전환 추적 코드 생성

<figure><img src="../../.gitbook/assets/동의 및 코드 생성 (2).png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 생성한 전환 추적 코드 ID를 복사해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

### 앱스플라이어 연동하기

{% stepper %}
{% step %}
#### 앱스플라이어 연동 경로&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2024-04-16 오전 11.50.47.png" alt=""><figcaption></figcaption></figure>

앱스플라이어 연동 링크 생성은 아래 경로에서 가능해요.

Partner Marketplace → \[Toss] 앱 검색 →  Set up intergration 선택&#x20;
{% endstep %}

{% step %}
#### 연동 활성화&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2024-04-16 오전 11.51.45.png" alt=""><figcaption></figcaption></figure>

Active partner 의 스위치 버튼을 클릭하여 파트너 연동을 활성화 하고 생성해둔 전환 추적 코드의 ID 값을 복사하여 cvr\_id 항목에 입력해주세요.

<figure><img src="../../.gitbook/assets/image (262).png" alt=""><figcaption></figcaption></figure>

* IOS 세팅을 하시는 경우, Advanced Privacy 모드가 'OFF'로 되어 있는지 확인해 주세요.&#x20;
  * 해당 설정을 꺼두셔야 데이터 익명화 처리를 방지하고, 토스 애즈와 AppsFlyer 간의 데이터 정합성을 확보할 수 있어요.
{% endstep %}

{% step %}
#### 연동 확인&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2024-07-17 오후 3.47.29.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2024-07-17 오후 3.48.40.png" alt=""><figcaption></figcaption></figure>

* Default Postbacks 에서 All media sources 항목이 있다면 해당 항목 선택하고 All media sources 항목이 없다면 This Partenr Only를 선택해주세요.&#x20;
* 앱 내에서의 이벤트 연동을 희망하는 경우 In-app event postbacks 토글을 ON으로 변경해주세요.&#x20;
* Save Integration 를 눌러 연동을 완료해주세요.


{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="120.41796875">이벤트 이름</th><th width="225.44140625">Toss Ads 이벤트 라벨</th><th width="495.55859375">Appsflyer 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>af_complete_registration</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>af_login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>af_purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>af_content_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>af_add_to_cart</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목

토스애즈에서 앱스플라이어(AppsFlyer)를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 들어가야 해요.

필수 항목이 누락되는 경우 **어떤 광고에서 전환이 일어났는지 알 수 없고** **앱스플라이어 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목              | 값                         | 설명                    |
| --------------- | ------------------------- | --------------------- |
| **pid**         | **tossa3u\_int**          | Toss Ads 고유 매체 식별자    |
| af\_c\_id       | **{TOSS\_CID}**           | 캠페인 ID                |
| clickid         | **{TOSS\_TK\_CLICK\_ID}** | 클릭 발생 시 부여되는 고유 클릭 ID |
| advertising\_id | **{USER\_ADID}**          | 유저의 ADID (광고 식별자)     |

#### 권장 항목

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재별 전환 데이터를 정확하게 추적하기 어려워지고 앱스플라이어 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목         | 값                        | 설명    |
| ---------- | ------------------------ | ----- |
| af\_siteid | **{SITE\_ID}**           | 매체 ID |
| af\_ad\_id | **{TOSS\_CREATIVE\_ID}** | 소재 ID |

#### 링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**[<mark style="color:blue;">**권장**</mark>](#user-content-fn-1)[^1] 항목이 포함된 예시 링크

> https://onelink.me/com.sample.app?<mark style="color:red;">pid=tossa3u\_int\&af\_c\_id={TOSS\_CID}\&clickid={TOSS\_TK\_CLICK\_ID}\&advertising\_id={USER\_ADID}</mark>&<mark style="color:blue;">af\_siteid={SITE\_ID}\&af\_ad\_id={TOSS\_CREATIVE\_ID}</mark>

{% hint style="success" %}
#### **링크 설정 Tip**

*   앱스플라이어 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.

    * 자세한 설정 방법은 Active Intergrations > Attribution link 탭에서 확인하실 수 있어요.&#x20;

    <figure><img src="../../.gitbook/assets/image (1).jpeg" alt="" width="375"><figcaption></figcaption></figure>
* 토스애즈 가이드에 있는 표준 이벤트와 파라미터가 들어 있는 링크 템플릿을 사용하는 걸 권장해요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
{% endhint %}

[^1]: 
