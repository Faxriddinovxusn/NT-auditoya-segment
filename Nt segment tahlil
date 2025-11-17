<!doctype html>
<html lang="uz">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Najot Ta'lim — Auditoriya Tahlili</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    :root{--bg:#f8fafc;--card:#ffffff;--muted:#6b7280;--accent:#0ea5e9}
    body{background:linear-gradient(135deg,#f0f4f8 0%,#e8eef5 25%,#f5f0ff 50%,#eff4fa 75%,#f8f1ff 100%);background-attachment:fixed;font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial;min-height:100vh;animation:bgShift 15s ease-in-out infinite}
    @keyframes bgShift{0%{background-position:0 0}50%{background-position:100% 100%}100%{background-position:0 0}}
    body::before{content:'';position:fixed;top:0;left:0;width:100%;height:100%;background:radial-gradient(circle at 15% 25%,rgba(14,165,233,0.06),transparent 40%),radial-gradient(circle at 85% 75%,rgba(124,77,255,0.05),transparent 40%);pointer-events:none;z-index:-1;animation:pulseGlow 8s ease-in-out infinite}
    @keyframes pulseGlow{0%,100%{opacity:1}50%{opacity:0.7}}

    /* Tabs */
    .tab-btn{transition:all .18s ease;border-radius:12px}
    .active-tab{box-shadow:0 10px 30px rgba(14,165,233,.12);transform:translateY(-6px)}

    /* Content reveal animation */
    .fade-enter{animation:fadeInUp .42s cubic-bezier(.2,.9,.2,1) both}
    @keyframes fadeInUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}

    /* Text animation - stagger for list items */
    .platform-section li{animation:slideInLeft .5s cubic-bezier(.2,.9,.2,1) both;opacity:0}
    .platform-section li:nth-child(1){animation-delay:.1s}
    .platform-section li:nth-child(2){animation-delay:.15s}
    .platform-section li:nth-child(3){animation-delay:.2s}
    .platform-section li:nth-child(4){animation-delay:.25s}
    .platform-section li:nth-child(5){animation-delay:.3s}
    .platform-section li:nth-child(6){animation-delay:.35s}
    .platform-section li:nth-child(7){animation-delay:.4s}
    @keyframes slideInLeft{from{opacity:0;transform:translateX(-16px)}to{opacity:1;transform:translateX(0)}}

    /* Section title animation */
    h2{animation:fadeInDown .6s cubic-bezier(.2,.9,.2,1) both}
    @keyframes fadeInDown{from{opacity:0;transform:translateY(-12px)}to{opacity:1;transform:translateY(0)}}

    /* Subtle card hover */
    .card-hover{transition:transform .28s ease,box-shadow .28s ease}
    .card-hover:hover{transform:translateY(-6px);box-shadow:0 18px 40px rgba(2,6,23,.08)}

    /* Animated underline for active tab */
    .tab-wrap{position:relative}
    .underline{position:absolute;left:0;bottom:-8px;height:3px;background:var(--accent);border-radius:6px;transition:all .28s cubic-bezier(.2,.9,.2,1);width:0}

    /* Growth sparkline canvas sizing */
    .growth-canvas{width:100%;max-width:320px;height:56px} /* reduced height */

    .doughnut-canvas{max-width:200px} /* smaller doughnut */

    /* Responsive tweaks */
    @media (max-width:640px){.doughnut-canvas{max-width:200px}.growth-canvas{max-width:240px}}

    /* ===== ADDED VISUAL / ANIMATION STYLES ===== */
    .logo-grid{display:flex;justify-content:center;gap:8px;margin-top:8px;flex-wrap:wrap} /* reduced gap & margin */
    .logo-card{background:linear-gradient(180deg,#fff,#fbfdff);border-radius:12px;padding:8px 10px;display:flex;align-items:center;gap:8px;box-shadow:0 6px 18px rgba(2,6,23,.05);transform:translateY(0);transition:transform .22s ease,box-shadow .22s ease;min-width:160px} /* smaller card */
    .logo-card:hover{transform:translateY(-6px) rotate(-0.6deg);box-shadow:0 14px 36px rgba(2,6,23,.06)}
    .logo-img{width:40px;height:40px;border-radius:8px;object-fit:cover;box-shadow:0 5px 14px rgba(2,6,23,.05)} /* smaller logo */
    .logo-name{font-weight:600;color:#0f172a;font-size:14px}
    .logo-stat{font-size:16px;font-weight:700;color:var(--accent)}
    .small-muted{font-size:11px;color:var(--muted)}

    /* Section reveal on scroll */
    .platform-section{opacity:.0;transform:translateY(8px) scale(.998);transition:opacity .45s cubic-bezier(.2,.9,.2,1),transform .45s cubic-bezier(.2,.9,.2,1)}
    .platform-section.in-view{opacity:1;transform:translateY(0) scale(1)}

  </style>
</head>
<body class="min-h-screen flex items-start justify-center p-4"> <!-- reduced padding -->
  <div class="w-full max-w-4xl"> <!-- narrower max width to cut side whitespace -->
    <header class="text-center mb-3"> <!-- reduced header spacing -->
      <h1 class="text-2xl font-semibold text-slate-800">Najot Ta'lim — Auditoriya Tahlili</h1>
      <p class="text-sm text-slate-500 mt-1">Tahlil</p>

      <!-- Visual logo cards with quick stats (animated) -->
      <div class="logo-grid" aria-hidden="false">
        <div class="logo-card" role="figure" title="Telegram segment">
          <img src="tg.jpg" alt="Telegram" class="logo-img" loading="lazy">
          <div class="logo-meta">
            <div class="logo-name">Telegram</div>
            <div><span id="tg-percent" class="logo-stat">81</span><span class="small-muted">%</span> <span class="logo-sub">Erkaklar</span></div>
          </div>
        </div>

        <div class="logo-card" role="figure" title="Instagram segment">
          <img src="ig.jpg" alt="Instagram" class="logo-img" loading="lazy">
          <div class="logo-meta">
            <div class="logo-name">Instagram</div>
            <div><span id="ig-percent" class="logo-stat">55</span><span class="small-muted">%</span> <span class="logo-sub">Ayollar</span></div>
          </div>
        </div>

        <div class="logo-card" role="figure" title="YouTube segment">
          <img src="yt.jpg" alt="YouTube" class="logo-img" loading="lazy">
          <div class="logo-meta">
            <div class="logo-name">YouTube</div>
            <div><span id="yt-percent" class="logo-stat">60</span><span class="small-muted">%</span> <span class="logo-sub">Erkaklar</span></div>
          </div>
        </div>
      </div>
    </header>

    <!-- Tabs -->
    <div class="flex justify-center mb-3 tab-wrap"> <!-- reduced space -->
      <div class="inline-flex gap-2 bg-white p-2 rounded-2xl shadow-sm"> <!-- slightly smaller gap -->
        <button id="tab-telegram" class="tab-btn px-4 py-2 rounded-xl text-sm font-medium active-tab bg-white border border-slate-100">Telegram</button>
        <button id="tab-instagram" class="tab-btn px-4 py-2 rounded-xl text-sm font-medium bg-white border border-slate-100">Instagram</button>
        <button id="tab-youtube" class="tab-btn px-4 py-2 rounded-xl text-sm font-medium bg-white border border-slate-100">YouTube</button>
      </div>
      <div id="tab-underline" class="underline"></div>
    </div>

    <!-- Content area -->
    <main class="bg-white rounded-2xl shadow p-4 fade-enter"> <!-- reduced padding -->
      <div id="content-area">

        <!-- TELEGRAM -->
        <section id="tele-section" class="platform-section">
          <div class="md:flex md:items-start md:gap-4"> <!-- reduced gap -->
            <div class="flex-1">
              <h2 class="text-lg font-semibold text-slate-800 mb-2">Telegram — tahlil (tegishli segment)</h2>
              <p class="text-sm text-slate-600 mb-3">Jins Nisbati: <strong>81% erkaklar / 19% ayollar</strong></p>

              <ul class="text-sm space-y-1 text-slate-700"> <!-- tighter list spacing -->
                <li><strong>Yoshi:</strong> 18–35 (asosiy: 20–30)</li>
                <li><strong>Daromad Darajasi:</strong> past–oʻrta (talaba va boshlangʻich mutaxassis)</li>
                <li><strong>Lokatsiya:</strong> Toshkent va viloyatlar — onlayn faol</li>
                <li><strong>Oilaviy Holati:</strong> ko'pchiligi yolgʻiz yoki boydoq</li>
                <li><strong>Qiziqishlari:</strong> dasturlash, IT/kompyuter kurslari, freelancing, kiberxavfsizlik</li>
                <li><strong>O'rganish Uslubi:</strong> onlayn, kechki/hafta oxiri darslar, telegram kanallardagi qisqa darslar</li>
                <li><strong>Maqsadi:</strong> ish topish, faoliyatini oshirish, amaliy portfolio yaratish</li>
              </ul>
            </div>

            <div class="w-full md:w-80 mt-4 md:mt-0 flex flex-col items-center gap-3"> <!-- reduced vertical gaps -->
              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover"> <!-- smaller padding -->
                <p class="text-xs text-slate-500 mb-1">Jins Nisbati</p>
                <canvas id="tg-gender" class="doughnut-canvas"></canvas>
              </div>

              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover">
                <p class="text-xs text-slate-500 mb-1">Oilaviy Holati</p>
                <canvas id="tg-marital" class="doughnut-canvas"></canvas>
              </div>
            </div>
          </div>
        </section>

        <!-- INSTAGRAM -->
        <section id="inst-section" class="platform-section hidden">
          <div class="md:flex md:items-start md:gap-4"> <!-- reduced gap -->
            <div class="flex-1">
              <h2 class="text-lg font-semibold text-slate-800 mb-2">Instagram — tahlil (tegishli segment)</h2>

              <ul class="text-sm space-y-1 text-slate-700"> <!-- tighter list spacing -->
                <li><strong>Yoshi:</strong> 16–30 (asosiy: 18–25)</li>
                <li><strong>Daromad Darajasi:</strong> past–oʻrta (talaba, yosh mutaxassis)</li>
                <li><strong>Lokatsiya:</strong> shaharlar </li>
                <li><strong>Oilaviy Holati:</strong> ko'pchiligi yolgʻiz yoki oila boshlanmagan</li>
                <li><strong>Qiziqishlari:</strong> dizayn, marketing, kreativ kontent, brend</li>
                <li><strong>O'rganish Uslubi:</strong> qisqa reel va story formatlari, vizual misollar</li>
                <li><strong>Maqsadi:</strong> Oson ish va kop daromad</li>
              </ul>
            </div>

            <div class="w-full md:w-80 mt-4 md:mt-0 flex flex-col items-center gap-3">
              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover">
                <p class="text-xs text-slate-500 mb-1">Jins Nisbati</p>
                <canvas id="ig-gender" class="doughnut-canvas"></canvas>
              </div>

              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover">
                <p class="text-xs text-slate-500 mb-1">Oilaviy Holati</p>
                <canvas id="ig-marital" class="doughnut-canvas"></canvas>
              </div>
            </div>
          </div>
        </section>

        <!-- YOUTUBE -->
        <section id="yt-section" class="platform-section hidden">
          <div class="md:flex md:items-start md:gap-4"> <!-- reduced gap -->
            <div class="flex-1">
              <h2 class="text-lg font-semibold text-slate-800 mb-2">YouTube — tahlil (tegishli segment)</h2>

              <ul class="text-sm space-y-1 text-slate-700"> <!-- tighter list spacing -->
                <li><strong>Yoshi:</strong> 16–35 (asosiy: 28–30)</li>
                <li><strong>Daromad Darajasi:</strong> o'rtacha </li>
                <li><strong>Lokatsiya:</strong> hududlar va shaharlar </li>
                <li><strong>Oilaviy Holati:</strong> aralash — talaba va ishlovchi qatlamlar</li>
                <li><strong>Qiziqishlari:</strong> batafsil tutoriallar, kurslar, loyiha tayyorlash</li>
                <li><strong>O'rganish Uslubi:</strong> uzun format videolar, step-by-step darslar</li>
                <li><strong>Maqsadi:</strong> malaka oshirish, hamkasb darajasiga yetish, loyiha yaratish</li>
              </ul>
            </div>

            <div class="w-full md:w-80 mt-4 md:mt-0 flex flex-col items-center gap-3">
              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover">
                <p class="text-xs text-slate-500 mb-1">Jinsi</p>
                <canvas id="yt-gender" class="doughnut-canvas"></canvas>
              </div>

              <div class="w-full bg-gray-50 p-3 rounded-xl card-hover">
                <p class="text-xs text-slate-500 mb-1">Oilaviy Holati</p>
                <canvas id="yt-marital" class="doughnut-canvas"></canvas>
              </div>
            </div>
          </div>
        </section>

      </div>
    </main>

    <footer class="text-center mt-2 text-xs text-slate-400">Husniddin</footer> <!-- smaller footer spacing -->
  </div>

  <script>
    // Ensure charts object exists before any function may reference it
    let charts = {};
    let chartsReady = false; // flag to prevent premature access

    // Tab logic with animated underline & fade
    const tabs = {
      telegram: document.getElementById('tab-telegram'),
      instagram: document.getElementById('tab-instagram'),
      youtube: document.getElementById('tab-youtube')
    };
    const sections = {
      telegram: document.getElementById('tele-section'),
      instagram: document.getElementById('inst-section'),
      youtube: document.getElementById('yt-section')
    };
    const underline = document.getElementById('tab-underline');

    function positionUnderline(activeBtn){
      if(!activeBtn || !underline) return;
      const rect = activeBtn.getBoundingClientRect();
      const parentRect = activeBtn.parentElement.getBoundingClientRect();
      const left = rect.left - parentRect.left + 4; // padding offset
      underline.style.transform = `translateX(${left}px)`;
      underline.style.width = `${Math.max(24, rect.width - 8)}px`;
    }

    function setActive(key){
      Object.keys(tabs).forEach(k=>{tabs[k].classList.remove('active-tab');});
      tabs[key].classList.add('active-tab');
      Object.keys(sections).forEach(k=>{sections[k].classList.add('hidden');});
      const sec = sections[key];
      sec.classList.remove('hidden');
      sec.classList.add('fade-enter');
      positionUnderline(tabs[key]);

      // animate associated growth chart only if charts are ready
      if(chartsReady) animateGrowth(key);
    }

    Object.keys(tabs).forEach(k=>{tabs[k].addEventListener('click',()=>setActive(k));});
    window.addEventListener('resize',()=>{
      const active = Object.keys(tabs).find(k=>tabs[k].classList.contains('active-tab')) || 'telegram';
      positionUnderline(tabs[active]);
    });

    // Initial underline positioning and set active visually (no chart animation yet)
    setTimeout(()=>positionUnderline(tabs.telegram),80);
    // Set visual active tab without touching charts
    tabs.telegram.classList.add('active-tab');

    // Chart data (labels in Uzbek)
    // Bar chart data (horizontal bars for better visual variety)
    const tgGenderData = {labels:['Erkaklar','Ayollar'],datasets:[{label:'Foiz',data:[81,19],backgroundColor:['rgba(14,165,233,0.85)','rgba(99,102,241,0.85)'],borderRadius:8,borderSkipped:false}]};
    const tgMaritalData = {labels:['Yolgʻiz','Oilali','Boshqa'],datasets:[{label:'Foiz',data:[60,36,4],backgroundColor:['rgba(59,130,246,0.85)','rgba(96,165,250,0.85)','rgba(148,163,184,0.85)'],borderRadius:8,borderSkipped:false}]};

    const igGenderData = {labels:['Erkaklar','Ayollar'],datasets:[{label:'Foiz',data:[45,55],backgroundColor:['rgba(14,165,233,0.85)','rgba(99,102,241,0.85)'],borderRadius:8,borderSkipped:false}]};
    const igMaritalData = {labels:['Yolgʻiz','Oilali','Boshqa'],datasets:[{label:'Foiz',data:[72,25,3],backgroundColor:['rgba(59,130,246,0.85)','rgba(96,165,250,0.85)','rgba(148,163,184,0.85)'],borderRadius:8,borderSkipped:false}]};

    const ytGenderData = {labels:['Erkaklar','Ayollar'],datasets:[{label:'Foiz',data:[60,40],backgroundColor:['rgba(14,165,233,0.85)','rgba(99,102,241,0.85)'],borderRadius:8,borderSkipped:false}]};
    const ytMaritalData = {labels:['Yolgʻiz','Oilali','Boshqa'],datasets:[{label:'Foiz',data:[55,42,3],backgroundColor:['rgba(59,130,246,0.85)','rgba(96,165,250,0.85)','rgba(148,163,184,0.85)'],borderRadius:8,borderSkipped:false}]};

    // Options
    const baseBarOptions = {indexAxis:'y',responsive:true,maintainAspectRatio:true,plugins:{legend:{display:false},tooltip:{padding:8,backgroundColor:'rgba(0,0,0,0.8)',titleFont:{size:12},bodyFont:{size:11}}},scales:{x:{beginAtZero:true,max:100,ticks:{font:{size:10}},grid:{color:'rgba(0,0,0,0.05)'}},y:{ticks:{font:{size:11},color:'#334155'}}},animation:{duration:1200,easing:'easeOutQuart',delay:(ctx)=>ctx.dataIndex*100}};

    function createBar(ctx,data,opts){return new Chart(ctx,{type:'bar',data:data,options:opts});}

    // Create charts once DOM + external libs are loaded
    window.addEventListener('load',()=>{
      // Create bar charts instead of doughnuts
      charts.tgGender = createBar(document.getElementById('tg-gender'),tgGenderData,baseBarOptions);
      charts.tgMarital = createBar(document.getElementById('tg-marital'),tgMaritalData,baseBarOptions);
      charts.igGender = createBar(document.getElementById('ig-gender'),igGenderData,baseBarOptions);
      charts.igMarital = createBar(document.getElementById('ig-marital'),igMaritalData,baseBarOptions);
      charts.ytGender = createBar(document.getElementById('yt-gender'),ytGenderData,baseBarOptions);
      charts.ytMarital = createBar(document.getElementById('yt-marital'),ytMaritalData,baseBarOptions);

      // Mark charts as ready so animateGrowth can run safely
      chartsReady = true;

      // Now that charts exist, mark ready (no growth charts present)
      const activeKey = Object.keys(tabs).find(k=>tabs[k].classList.contains('active-tab')) || 'telegram';
    });

    // Trigger a subtle animation on growth charts when switching tabs
    function animateGrowth(key){
      // growth charts removed — nothing to animate
      return;
    }

    // Accessibility: keyboard nav for tabs
    Object.values(tabs).forEach(btn=>{btn.setAttribute('tabindex','0');btn.addEventListener('keydown',e=>{if(e.key==='Enter'||e.key===' ')btn.click();});});

    /* ===== ADDED JS: animated counters + reveal observer ===== */
    // animate a number in element from 0 to target
    function animateNumber(el, to, ms = 900) {
      if(!el) return;
      const start = 0;
      const startTime = performance.now();
      function step(now){
        const t = Math.min(1, (now - startTime) / ms);
        const eased = t<.5 ? 2*t*t : -1 + (4 - 2*t)*t; // simple ease
        const val = Math.round(start + (to - start) * eased);
        el.textContent = val;
        if(t < 1) requestAnimationFrame(step);
      }
      requestAnimationFrame(step);
    }

    // Reveal platform sections when they scroll into view and nudge growth chart animation
    const observer = new IntersectionObserver((entries)=>{
      entries.forEach(en=>{
        if(en.isIntersecting){
          en.target.classList.add('in-view');
          const id = en.target.id;
          if(id === 'tele-section' && chartsReady) animateGrowth('telegram');
          if(id === 'inst-section' && chartsReady) animateGrowth('instagram');
          if(id === 'yt-section' && chartsReady) animateGrowth('youtube');
        }
      });
    },{threshold:0.18});

    // Observe each platform section
    document.querySelectorAll('.platform-section').forEach(s=>observer.observe(s));

    // Run counter animations once window loaded (after charts created)
    window.addEventListener('load',()=>{
      // small delays for nicer stagger
      setTimeout(()=>animateNumber(document.getElementById('tg-percent'),81),120);
      setTimeout(()=>animateNumber(document.getElementById('ig-percent'),55),240);
      setTimeout(()=>animateNumber(document.getElementById('yt-percent'),60),360);
    });

    // Small improvement: clicking logos focuses related tab
    document.querySelectorAll('.logo-card').forEach(card=>{
      card.addEventListener('click',()=>{
        const title = card.getAttribute('title') || '';
        if(title.toLowerCase().startsWith('telegram')) tabs.telegram.click();
        if(title.toLowerCase().startsWith('instagram')) tabs.instagram.click();
        if(title.toLowerCase().startsWith('youtube')) tabs.youtube.click();
      });
      card.style.cursor = 'pointer';
    });
  </script>
</body>
</html>
