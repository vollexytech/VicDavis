# Institutional Steel Overhaul — Implementation Blocks

This file contains the exact CSS, HTML replacement blocks, and Vanilla JS to apply the Institutional Steel overhaul. It's committed to the branch `institutional-steel-overhaul` so you can review or apply the changes easily.

---

1) Optimized CSS block (paste into <head> inside a <style> or into your CSS file)

```html
<style>
/* Institutional Steel design tokens */
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@400;600;700;800&family=Inter:wght@300;400;600;700&display=swap');

:root{
  --navy:#0A192F;            /* Primary */
  --red:#D90429;             /* Accent */
  --steel:#E9ECEF;           /* Background clinical steel / light grey */
  --muted:#98A0A8;
  --glass: rgba(255,255,255,0.06);
  --glass-2: rgba(10,25,47,0.26);
  --glass-3: rgba(255,255,255,0.035);
  --txt:#0F1724;
  --white:#ffffff;
  --radius:14px;
  --shadow-1: 0 6px 24px rgba(10,25,47,0.18);
  --shadow-2: 0 10px 40px rgba(10,25,47,0.22);
  --ex-rate: 14.5; /* USD -> GHS default (edit value in JS too if needed) */
  --max-width:1200px;
  --transition:0.25s cubic-bezier(.2,.9,.25,1);
  font-synthesis: none;
}

/* Global */
html,body{height:100%}
body{
  font-family: 'Inter', system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  color:var(--txt);
  background:linear-gradient(180deg,var(--steel) 0%, #F4F6F8 100%);
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
}

/* Header - frosted glass */
#nb{
  position:fixed;top:16px;left:50%;transform:translateX(-50%);
  width:calc(100% - 40px);max-width:calc(var(--max-width) + 40px);
  z-index:1200;border-radius:12px;padding:10px 18px;
  display:flex;align-items:center;justify-content:space-between;
  backdrop-filter: blur(10px) saturate(120%);
  background: linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0.02));
  box-shadow:var(--shadow-1);
  transition:transform var(--transition), box-shadow var(--transition);
}
#nb .brand{display:flex;align-items:center;gap:12px}
.brand .logo-mark{
  width:46px;height:46px;border-radius:8px;
  display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,var(--navy),#0B2440);
}
.brand .title{font-family: 'Oswald', sans-serif;font-weight:700;color:var(--navy);letter-spacing:0.6px}
.brand .meta{font-size:11px;color:var(--muted);line-height:1}

/* Nav links */
#nb .nav-links{display:flex;gap:18px;align-items:center;margin-left:18px}
#nb .nav-links a{
  font-weight:600;color:var(--navy);padding:8px 10px;border-radius:8px;transition:all .18s;
  text-decoration:none;font-size:14px;background:transparent;
}
#nb .nav-links a:hover{color:var(--red);transform:translateY(-2px)}

/* Sell CTA */
#nb .cta-sell{
  background:var(--red);color:var(--white);padding:10px 16px;border-radius:10px;font-weight:700;
  box-shadow:0 8px 30px rgba(217,4,41,0.18);border:1px solid rgba(255,255,255,0.06);
}

/* Hero - Billion-Dollar (video background + right social bar) */
#hero{position:relative;min-height:86vh;display:flex;align-items:center;overflow:hidden;border-radius:18px;margin:28px auto;max-width:var(--max-width);background:linear-gradient(180deg,rgba(10,25,47,0.86),rgba(10,25,47,0.66));box-shadow:var(--shadow-2)}
#hero video#hero-vid{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:0.28;filter:contrast(1.05) saturate(0.9)}
#hero .hc{position:relative;z-index:3;display:flex;gap:48px;padding:80px 56px;align-items:center;width:100%}
#hero .hero-left{flex:1;color:var(--white);max-width:60%}
#hero h1{font-family:'Oswald',sans-serif;font-size:clamp(34px,5.6vw,64px);line-height:1;color:var(--white);letter-spacing:-1px;margin-bottom:12px;font-weight:700}
#hero p.lead{color:rgba(255,255,255,0.85);max-width:640px;margin-bottom:22px}

/* Search bar — 60% opacity with white text */
.hero-search{
  display:flex;gap:10px;align-items:center;background:rgba(255,255,255,0.10);padding:12px;border-radius:12px;
  color:var(--white);backdrop-filter:blur(6px);width:75%;
}
.hero-search select,input{background:transparent;border:none;outline:none;color:var(--white);font-weight:600}
.hero-search .search-btn{background:var(--white);color:var(--navy);padding:10px 14px;border-radius:10px;font-weight:700}

/* Right-hand social / quick actions (vertical) */
.social-fixed{position:absolute;right:12px;top:50%;transform:translateY(-50%);z-index:4;display:flex;flex-direction:column;gap:12px}
.social-fixed a{display:flex;width:56px;height:56px;border-radius:12px;background:rgba(255,255,255,0.04);align-items:center;justify-content:center;border:1px solid rgba(255,255,255,0.03);transition:transform .18s}
.social-fixed a:hover{transform:translateX(-6px);box-shadow:var(--shadow-1)}

/* Apex Gallery (Inventory) */
#inv{padding:56px 20px;background:transparent}
.apex-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:22px;max-width:var(--max-width);margin:0 auto}
@media(max-width:1100px){.apex-grid{grid-template-columns:repeat(2,1fr)}}
@media(max-width:700px){.apex-grid{grid-template-columns:1fr}}

/* Glassmorphism card */
.apex-card{
  position:relative;border-radius:16px;padding:14px;background:linear-gradient(180deg,var(--glass), rgba(255,255,255,0.02));
  backdrop-filter: blur(8px) saturate(120%);box-shadow:var(--shadow-1);overflow:hidden;border:1px solid rgba(255,255,255,0.04);
  display:flex;flex-direction:column;gap:12px;min-height:320px;transition:transform var(--transition);
}
.apex-card:hover{transform:translateY(-10px)}
.apex-card .img-wrap{border-radius:12px;overflow:hidden;flex:1;display:block;background:#0b1a2b}
.apex-card img{width:100%;height:220px;object-fit:cover;display:block}

/* meta row */
.apex-meta{display:flex;align-items:center;justify-content:space-between;gap:10px}
.apex-title{font-family:'Oswald',sans-serif;font-size:18px;color:var(--navy);font-weight:700}
.apex-sub{font-size:13px;color:var(--muted)}

/* price in GH₵ */
.apex-price{font-family:'Oswald',sans-serif;font-size:20px;color:var(--navy);font-weight:700}

/* utility row */
.apex-actions{display:flex;align-items:center;gap:10px;justify-content:space-between}
.icon-btn{width:44px;height:44px;border-radius:10px;border:1px solid rgba(10,25,47,0.06);display:flex;align-items:center;justify-content:center;background:#fff;cursor:pointer;transition:all var(--transition)}
.icon-btn svg{width:18px;height:18px;fill:var(--navy)}
.icon-btn.saved{background:linear-gradient(180deg, var(--red), #b30a18);color:#fff}
.icon-btn.saved svg{fill:#fff}

/* scarcity badge */
.scarcity{
  display:inline-flex;gap:8px;align-items:center;padding:8px 10px;border-radius:10px;background:linear-gradient(90deg,var(--red),#b30a18);color:#fff;font-weight:700;font-size:13px;
}

/* small countdown */
.countdown{font-family:'Oswald',sans-serif;font-size:14px;letter-spacing:0.5px}

/* Selling (multi-step) */
#sell .sell-panel{max-width:980px;margin:0 auto;background:var(--white);padding:22px;border-radius:14px;box-shadow:var(--shadow-1);border:1px solid rgba(10,25,47,0.04)}
.stepper{display:flex;gap:10px;align-items:center;margin-bottom:16px}
.step{flex:1;padding:10px;border-radius:10px;background:var(--glass-3);text-align:center;font-weight:700}
.step.active{background:linear-gradient(180deg,var(--navy),#0b2a4a);color:#fff}

/* Map area */
.map-embed{width:100%;height:260px;border-radius:12px;overflow:hidden;border:1px solid rgba(10,25,47,0.06);box-shadow:var(--shadow-1);}

/* modal (Google Review emulator) */
.vd-modal{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(4,8,12,0.45);z-index:20000;opacity:0;pointer-events:none;transition:opacity .18s}
.vd-modal.op{opacity:1;pointer-events:all}
.vd-modal .card{width:420px;background:var(--white);border-radius:12px;padding:18px;box-shadow:var(--shadow-2);text-align:center}
.vd-modal .stars{display:flex;gap:6px;justify-content:center;margin:10px 0}
.vd-modal button{background:var(--red);color:#fff;border:none;padding:10px 14px;border-radius:10px;font-weight:700}

/* flash overlay (new tab transition) */
.flash-overlay{
  position:fixed;inset:0;background:var(--white);opacity:0;z-index:15000;pointer-events:none;transition:opacity .18s;
}
.flash-overlay.show{opacity:1;pointer-events:none}
</style>
```

---

2) HTML replacements: use the following fragments to replace the matching sections in your index.html. You can (A) replace in-place, or (B) append the JS below to perform DOM replacement automatically. I will include the JS replacement approach so you don't need to manually edit HTML.

A) NAVBAR replacement markup (for manual replacement)

```html
<nav id="nb" aria-label="Main navigation">
  <div class="brand" style="align-items:center;">
    <div class="logo-mark" aria-hidden="true">
      <!-- minimalist car monogram SVG -->
      <svg width="34" height="34" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <path d="M2 13c0-1.8 2-4 6-4h8c4 0 6 2.2 6 4v3H2v-3z" fill="#FFFFFF" opacity="0.06"/>
        <path d="M3 14s1-4 6-4h6s3 0 4 2" stroke="#FFFFFF" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
    <div>
      <div class="title">VICDAVIS</div>
      <div class="meta">Founded 2009 · 500+ Cars Imported · Official Copart Partner · Dansoman, Accra</div>
    </div>
  </div>

  <div style="display:flex;align-items:center;gap:18px">
    <div class="nav-links" role="menubar">
      <a href="#inv" class="newtab-link">Inventory</a>
      <a href="#imp" class="newtab-link">Import</a>
      <a href="#svcs" class="newtab-link">Services</a>
      <a href="#about" class="newtab-link">About</a>
      <a href="#ct" class="newtab-link">Contact</a>
    </div>
    <a href="#sell" class="cta-sell newtab-link" role="button">Sell Your Car</a>
  </div>
</nav>
```

B) HERO replacement (manual)

```html
<section id="hero" aria-label="Hero">
  <video id="hero-vid" autoplay muted loop playsinline poster="hero-poster.jpg">
    <source src="vid11.mp4" type="video/mp4">
  </video>

  <div class="hc">
    <div class="hero-left">
      <h1>Premium Imports. Institutional Trust.</h1>
      <p class="lead">Direct-source vehicles from the USA. Transparent bidding, certified clearance, and white-glove delivery to Accra.</p>

      <div class="hero-search" role="search" aria-label="Inventory search">
        <select id="hs-make" aria-label="Make">
          <option value="">Any Make</option>
          <option>Toyota</option><option>Mercedes-Benz</option><option>BMW</option>
        </select>
        <select id="hs-type" aria-label="Type">
          <option value="">Any Type</option>
          <option>SUV</option><option>Sedan</option><option>Truck</option>
        </select>
        <input id="hs-budget" placeholder="Max Budget (USD)" aria-label="Max Budget" />
        <button class="search-btn newtab-link" data-target="#inv">Search</button>
      </div>
    </div>

    <div style="flex:0 0 300px;position:relative">
      <!-- small info panel with brand claims -->
      <div style="background:linear-gradient(180deg,rgba(255,255,255,0.03),rgba(255,255,255,0.02));backdrop-filter:blur(6px);padding:16px;border-radius:12px;">
        <div style="font-weight:700;color:var(--white)">VICDAVIS AUTO LINK</div>
        <div style="color:rgba(255,255,255,0.78);font-size:13px;margin-top:8px">Official Copart Partner — Serving Ghana since 2009</div>
      </div>
    </div>
  </div>

  <!-- right-hand social / quick actions -->
  <div class="social-fixed" aria-hidden="false">
    <a href="https://wa.me/233577551078" target="_blank" title="WhatsApp">
      <!-- WhatsApp-like minimalist SVG -->
      <svg viewBox="0 0 24 24"><path d="M2 12a10 10 0 1 1 18 6l2 2-2 0A10 10 0 0 1 2 12z" fill="#fff" opacity="0.06"/><path d="M17.4 14.6c-.3-.1-1.7-.8-1.9-.9-.2-.1-.4-.1-.6.1-.2.2-.9.9-1.1 1.2-.2.3-.4.3-.7.1-1.5-.9-2.5-2.7-2.8-4.4-.1-.5.4-1 .7-1.3.3-.3.4-.3.6-.3.2 0 .4 0 .6.0.2 0 .5-.1.8-.1.3 0 .6 0 .9.1.3.1 1 .1 1.5.1.5 0 .9.0 1.2.7s.4 1.5.4 1.9-.2 1.1-.4 1.3c-.2.2-.5.4-.8.3z" fill="#fff"/></svg>
    </a>
    <a href="tel:+233545272848" title="Call">
      <svg viewBox="0 0 24 24"><path d="M2 3l6 1 2 4-3 3a12 12 0 0 0 6 6l3-3 4 2 1 6" stroke="#fff" stroke-width="1.2" fill="none"/></svg>
    </a>
    <a href="#sell" class="newtab-link" title="Sell">
      <svg viewBox="0 0 24 24"><rect x="4" y="3" width="16" height="18" rx="2" stroke="#fff" stroke-width="1.2" fill="none"/></svg>
    </a>
  </div>
</section>
```

C) INVENTORY replacement (manual)

```html
<section id="inv" class="sec" aria-label="Inventory">
  <div style="max-width:var(--max-width);margin:0 auto;padding:28px;">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:18px">
      <div>
        <div style="font-size:12px;font-weight:800;color:var(--muted);letter-spacing:1px">OUR INVENTORY</div>
        <h2 style="font-family:'Oswald',sans-serif;margin-top:6px">Apex Collection</h2>
      </div>
      <div>
        <button id="load-more" class="search-btn">Load 15</button>
      </div>
    </div>

    <div class="apex-grid" id="apex-grid" aria-live="polite" role="list"></div>

    <div style="text-align:center;margin-top:20px;">
      <button id="show-more-btn" class="search-btn" aria-label="Show more inventory">Show More</button>
    </div>
  </div>
</section>
```

D) SELL replacement (manual)

```html
<section id="sell" aria-label="Sell your car" style="padding:56px 20px">
  <div class="sell-panel">
    <div class="stepper" role="tablist">
      <div class="step active" data-step="1">1. Details</div>
      <div class="step" data-step="2">2. Photos</div>
      <div class="step" data-step="3">3. Confirm</div>
    </div>

    <form id="appraisal-form" novalidate>
      <div class="step-content" data-step="1">
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
          <input id="app-make" placeholder="Make" required />
          <input id="app-model" placeholder="Model" required />
          <input id="app-year" placeholder="Year" />
          <input id="app-mileage" placeholder="Mileage (km)" />
        </div>
        <div style="margin-top:12px">
          <label style="font-weight:700">Condition (select)</label>
          <select id="app-condition"><option>Excellent</option><option>Good</option><option>Fair</option></select>
        </div>
      </div>

      <div class="step-content" data-step="2" style="display:none">
        <div style="margin-bottom:12px">Add up to 6 photos (optional)</div>
        <input id="app-photos" type="file" accept="image/*" multiple />
      </div>

      <div class="step-content" data-step="3" style="display:none">
        <div style="margin-bottom:12px">Preview and submit - we'll contact you within 24 hours</div>
        <div id="app-preview" style="background:var(--glass-3);padding:12px;border-radius:10px"></div>
      </div>

      <div style="display:flex;gap:10px;margin-top:14px;justify-content:flex-end">
        <button type="button" id="app-prev" style="background:transparent;border:1px solid var(--muted);padding:10px 12px;border-radius:8px">Back</button>
        <button type="button" id="app-next" style="background:var(--navy);color:#fff;padding:10px 12px;border-radius:8px">Next</button>
      </div>
    </form>
  </div>
</section>
```

E) Footer map embed (manual)

```html
<div style="max-width:var(--max-width);margin:18px auto;padding:0 18px;">
  <h4 style="font-family:'Oswald',sans-serif;margin-bottom:8px">Find Us</h4>
  <div class="map-embed" id="map-embed">
    <!-- JS will populate iframe for Dansoman, Accra -->
  </div>
</div>
```

---

3) Vanilla JS — DOM replacement + interactions (append as a new <script> before </body>)

```html
<script>
/* Institutional Steel bootstrap — This script replaces the NAV/HERO/INV/SELL sections in-place and wires the interactions.
   Paste this as a new <script> before </body> or merge with your main JS. */
(function(){
  const EX_RATE = 14.5; // update if needed
  const APEX_COUNT = 15;
  const REVIEW_PROMPT_KEY = 'vd_google_review_prompt';
  const REVIEW_PROMPT_INTERVAL_HOURS = 24;
  const LIKES_KEY = 'vd_likes';

  function ghc(n){ if(isNaN(n)) return 'GH₵0'; return 'GH₵' + Number(n).toLocaleString('en-GH', {maximumFractionDigits:0}); }

  function replaceHTML(){
    try{
      // NAV
      const nav = document.getElementById('nb');
      if(nav){
        nav.replaceWith((()=>{ const el = document.createElement('div'); el.innerHTML = `
          <nav id="nb" aria-label="Main navigation">\n  <div class="brand" style="align-items:center;">\n    <div class="logo-mark" aria-hidden="true">\n      <svg width=\"34\" height=\"34\" viewBox=\"0 0 24 24\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"><path d=\"M2 13c0-1.8 2-4 6-4h8c4 0 6 2.2 6 4v3H2v-3z\" fill=\"#FFFFFF\" opacity=\"0.06\"/><path d=\"M3 14s1-4 6-4h6s3 0 4 2\" stroke=\"#FFFFFF\" stroke-width=\"1.2\" stroke-linecap=\"round\" stroke-linejoin=\"round\"/></svg>\n    </div>\n    <div>\n      <div class=\"title\">VICDAVIS</div>\n      <div class=\"meta\">Founded 2009 · 500+ Cars Imported · Official Copart Partner · Dansoman, Accra</div>\n    </div>\n  </div>\n  <div style=\"display:flex;align-items:center;gap:18px\">\n    <div class=\"nav-links\" role=\"menubar\">\n      <a href=\"#inv\" class=\"newtab-link\">Inventory</a>\n      <a href=\"#imp\" class=\"newtab-link\">Import</a>\n      <a href=\"#svcs\" class=\"newtab-link\">Services</a>\n      <a href=\"#about\" class=\"newtab-link\">About</a>\n      <a href=\"#ct\" class=\"newtab-link\">Contact</a>\n    </div>\n    <a href=\"#sell\" class=\"cta-sell newtab-link\" role=\"button\">Sell Your Car</a>\n  </div>\n</nav>`; return el.firstElementChild; })());
      }

      // HERO
      const hero = document.getElementById('hero');
      if(hero){
        hero.replaceWith((()=>{ const s = document.createElement('div'); s.innerHTML = `
<section id="hero" aria-label="Hero">\n  <video id="hero-vid" autoplay muted loop playsinline poster="hero-poster.jpg">\n    <source src="vid11.mp4" type="video/mp4">\n  </video>\n  <div class=\"hc\">\n    <div class=\"hero-left\">\n      <h1>Premium Imports. Institutional Trust.</h1>\n      <p class=\"lead\">Direct-source vehicles from the USA. Transparent bidding, certified clearance, and white-glove delivery to Accra.</p>\n      <div class=\"hero-search\" role=\"search\" aria-label=\"Inventory search\">\n        <select id=\"hs-make\" aria-label=\"Make\">\n          <option value=\"\">Any Make</option>\n          <option>Toyota</option><option>Mercedes-Benz</option><option>BMW</option>\n        </select>\n        <select id=\"hs-type\" aria-label=\"Type\">\n          <option value=\"\">Any Type</option>\n          <option>SUV</option><option>Sedan</option><option>Truck</option>\n        </select>\n        <input id=\"hs-budget\" placeholder=\"Max Budget (USD)\" aria-label=\"Max Budget\" />\n        <button class=\"search-btn newtab-link\" data-target=\"#inv\">Search</button>\n      </div>\n    </div>\n    <div style=\"flex:0 0 300px;position:relative\">\n      <div style=\"background:linear-gradient(180deg,rgba(255,255,255,0.03),rgba(255,255,255,0.02));backdrop-filter:blur(6px);padding:16px;border-radius:12px;\">\n        <div style=\"font-weight:700;color:var(--white)\">VICDAVIS AUTO LINK</div>\n        <div style=\"color:rgba(255,255,255,0.78);font-size:13px;margin-top:8px\">Official Copart Partner — Serving Ghana since 2009</div>\n      </div>\n    </div>\n  </div>\n  <div class=\"social-fixed\" aria-hidden=\"false\">\n    <a href=\"https://wa.me/233577551078\" target=\"_blank\" title=\"WhatsApp\">\n      <svg viewBox=\"0 0 24 24\"><path d=\"M2 12a10 10 0 1 1 18 6l2 2-2 0A10 10 0 0 1 2 12z\" fill=\"#fff\" opacity=\"0.06\"/><path d=\"M17.4 14.6c-.3-.1-1.7-.8-1.9-.9-.2-.1-.4-.1-.6.1-.2.2-.9.9-1.1 1.2-.2.3-.4.3-.7.1-1.5-.9-2.5-2.7-2.8-4.4-.1-.5.4-1 .7-1.3.3-.3.4-.3.6-.3.2 0 .4 0 .6.0.2 0 .5-.1.8-.1.3 0 .6 0 .9.1.3.1 1 .1 1.5.1.5 0 .9.0 1.2.7s.4 1.5.4 1.9-.2 1.1-.4 1.3c-.2.2-.5.4-.8.3\" fill=\"#fff\"/></svg>\n    </a>\n    <a href=\"tel:+233545272848\" title=\"Call\">\n      <svg viewBox=\"0 0 24 24\"><path d=\"M2 3l6 1 2 4-3 3a12 12 0 0 0 6 6l3-3 4 2 1 6\" stroke=\"#fff\" stroke-width=\"1.2\" fill=\"none\"/></svg>\n    </a>\n    <a href=\"#sell\" class=\"newtab-link\" title=\"Sell\">\n      <svg viewBox=\"0 0 24 24\"><rect x=\"4\" y=\"3\" width=\"16\" height=\"18\" rx=\"2\" stroke=\"#fff\" stroke-width=\"1.2\" fill=\"none\"/></svg>\n    </a>\n  </div>\n</section>`; return s.firstElementChild; })());
      }

      // INVENTORY — replace the section with id 'inv' (we keep original but swap)
      const inv = document.getElementById('inv');
      if(inv){
        inv.replaceWith((()=>{ const d = document.createElement('div'); d.innerHTML = `
<section id="inv" class="sec" aria-label="Inventory">\n  <div style="max-width:var(--max-width);margin:0 auto;padding:28px;">\n    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:18px">\n      <div>\n        <div style="font-size:12px;font-weight:800;color:var(--muted);letter-spacing:1px">OUR INVENTORY</div>\n        <h2 style="font-family:'Oswald',sans-serif;margin-top:6px">Apex Collection</h2>\n      </div>\n      <div>\n        <button id="load-more" class="search-btn">Load 15</button>\n      </div>\n    </div>\n    <div class="apex-grid" id="apex-grid" aria-live="polite" role="list"></div>\n    <div style="text-align:center;margin-top:20px;">\n      <button id="show-more-btn" class="search-btn" aria-label="Show more inventory">Show More</button>\n    </div>\n  </div>\n</section>`; return d.firstElementChild; })());
      }

      // SELL section
      const sell = document.getElementById('sell');
      if(sell){
        sell.replaceWith((()=>{ const d = document.createElement('div'); d.innerHTML = `
<section id="sell" aria-label="Sell your car" style="padding:56px 20px">\n  <div class="sell-panel">\n    <div class="stepper" role="tablist">\n      <div class="step active" data-step="1">1. Details</div>\n      <div class="step" data-step="2">2. Photos</div>\n      <div class="step" data-step="3">3. Confirm</div>\n    </div>\n    <form id="appraisal-form" novalidate>\n      <div class="step-content" data-step="1">\n        <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">\n          <input id="app-make" placeholder="Make" required />\n          <input id="app-model" placeholder="Model" required />\n          <input id="app-year" placeholder="Year" />\n          <input id="app-mileage" placeholder="Mileage (km)" />\n        </div>\n        <div style="margin-top:12px">\n          <label style="font-weight:700">Condition (select)</label>\n          <select id="app-condition"><option>Excellent</option><option>Good</option><option>Fair</option></select>\n        </div>\n      </div>\n      <div class="step-content" data-step="2" style="display:none">\n        <div style="margin-bottom:12px">Add up to 6 photos (optional)</div>\n        <input id="app-photos" type="file" accept="image/*" multiple />\n      </div>\n      <div class="step-content" data-step="3" style="display:none">\n        <div style="margin-bottom:12px">Preview and submit - we'll contact you within 24 hours</div>\n        <div id="app-preview" style="background:var(--glass-3);padding:12px;border-radius:10px"></div>\n      </div>\n      <div style="display:flex;gap:10px;margin-top:14px;justify-content:flex-end">\n        <button type="button" id="app-prev" style="background:transparent;border:1px solid var(--muted);padding:10px 12px;border-radius:8px">Back</button>\n        <button type="button" id="app-next" style="background:var(--navy);color:#fff;padding:10px 12px;border-radius:8px">Next</button>\n      </div>\n    </form>\n  </div>\n</section>`; return d.firstElementChild; })());
      }

      // Footer map embed — insert map embed container after the first .fbrand if not present
      const fbrand = document.querySelector('.fbrand');
      if(fbrand && !document.getElementById('map-embed')){
        const wrapper = document.createElement('div'); wrapper.style.maxWidth = 'var(--max-width)'; wrapper.style.margin = '18px auto'; wrapper.style.padding = '0 18px';
        wrapper.innerHTML = `<h4 style="font-family:'Oswald',sans-serif;margin-bottom:8px">Find Us</h4><div class="map-embed" id="map-embed"></div>`;
        fbrand.parentNode.parentNode.insertBefore(wrapper, fbrand.parentNode.nextSibling);
      }

    } catch(err){ console.error('ReplaceHTML error',err); }
  }

  function setupNewTabFlash(){
    const flash = document.createElement('div'); flash.className = 'flash-overlay'; document.body.appendChild(flash);
    function openNewTab(url){ flash.classList.add('show'); setTimeout(()=>{ window.open(url,'_blank'); setTimeout(()=>flash.classList.remove('show'),220); }, 220); }
    document.addEventListener('click', e=>{
      const a = e.target.closest('.newtab-link'); if(!a) return; e.preventDefault(); const href = a.getAttribute('href') || a.dataset.target || '#';
      if(href.startsWith('#')){ const base = location.origin + location.pathname; openNewTab(base + href); } else { openNewTab(href); }
    }, {capture:false});
  }

  function renderApex(){
    const container = document.getElementById('apex-grid'); if(!container) return;
    const baseCars = (typeof CARS !== 'undefined' && Array.isArray(CARS) && CARS.length) ? CARS.slice() : [];
    if(baseCars.length === 0){ // create placeholders
      for(let i=0;i<APEX_COUNT;i++){ baseCars.push({ id:1000+i, make:'Premium', model:'Model '+(i+1), year:2020+i%3, type:'SUV', price:25000 + i*5000, mi:'0 km', fuel:'Petrol', img:'https://placehold.co/700x400/0A192F/FFFFFF?text=Vehicle+'+(i+1) }); }
    }
    while(baseCars.length < APEX_COUNT){ baseCars.push(Object.assign({}, baseCars[baseCars.length%baseCars.length] || baseCars[0] || { id:1, make:'Generic', model:'Model', year:2021, type:'Sedan', price:25000, mi:'0 km', fuel:'Petrol', img:'https://placehold.co/700x400/0A192F/FFFFFF?text=Vehicle'})); }

    const sorted = baseCars.slice().sort((a,b)=>(b.price||0)-(a.price||0));
    const scarcitySet = new Set(sorted.slice(0,3).map(c=>c.id));

    let likes = [];
    try{ likes = JSON.parse(localStorage.getItem(LIKES_KEY) || '[]'); }catch(e){ likes=[]; }

    function createCard(c){
      const priceGHS = (c.price || 0) * EX_RATE;
      const wrapper = document.createElement('article'); wrapper.className = 'apex-card';
      wrapper.innerHTML = `
        <div class="img-wrap"><img loading="lazy" src="${c.img}" alt="${(c.make||'') + ' ' + (c.model||'')}"></div>
        <div class="apex-meta">
          <div>
            <div class="apex-title">${c.make || ''} ${c.model || ''} · ${c.year || ''}</div>
            <div class="apex-sub">${c.type || ''} · ${c.mi || ''}</div>
          </div>
          <div style="text-align:right">
            <div class="apex-price" data-usd="${c.price || 0}">${ghc(priceGHS)}</div>
            <div style="font-size:12px;color:var(--muted)">est. monthly</div>
          </div>
        </div>
        <div class="apex-actions">
          <div style="display:flex;gap:8px;align-items:center">
            <button class="icon-btn like-btn" data-id="${c.id}" title="Like"> <svg viewBox="0 0 24 24"><path d="M12 21s-8-4.8-8-10a5 5 0 0 1 9-3 5 5 0 0 1 9 3c0 5.2-8 10-8 10z" fill="none" stroke="currentColor" stroke-width="1.2"/></svg></button>
            <button class="icon-btn save-btn" data-id="${c.id}" title="Save"> <svg viewBox="0 0 24 24"><path d="M6 2h12v20l-6-4-6 4V2z" fill="none" stroke="currentColor" stroke-width="1.1"/></svg></button>
          </div>
          <div style="display:flex;align-items:center;gap:10px">
            ${scarcitySet.has(c.id) ? `<div class="scarcity"><span style="font-size:12px">Deal ends in</span>&nbsp;<span class="countdown" data-id="${c.id}">--:--:--</span></div>` : ''}
            <a class="search-btn" href="https://wa.me/233577551078" target="_blank">Enquire</a>
          </div>
        </div>`;

      const likeBtn = wrapper.querySelector('.like-btn');
      const saveBtn = wrapper.querySelector('.save-btn');
      if(likes.includes(c.id)){
        likeBtn.classList.add('saved'); likeBtn.innerHTML = `<svg viewBox="0 0 24 24"><path d="M12 21s-8-4.8-8-10a5 5 0 0 1 9-3 5 5 0 0 1 9 3c0 5.2-8 10-8 10z" fill="#D90429"/></svg>`;
      }
      likeBtn.addEventListener('click', ()=>{
        const id = Number(likeBtn.dataset.id);
        if(likes.includes(id)){ likes = likes.filter(x=>x!==id); likeBtn.classList.remove('saved'); likeBtn.innerHTML = `<svg viewBox=\"0 0 24 24\"><path d=\"M12 21s-8-4.8-8-10a5 5 0 0 1 9-3 5 5 0 0 1 9 3c0 5.2-8 10-8 10z\" fill=\"none\" stroke=\"currentColor\" stroke-width=\"1.2\"/></svg>`; }
        else{ likes.push(id); likeBtn.classList.add('saved'); likeBtn.innerHTML = `<svg viewBox=\"0 0 24 24\"><path d=\"M12 21s-8-4.8-8-10a5 5 0 0 1 9-3 5 5 0 0 1 9 3c0 5.2-8 10-8 10z\" fill=\"#D90429\"/></svg>`; }
        try{ localStorage.setItem(LIKES_KEY, JSON.stringify(likes)); }catch(e){}
      });

      saveBtn.addEventListener('click', ()=>{ saveBtn.classList.toggle('saved'); if(saveBtn.classList.contains('saved')) saveBtn.innerHTML = `<svg viewBox=\"0 0 24 24\"><path d=\"M6 2h12v20l-6-4-6 4V2z\" fill=\"#0A192F\"/></svg>`; else saveBtn.innerHTML = `<svg viewBox=\"0 0 24 24\"><path d=\"M6 2h12v20l-6-4-6 4V2z\" fill=\"none\" stroke=\"currentColor\" stroke-width=\"1.1\"/></svg>`; });

      return wrapper;
    }

    container.innerHTML = '';
    for(let i=0;i<APEX_COUNT;i++){ const item = baseCars[i % baseCars.length]; const cardData = Object.assign({}, item, { id: item.id || (i+1) }); container.appendChild(createCard(cardData)); }

    const countdownEls = container.querySelectorAll('.countdown');
    countdownEls.forEach((el, idx)=>{
      const hours = 2 + (idx * 12) + 1; const end = Date.now() + hours*3600*1000 + (Math.floor(Math.random()*3600)*1000);
      el.dataset.end = end; updateCountdown(el); setInterval(()=>updateCountdown(el),1000);
    });

    function updateCountdown(el){ const end = Number(el.dataset.end); const diff = Math.max(0,end - Date.now()); if(diff<=0){ el.textContent='00:00:00'; return; } const hrs = Math.floor(diff/3600000); const mins = Math.floor((diff%3600000)/60000); const secs = Math.floor((diff%60000)/1000); el.textContent = `${String(hrs).padStart(2,'0')}:${String(mins).padStart(2,'0')}:${String(secs).padStart(2,'0')}`; }
  }

  function convertDisplayedPrices(){ document.querySelectorAll('[data-usd]').forEach(el=>{ const usd = Number(el.dataset.usd||0); el.textContent = ghc(usd*EX_RATE); }); }

  function googleReviewEmulator(){ try{ const raw = localStorage.getItem(REVIEW_PROMPT_KEY); if(raw && !isNaN(Number(raw)) && (Date.now()-Number(raw)) < REVIEW_PROMPT_INTERVAL_HOURS*3600*1000) return; }catch(e){}
    setTimeout(()=>{
      const modal = document.createElement('div'); modal.className='vd-modal op'; modal.id='vd-review-modal'; modal.innerHTML = `<div class=\"card\" role=\"dialog\" aria-modal=\"true\" aria-label=\"Customer Review\">\n        <div style=\"font-weight:800;font-family:Oswald, sans-serif;\">How would you rate your experience?</div>\n        <div class=\"stars\">${'<svg width=\"22\" height=\"22\" viewBox=\"0 0 24 24\" fill=\"#F59E0B\"><path d=\"M12 .587l3.668 7.431L23.5 9.75l-5.5 5.36L19.335 24 12 19.897 4.665 24 6 15.11 0.5 9.75l7.832-1.732L12 .587z\"/></svg>'.repeat(5)}</div>\n        <div style=\"margin:8px 0;color:var(--muted);font-size:13px\">Leave feedback and help others trust us — your voice matters.</div>\n        <div style=\"display:flex;gap:10px;justify-content:center;margin-top:10px\">\n          <button id=\"vd-review-yes\">Rate Us</button>\n          <button id=\"vd-review-no\" style=\"background:transparent;border:1px solid var(--muted);color:var(--muted)\">Not now</button>\n        </div>\n      </div>`;
      document.body.appendChild(modal);
      document.getElementById('vd-review-yes').addEventListener('click', ()=>{ window.open('https://www.google.com/search?q=VicDavis+Auto+Link+Dansoman+Accra+reviews','_blank'); localStorage.setItem(REVIEW_PROMPT_KEY,String(Date.now())); modal.classList.remove('op'); setTimeout(()=>modal.remove(),220); });
      document.getElementById('vd-review-no').addEventListener('click', ()=>{ localStorage.setItem(REVIEW_PROMPT_KEY,String(Date.now())); modal.classList.remove('op'); setTimeout(()=>modal.remove(),220); });
      modal.addEventListener('click',(evt)=>{ if(evt.target===modal){ localStorage.setItem(REVIEW_PROMPT_KEY,String(Date.now())); modal.classList.remove('op'); setTimeout(()=>modal.remove(),220); } });
    },33000);
  }

  function loadMap(){ const el = document.getElementById('map-embed'); if(!el) return; const q = encodeURIComponent('Dansoman, Accra, Ghana'); const iframe = document.createElement('iframe'); iframe.style.border='0'; iframe.style.width='100%'; iframe.style.height='100%'; iframe.loading='lazy'; iframe.referrerPolicy='no-referrer-when-downgrade'; iframe.src = `https://www.google.com/maps?q=${q}&output=embed`; el.appendChild(iframe); }

  function sellFormLogic(){ const form = document.getElementById('appraisal-form'); if(!form) return; let step=1; const total=3; const stepEls = form.querySelectorAll('.step-content'); const stepsui = document.querySelectorAll('#sell .step'); const nextBtn = document.getElementById('app-next'); const prevBtn = document.getElementById('app-prev'); const preview = document.getElementById('app-preview'); function showStep(n){ stepEls.forEach(el=>el.style.display = (Number(el.dataset.step) === n) ? '' : 'none'); stepsui.forEach(s=> s.classList.toggle('active', Number(s.dataset.step) === n)); prevBtn.style.display = n===1 ? 'none' : ''; nextBtn.textContent = n===total ? 'Submit' : 'Next'; if(n===total){ const make = document.getElementById('app-make').value||'-'; const model = document.getElementById('app-model').value||'-'; const year = document.getElementById('app-year').value||'-'; const mileage = document.getElementById('app-mileage').value||'-'; const cond = document.getElementById('app-condition').value||'-'; preview.innerHTML = `<strong>${make} ${model} · ${year}</strong><div style=\"color:var(--muted);margin-top:6px\">${mileage} · ${cond}</div>`; } }
    showStep(1); nextBtn.addEventListener('click', ()=>{ if(step<total){ step++; showStep(step); return; } const make = document.getElementById('app-make').value||'-'; const model = document.getElementById('app-model').value||'-'; const year = document.getElementById('app-year').value||'-'; const mileage = document.getElementById('app-mileage').value||'-'; const cond = document.getElementById('app-condition').value||'-'; const msg = `Sell Request - ${make} ${model} ${year}\nMileage: ${mileage}\nCondition: ${cond}`; window.open(`https://wa.me/233577551078?text=${encodeURIComponent(msg)}`,'_blank'); form.reset(); step=1; showStep(step); }); prevBtn.addEventListener('click', ()=>{ if(step>1){ step--; showStep(step); } }); }

  document.addEventListener('DOMContentLoaded', ()=>{ replaceHTML(); setupNewTabFlash(); renderApex(); convertDisplayedPrices(); googleReviewEmulator(); loadMap(); sellFormLogic();
    const loadBtn = document.getElementById('load-more'); if(loadBtn) loadBtn.addEventListener('click', ()=>{ document.getElementById('apex-grid').scrollIntoView({behavior:'smooth'}); });
    const showMore = document.getElementById('show-more-btn'); if(showMore) showMore.addEventListener('click', ()=>{ alert('More inventory loading — integrate with backend or expand client-side dataset.'); });
  });
})();
</script>
```

---

How I committed this:
- I created the branch `institutional-steel-overhaul` in the repository.
- This file documents the changes needed and contains the exact CSS, HTML, and JS.

Next steps I can take for you (pick one):
- I can attempt to update index.html in the branch directly with these changes (I will need to create a file commit on the branch). Reply "Apply changes to index.html" and I will push the edits to the branch.
- Or I can create a smaller patch file that you or a reviewer can apply locally.

If you want me to proceed and apply changes directly to index.html on the branch, reply "Apply changes to index.html". If you prefer to review first, open the branch: https://github.com/vollexytech/VicDavis/tree/institutional-steel-overhaul and I will wait for your instruction.
