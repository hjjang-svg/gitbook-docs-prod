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

# 광고 성과 측정 연동 알아보기

광고 성과를 측정하거나 잠재고객 정보를 자동으로 받으려면 캠페인 목적, 랜딩 환경, 사용 중인 측정 도구를 함께 확인해요. 모든 광고에 같은 연동이 필요한 것은 아니니, 만들려는 캠페인 문서에서 필요한 연동을 먼저 확인해 주세요.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FbGIS7WpOZAYONLpc67qM%2Ftracking.png?alt=media&#x26;token=de71ed18-21fb-46e1-baa8-5596e8af7310" alt="전환 추적 코드에서 MMP와 토스 픽셀로 이어지는 광고 성과 측정 연동 구조"><figcaption><p>MMP와 토스 픽셀을 활용한 광고 성과 측정 연동 방법</p></figcaption></figure>

## 전환 추적 코드 준비하기

앱 또는 웹 광고 성과 측정에 사용할 전환 추적 코드를 만들고 관리해요. 기존 코드를 공유·이관하거나 지원하는 전환 이벤트와 연동 상태도 확인할 수 있어요.

{% content-ref url="tag/" %}
[tag](tag/)
{% endcontent-ref %}

## MMP로 광고 성과 측정하기

사용 중인 모바일 측정 파트너(MMP)를 토스애즈와 연동해 광고 성과를 측정해요. MMP는 앱과 웹 측정을 지원할 수 있으며, 지원 범위와 설정 방법은 MMP마다 달라요.

{% content-ref url="mat/" %}
[mat](mat/)
{% endcontent-ref %}

## 토스 픽셀로 웹 광고 성과 측정하기

웹사이트에서 발생한 전환 이벤트를 수집하려면 토스 픽셀을 설치해요. 자사몰, 카페24, 메이크샵 가운데 사용하는 환경에 맞는 설치 문서를 확인할 수 있어요.

{% content-ref url="tosspixel/" %}
[tosspixel](tosspixel/)
{% endcontent-ref %}

웹 광고 성과는 MMP나 토스 픽셀로 측정할 수 있어요. 사용 중인 도구와 지원 범위를 기준으로 연동 방법을 선택해 주세요.

## 잠재고객 정보를 자동으로 받기

잠재고객 모으기 캠페인에서 제출된 정보를 광고주 서버로 자동 전송하려면 웹훅을 연동해요.

[잠재고객 모으기 웹훅 연동 가이드](webhook.md)
