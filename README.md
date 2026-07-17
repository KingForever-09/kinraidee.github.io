<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>วันนี้กินอะไรดีนะ?</title>
<style>
  :root{
    --maroon:#c91a5c;
    --header-maroon:#7B1D1D;
    --cream:#fef0d6;
    --teal:#3ddbb8;
    --blue:#4f8eea;
    --pink:#f5618a;
    --yellow:#ffb648;
    --brown:#60391f;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    font-family:'Segoe UI',Tahoma,sans-serif;
    background:var(--cream);
    color:#222;
  }
  /* HEADER */
  header{
    background:var(--header-maroon);
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:14px 30px;
    flex-wrap:wrap;
    gap:10px;
    position:sticky;
    top:0;
    z-index:300;
  }
  .close-btn{
    background:none;
    border:none;
    color:#fff;
    font-size:28px;
    cursor:pointer;
    line-height:1;
  }
  nav{
    display:flex;
    gap:14px;
    flex-wrap:wrap;
    flex:1;
    justify-content:center;
  }
  nav a{
    background:#fff;
    border:2px solid #fff;
    border-radius:25px;
    padding:8px 22px;
    font-weight:bold;
    cursor:pointer;
    color:var(--header-maroon);
    font-size:14px;
    text-decoration:none;
    transition:background .2s;
  }
  nav a:hover{ background:var(--cream); }
  .auth-buttons{ display:flex; gap:10px; }
  .login-btn{
    background:transparent;
    border:2px solid #fff;
    color:#fff;
    border-radius:25px;
    padding:8px 22px;
    font-weight:bold;
    cursor:pointer;
  }
  .signup-btn{
    background:#fff;
    border:2px solid #fff;
    color:var(--header-maroon);
    border-radius:25px;
    padding:8px 22px;
    font-weight:bold;
    cursor:pointer;
  }

  /* HERO */
  .hero{
    position:relative;
    overflow:hidden;
    padding:50px 20px 30px;
    text-align:center;
  }
  h1.title{
    color:var(--maroon);
    font-size:3.2rem;
    margin:0 0 10px;
    position:relative;
    z-index:2;
  }
  .subtitle{
    max-width:650px;
    margin:0 auto 25px;
    position:relative;
    z-index:2;
    line-height:1.6;
  }

  /* CATEGORY SELECT */
  .category-select{
    position:relative;
    z-index:2;
    margin-bottom:25px;
  }
  .category-select p{
    font-weight:bold;
    color:var(--brown);
    margin-bottom:12px;
    font-size:1.05rem;
  }
  .cat-buttons{
    display:flex;
    gap:16px;
    justify-content:center;
    flex-wrap:wrap;
  }
  .cat-btn{
    background:#fff;
    border:3px solid var(--maroon);
    color:var(--maroon);
    padding:14px 28px;
    border-radius:20px;
    font-weight:bold;
    font-size:1.05rem;
    cursor:pointer;
    transition:all .2s;
    display:flex;
    align-items:center;
    gap:8px;
  }
  .cat-btn:hover{ transform:translateY(-3px); box-shadow:0 6px 14px rgba(0,0,0,0.15); }
  .cat-btn.active{
    background:var(--maroon);
    color:#fff;
  }

  .spin-btn{
    background:var(--brown);
    color:#fff;
    border:none;
    padding:14px 50px;
    font-size:1.3rem;
    font-weight:bold;
    border-radius:30px;
    cursor:pointer;
    position:relative;
    z-index:2;
    margin-bottom:30px;
    transition:transform .15s ease, background .2s;
  }
  .spin-btn:hover:not(:disabled){ background:#5e3a26; transform:scale(1.05); }
  .spin-btn:disabled{ opacity:0.5; cursor:not-allowed; transform:none; }

  /* WHEEL */
  .wheel-wrap{
    position:relative;
    width:660px;
    max-width:90vw;
    margin:0 auto 20px;
    z-index:2;
  }
  .pointer{
    width:0;
    height:0;
    border-left:30px solid transparent;
    border-right:30px solid transparent;
    border-top:40px solid var(--pink);
    margin:0 auto;
    position:relative;
    top:10px;
    z-index:5;
  }
  #wheelCanvas{
    width:100%;
    height:auto;
    border-radius:50%;
    border:10px solid var(--pink);
    box-shadow:0 0 0 6px #fff inset;
    display:block;
    transition: transform 4s cubic-bezier(0.17, 0.67, 0.12, 0.99);
  }
  .wheel-wrap.disabled #wheelCanvas{ opacity:0.4; filter:grayscale(60%); }
  .result-banner{
    margin-top:15px;
    font-size:1.6rem;
    font-weight:bold;
    color:var(--maroon);
    min-height:40px;
    position:relative;
    z-index:2;
  }

  /* DECORATIVE FOOD EMOJI (replaces broken hot-linked PNGs — no network dependency, never breaks) */
  .deco-emoji{
    position:absolute;
    z-index:1;
    user-select:none;
    pointer-events:none;
    filter:drop-shadow(0 8px 14px rgba(0,0,0,0.20));
    line-height:1;
  }

  /* CONFETTI / SQUIGGLY DECORATIONS */
  .confetti-layer{
    position:absolute;
    inset:0;
    width:100%;
    height:100%;
    z-index:0;
    pointer-events:none;
    overflow:hidden;
  }

  /* CONTENT SECTION */
  .content-section{
    display:flex;
    gap:30px;
    padding:30px 60px 60px;
    flex-wrap:wrap;
    align-items:flex-start;
    scroll-margin-top:90px;
  }
  .description-box{
    background:#fff;
    border-radius:20px;
    padding:30px;
    flex:2;
    min-width:300px;
    line-height:1.9;
    box-shadow:0 4px 10px rgba(0,0,0,0.05);
  }
  .menu-list-box{
    background:#fff;
    border-radius:20px;
    padding:30px;
    flex:1;
    min-width:250px;
    box-shadow:0 4px 10px rgba(0,0,0,0.05);
    max-height:560px;
    overflow-y:auto;
  }
  .menu-list-box h2{
    color:var(--maroon);
    margin-top:0;
  }
  .menu-list-box .edit-hint{
    font-size:0.85rem;
    color:#888;
    margin-bottom:15px;
  }
  #foodList{
    list-style:none;
    padding:0;
    margin:0;
  }
  #foodList li{
    background:var(--cream);
    border-radius:10px;
    padding:10px 14px;
    margin-bottom:8px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    cursor:pointer;
  }
  #foodList li .del-btn{
    background:var(--pink);
    color:#fff;
    border:none;
    border-radius:50%;
    width:24px;
    height:24px;
    cursor:pointer;
    font-size:14px;
    line-height:1;
    flex-shrink:0;
  }
  .add-food-form{
    display:flex;
    gap:8px;
    margin-top:15px;
  }
  .add-food-form input{
    flex:1;
    padding:8px 12px;
    border-radius:8px;
    border:1px solid #ddd;
  }
  .add-food-form button{
    background:var(--teal);
    color:#fff;
    border:none;
    padding:8px 16px;
    border-radius:8px;
    cursor:pointer;
    font-weight:bold;
  }

  /* OUR MENU SECTION */
  .our-menu{
    padding:30px 60px 60px;
  }
  .our-menu h2{
    font-size:2.2rem;
    margin-bottom:10px;
  }
  .our-menu > p.menu-intro{
    margin-bottom:30px;
    color:#555;
  }
  .category-box-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit, minmax(260px, 1fr));
    gap:26px;
  }
  .category-box{
    position:relative;
    border-radius:20px;
    overflow:hidden;
    cursor:pointer;
    height:220px;
    box-shadow:0 6px 16px rgba(0,0,0,0.12);
    transition:transform .2s, box-shadow .2s;
    background:#e8e0d0;
  }
  .category-box:hover{
    transform:translateY(-5px);
    box-shadow:0 12px 24px rgba(0,0,0,0.18);
  }
  .category-box img{
    width:100%;
    height:100%;
    object-fit:cover;
    display:block;
    filter:brightness(0.75);
  }
  .category-box .cat-box-overlay{
    position:absolute;
    inset:0;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    color:#fff;
    text-align:center;
    padding:10px;
  }
  .category-box .cat-box-overlay h3{
    font-size:1.8rem;
    margin:0 0 6px;
    text-shadow:0 2px 6px rgba(0,0,0,0.5);
  }
  .category-box .cat-box-overlay span{
    font-size:0.95rem;
    background:rgba(255,255,255,0.25);
    padding:6px 16px;
    border-radius:20px;
    backdrop-filter:blur(2px);
  }
  .menu-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill, minmax(210px, 1fr));
    gap:22px;
  }
  .full-menu-modal-box{
    max-width:1000px;
    width:95%;
    max-height:85vh;
    overflow-y:auto;
    text-align:left;
  }
  .full-menu-modal-box .modal-top-bar{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:18px;
  }
  .full-menu-modal-box .modal-top-bar h2{
    color:var(--maroon);
    margin:0;
  }
  .full-menu-modal-box .modal-close-x{
    background:var(--cream);
    border:none;
    border-radius:50%;
    width:36px;
    height:36px;
    font-size:18px;
    cursor:pointer;
    color:var(--brown);
  }
  .menu-card{
    background:#fff;
    border-radius:14px;
    overflow:hidden;
    box-shadow:0 4px 10px rgba(0,0,0,0.08);
    cursor:pointer;
    transition:transform .15s;
  }
  .menu-card:hover{ transform:translateY(-4px); }
  .menu-card .num{
    color:#999;
    font-size:0.8rem;
    padding:8px 12px 0;
  }
  .menu-card h4{
    margin:4px 0 10px;
    font-size:1.05rem;
    padding:0 12px;
    min-height:48px;
  }
  .menu-card img{
    width:100%;
    height:150px;
    object-fit:cover;
    display:block;
    background:#e8e0d0;
  }
  .menu-card .kcal-badge{
    display:inline-block;
    background:var(--cream);
    color:var(--brown);
    font-size:0.8rem;
    font-weight:bold;
    padding:4px 10px;
    border-radius:20px;
    margin:0 12px 12px;
  }
  .more-below{
    text-align:center;
    padding:0 0 50px;
    font-weight:bold;
    color:var(--brown);
  }
  .arrow-down{
    font-size:2rem;
    margin-top:10px;
    animation: bounce 1.5s infinite;
  }
  @keyframes bounce{
    0%,100%{transform:translateY(0);}
    50%{transform:translateY(10px);}
  }

  /* MODAL (generic - edit + result + nutrition) */
  .modal-overlay{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.55);
    display:none;
    align-items:center;
    justify-content:center;
    z-index:400;
    padding:20px;
  }
  .modal-overlay.active{ display:flex; }
  .modal-box{
    background:#fff;
    border-radius:16px;
    padding:30px;
    max-width:400px;
    width:90%;
    text-align:center;
  }
  .modal-box h3{ color:var(--maroon); }
  .modal-box input{
    width:100%;
    padding:10px;
    border-radius:8px;
    border:1px solid #ddd;
    margin:15px 0;
  }
  .modal-actions{
    display:flex;
    gap:10px;
    justify-content:center;
  }
  .modal-actions button{
    padding:10px 20px;
    border-radius:8px;
    border:none;
    cursor:pointer;
    font-weight:bold;
  }
  .save-btn{ background:var(--teal); color:#fff; }
  .cancel-btn{ background:#eee; color:#333; }

  /* Result / nutrition modal */
  .result-modal-box{
    max-width:440px;
  }
  .result-modal-box img{
    width:100%;
    height:200px;
    object-fit:cover;
    border-radius:12px;
    margin-bottom:16px;
    background:#e8e0d0;
  }
  .result-modal-box h2{
    color:var(--maroon);
    margin:0 0 4px;
  }
  .result-cat-tag{
    display:inline-block;
    background:var(--cream);
    color:var(--brown);
    font-size:0.8rem;
    font-weight:bold;
    padding:4px 12px;
    border-radius:20px;
    margin-bottom:14px;
  }
  .nutrition-grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:10px;
    margin:14px 0;
    text-align:left;
  }
  .nutrition-item{
    background:var(--cream);
    border-radius:10px;
    padding:10px 12px;
  }
  .nutrition-item .label{ font-size:0.78rem; color:#777; }
  .nutrition-item .value{ font-size:1.1rem; font-weight:bold; color:var(--brown); }
  .benefit-box{
    background:#eafaf4;
    border-left:4px solid var(--teal);
    border-radius:10px;
    padding:12px 14px;
    text-align:left;
    margin-top:14px;
    font-size:0.92rem;
    line-height:1.5;
  }
  .benefit-box b{ color:#1a8c6f; }
  .close-modal-btn{
    margin-top:20px;
    background:var(--maroon);
    color:#fff;
    border:none;
    padding:10px 28px;
    border-radius:25px;
    font-weight:bold;
    cursor:pointer;
  }

  /* CONTACT MODAL (from code #2) */
  .contact-modal-box{
    max-width:380px;
  }
  .contact-modal-box h3{
    font-size:1.4rem;
    margin-bottom:4px;
  }
  .contact-modal-box .cm-sub{
    font-size:0.85rem;
    color:#999;
    margin-bottom:20px;
  }
  .social-links{
    display:flex;
    flex-direction:column;
    gap:12px;
    margin-bottom:10px;
    text-align:left;
  }
  .social-link{
    display:flex;
    align-items:center;
    gap:14px;
    padding:12px 18px;
    border-radius:14px;
    text-decoration:none;
    font-weight:700;
    font-size:14px;
    transition:transform .15s, box-shadow .15s;
    box-shadow:0 2px 8px rgba(0,0,0,0.08);
  }
  .social-link:hover{ transform:translateY(-2px); box-shadow:0 6px 16px rgba(0,0,0,0.14); }
  .social-link .sl-icon{
    width:38px;
    height:38px;
    border-radius:10px;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-shrink:0;
    font-size:20px;
  }
  .social-link .sl-info{ text-align:left; }
  .social-link .sl-name{ font-size:13px; font-weight:800; display:block; color:#333; }
  .social-link .sl-handle{ font-size:12px; font-weight:400; opacity:0.7; display:block; color:#333; }
  .ig-link{ background:#fff3f8; }
  .ig-link .sl-icon{ background:linear-gradient(135deg,#f09433,#e6683c,#dc2743,#cc2366,#bc1888); }
  .ig2-link{ background:#f3f0ff; }
  .ig2-link .sl-icon{ background:linear-gradient(135deg,#833ab4,#fd1d1d,#fcb045); }
  .ig3-link{ background:#f0faff; }
  .ig3-link .sl-icon{ background:linear-gradient(135deg,#405de6,#5851db,#833ab4,#c13584,#e1306c,#fd1d1d); }

  /* FAQ MODAL */
  .faq-modal-box{
    max-width:520px;
    text-align:left;
    max-height:80vh;
    overflow-y:auto;
  }
  .faq-modal-box h3{ text-align:center; margin-bottom:18px; }
  .faq-item{ margin-bottom:16px; }
  .faq-item .q{ font-weight:bold; color:var(--brown); margin-bottom:4px; }
  .faq-item .a{ font-size:0.92rem; color:#555; line-height:1.6; }

  /* CREATORS / FOOTER (styled like code #2) */
  footer{
    background:var(--header-maroon);
    color:#fff;
    padding:36px 24px 26px;
    text-align:center;
    scroll-margin-top:90px;
  }
  footer .footer-title{
    font-size:16px;
    font-weight:800;
    margin-bottom:18px;
    letter-spacing:0.5px;
    opacity:0.9;
  }
  .creators-grid{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:16px;
    margin-bottom:22px;
  }
  .creator-card{
    background:rgba(255,255,255,0.10);
    border:1px solid rgba(255,255,255,0.18);
    border-radius:14px;
    padding:12px 22px;
    min-width:210px;
  }
  .creator-card .cr-num{ font-size:11px; opacity:0.55; margin-bottom:2px; }
  .creator-card .cr-name{ font-size:14px; font-weight:700; }
  .creator-card .cr-class{ font-size:12px; opacity:0.65; margin-top:2px; }
  footer .footer-copy{ font-size:12px; opacity:0.5; margin-top:8px; }

  /* TOAST */
  .toast{
    position:fixed;
    bottom:22px;
    left:50%;
    transform:translateX(-50%) translateY(70px);
    background:#222;
    color:#fff;
    padding:10px 24px;
    border-radius:26px;
    font-size:13px;
    opacity:0;
    transition:opacity .25s, transform .25s;
    z-index:999;
    pointer-events:none;
    white-space:nowrap;
  }
  .toast.on{ opacity:1; transform:translateX(-50%) translateY(0); }

  @media (max-width:700px){
    h1.title{ font-size:2rem; }
    .content-section{ padding:20px; }
    .our-menu{ padding:20px; }
    .deco-emoji{ display:none; }
  }
</style>
</head>
<body>

<header>
  <button class="close-btn" aria-label="close" onclick="showToast('ปิดหน้าต่าง (demo)')">&times;</button>
  <nav>
    <a href="#home" onclick="goHome(event)">Home</a>
    <a href="#about" onclick="goAbout(event)">About</a>
    <a href="#contact" onclick="openContact(event)">Contact</a>
    <a href="#faqs" onclick="openFaq(event)">FAQs</a>
  </nav>
  <div class="auth-buttons">
    <button class="login-btn" onclick="showToast('กรุณาเข้าสู่ระบบ (demo)')">Login</button>
    <button class="signup-btn" onclick="showToast('สมัครสมาชิก (demo)')">Sign up</button>
  </div>
</header>

<section class="hero" id="home">

  <!-- CONFETTI / SQUIGGLY DECORATIONS -->
  <div class="confetti-layer" aria-hidden="true">
    <svg width="100%" height="100%" viewBox="0 0 1000 700" preserveAspectRatio="xMidYMid slice" xmlns="http://www.w3.org/2000/svg">
      <path d="M 20 580 Q 60 540 100 580 Q 140 620 180 580 Q 220 540 260 580 Q 300 620 340 580" stroke="#3ddbb8" stroke-width="14" fill="none" stroke-linecap="round"/>
      <path d="M 30 120 Q 70 80 110 120 Q 150 160 190 120 Q 230 80 270 120 Q 310 160 350 120" stroke="#4f8eea" stroke-width="14" fill="none" stroke-linecap="round"/>
      <path d="M 650 60 Q 690 20 730 60 Q 770 100 810 60 Q 850 20 890 60 Q 930 100 970 60" stroke="#f5618a" stroke-width="14" fill="none" stroke-linecap="round"/>
      <path d="M 820 380 Q 860 340 900 380 Q 940 420 980 380" stroke="#ffb648" stroke-width="14" fill="none" stroke-linecap="round"/>
      <path d="M 200 30 Q 220 10 240 30 Q 260 50 280 30" stroke="#3ddbb8" stroke-width="10" fill="none" stroke-linecap="round"/>
      <path d="M 10 340 Q 50 300 90 340 Q 130 380 170 340" stroke="#f5618a" stroke-width="12" fill="none" stroke-linecap="round"/>
      <path d="M 700 620 Q 740 580 780 620 Q 820 660 860 620 Q 900 580 940 620" stroke="#4f8eea" stroke-width="13" fill="none" stroke-linecap="round"/>
      <path d="M 50 200 Q 80 170 110 200 Q 140 230 170 200 Q 200 170 230 200" stroke="#ffb648" stroke-width="11" fill="none" stroke-linecap="round"/>
      <circle cx="380" cy="55" r="14" fill="#3ddbb8" opacity="0.7"/>
      <circle cx="630" cy="640" r="12" fill="#ffb648" opacity="0.7"/>
      <circle cx="960" cy="220" r="10" fill="#f5618a" opacity="0.7"/>
      <circle cx="70" cy="480" r="11" fill="#4f8eea" opacity="0.7"/>
    </svg>
  </div>

  <!-- DECORATIVE FOOD EMOJI (no network calls — cannot break) -->
  <div class="deco-emoji" style="top:10px;left:3%;font-size:80px;transform:rotate(-8deg);">🍗</div>
  <div class="deco-emoji" style="top:90px;left:16%;font-size:60px;transform:rotate(10deg);">🍊</div>
  <div class="deco-emoji" style="top:40px;right:7%;font-size:68px;transform:rotate(6deg);">🧁</div>
  <div class="deco-emoji" style="top:165px;right:20%;font-size:64px;transform:rotate(-5deg);">🍞</div>
  <div class="deco-emoji" style="top:420px;left:4%;font-size:74px;transform:rotate(4deg);">🥗</div>
  <div class="deco-emoji" style="top:445px;right:5%;font-size:64px;transform:rotate(-7deg);">🥦</div>
  <div class="deco-emoji" style="top:510px;right:15%;font-size:68px;transform:rotate(9deg);">🍣</div>

  <h1 class="title">วันนี้กินอะไรดีนะ?</h1>
  <p class="subtitle">ยินดีต้อนรับเข้าสู่เว็บไซต์ วันนี้กินอะไรดีนะ? เลือกหมวดหมู่อาหารที่ต้องการ แล้วคลิกปุ่มด้านล่างเพื่อทำการเริ่มสุ่มอาหาร สามารถแก้ไขได้โดยกดที่รายการอาหารเพื่อแก้ไขรายการอาหาร</p>

  <div class="category-select">
    <p>เลือกหมวดหมู่ก่อนหมุนวงล้อ:</p>
    <div class="cat-buttons">
      <button class="cat-btn" id="catNoodles" onclick="selectCategory('noodles')">🍜 Noodles</button>
      <button class="cat-btn" id="catRice" onclick="selectCategory('rice')">🍚 Rice</button>
      <button class="cat-btn" id="catSweets" onclick="selectCategory('sweets')">🍰 Sweets</button>
    </div>
  </div>

  <button class="spin-btn" id="spinBtn" disabled>หมุน</button>

  <div class="wheel-wrap disabled" id="wheelWrap">
    <div class="pointer"></div>
    <canvas id="wheelCanvas" width="600" height="600"></canvas>
  </div>
  <div class="result-banner" id="resultBanner"></div>
</section>

<section class="content-section" id="about">
  <div class="description-box">
    <p>
      เว็บไซต์นี้มีจุดประสงค์เพื่อช่วยในการตัดสินใจในการเลือกเมนูอาหารที่จะรับประทาน
      โดยที่สามารถเลือกหมวดหมู่ของอาหารที่ประสงค์จะสุ่มได้ และผู้ใช้ยังสามารถแก้ไขรายการอาหารที่จะนำไปสุ่มด้วยตนเองอีกด้วย
      อาหารสามารถทำการสืบค้นได้ภายในเว็บไซต์ตามที่ในฐานข้อมูลมีอยู่ หากไม่พบรายการอาหารที่ท่านต้องการเพิ่ม
      สามารถติดต่อเราโดยกดปุ่ม Contact ด้านบนเพื่อเสนอแนะหรือเพิ่มเมนูอาหารได้ โดยอาหารแต่ละชนิดจะมีการระบุโภชนาการในด้านต่างๆ
      ซึ่งสามารถคลิกที่รายละเอียดของแต่ละเมนูเพื่อดูโภชนาการ รูปภาพอาหารแต่ละเมนูจะถูกดึงมาแบบอัตโนมัติจาก Wikimedia Commons
      ตามชื่อเมนูที่เลือก
    </p>
  </div>

  <div class="menu-list-box">
    <h2 id="foodListTitle">รายการอาหาร</h2>
    <p class="edit-hint">กดเพื่อแก้ไข ✏️ &nbsp;|&nbsp; กดปุ่ม ✕ เพื่อลบ &nbsp;|&nbsp; เลือกหมวดหมู่ก่อนเพื่อแก้ไขรายการ</p>
    <ul id="foodList"></ul>
    <div class="add-food-form">
      <input type="text" id="newFoodInput" placeholder="เพิ่มเมนูใหม่...">
      <button onclick="addFood()">เพิ่ม</button>
    </div>
  </div>
</section>

<section class="our-menu">
  <h2>Our Menu</h2>
  <p class="menu-intro">คลิกที่กล่องหมวดหมู่ด้านล่างเพื่อดูเมนูทั้งหมด 20 รายการในหมวดนั้น — เมนูชุดเดียวกับที่วงล้อด้านบนใช้สุ่ม</p>
  <div class="category-box-grid" id="categoryBoxGrid"></div>
</section>

<div class="more-below">
  More below !
  <div class="arrow-down">⬇️</div>
</div>

<!-- Full Menu Modal -->
<div class="modal-overlay" id="fullMenuModal">
  <div class="modal-box full-menu-modal-box" id="fullMenuModalBox">
    <!-- filled dynamically -->
  </div>
</div>

<!-- Edit Modal -->
<div class="modal-overlay" id="editModal">
  <div class="modal-box">
    <h3>แก้ไขรายการอาหาร</h3>
    <input type="text" id="editInput">
    <div class="modal-actions">
      <button class="save-btn" onclick="saveEdit()">บันทึก</button>
      <button class="cancel-btn" onclick="closeModal()">ยกเลิก</button>
    </div>
  </div>
</div>

<!-- Result / Nutrition Modal -->
<div class="modal-overlay" id="resultModal">
  <div class="modal-box result-modal-box" id="resultModalBox">
    <!-- filled dynamically -->
  </div>
</div>

<!-- Contact Modal (from code #2) -->
<div class="modal-overlay" id="contactModal">
  <div class="modal-box contact-modal-box">
    <h3>ติดต่อเรา</h3>
    <p class="cm-sub">ติดตามเราหรือส่งข้อเสนอแนะเมนูได้ที่ Social Media ด้านล่าง</p>
    <div class="social-links">
      <a class="social-link ig-link" href="https://www.instagram.com/yatsyeyoyo" target="_blank" rel="noopener">
        <div class="sl-icon">📸</div>
        <div class="sl-info">
          <span class="sl-name">Instagram</span>
          <span class="sl-handle">@yatsyeyoyo</span>
        </div>
      </a>
      <a class="social-link ig2-link" href="https://www.instagram.com/4catfart" target="_blank" rel="noopener">
        <div class="sl-icon">📸</div>
        <div class="sl-info">
          <span class="sl-name">Instagram</span>
          <span class="sl-handle">@4catfart</span>
        </div>
      </a>
      <a class="social-link ig3-link" href="https://www.instagram.com/llptsrtx_" target="_blank" rel="noopener">
        <div class="sl-icon">📸</div>
        <div class="sl-info">
          <span class="sl-name">Instagram</span>
          <span class="sl-handle">@llptsrtx_</span>
        </div>
      </a>
    </div>
    <button class="close-modal-btn" onclick="closeContact()">ปิด</button>
  </div>
</div>

<!-- FAQ Modal -->
<div class="modal-overlay" id="faqModal">
  <div class="modal-box faq-modal-box">
    <h3>คำถามที่พบบ่อย (FAQs)</h3>

    <div class="faq-item">
      <div class="q">วงล้อนี้ทำงานอย่างไร?</div>
      <div class="a">เลือกหมวดหมู่อาหารก่อน (Noodles / Rice / Sweets) ปุ่ม "หมุน" จะเปิดใช้งานทันที จากนั้นกดหมุนเพื่อสุ่มเมนูจริงแบบสุ่มทุกครั้ง</div>
    </div>
    <div class="faq-item">
      <div class="q">แก้ไขหรือเพิ่มรายการอาหารได้อย่างไร?</div>
      <div class="a">หลังเลือกหมวดหมู่แล้ว คลิกที่ชื่อเมนูในกล่อง "รายการอาหาร" เพื่อแก้ไขชื่อ กดปุ่ม ✕ เพื่อลบ หรือพิมพ์ชื่อเมนูใหม่ในช่องด้านล่างแล้วกด "เพิ่ม"</div>
    </div>
    <div class="faq-item">
      <div class="q">ข้อมูลโภชนาการแม่นยำแค่ไหน?</div>
      <div class="a">ตัวเลขแคลอรี โปรตีน คาร์โบไฮเดรต และไขมันเป็นค่าประมาณต่อหนึ่งเสิร์ฟเพื่อให้ข้อมูลเบื้องต้นเท่านั้น ไม่สามารถใช้แทนคำแนะนำจากนักโภชนาการได้</div>
    </div>
    <div class="faq-item">
      <div class="q">รูปภาพอาหารมาจากไหน?</div>
      <div class="a">ระบบดึงภาพจาก Wikimedia Commons โดยอัตโนมัติตามชื่อเมนูที่เลือก หากไม่พบภาพที่ตรงกันจะแสดงไอคอนอาหารแทนเพื่อไม่ให้เห็นรูปภาพเสีย</div>
    </div>
    <div class="faq-item">
      <div class="q">อยากเสนอเมนูที่ยังไม่มีในระบบ ทำอย่างไร?</div>
      <div class="a">เพิ่มเองได้ทันทีผ่านช่อง "เพิ่มเมนูใหม่" หรือติดต่อทีมงานผ่านปุ่ม Contact ด้านบนของเว็บไซต์</div>
    </div>

    <button class="close-modal-btn" onclick="closeFaq()">ปิด</button>
  </div>
</div>

<script>
/* ========================================================
   FOOD DATABASE — 20 meals per category, each with
   approximate nutrition facts (per serving) and a benefit note
   (UNCHANGED from the base version — spin & food-db logic untouched)
   ======================================================== */
const FOOD_DB = {
  noodles: [
    {name:"Pad Thai (ผัดไทย)", kcal:486, protein:18, carbs:60, fat:18, benefit:"มีโปรตีนจากกุ้ง/ไข่และถั่วลิสงช่วยเสริมพลังงาน พร้อมถั่วงอกที่ให้ใยอาหาร", img: "https://thai-foodie.com/wp-content/uploads/2025/08/plated-gluten-free-pad-thai.jpg"},
    {name:"Ramen (ราเมง)", kcal:520, protein:24, carbs:65, fat:16, benefit:"น้ำซุปกระดูกอุดมคอลลาเจนช่วยบำรุงข้อต่อและผิวพรรณ", img: "https://cdn.apartmenttherapy.info/image/upload/f_auto,q_auto:eco,c_fill,g_auto,w_1500,ar_3:2/k%2FPhoto%2FRecipes%2F2024-03-tonkotsu-ramen%2Ftonkotsu-ramen-195"},
    {name:"Spaghetti Carbonara", kcal:610, protein:22, carbs:64, fat:26, benefit:"ไข่และชีสให้แคลเซียมและโปรตีนคุณภาพสูงสำหรับซ่อมแซมกล้ามเนื้อ", img: "https://images.services.kitchenstories.io/6glN_4JhpVS9aUiBS7JnGsuDULA=/3840x0/filters:quality(80)/images.kitchenstories.io/wagtailOriginalImages/R2568-photo-final-_0.jpg"},
    {name:"Pho (เฝอ)", kcal:400, protein:25, carbs:55, fat:8, benefit:"ซุปสมุนไพรอบเชย โป๊ยกั๊ก ช่วยลดการอักเสบและดีต่อระบบย่อยอาหาร", img: "https://www.recipetineats.com/tachyon/2019/04/Beef-Pho_6.jpg"},
    {name:"Lasagna", kcal:660, protein:30, carbs:55, fat:32, benefit:"ชั้นชีสและเนื้อสัตว์ให้แคลเซียมและธาตุเหล็กสูง เหมาะมื้อมื้อหลัก", img:"https://amandascookin.com/wp-content/uploads/2025/08/Italian-Lasagna-RCSQ.jpg"},
    {name:"Mac and Cheese", kcal:570, protein:20, carbs:58, fat:27, benefit:"ชีสอุดมแคลเซียมช่วยเสริมสร้างกระดูกให้แข็งแรง", img: "https://images.services.kitchenstories.io/FQPoYXqopSF8apn6ZCB6uEaXVyk=/3840x0/filters:quality(85)/images.kitchenstories.io/wagtailOriginalImages/R3072-final-photo-2.jpg"},
    {name:"Udon (อุด้ง)", kcal:430, protein:14, carbs:78, fat:5, benefit:"คาร์โบไฮเดรตเชิงซ้อนให้พลังงานยาวนาน ไขมันต่ำ", img: "https://thewoksoflife.com/wp-content/uploads/2026/03/beef-udon-niku-udon-16.jpg"},
    {name:"Lo Mein", kcal:480, protein:16, carbs:62, fat:16, benefit:"ผักหลากสีในจานช่วยเพิ่มวิตามินและสารต้านอนุมูลอิสระ", img: "https://static01.nyt.com/images/2025/01/23/multimedia/kc-chicken-lo-mein-plated-lfpb/kc-chicken-lo-mein-plated-lfpb-mediumSquareAt3X.jpg"},
    {name:"Pad See Ew (ผัดซีอิ๊ว)", kcal:455, protein:17, carbs:58, fat:15, benefit:"คะน้าอุดมวิตามินเค ช่วยการแข็งตัวของเลือดและสุขภาพกระดูก", img: "https://s359.kapook.com/pagebuilder/09a92003-6eb9-4d67-b0b5-5334af7bc019.jpg"},
    {name:"Yakisoba (ยากิโซบะ)", kcal:410, protein:15, carbs:56, fat:13, benefit:"กะหล่ำปลีและผักตามฤดูช่วยเสริมใยอาหารและวิตามินซี", img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThhoIBquAjpLzpD8p3iH0LGbyfsU06Epa2_SPstMBNswxFDyhUTffzM5L0&s=10"},
    {name:"Khao Soi (ข้าวซอย)", kcal:540, protein:20, carbs:48, fat:28, benefit:"กะทิและขมิ้นมีสารต้านการอักเสบตามธรรมชาติ", img: "https://www.unileverfoodsolutions.co.th/dam/global-ufs/mcos/SEA/calcmenu/recipes/TH-recipes/chicken-&-other-poultry-dishes/%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B8%A7%E0%B8%8B%E0%B8%AD%E0%B8%A2%E0%B9%84%E0%B8%81%E0%B9%88/main-header.jpg"},
    {name:"Drunken Noodles (ผัดขี้เมา)", kcal:470, protein:18, carbs:55, fat:18, benefit:"ใบกะเพราและพริกช่วยกระตุ้นการเผาผลาญและระบบไหลเวียน", img:"https://www.unileverfoodsolutions.co.th/dam/global-ufs/mcos/SEA/calcmenu/recipes/TH-recipes/pasta-dishes/red-sea-fried-instant-noodle/main-header.jpg"},
    {name:"Singapore Noodles", kcal:445, protein:19, carbs:54, fat:15, benefit:"ผงกะหรี่มีสารต้านอนุมูลอิสระ ช่วยเสริมภูมิคุ้มกัน", img:"https://www.k33kitchen.com/wp-content/uploads/2019/07/k33kitchen_vegan_singapore_noodles_feature.jpg"},
    {name:"Bolognese", kcal:590, protein:28, carbs:58, fat:24, benefit:"เนื้อบดอุดมธาตุเหล็กและวิตามินบี12 ดีต่อการสร้างเม็ดเลือด", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT5Kh-YVPi-5iyGP3H9aOMB3OdtNZfeId2h2AtwxZ1OG91X5Pr-SPrO6qs&s=10"},
    {name:"Soba (โซบะ)", kcal:340, protein:14, carbs:63, fat:2, benefit:"เส้นบัควีตมีรูตินช่วยเสริมความแข็งแรงของหลอดเลือด", img:"https://japanesecooking101.com/zaru-soba-recipe/"},
    {name:"Japchae (จับแช)", kcal:380, protein:10, carbs:60, fat:11, benefit:"วุ้นเส้นมันเทศไขมันต่ำ ผักหลายชนิดเสริมไฟเบอร์", img:"https://aroifin.com/wp-content/uploads/2025/05/cover-Japchae_result.webp"},
    {name:"Bun Cha (บุนฉ่า)", kcal:420, protein:22, carbs:50, fat:14, benefit:"สมุนไพรสดอย่างสะระแหน่ช่วยระบบย่อยอาหารและให้วิตามินเอ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQZHqzjn4kjBdYiNzgIHzwE0mbOtI3xR47e8W9rLUW6NEZTgrx-X1ynQzuv&s=10"},
    {name:"Chow Mein", kcal:460, protein:16, carbs:60, fat:15, benefit:"ผักผัดหลากชนิดช่วยเพิ่มวิตามินซีและใยอาหาร", img:"https://tastesbetterfromscratch.com/wp-content/uploads/2023/10/Chow-Mein-1-500x500.jpg"},
    {name:"Topokki (ต๊อกบกกี)", kcal:400, protein:10, carbs:80, fat:3, benefit:"คาร์โบไฮเดรตสูงให้พลังงานเยอะ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS8b3U0jKlYQ90IB_W-QVkvkdGSAjn1QIn-vKnwG0P0bVLWwoCoiS-ZHUlp&s=10"},

    {name:"Spätzle (เส้นเยอรมัน)", kcal:520, protein:17, carbs:65, fat:18, benefit:"ไข่ในเส้นให้โคลีนช่วยการทำงานของสมองและตับ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThnSZqjQu5-zg8F8ZTqzp-51SIbqTsdsmsWsqvvOww8U2pUERmGIrIZSs&s=10"}
  ],


  rice: [
    {name:"Khao Pad (ข้าวผัด)", kcal:520, protein:18, carbs:68, fat:18, benefit:"ไข่และผักรวมให้พลังงานครบถ้วนในจานเดียว", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSjldz_6Urxw2lnUgksVUJsuRr0giEjAZ--S3fBszRp6Zm3LuAFrj2Sim4&s=10"},
    {name:"Sushi (ซูชิ)", kcal:350, protein:20, carbs:50, fat:8, benefit:"ปลาดิบอุดมโอเมก้า-3 ช่วยบำรุงสมองและหัวใจ", img:"https://takestwoeggs.com/wp-content/uploads/2025/02/Sushi-at-home.jpg"},
    {name:"Biryani (บิรยานี)", kcal:600, protein:24, carbs:70, fat:22, benefit:"เครื่องเทศอย่างขมิ้นและอบเชยมีสารต้านการอักเสบ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSIqWaGoNYGlMXeSbsAt_LDvjKIN8umWidQ-fuFwoDFeQiLJIL_h3x-0E4&s=10"},
    {name:"Paella (ปาเอย่า)", kcal:540, protein:26, carbs:60, fat:18, benefit:"อาหารทะเลให้สังกะสีและซีลีเนียมเสริมภูมิคุ้มกัน", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQPpPSa5sIlosdp5SIdB1LrGrsm31JxjP_T5L7Du7vUcRrjSBhhtyQGIA&s=10"},
    {name:"Risotto", kcal:480, protein:12, carbs:62, fat:18, benefit:"ชีสพาร์เมซานให้แคลเซียมและโปรตีนคุณภาพดี", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQoAO5pBzz8xRKl1c5RkwQySwS0iYYsRckfDa0UhXKLlTR3V8PpmRINu4A&s=10"},
    {name:"Nasi Goreng", kcal:510, protein:17, carbs:65, fat:18, benefit:"พริกและกระเทียมช่วยกระตุ้นระบบเผาผลาญ", img:"https://takestwoeggs.com/wp-content/uploads/2025/03/Overhead-plate-Nasi-Goreng-Indonesian-Fried-Rice-500x500.jpg"},
    {name:"Jollof Rice", kcal:470, protein:13, carbs:70, fat:14, benefit:"มะเขือเทศอุดมไลโคปีนช่วยต้านอนุมูลอิสระ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQbUTmAkVq8NPaHSREK09bmQMtDhN_StzlW2UvtmENcH_Iyk3fLEDOHzyc&s=10"},
    {name:"Bibimbap (บิบิมบับ)", kcal:560, protein:22, carbs:65, fat:20, benefit:"ผักหลากสีให้วิตามินครบถ้วน เหมาะสำหรับมื้อสมดุล", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTX5P2uikUTahMwNLGjYZu8bgfV8hYbVwYBtGM9h3LGtnwPA4Ej0wcKrCnp&s=10"},
    {name:"Khao Man Gai (ข้าวมันไก่)", kcal:600, protein:30, carbs:62, fat:24, benefit:"อกไก่ให้โปรตีนสูง ช่วยซ่อมแซมกล้ามเนื้อ", img:"https://www.allrecipes.com/thmb/dInTiw4LBN4FfnAJG6-mDE4RpLA=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/3572007-5ab08518c35e464bb04fd7dfc535ee47.jpg"},
    {name:"Congee (โจ๊ก)", kcal:250, protein:10, carbs:45, fat:3, benefit:"ย่อยง่าย เหมาะสำหรับผู้ป่วยหรือมื้อเช้าเบาๆ", img:"https://pickledplum.com/wp-content/uploads/2019/11/basic-congee-recipe-3-1200.jpg"},
    {name:"Jambalaya", kcal:540, protein:25, carbs:58, fat:18, benefit:"ไส้กรอกและกุ้งให้โปรตีนและธาตุเหล็กสูง", img:"https://kitchenfunwithmy3sons.com/wp-content/uploads/2022/01/Jambalaya-feature.jpg"},
    {name:"Onigiri (โอนิกิริ)", kcal:180, protein:4, carbs:38, fat:1, benefit:"แคลอรีต่ำ พกพาง่าย เหมาะเป็นของว่างให้พลังงานเร็ว", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRk9VxAjvXalmLtmDwcZkzwn1Nk4-XxTGYck6AO60b64HUT3mrZ07CAfskA&s=10"},
    {name:"Arroz con Pollo", kcal:520, protein:28, carbs:58, fat:18, benefit:"ไก่และข้าวให้พลังงานและโปรตีนสมดุลในจานเดียว", img:"https://www.allrecipes.com/thmb/lb_7c2jBCJYNpcIVfFhJAQlPo9s=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/8541-carols-arroz-con-pollo-VAT-Beauty-4x3-1dab48aa662d497eba82dae91999e4dd.jpg"},
    {name:"Pulao", kcal:430, protein:11, carbs:62, fat:14, benefit:"เครื่องเทศหอมช่วยกระตุ้นระบบย่อยอาหาร", img:"https://sinfullyspicy.com/wp-content/uploads/2024/06/2-1.jpg"},
    {name:"Pilaf", kcal:410, protein:10, carbs:64, fat:12, benefit:"ถั่วและลูกเกดเสริมใยอาหารและธาตุเหล็ก", img:"https://www.allrecipes.com/thmb/ohqQTWBnC0VwlTxxb_E4-H5pCWk=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/203951-Sarahs-rice-pilaf-Beauty-3x4_38497-f2f18ff1bcc04abcac58ccbd8c6a17c9.jpg"},
    {name:"Donburi (ดงบุริ)", kcal:550, protein:26, carbs:64, fat:18, benefit:"ซอสถั่วเหลืองหมักให้โปรไบโอติกที่ดีต่อลำไส้", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTo4SOOJspdzBfLt9iaJkGs01L_wsW--BLFYngp6qoc6I1h6an1ttG6YfYF&s=10"},
    {name:"Khao Kha Moo (ข้าวขาหมู)", kcal:640, protein:28, carbs:55, fat:30, benefit:"คอลลาเจนจากขาหมูช่วยบำรุงผิวและข้อต่อ", img:"https://hungryinthailand.com/wp-content/uploads/2024/02/khao-kha-moo.webp"},
    {name:"Gimbap (กิมบับ)", kcal:380, protein:14, carbs:55, fat:10, benefit:"สาหร่ายอุดมไอโอดีนช่วยการทำงานของไทรอยด์", img:"https://stellanspice.com/wp-content/uploads/2022/01/gimbap-4.jpeg"},
    {name:"Kimchi Fried Rice", kcal:490, protein:14, carbs:62, fat:16, benefit:"กิมจิหมักให้โปรไบโอติกดีต่อระบบย่อยอาหาร", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS-jlK0i9449IL9lSdmIhd1CtTuJZfxLi1qDILMdpPk5DqmehPpUnZWfftq&s=10"},
    {name:"Tahdig (ทาห์ดิก)", kcal:460, protein:9, carbs:70, fat:14, benefit:"ข้าวกรอบทอดให้พลังงานสูง เหมาะเป็นมื้อพิเศษ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQEQ78LKQYU2zp4o9mJAhUfUFp8ag6G-N2nM-gIHeDKU1-L4SlRFqZC0s5d&s=10"}
  ],

  sweets: [
    {name:"Tiramisu", kcal:420, protein:6, carbs:38, fat:26, benefit:"คาเฟอีนจากกาแฟช่วยกระตุ้นความตื่นตัวและสมาธิ", img:"https://www.bunsenburnerbakery.com/wp-content/uploads/2016/06/easy-tiramisu-square-29-720x540.jpg"},
    {name:"Mango Sticky Rice (ข้าวเหนียวมะม่วง)", kcal:380, protein:5, carbs:68, fat:10, benefit:"มะม่วงอุดมวิตามินเอและซีช่วยบำรุงผิวและภูมิคุ้มกัน", img:"https://assets.tmecosys.com/image/upload/t_web_rdp_recipe_584x480_1_5x/img/recipe/ras/Assets/db5ef13f0825b81a5445ae9d30b97ed6/Derivates/dc31adf30cce05a9f858beccb77038d992175aa6.jpg"},
    {name:"Macarons", kcal:90, protein:2, carbs:12, fat:4, benefit:"อัลมอนด์ในตัวขนมให้ไขมันดีและวิตามินอี", img:"https://www.midwestliving.com/thmb/vRf9ewBdA6xvB7AFy_POTgZqn9M=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/CD_1140_macarons-2000-4425cb0d8eaf4dcfbdb20225b0ed1e2a.jpg"},
    {name:"Churros", kcal:300, protein:4, carbs:38, fat:15, benefit:"ให้พลังงานเร็วจากคาร์โบไฮเดรต เหมาะเป็นของว่างมื้อบ่าย", img:"https://www.tasteofhome.com/wp-content/uploads/2026/01/Homemade-Churros_EXPS_FT25_29403_AC_1010_1.jpg"},
    {name:"Baklava", kcal:330, protein:5, carbs:40, fat:18, benefit:"ถั่วพิสตาชิโอ/วอลนัทให้กรดไขมันโอเมก้า-3", img:"https://assets.tmecosys.com/image/upload/t_web_rdp_recipe_584x480/img/recipe/ras/Assets/5b3a4f1ef35536dd44ed1a64ed55f2f2/Derivates/78efec556a9f9d444cae9fac03247ba34195c621.jpg"},
    {name:"Brownie", kcal:340, protein:4, carbs:45, fat:17, benefit:"โกโก้มีฟลาโวนอยด์ช่วยต้านอนุมูลอิสระ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSh-wgkXjr7bCVowjSQbuKmCK85iOryBHRJMb1W5iL9HvYqSaYcNG_odt0e&s=10"},
    {name:"Mochi (โมจิ)", kcal:180, protein:2, carbs:40, fat:1, benefit:"ไขมันต่ำ ย่อยง่าย เหมาะเป็นของหวานเบาๆ", img:"https://www.allrecipes.com/thmb/000r0A_ZMGgxTNScWQKJK1AJx8M=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/102109045-Mochi-Photo-by-Meredith-650x465-daf1a49a814b4648875d99897a181d9f.jpg"},
    {name:"Cheesecake", kcal:400, protein:7, carbs:32, fat:27, benefit:"ครีมชีสให้แคลเซียมช่วยเสริมสร้างกระดูก", img:"https://assets.tmecosys.com/image/upload/t_web_rdp_recipe_584x480_1_5x/img/recipe/ras/Assets/63437ceaaca08392d64a4f54abcbe225/Derivates/d34ad6dd998b08781eb1b5cebdb014f3673fcf81.jpg"},
    {name:"Crème Brûlée", kcal:350, protein:5, carbs:28, fat:24, benefit:"ไข่แดงอุดมวิตามินดีและโคลีนดีต่อสมอง", img:"https://confessionsofabakingqueen.com/wp-content/uploads/2019/10/vanilla-bean-creme-brulee-recipe-1-of-1-2.jpg"},
    {name:"Gulab Jamun", kcal:300, protein:4, carbs:50, fat:10, benefit:"นมผงให้แคลเซียม เหมาะของหวานหลังมื้ออาหาร", img:"https://pipingpotcurry.com/wp-content/uploads/2023/12/Gulab-Jamun-Recipe-Piping-Pot-Curry-500x500.jpg"},
    {name:"Pavlova", kcal:280, protein:3, carbs:48, fat:8, benefit:"ผลไม้สดด้านบนให้วิตามินซีและใยอาหาร", img:"https://www.tamingtwins.com/wp-content/uploads/2025/08/Pavlova_-7.jpg"},
    {name:"Apple Pie", kcal:320, protein:3, carbs:50, fat:13, benefit:"แอปเปิลมีเพคตินช่วยควบคุมระดับน้ำตาลในเลือด", img:"https://www.occasionallyeggs.com/wp-content/uploads/2023/07/Honey-apple-pie.jpg"},
    {name:"Tarte Tatin", kcal:310, protein:3, carbs:46, fat:13, benefit:"แอปเปิลคาราเมลให้ใยอาหารและความหวานธรรมชาติ", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7UKm3VsiBe4CmiVWxv2kYnPlKRXjxBQY8gWspQera8tuY2gIZ7c-Hwjh0&s=10"},
    {name:"Banoffee Pie", kcal:430, protein:5, carbs:55, fat:21, benefit:"กล้วยอุดมโพแทสเซียมช่วยควบคุมความดันโลหิต", img:"https://www.simplyrecipes.com/thmb/hIjJ4mAb-pRcixCaACjz791LAxE=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/Simply-Recipes-Banoffee-Pie-LEAD-03-f508bdde2cb34aca9fdb7a392328dfb2.jpg"},
    {name:"Tres Leches Cake", kcal:380, protein:6, carbs:48, fat:17, benefit:"นมสามชนิดให้แคลเซียมและโปรตีนสูง", img:"https://www.lemonblossoms.com/wp-content/uploads/2023/03/Tres-Leches-Cake-S2.jpg"},
    {name:"Doughnut", kcal:300, protein:4, carbs:35, fat:16, benefit:"ให้พลังงานเร็ว เหมาะเป็นของว่างยามเช้า", img:"https://images.food52.com/DvibKSMrlrXXM4eGpBbh41LugBo=/c200ef52-883c-4a1a-8ce7-6130ad90aea3--2015_0305_donut_beauty_smoot_209.jpg"},
    {name:"Panna Cotta", kcal:280, protein:4, carbs:24, fat:18, benefit:"เจลาตินช่วยบำรุงข้อต่อและผิวพรรณ", img:"https://www.allrecipes.com/thmb/NlP50cO2BjJdN4uGvl5JhW0Rx2A=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/AR-72567-Panna-cotta-ddmfs-4x3-14ae724a2a8e4ca3a79c5e27b2b61994.jpg"},
    {name:"Éclair", kcal:290, protein:5, carbs:30, fat:17, benefit:"ครีมคัสตาร์ดให้พลังงานและโปรตีนเล็กน้อย", img:"https://www.recipetineats.com/tachyon/2022/11/Eclairs_0a.jpg"},
    {name:"Red Velvet Cake", kcal:410, protein:5, carbs:52, fat:20, benefit:"โกโก้และครีมชีสให้สารต้านอนุมูลอิสระและแคลเซียม", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTtMv2COkuYRmlp_GCcwHMlEoTfBglSlaA98_FAUdCf_ucDwnamGAtycqc&s=10"},
    {name:"Egg Tart (ทาร์ตไข่)", kcal:260, protein:5, carbs:26, fat:15, benefit:"ไข่ให้โปรตีนคุณภาพดีและวิตามินบี12", img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTwbPPp85YLmttWrFK4aYHl5uROhJfBdlGPYHnvPC8EslhLPk_HcVgGcZtf&s=10"}
  ]
};

const CATEGORY_LABELS = { noodles:"Noodles 🍜", rice:"Rice 🍚", sweets:"Sweets 🍰" };
const colors = ["#3ddbb8","#4f8eea","#ffb648","#f5618a"]; // repeating teal/blue/yellow/pink pattern

let activeCategory = null;
let currentList = []; // working copy of selected category's items (editable)
let editIndex = null;

const canvas = document.getElementById('wheelCanvas');
const ctx = canvas.getContext('2d');
let currentRotation = 0;

/* ========================================================
   IMAGE SYSTEM — editable by you.
   Every item in FOOD_DB has an `img:""` field. Paste your own
   image URL between the quotes for each dish (and for the 3
   category tiles in CATEGORY_IMG below) and it will show up
   automatically. Leave it blank ("") to show the placeholder icon.
   ======================================================== */
const CATEGORY_IMG = {  noodles:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQRqrtEUqD2TRbUUdYc55GKaZRYQx4QcwmLYtBnSUNBjztDJtVPIeSmNL4&s=10",
rice:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThjpaixFguvR29T9CmpHzJf0_IZpqyTITf5XTYe2Bnntlk2DGOqWFRZ-w&s=10",
sweets:"https://thebaklavabox.com/cdn/shop/products/sugar-free-assorted-indian-fusion-sweets-400g-416448.jpg?v=1745425387"
};

const FALLBACK_IMAGE = "data:image/svg+xml;utf8," + encodeURIComponent(
  '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 300"><rect width="400" height="300" fill="#fef0d6"/><text x="50%" y="52%" font-size="70" text-anchor="middle" dominant-baseline="middle">🍽️</text></svg>'
);

// Returns the item's own image if one has been pasted in, otherwise the placeholder icon
function pickImg(url){
  return (url && url.trim() !== "") ? url : FALLBACK_IMAGE;
}

/* ---------- CATEGORY SELECTION ---------- */
function selectCategory(cat){
  activeCategory = cat;
  currentList = FOOD_DB[cat].map(item => ({...item})); // copy so edits don't mutate master DB

  document.querySelectorAll('.cat-btn').forEach(btn => btn.classList.remove('active'));
  document.getElementById('cat' + cat.charAt(0).toUpperCase() + cat.slice(1)).classList.add('active');

  document.getElementById('spinBtn').disabled = false;
  document.getElementById('wheelWrap').classList.remove('disabled');
  document.getElementById('foodListTitle').textContent = "รายการอาหาร — " + CATEGORY_LABELS[cat];
  document.getElementById('resultBanner').textContent = "";
  currentRotation = 0;
  canvas.style.transition = "none";
  canvas.style.transform = "rotate(0deg)";
  requestAnimationFrame(()=>{ canvas.style.transition = "transform 4s cubic-bezier(0.17, 0.67, 0.12, 0.99)"; });

  renderFoodList();
}

/* ---------- DRAW WHEEL ---------- */
function drawWheel(){
  const radius = canvas.width/2;
  ctx.clearRect(0,0,canvas.width,canvas.height);

  if(currentList.length === 0){
    ctx.beginPath();
    ctx.arc(radius,radius,radius-10,0,2*Math.PI);
    ctx.fillStyle = "#e8e0d0";
    ctx.fill();
    ctx.fillStyle = "#999";
    ctx.font = "bold 22px sans-serif";
    ctx.textAlign = "center";
    ctx.fillText("เลือกหมวดหมู่ก่อน", radius, radius);
    return;
  }

  const n = currentList.length;
  const sliceAngle = (2*Math.PI)/n;
  const fontSize = n > 14 ? 13 : (n > 9 ? 16 : 22);

  for(let i=0;i<n;i++){
    const startAngle = i*sliceAngle;
    const endAngle = startAngle+sliceAngle;
    ctx.beginPath();
    ctx.moveTo(radius,radius);
    ctx.arc(radius,radius,radius-10,startAngle,endAngle);
    ctx.closePath();
    ctx.fillStyle = colors[i % colors.length];
    ctx.fill();

    ctx.save();
    ctx.translate(radius,radius);
    ctx.rotate(startAngle+sliceAngle/2);
    ctx.textAlign = "right";
    ctx.fillStyle = "#1a1a1a";
    ctx.font = `bold ${fontSize}px 'Segoe UI', Tahoma, sans-serif`;
    let label = currentList[i].name.split('(')[0].trim();
    if(label.length > 16) label = label.slice(0,15) + "…";
    ctx.fillText(label, radius-38, fontSize/3);
    ctx.restore();
  }

  ctx.beginPath();
  ctx.arc(radius,radius,28,0,2*Math.PI);
  ctx.fillStyle = "#fff";
  ctx.fill();
}

/* ---------- EDITABLE FOOD LIST ---------- */
function renderFoodList(){
  const list = document.getElementById('foodList');
  list.innerHTML = "";
  if(!activeCategory){
    list.innerHTML = '<li style="cursor:default;">โปรดเลือกหมวดหมู่ด้านบนก่อน</li>';
    drawWheel();
    return;
  }
  currentList.forEach((item, idx)=>{
    const li = document.createElement('li');
    const span = document.createElement('span');
    span.textContent = item.name;
    span.style.flex = "1";
    span.onclick = ()=> openEditModal(idx);

    const delBtn = document.createElement('button');
    delBtn.className = "del-btn";
    delBtn.textContent = "✕";
    delBtn.onclick = (e)=>{ e.stopPropagation(); removeFood(idx); };

    li.appendChild(span);
    li.appendChild(delBtn);
    list.appendChild(li);
  });
  drawWheel();
}

function addFood(){
  if(!activeCategory){ alert("กรุณาเลือกหมวดหมู่ก่อน"); return; }
  const input = document.getElementById('newFoodInput');
  const val = input.value.trim();
  if(val === ""){ return; }
  currentList.push({name:val, kcal:300, protein:8, carbs:40, fat:10, benefit:"เมนูที่เพิ่มเองโดยผู้ใช้ — ข้อมูลโภชนาการเป็นค่าประมาณ"});
  input.value = "";
  renderFoodList();
}

function removeFood(idx){
  if(currentList.length <= 2){
    alert("ต้องมีรายการอาหารอย่างน้อย 2 รายการ");
    return;
  }
  currentList.splice(idx,1);
  renderFoodList();
}

function openEditModal(idx){
  editIndex = idx;
  document.getElementById('editInput').value = currentList[idx].name;
  document.getElementById('editModal').classList.add('active');
}
function closeModal(){
  document.getElementById('editModal').classList.remove('active');
  editIndex = null;
}
function saveEdit(){
  const val = document.getElementById('editInput').value.trim();
  if(val !== "" && editIndex !== null){
    currentList[editIndex].name = val;
    renderFoodList();
  }
  closeModal();
}

/* ---------- SPIN LOGIC ---------- */
let spinning = false;
function spinWheel(){
  if(spinning) return;
  if(!activeCategory || currentList.length === 0){
    alert("กรุณาเลือกหมวดหมู่ก่อนหมุนวงล้อ");
    return;
  }
  spinning = true;
  document.getElementById('spinBtn').disabled = true;
  document.getElementById('resultBanner').textContent = "";

  const n = currentList.length;
  const sliceAngle = 360/n;
  const winnerIndex = Math.floor(Math.random()*n);

  const extraSpins = 5 + Math.floor(Math.random()*3);
  const winnerCenterAngle = winnerIndex*sliceAngle + sliceAngle/2;
  let targetMod = (270 - winnerCenterAngle + 360) % 360;
  const totalRotation = currentRotation + extraSpins*360 + targetMod - (currentRotation % 360);

  canvas.style.transform = `rotate(${totalRotation}deg)`;
  currentRotation = totalRotation;

  setTimeout(()=>{
    spinning = false;
    document.getElementById('spinBtn').disabled = false;
    const winner = currentList[winnerIndex];
    document.getElementById('resultBanner').textContent = "🎉 ได้เมนู: " + winner.name + " 🎉";
    showResultModal(winner);
  }, 4100);
}

/* ---------- RESULT / NUTRITION MODAL ---------- */
function showResultModal(item){
  const box = document.getElementById('resultModalBox');
  box.innerHTML = `
    <img src="${pickImg(item.img)}" alt="${item.name}">
    <span class="result-cat-tag">${CATEGORY_LABELS[activeCategory]}</span>
    <h2>🎉 ${item.name}</h2>
    <p style="color:#777;margin-top:0;">นี่คือเมนูที่วงล้อสุ่มให้คุณ!</p>
    <div class="nutrition-grid">
      <div class="nutrition-item"><div class="label">พลังงาน</div><div class="value">${item.kcal} kcal</div></div>
      <div class="nutrition-item"><div class="label">โปรตีน</div><div class="value">${item.protein} g</div></div>
      <div class="nutrition-item"><div class="label">คาร์โบไฮเดรต</div><div class="value">${item.carbs} g</div></div>
      <div class="nutrition-item"><div class="label">ไขมัน</div><div class="value">${item.fat} g</div></div>
    </div>
    <div class="benefit-box"><b>ประโยชน์:</b> ${item.benefit}</div>
    <button class="close-modal-btn" onclick="closeResultModal()">ปิด</button>
  `;
  document.getElementById('resultModal').classList.add('active');
}
function closeResultModal(){
  document.getElementById('resultModal').classList.remove('active');
}

/* ---------- OUR MENU SECTION (category boxes -> full menu modal) ---------- */
function renderMenuSection(){
  const grid = document.getElementById('categoryBoxGrid');
  grid.innerHTML = "";
  Object.keys(FOOD_DB).forEach(cat=>{
    const box = document.createElement('div');
    box.className = "category-box";
    box.onclick = ()=> openFullMenuModal(cat);
    box.innerHTML = `
      <img src="${pickImg(CATEGORY_IMG[cat])}" alt="${cat}" loading="lazy">
      <div class="cat-box-overlay">
        <h3>${CATEGORY_LABELS[cat]}</h3>
        <span>ดูเมนูทั้งหมด 20 รายการ →</span>
      </div>
    `;
    grid.appendChild(box);
  });
}

function openFullMenuModal(cat){
  const box = document.getElementById('fullMenuModalBox');
  let cardsHtml = "";
  FOOD_DB[cat].forEach((item, idx)=>{
    cardsHtml += `
      <div class="menu-card" onclick="showResultModalFromCatalog('${cat}', ${idx})">
        <div class="num">[${idx+1}]</div>
        <h4>${item.name}</h4>
        <img src="${pickImg(item.img)}" alt="${item.name}" loading="lazy">
        <div class="kcal-badge">${item.kcal} kcal</div>
      </div>
    `;
  });
  box.innerHTML = `
    <div class="modal-top-bar">
      <h2>${CATEGORY_LABELS[cat]} — เมนูทั้งหมด</h2>
      <button class="modal-close-x" onclick="closeFullMenuModal()">&times;</button>
    </div>
    <div class="menu-grid">${cardsHtml}</div>
  `;
  document.getElementById('fullMenuModal').classList.add('active');
}
function closeFullMenuModal(){
  document.getElementById('fullMenuModal').classList.remove('active');
}

function showResultModalFromCatalog(cat, idx){
  const item = FOOD_DB[cat][idx];
  const prevActive = activeCategory;
  activeCategory = cat; // temporarily so the category tag shows correctly
  showResultModal(item);
  activeCategory = prevActive;
}

document.getElementById('spinBtn').addEventListener('click', spinWheel);

/* ---------- NAVIGATION (Home / About / Contact / FAQs — from code #2) ---------- */
function goHome(e){
  e.preventDefault();
  window.scrollTo({top:0, behavior:'smooth'});
}
function goAbout(e){
  e.preventDefault();
  document.getElementById('about').scrollIntoView({behavior:'smooth'});
}
function openContact(e){
  if(e) e.preventDefault();
  document.getElementById('contactModal').classList.add('active');
}
function closeContact(){
  document.getElementById('contactModal').classList.remove('active');
}
function openFaq(e){
  if(e) e.preventDefault();
  document.getElementById('faqModal').classList.add('active');
}
function closeFaq(){
  document.getElementById('faqModal').classList.remove('active');
}

/* ---------- TOAST (from code #2) ---------- */
let toastTimer;
function showToast(msg){
  let el = document.getElementById('toastEl');
  if(!el){
    el = document.createElement('div');
    el.id = 'toastEl';
    el.className = 'toast';
    document.body.appendChild(el);
  }
  el.textContent = msg;
  el.classList.add('on');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=> el.classList.remove('on'), 2600);
}

/* close modals on outside click */
document.getElementById('editModal').addEventListener('click', function(e){
  if(e.target === this) closeModal();
});
document.getElementById('resultModal').addEventListener('click', function(e){
  if(e.target === this) closeResultModal();
});
document.getElementById('fullMenuModal').addEventListener('click', function(e){
  if(e.target === this) closeFullMenuModal();
});
document.getElementById('contactModal').addEventListener('click', function(e){
  if(e.target === this) closeContact();
});
document.getElementById('faqModal').addEventListener('click', function(e){
  if(e.target === this) closeFaq();
});

/* allow Enter key to add/edit food */
document.getElementById('newFoodInput').addEventListener('keypress', function(e){
  if(e.key === 'Enter') addFood();
});
document.getElementById('editInput').addEventListener('keypress', function(e){
  if(e.key === 'Enter') saveEdit();
});

/* init */
renderFoodList();
renderMenuSection();
</script>

<footer id="contact">
  <div class="footer-title">👩‍💻 ผู้จัดทำ</div>
  <div class="creators-grid">
    <div class="creator-card">
      <div class="cr-num">เลขที่ 25</div>
      <div class="cr-name">นางสาวญาตานุช เพชรพราว</div>
      <div class="cr-class">ม.5/2</div>
    </div>
    <div class="creator-card">
      <div class="cr-num">เลขที่ 26</div>
      <div class="cr-name">นางสาวณัฐนันท์ ไพรวรรณ์</div>
      <div class="cr-class">ม.5/2</div>
    </div>
    <div class="creator-card">
      <div class="cr-num">เลขที่ 27</div>
      <div class="cr-name">นางสาวลลิภัทร สัตย์ศรี</div>
      <div class="cr-class">ม.5/2</div>
    </div>
  </div>
  <div class="footer-copy">© 2568 วันนี้กินอะไรดีนะ?</div>
</footer>

<div class="toast" id="toastEl"></div>

</body>
</html>





