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
---

# 토스 픽셀 TCID 보존 가이드

## tcid 보존 가이드

이 가이드는 토스 픽셀을 설치한 사이트에서 <mark style="color:red;">`tcid`</mark>를 유지하는 방법을 안내해요.

픽셀이 실행되기 전에 <mark style="color:red;">`tcid`</mark>가 사라지면 광고 클릭과 전환을 연결할 수 없어요.

#### tcid란?

<mark style="color:red;">`tcid`</mark>는 토스 광고를 클릭한 사용자를 식별하는 값이에요.

사용자가 토스 광고를 클릭하면 랜딩 URL에 <mark style="color:red;">`tcid`</mark>가 함께 전달돼요.

토스 픽셀은 <mark style="color:red;">`tcid`</mark>를 이용해 광고 클릭과 구매, 회원가입, 상담 신청 같은 전환을 연결해요.

***

#### 꼭 확인해 주세요

* 광고 랜딩 URL의 <mark style="color:red;">`tcid`</mark>를 삭제하거나 이름을 변경하지 마세요.
* CDN, WAF, 서버 리다이렉트, 프론트엔드 라우터가 쿼리 스트링을 유지하는지 확인해 주세요.
* 픽셀이 처음 실행되는 페이지까지 <mark style="color:red;">`tcid`</mark>가 유지되어야 해요.
* 결제, 회원가입처럼 페이지가 바뀌는 경우에도 첫 랜딩 페이지에서 픽셀이 먼저 실행되어야 해요.
* 쿼리 파라미터 Allowlist를 사용하는 경우 <mark style="color:red;">`tcid`</mark>를 포함해 주세요.

***

#### 픽셀이 읽는 키

픽셀은 URL쿼리 스트링에서  <mark style="color:red;">`tcid`</mark>키를 확인해요&#x20;

예시:

```
https://www.example.com/products/123?tcid=...&utm_source=toss
```

<mark style="color:red;">`tcid`</mark>는 URL로 전달된 값을 그대로 사용해요.

값을 새로 만들거나 수정하지 말아 주세요. 값을 변경하거나 일부를 삭제하면 정상적으로 인식하지 못할 수 있어요.

***

#### tcid 저장 방식

픽셀은 현재 URL에서 <mark style="color:red;">`tcid`</mark>를 확인하면 브라우저에 저장해요.

이후 같은 브라우저에서 발생한 전환 이벤트에 저장된 값을 함께 전송해요.

조회 순서는 아래와 같아요.

1. 현재 URL의 쿼리 스트링
2. 브라우저 쿠키
3. 브라우저 localStorage

픽셀이 실행되기 전에 <mark style="color:red;">`tcid`</mark>가 제거되면 저장할 수 없어요.

서버나 프론트엔드에서 URL을 변경하는 경우 <mark style="color:red;">`tcid`</mark>를 유지하도록 설정해 주세요.

***

## tcid 보존 원칙

{% stepper %}
{% step %}
#### 첫 랜딩 URL의 tcid를 유지해 주세요.

좋은 예시:

```
요청 URL: https://www.example.com/?tcid=abc...&utm_source=toss
브라우저 최종 URL: https://www.example.com/?tcid=abc...&utm_source=toss
```

좋지 않은 예시:

```
요청 URL: https://www.example.com/?tcid=abc...&utm_source=toss
브라우저 최종 URL: https://www.example.com/
```
{% endstep %}

{% step %}
#### URL을 변경해야 한다면 픽셀 실행 후에 진행해 주세요.

사이트 정책상 URL을 정리해야 하는 경우에는 픽셀이 먼저 실행되어 <mark style="color:red;">`tcid`</mark>를 저장한 뒤 URL을 변경해 주세요.

예시:

```javascript
const pixel = new TossPixel('YOUR_CONVERSION_ID');
pixel.pageView();

// 픽셀 실행 후 필요한 경우에만 주소창 정리
const url = new URL(window.location.href);
url.searchParams.delete('utm_source');
url.searchParams.delete('utm_medium');
window.history.replaceState({}, '', url);
```

<mark style="color:red;">`tcid`</mark>는 가능한 한 삭제하지 않는 것을 권장해요. 부득이하게 삭제해야 하는 경우에는 픽셀이 먼저 실행되는지 확인해 주세요.
{% endstep %}

{% step %}
#### 가능하면 쿼리 스트링 전체를 유지해 주세요.

리다이렉트나 라우팅 과정에서는 기존 쿼리 스트링 전체를 유지하는 것을 권장해요.

좋은 예시:

```
/landing?tcid=...&utm_source=toss
→ /products?tcid=...&utm_source=toss
```

좋지 않은 예시:

```
/landing?tcid=...&utm_source=toss
→ /products?utm_source=toss
```
{% endstep %}
{% endstepper %}

***

## 유실 원인별 대응 방법

#### CDN 또는 Edge Rewrite

CDN이나 Edge Function에서 <mark style="color:red;">`/promo`</mark>를 <mark style="color:red;">`/products/123`</mark>으로 rewrite하거나 redirect할 때 쿼리 스트링이 사라질 수 있어요.



* **확인해 주세요**
  * rewrite 후에도 원래 query string이 origin 또는 브라우저 최종 URL이 유지되는지
  * 캐시 키를 만들 때 query string을 제거하면서 브라우저 URL까지 바꾸고 있지 않은지
  * Edge Function 코드에서 새 URL을 만들 때 <mark style="color:red;">`search`</mark>값을 복사하는지
* **권장해요**
  * redirect 대상 URL에 기존 query string을 그대로 유지해 주세요.&#x20;
  * query allowlist를 쓰는 경우 tcid를 포함해 주세요.
  * 캐시 최적화를 위해 query string을 무시하더라도, 사용자의 브라우저 URL이나 origin 요청에서 tcid가 제거되지 않게 유지해 주세요.

***

#### 서버 리다이렉트

HTTP 응답의 <mark style="color:red;">`Location`</mark> 헤더로 다른 페이지에 보내는 과정에서 query string이 빠질 수 있습니다. 예를 들어 비로그인 사용자를 로그인 페이지로 보내거나, 모바일 경로로 보내거나, trailing slash를 붙이는 리다이렉트가 여기에 해당해요.



* **확인해 주세요**

좋지 않은 예시:

```
GET /promo?tcid=...&utm_source=toss
302 Location: /products
```

좋은 예시:

```
GET /promo?tcid=...&utm_source=toss
302 Location: /products?tcid=...&utm_source=toss
```

* **권장해요**
  * 리다이렉트 대상 URL을 만들 때 기존 query string을 복사해 주세요.
  * canonical URL로 이동시키는 리다이렉트에서도 query string을 유지해 주세요.
  * 로그인, 회원가입, 장바구니, 결제 시작 페이지로 이동할 때도 <mark style="color:red;">`tcid`</mark>를 보존해 주세요.&#x20;

***

#### 클라이언트 URL 정규화

프론트엔드 코드에서 <mark style="color:red;">`history.replaceState`</mark>, <mark style="color:red;">`router.replace`</mark>, <mark style="color:red;">`router.push`</mark> 등으로 URL을 정리하면서 query string이 사라질 수 있어요.



* **확인해 주세요**

좋지 않은 예시:&#x20;

```javascript
window.history.replaceState({}, '', window.location.pathname);
```

좋은 예시:

```javascript
const currentUrl = new URL(window.location.href);
window.history.replaceState({}, '', currentUrl.pathname + currentUrl.search + currentUrl.hash);
```

* **권장해요**
  * 페이지 초기화 직후 실행되는 URL 정리 코드가 있는지 확인합니다.
  * 라우터 전환 시 <mark style="color:red;">`query`</mark>, <mark style="color:red;">`searchParams`</mark>, <mark style="color:red;">`location.search`</mark>를 유지합니다.
  * URL을 정리해야 한다면 픽셀 초기화와 <mark style="color:red;">`pageView()`</mark> 호출 이후에 실행합니다.

***

#### SPA 라우팅

Single Page Application에서는 첫 진입 이후 페이지 이동이 브라우저 새로고침 없이 발생해요. 첫 진입 URL의 <mark style="color:red;">`tcid`</mark>가 유지되면 픽셀이 저장할 수 있지만, 초기 라우터가 query string을 제거하면 값이 유실돼요.



* **권장해요**
  * 앱 bootstrap 시점에 query string을 보존합니다.
  * 첫 <mark style="color:red;">`pageView()`</mark> 호출 전에 라우터가 <mark style="color:red;">`tcid`</mark>를 제거하지 않게 합니다.
  * 내부 페이지 이동에서 URL을 재구성할 때 기존 query string을 무조건 버리는 공통 유틸을 사용하지 않습니다.

***

#### 도메인 또는 서브도메인 이동

광고 랜딩은 <mark style="color:red;">`www.example.com`</mark>이고 결제 완료는 <mark style="color:red;">`order.example.com`</mark> 또는 외부 결제 도메인에서 발생할 수 있어요.



* **확인해 주세요**
  * 픽셀은 브라우저 쿠키와 localStorage를 활용해 식별자를 보존해요.
  * 같은 루트 도메인의 서브도메인으로 이동하는 경우에는 쿠키를 통해 <mark style="color:red;">`tcid`</mark>가 유지될 수 있어요.\
    <mark style="color:red;">`localStorage`</mark>는 도메인(origin)별로 분리되어 있어 다른 도메인에서는 이어지지 않아요. (쿠키를 사용할 수 없는 경우에만 사용돼요.)
  * 첫 랜딩 페이지에서 픽셀이 실행되지 않았거나 다른 도메인으로 바로 이동하면 <mark style="color:red;">`tcid`</mark>를 저장할 수 없어요.
* **권장해요**
  * 광고 랜딩 페이지에서 픽셀이 먼저 실행되는지 확인해요.
  * 결제, 회원가입, 예약 같은 전환 완료 페이지에도 픽셀을 설치해요.
  * 외부 도메인을 거쳐 돌아오는 흐름에서는 복귀 URL에 <mark style="color:red;">`tcid`</mark>를 계속 붙일 수 있는지 결제사 또는 플랫폼 설정을 확인해요.

***

#### 마케팅 링크 단축과 추적 링크

광고 클릭 URL 앞에 링크 단축 서비스, 내부 추적 링크 또는 캠페인 라우터를 사용하는 경우, 중간 과정에서 query string이 변경되거나 삭제될 수 있어요.



* **확인해 주세요**
  * 중간 추적 링크가 기존 query string을 삭제하거나 변경하지 않는지 확인해 주세요.
  * 링크 단축 서비스 또는 내부 라우터가 <mark style="color:red;">`tcid`</mark>를 포함한 query string을 유지하는지 확인해 주세요.
* **권장해요**
  * 실제 광고 클릭과 동일한 방식으로 테스트해 최종 랜딩 URL까지 <mark style="color:red;">`tcid`</mark>가 전달되는지 확인해 주세요.
  * 중간 추적 링크는 자체 파라미터만 추가하고 기존 query string은 유지해 주세요.
  * 링크 단축 서비스를 사용하는 경우 "query parameter forwarding"또는 동일한 기능을 활성화해 주세요.

***

#### 캐시와 정적 페이지 생성

정적 페이지, CDN 캐시, 서버 사이드 렌더링(SSR) 캐시에서는 query string을 제외하도록 설정하는 경우가 많아요.

캐시 키에서 query string을 제외하는 것과 브라우저 URL에서 query string을 제거하는 것은 서로 다른 동작이에요.



* **확인해 주세요**
  * 캐시 또는 Redirect 설정으로 브라우저 최종 URL에서 <mark style="color:red;">`tcid`</mark>가 삭제되지 않는지 확인해 주세요.
  * 정적 페이지 생성 과정에서 Canonical Redirect가 query string을 삭제하지 않는지 확인해 주세요.
  * 캐시된 HTML이 로드될 때 현재 브라우저 URL에 <mark style="color:red;">`tcid`</mark>가 남아 있는지 확인해 주세요.
* **권장해요**
  * 캐시 키 최적화는 가능하지만, 사용자의 요청 URL과 브라우저 최종 URL에서는 <mark style="color:red;">`tcid`</mark>를 유지해 주세요.
  * 캐시된 HTML에서도 픽셀이 현재 URL의 <mark style="color:red;">`tcid`</mark>를 정상적으로 읽을 수 있도록 설정해 주세요.

***

## QA 체크리스트

사이트 배포 전후 아래 항목을 확인해 주세요.

1. 테스트용 랜딩 URL을 열어주세요.

```
https://www.example.com/?tcid=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaa-00000000000000000000000000000000&utm_source=toss
```

1. 페이지가 완전히 로드된 뒤 주소창에 <mark style="color:red;">`tcid`</mark>가 남아 있는지 확인해주세요.
2. 주소창에서 <mark style="color:red;">`tcid`</mark>가 사라진다면, 사라지는 시점이 서버 리다이렉트인지 프론트엔드 URL 정리인지 확인해주세요.
3. 브라우저 개발자 도구의 Network 탭에서 픽셀 이벤트 요청을 찾아주새요.

```
https://lex.toss.im/api/lex/event/v2
```

1. 요청 본문에 <mark style="color:red;">`tcid`</mark>가 포함되어 있는지 확인해주세요.
2. 구매, 회원가입, 상담 신청 같은 실제 전환 완료 페이지에서도 이벤트 요청이 발생하고 <mark style="color:red;">`tcid`</mark>가 포함되는지 확인해주세요.
3. CDN, WAF, 서버, 프론트엔드 라우터 설정 변경 후 같은 테스트를 반복해주세요.

***

## 개발팀 확인 사항

아래 항목을 개발팀 또는 인프라 담당자에게 전달해 주세요.

* 광고 랜딩 URL의 query string을 삭제하지 않아요.
* 서버 리다이렉트의 Location URL에 기존 query string을 유지해요.
* CDN/Edge rewrite에서 기존 query string을 목적지 URL에 전달해요.
* WAF 또는 보안 프록시의 query allowlist에 tcid를 포함해요.
* 프론트엔드 URL 정규화 로직이 픽셀 실행 전에 tcid 삭제되지 않도록 설정해요.
* 전환 완료 페이지에도 픽셀이 설치되어 있고 정상적으로 이벤트를 전송하는지 확인해요.

***

## 전환 누락이 의심된다면

아래 순서대로 확인해 주세요.

1. 광고 클릭 URL에 <mark style="color:red;">`tcid`</mark>가 포함되어 있는지 확인해요.
2. 최종 랜딩 URL까지 <mark style="color:red;">`tcid`</mark>가 유지되는지 확인해요.
3. 픽셀 이벤트 요청에 <mark style="color:red;">`tcid`</mark>가 포함되어 있는지 확인해요.
4. 전환 완료 페이지에서 이벤트가 정상적으로 전송되는지 확인해요.
5. 최근 CDN, WAF, 리다이렉트, 라우터 설정이 변경된 것은 없는지 확인해요.

최종 랜딩 URL에는 <mark style="color:red;">`tcid`</mark>가 있지만 이벤트 요청에는 없다면 픽셀 설치 또는 실행 순서를 확인해 주세요.

반대로 최종 랜딩 URL에서 <mark style="color:red;">`tcid`</mark>가 이미 사라졌다면 픽셀 문제가 아니라 URL 전달 과정에서 값이 유실된 것이에요.
