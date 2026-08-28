---
layout: linkpage
title: "카카오몬 추천 제품"
date: 2026-08-25 10:00:00 +0900
categories: review
permalink: /kakaomon/
brand: "카카오몬"
brand_short: "카카오몬"

# ── 쿠팡 파트너스 설정 ───────────────────────────────
# partner_id: 쿠팡 파트너스 아이디(lptag). 본인 것으로 교체하세요.
partner_id: "AF5631083"

# ── 제품 목록 ────────────────────────────────────────
# id    : 쿠팡 제품번호 (상품 URL의 /vp/products/ 뒤 숫자) ← 필수
# name  : 화면에 표시할 상품명                              ← 필수
# link  : 파트너스에서 생성한 단축링크(link.coupang.com/a/…) ← 있으면 이걸 우선 사용
# price : 가격 표기 (선택)
# image : 상품 이미지 주소 (선택, 없으면 자리표시자 표시)
# note  : 한 줄 코멘트 (선택)
products:
  - id: "9629242446"
    name: "파르셀 계란찜기 에그쿠커 2단 14구 올스텐 타이머 SUS304, CES-397W"
    link: ""
    price: "32,900원"
    image: "https://thumbnail.coupangcdn.com/thumbnails/remote/657x657q90trim/image/vendor_inventory/28a6/0bc406dea099ad0b92692cde8e187444a1f53f15965f63e5351e27545784.png"
    note: ""

  - id: "9624994677"
    name: "슈퍼인 헬스장 맥세이프 핸드폰 거치대 360도 회전 양면자석 스마트폰 홀더"
    link: ""
    price: "28,620원"
    image: "/assets/img/kakaomon/mount.jpg"
    note: ""

  - id: "9557438411"
    name: "톰앤하이크 철봉 후크 스트랩 매달리기 턱걸이 풀업 그립"
    link: ""
    price: "13,400원"
    image: "/assets/img/kakaomon/pullup-strap.jpg"
    note: ""

  - id: "9198377251"
    name: "Mirsh 헬스 손바닥 보호 턱걸이 그립 스트랩 밴드"
    link: ""
    price: "8,910원"
    image: "/assets/img/kakaomon/palm-grip.jpg"
    note: ""
---

<div class="ap">

  <p class="ap-disclose">이 게시물은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.</p>

  <header class="ap-hero">
    <svg class="ap-logo" viewBox="0 0 120 120" role="img" aria-label="카카오몬 로고">
      <!-- 배경 -->
      <circle cx="60" cy="60" r="58" fill="#FFC12B"/>
      <!-- 귀 -->
      <circle cx="27" cy="57" r="11.5" fill="#8B5E3C"/>
      <circle cx="27" cy="57" r="6" fill="#C9926A"/>
      <circle cx="93" cy="57" r="11.5" fill="#8B5E3C"/>
      <circle cx="93" cy="57" r="6" fill="#C9926A"/>
      <!-- 머리 -->
      <circle cx="60" cy="62" r="29" fill="#8B5E3C"/>
      <!-- 이마 앞머리 -->
      <path d="M42 46c4-8 11-12 18-12s14 4 18 12c-5-4-11-6-18-6s-13 2-18 6z" fill="#6F4728"/>
      <!-- 얼굴 -->
      <ellipse cx="60" cy="70" rx="19" ry="15.5" fill="#F7E6D2"/>
      <!-- 눈 -->
      <circle cx="52" cy="65.5" r="3.6" fill="#3B2A1E"/>
      <circle cx="68" cy="65.5" r="3.6" fill="#3B2A1E"/>
      <circle cx="53.2" cy="64.3" r="1.2" fill="#FFFFFF"/>
      <circle cx="69.2" cy="64.3" r="1.2" fill="#FFFFFF"/>
      <!-- 코 -->
      <ellipse cx="56.6" cy="73" rx="1.6" ry="1.2" fill="#B08968"/>
      <ellipse cx="63.4" cy="73" rx="1.6" ry="1.2" fill="#B08968"/>
      <!-- 입 -->
      <path d="M53 77.5c3.4 3.8 10.6 3.8 14 0" fill="none" stroke="#B08968"
            stroke-width="2.6" stroke-linecap="round"/>
    </svg>
    <h1 class="ap-title">{{ page.brand | default: site.title }}</h1>
    <p class="ap-sub">추천 제품 모음</p>
  </header>

  <ul class="ap-list">
  {%- for p in page.products -%}
    {%- if p.link and p.link != "" -%}
      {%- assign product_url = p.link -%}
    {%- else -%}
      {%- assign product_url = "https://www.coupang.com/vp/products/" | append: p.id | append: "?lptag=" | append: page.partner_id | append: "&subid=blog" -%}
    {%- endif -%}
    <li class="ap-item">
      <a class="ap-row" href="{{ product_url }}" target="_blank" rel="nofollow sponsored noopener">
        <span class="ap-num">{{ forloop.index | prepend: '0' | slice: -2, 2 }}</span>
        <span class="ap-thumb">
          {%- if p.image and p.image != "" -%}
          <img src="{{ p.image }}" alt="{{ p.name | escape }}" loading="lazy">
          {%- endif -%}
        </span>
        <span class="ap-body">
          <span class="ap-name">{{ p.name }}</span>
        </span>
        <svg class="ap-chev" viewBox="0 0 12 20" aria-hidden="true"><polyline points="2,2 10,10 2,18"></polyline></svg>
      </a>
    </li>
  {%- endfor -%}
  </ul>

  <p class="ap-disclose ap-disclose-bottom">이 게시물은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.</p>
</div>

<style>
body.layout-linkpage{
  background:#fff;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}
body.layout-linkpage .page-content{ padding:0; }
body.layout-linkpage .wrapper{ max-width:none; margin:0; padding:0; }

.ap{
  max-width:680px; margin:0 auto; padding:0 22px 96px;
  font-family:-apple-system,BlinkMacSystemFont,"SF Pro Text","SF Pro Display",
    "Pretendard","Apple SD Gothic Neo","Noto Sans KR",sans-serif;
  color:#1d1d1f;
}

.ap-disclose{
  margin:18px 0 0; padding:14px 18px;
  background:#f5f5f7; border-radius:14px;
  font-size:14.5px; line-height:1.55; font-weight:500;
  color:#3f3f45; letter-spacing:-.012em; text-align:center;
}
.ap-disclose-bottom{
  margin:56px 0 0; padding:14px 18px;
  background:transparent; border-top:1px solid #ececee; border-radius:0;
  font-size:13px; font-weight:400; color:#86868b;
  padding-top:22px;
}

.ap-hero{ padding:44px 0 44px; text-align:center; }
.ap-logo{ width:86px; height:86px; display:block; margin:0 auto 20px; }
.ap-title{
  margin:0; font-size:44px; line-height:1.08; font-weight:600;
  letter-spacing:-.024em; color:#1d1d1f;
}
.ap-sub{
  margin:10px 0 0; font-size:19px; line-height:1.42;
  font-weight:400; letter-spacing:-.012em; color:#86868b;
}

.ap-list{ list-style:none; margin:0; padding:0; }
.ap-item + .ap-item{ border-top:1px solid #ececee; }

.ap-row{
  display:flex; align-items:center; gap:18px;
  padding:18px 12px; margin:0 -12px; border-radius:14px;
  text-decoration:none !important; color:inherit;
  transition:background-color .18s ease;
}
.ap-row:hover{ background:#f5f5f7; }
.ap-row:hover .ap-chev{ transform:translateX(2px); }

.ap-num{
  flex:0 0 auto; width:38px;
  font-size:22px; font-weight:600; color:#1d1d1f;
  letter-spacing:-.02em; font-variant-numeric:tabular-nums;
  text-align:center;
}

.ap-thumb{
  flex:0 0 76px; width:76px; height:76px;
  border-radius:14px; overflow:hidden; background:#f5f5f7;
  display:flex; align-items:center; justify-content:center;
}
.ap-thumb img{ width:100%; height:100%; object-fit:cover; display:block; }

.ap-body{ flex:1 1 auto; min-width:0; display:flex; flex-direction:column; justify-content:center; }
.ap-name{
  font-size:17px; line-height:1.38; font-weight:500;
  letter-spacing:-.014em; color:#1d1d1f; word-break:keep-all;
}
.ap-chev{
  flex:0 0 auto; width:9px; height:15px; margin-left:4px;
  fill:none; stroke:#c7c7cc; stroke-width:2;
  stroke-linecap:round; stroke-linejoin:round;
  transition:transform .18s ease;
}

@media (max-width:520px){
  .ap{ padding:0 18px 72px; }
  .ap-hero{ padding:34px 0 32px; }
  .ap-logo{ width:74px; height:74px; margin-bottom:16px; }
  .ap-disclose{ font-size:13.5px; padding:13px 15px; }
  .ap-title{ font-size:34px; }
  .ap-sub{ font-size:17px; }
  .ap-row{ gap:14px; padding:16px 10px; margin:0 -10px; }
  .ap-num{ width:32px; font-size:19px; }
  .ap-thumb{ flex-basis:66px; width:66px; height:66px; }
  .ap-name{ font-size:16px; }
}
</style>
