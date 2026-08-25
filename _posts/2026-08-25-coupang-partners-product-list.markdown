---
layout: post
title: "쿠팡 파트너스 추천 제품 리스트"
date: 2026-08-25 10:00:00 +0900
categories: review

# ── 쿠팡 파트너스 설정 ───────────────────────────────
# partner_id: 쿠팡 파트너스 아이디(lptag). 본인 것으로 교체하세요.
partner_id: "AF0000000"

# ── 제품 목록 ────────────────────────────────────────
# id    : 쿠팡 제품번호 (상품 URL의 /vp/products/ 뒤 숫자) ← 필수
# name  : 화면에 표시할 상품명                              ← 필수
# link  : 파트너스에서 생성한 단축링크(link.coupang.com/a/…) ← 있으면 이걸 우선 사용
# price : 가격 표기 (선택)
# image : 상품 이미지 주소 (선택, 없으면 자리표시자 표시)
# note  : 한 줄 코멘트 (선택)
products:
  - id: "0000000001"
    name: "제주 탐사수 2L, 12개"
    link: ""
    price: "9,900원"
    image: ""
    note: "물은 역시 탐사수. 저렴하면서 물맛이 괜찮아 항상 믿고 구매합니다."

  - id: "0000000002"
    name: "두 번째 상품명"
    link: ""
    price: ""
    image: ""
    note: "한 줄 사용 후기를 적는 자리입니다."

  - id: "0000000003"
    name: "세 번째 상품명"
    link: ""
    price: ""
    image: ""
    note: ""
---

<p class="cp-disclosure">* 이 게시물은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.</p>

직접 사용해보고 괜찮았던 제품들을 한자리에 모아 정리합니다. 각 카드의 제품번호는 쿠팡 상품 페이지 주소에 들어가는 번호와 같습니다. 목록은 계속 업데이트할 예정입니다.

<div class="cp-grid">
{% for p in page.products %}
  {% if p.link and p.link != "" %}
    {% assign product_url = p.link %}
  {% else %}
    {% assign product_url = "https://www.coupang.com/vp/products/" | append: p.id | append: "?lptag=" | append: page.partner_id | append: "&subid=blog" %}
  {% endif %}
  <a class="cp-card" href="{{ product_url }}" target="_blank" rel="nofollow sponsored noopener">
    <div class="cp-thumb">
      {% if p.image and p.image != "" %}
        <img src="{{ p.image }}" alt="{{ p.name }}" loading="lazy">
      {% else %}
        <span class="cp-thumb-empty">이미지 준비중</span>
      {% endif %}
    </div>
    <div class="cp-body">
      <div class="cp-name">{{ p.name }}</div>
      {% if p.note and p.note != "" %}<div class="cp-note">{{ p.note }}</div>{% endif %}
      <div class="cp-meta">
        {% if p.price and p.price != "" %}<span class="cp-price">{{ p.price }}</span>{% endif %}
        <span class="cp-pid">제품번호 {{ p.id }}</span>
      </div>
      <div class="cp-cta">COUPANG 에서 보기 →</div>
    </div>
  </a>
{% endfor %}
</div>

<p class="cp-disclosure cp-disclosure-bottom">* 이 게시물은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.</p>

<style>
.cp-disclosure{
  background:#fbfbfb; border:1px solid #e6e6e6; border-left:3px solid #d33;
  border-radius:4px; padding:12px 14px; margin:0 0 28px;
  font-size:13.5px; color:#666; line-height:1.6;
}
.cp-disclosure-bottom{ margin:36px 0 0; }
.cp-grid{
  display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr));
  gap:16px; margin:28px 0;
}
.cp-card{
  display:flex; gap:14px; align-items:stretch;
  border:1px solid #e6e6e6; border-radius:8px; padding:14px;
  background:#fff; text-decoration:none !important; color:inherit;
  transition:box-shadow .15s ease, border-color .15s ease, transform .15s ease;
}
.cp-card:hover{ border-color:#c9c9c9; box-shadow:0 3px 12px rgba(0,0,0,.07); transform:translateY(-1px); }
.cp-thumb{
  flex:0 0 84px; width:84px; height:84px; border-radius:6px; overflow:hidden;
  background:#f4f5f6; display:flex; align-items:center; justify-content:center;
}
.cp-thumb img{ width:100%; height:100%; object-fit:contain; display:block; }
.cp-thumb-empty{ font-size:11px; color:#aaa; text-align:center; line-height:1.4; }
.cp-body{ flex:1 1 auto; min-width:0; display:flex; flex-direction:column; }
.cp-name{ font-size:15.5px; font-weight:600; color:#111; line-height:1.4; margin-bottom:4px; }
.cp-note{ font-size:13px; color:#777; line-height:1.55; margin-bottom:6px; }
.cp-meta{ display:flex; flex-wrap:wrap; gap:8px; align-items:center; margin-top:auto; }
.cp-price{ font-size:14px; font-weight:700; color:#111; }
.cp-pid{ font-size:11.5px; color:#999; background:#f4f5f6; border-radius:3px; padding:2px 6px; }
.cp-cta{ font-size:12.5px; color:#346aff; margin-top:8px; font-weight:600; }
@media (max-width:480px){ .cp-thumb{ flex-basis:66px; width:66px; height:66px; } }
</style>
