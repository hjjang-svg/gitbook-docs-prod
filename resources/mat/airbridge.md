# 에어브릿지

### 전환 추적 코드 생성하기&#x20;

{% stepper %}
{% step %}
#### 전환 및 추적 연동

<figure><img src="../../.gitbook/assets/Group 335 (5).png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
#### 전환 추적 코드 생성

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-1.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성해주세요.
{% endstep %}

{% step %}
#### 생성 여부 확인

<figure><img src="../../.gitbook/assets/스크린샷 2026-02-20 오후 2.20.00 2.png" alt=""><figcaption></figcaption></figure>

설정한 정보에 맞게 생성된 전환 추적 코드의 ID를 복사하여 연동할 수 있어요.
{% endstep %}
{% endstepper %}

***

### 에어브릿지 연동하기

{% stepper %}
{% step %}
#### 에어브릿지 연동 경로&#x20;

<figure><img src="../../.gitbook/assets/toss-ads-01.png" alt=""><figcaption></figcaption></figure>

&#x20;에어브릿지 연동 링크 생성은 아래 경로에서 가능해요.&#x20;

&#x20;Integrations → Intergrated Ad Channels 선택 → \[Toss]앱 검색
{% endstep %}

{% step %}
#### 연동 앱 선택 및 입력&#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* 전송할 이벤트를 선택하고 다음 버튼을 클릭해주세요.&#x20;
  * 전송 규칙은 `채널 기여와 상관 없이 모든 이벤트 전송`으로 설정해주세요.&#x20;
* Conversion\_id 수정이 필요하다면 포스트백 전송을 중지한 이후 수정 해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

### 미디어 파트너 권한 부여하기

{% stepper %}
{% step %}
#### &#x20;미디어 파트너 권한 부여&#x20;

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

&#x20;에어브릿지를 연동한 후 데이터 관리 및 최적화를 위해 toss-ads@toss.im 계정에 미디어 파트너 권한을 부여해주세요.&#x20;

&#x20;권한 부여 경로는 아래와 같아요.

에어브릿지 접속 → \[Settings] → \[User Management] 접속
{% endstep %}

{% step %}
#### &#x20;앱 접근 권한 부여

<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

\[앱 접근 권한 부여] 버튼을 클릭해주세요.&#x20;

팝업창에서 toss-ads@toss.im 계정을 입력하고 앱 역할을 "미디어 파트너"로 설정해주세요.&#x20;

자세한 가이드는 [에어브릿지 > 앱에서 앱 접근 권한 관리하기 가이드](https://help.airbridge.io/ko/guides/app-access-management)를 참고해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="127">이벤트 이름</th><th width="204.6953125">Toss Ads 이벤트 라벨</th><th width="351.6484375">Airbridge 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>app_install</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>app_open</td></tr><tr><td>딥링크 앱 오픈</td><td>APP_DEEPLINK_OPEN</td><td>app_deeplink_open</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>airbridge.user.signup</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>airbridge.user.signin</td></tr><tr><td>결제</td><td>PURCHASE</td><td>airbridge.ecommerce.order.completed</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>airbridge.ecommerce.product.viewed</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>airbridge.ecommerce.product.addedToCart</td></tr><tr><td>홈 조회</td><td>VIEW_HOME</td><td>airbridge.ecommerce.home.viewed</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목

토스애즈에서 에어브릿지를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 들어가야 해요.

필수 항목이 누락되는 경우 **어떤 광고에서 전환이 일어났는지 알 수 없고** **에어브릿지 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목           | 값                     | 설명                    |
| ------------ | --------------------- | --------------------- |
| ad\_id       | {USER\_ADID}          | 유저의 ADID (광고 식별자)     |
| campaign\_id | {TOSS\_CID}           | 캠페인 ID                |
| click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 발생 시 부여되는 고유 클릭 ID |

#### 권장 항목

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재별 전환 데이터를 정확하게 추적하기 어려워지고 에어브릿지 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목               | 값                    | 설명    |
| ---------------- | -------------------- | ----- |
| sub\_id          | {SITE\_ID}           | 매체 ID |
| ad\_creative\_id | {TOSS\_CREATIVE\_ID} | 소재 ID |

### &#x20;링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://abr.ge/@demolv4xh8pxqh/toss?<mark style="color:red;">**ad\_id={USER\_ADID}\&campaign\_id={TOSS\_CID}\&click\_id={TOSS\_TK\_CLICK\_ID}**</mark>&<mark style="color:blue;">**sub\_id={SITE\_ID}\&ad\_creative\_id={TOSS\_CREATIVE\_ID}**</mark>

{% hint style="success" %}
#### **링크 설정 Tip**

* 에어브릿지 콘솔에서 제공하는 트래킹 링크를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
* 토스애즈 가이드에 있는 표준 이벤트와 파라미터가 들어 있는 링크 템플릿을 사용하는 걸 권장해요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
{% endhint %}
