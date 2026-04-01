# Rudra
#Very nice and good for drivers
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RideLocal — Find Your Nearest Cab Driver</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Inter',sans-serif;background:#050505;color:#fff;overflow-x:hidden}
::-webkit-scrollbar{width:5px}::-webkit-scrollbar-track{background:transparent}::-webkit-scrollbar-thumb{background:linear-gradient(180deg,#3B82F6,#7C3AED);border-radius:10px}

/* Cursor */
.cursor-dot,.cursor-ring{position:fixed;pointer-events:none;z-index:99999;border-radius:50%}
.cursor-dot{width:6px;height:6px;background:#fff;transition:transform .08s}
.cursor-ring{width:36px;height:36px;border:1.5px solid rgba(59,130,246,.4);transform:translate(-50%,-50%);transition:width .25s,height .25s,border-color .25s}
.cursor-ring.hover{width:56px;height:56px;border-color:rgba(59,130,246,.7)}
@media(pointer:coarse){.cursor-dot,.cursor-ring{display:none!important}}

/* Keyframes */
@keyframes floatUp{0%{transform:translateY(0) scale(1);opacity:0}10%{opacity:.5}90%{opacity:.5}100%{transform:translateY(-100vh) scale(.2);opacity:0}}
@keyframes fadeUp{from{opacity:0;transform:translateY(60px);filter:blur(4px)}to{opacity:1;transform:translateY(0);filter:blur(0)}}
@keyframes fadeDown{from{opacity:0;transform:translateY(-30px)}to{opacity:1;transform:translateY(0)}}
@keyframes scaleIn{from{opacity:0;transform:scale(.85)}to{opacity:1;transform:scale(1)}}
@keyframes slideL{from{opacity:0;transform:translateX(-50px)}to{opacity:1;transform:translateX(0)}}
@keyframes slideR{from{opacity:0;transform:translateX(50px)}to{opacity:1;transform:translateX(0)}}
@keyframes pulseGlow{0%,100%{box-shadow:0 0 20px rgba(59,130,246,.2)}50%{box-shadow:0 0 40px rgba(59,130,246,.5)}}
@keyframes textShimmer{0%{background-position:-200% center}100%{background-position:200% center}}
@keyframes morphBlob{0%,100%{border-radius:60% 40% 30% 70%/60% 30% 70% 40%}33%{border-radius:30% 60% 70% 40%/50% 60% 30% 60%}66%{border-radius:50% 60% 30% 60%/30% 60% 70% 40%}}
@keyframes spin{to{transform:rotate(360deg)}}
@keyframes spinR{to{transform:rotate(-360deg)}}
@keyframes ripple{0%{transform:scale(1);opacity:.4}100%{transform:scale(2.8);opacity:0}}
@keyframes blink{50%{opacity:0}}
@keyframes floatY{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}
@keyframes carDrive{0%{transform:translateX(-120px)}100%{transform:translateX(calc(100vw + 120px))}}
@keyframes notifIn{from{transform:translateX(110%);opacity:0}to{transform:translateX(0);opacity:1}}
@keyframes notifOut{to{transform:translateX(110%);opacity:0}}
@keyframes camFlash{0%{opacity:.9}100%{opacity:0}}
@keyframes borderRun{0%{background-position:0% 50%}50%{background-position:100% 50%}100%{background-position:0% 50%}}
@keyframes typewriter{from{width:0}to{width:100%}}
@keyframes expandWidth{from{transform:scaleX(0)}to{transform:scaleX(1)}}
@keyframes cardIn{from{opacity:0;transform:translateY(30px) scale(.96)}to{opacity:1;transform:translateY(0) scale(1)}}
@keyframes dotPulse{0%,80%,100%{transform:scale(0)}40%{transform:scale(1)}}
@keyframes glowPulse{0%,100%{opacity:.2}50%{opacity:.6}}

/* Scroll reveal */
.rv{opacity:0;transform:translateY(40px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.rv.on{opacity:1;transform:translateY(0)}
.rv-l{opacity:0;transform:translateX(-40px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.rv-l.on{opacity:1;transform:translateX(0)}
.rv-r{opacity:0;transform:translateX(40px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.rv-r.on{opacity:1;transform:translateX(0)}
.rv-s{opacity:0;transform:scale(.9);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.rv-s.on{opacity:1;transform:scale(1)}
.d1{transition-delay:.08s}.d2{transition-delay:.16s}.d3{transition-delay:.24s}.d4{transition-delay:.32s}.d5{transition-delay:.4s}.d6{transition-delay:.48s}

/* Glass */
.gl{background:rgba(20,20,20,.45);backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border:1px solid rgba(255,255,255,.06)}
.gl-s{background:rgba(12,12,12,.88);backdrop-filter:blur(28px);-webkit-backdrop-filter:blur(28px);border:1px solid rgba(255,255,255,.07)}

/* Gradient text */
.gt{background:linear-gradient(135deg,#60A5FA,#3B82F6 50%,#A855F7);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.gt-shimmer{background:linear-gradient(90deg,#60A5FA,#3B82F6,#A855F7,#3B82F6,#60A5FA);background-size:200% auto;-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;animation:textShimmer 4s linear infinite}

/* Buttons */
.bp{background:linear-gradient(135deg,#1D4ED8,#2563EB);position:relative;overflow:hidden;transition:all .4s cubic-bezier(.16,1,.3,1)}
.bp::after{content:'';position:absolute;top:50%;left:50%;width:0;height:0;background:rgba(255,255,255,.12);border-radius:50%;transform:translate(-50%,-50%);transition:width .5s,height .5s}
.bp:hover::after{width:320px;height:320px}
.bp:hover{transform:translateY(-3px);box-shadow:0 14px 44px rgba(29,78,216,.35)}
.bp:active{transform:translateY(0) scale(.97)}
.bp span,.bp i{position:relative;z-index:2}
.bs{border:1px solid rgba(255,255,255,.08);transition:all .4s cubic-bezier(.16,1,.3,1);position:relative;overflow:hidden}
.bs::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(59,130,246,.08),rgba(168,85,247,.04));opacity:0;transition:opacity .4s}
.bs:hover::before{opacity:1}
.bs:hover{border-color:rgba(59,130,246,.35);transform:translateY(-3px);box-shadow:0 8px 30px rgba(59,130,246,.08)}
.bgo{background:linear-gradient(135deg,#16A34A,#22C55E);position:relative;overflow:hidden;transition:all .4s cubic-bezier(.16,1,.3,1)}
.bgo:hover{transform:translateY(-3px);box-shadow:0 14px 40px rgba(22,163,74,.3)}
.brd{background:linear-gradient(135deg,#DC2626,#EF4444);position:relative;overflow:hidden;transition:all .4s cubic-bezier(.16,1,.3,1)}
.brd:hover{transform:translateY(-3px);box-shadow:0 14px 40px rgba(220,38,38,.3)}

/* Driver card */
.dc{transition:all .55s cubic-bezier(.16,1,.3,1);position:relative;overflow:hidden}
.dc::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,#3B82F6,#A855F7);transform:scaleX(0);transition:transform .55s cubic-bezier(.16,1,.3,1);transform-origin:left}
.dc:hover::after{transform:scaleX(1)}
.dc:hover{transform:translateY(-8px);border-color:rgba(59,130,246,.18);box-shadow:0 24px 64px rgba(59,130,246,.08)}

/* Status */
.st-on{width:8px;height:8px;background:#22C55E;border-radius:50%;position:relative;flex-shrink:0}
.st-on::after{content:'';position:absolute;inset:-3px;border:1.5px solid rgba(34,197,94,.3);border-radius:50%;animation:ripple 1.5s infinite}

/* Nav */
.nav{backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);background:rgba(5,5,5,.5);border-bottom:1px solid rgba(255,255,255,.03);transition:all .4s}
.nav.scrolled{background:rgba(5,5,5,.88);border-bottom-color:rgba(255,255,255,.06)}

/* Divider */
.divider{height:1px;background:linear-gradient(90deg,transparent,rgba(59,130,246,.2),rgba(168,85,247,.12),transparent)}

/* Modal */
.mo{position:fixed;inset:0;z-index:9000;background:rgba(0,0,0,.7);backdrop-filter:blur(8px);display:flex;align-items:center;justify-content:center;opacity:0;visibility:hidden;transition:all .45s cubic-bezier(.16,1,.3,1)}
.mo.on{opacity:1;visibility:visible}
.mc{transform:scale(.9) translateY(24px);transition:all .45s cubic-bezier(.16,1,.3,1)}
.mo.on .mc{transform:scale(1) translateY(0)}

/* Toast */
.toast{position:fixed;bottom:24px;right:24px;z-index:9998;padding:14px 20px;border-radius:14px;animation:notifIn .45s cubic-bezier(.16,1,.3,1);transition:all .35s;max-width:380px}
.toast.out{animation:notifOut .35s ease forwards}

/* Notification */
.nb{position:absolute;top:-5px;right:-5px;min-width:16px;height:16px;background:linear-gradient(135deg,#EF4444,#F97316);border-radius:8px;font-size:8px;font-weight:700;display:flex;align-items:center;justify-content:center;padding:0 3px;animation:scaleIn .35s cubic-bezier(.16,1,.3,1);box-shadow:0 2px 8px rgba(239,68,68,.3)}

/* Page */
.pg{display:none}.pg.on{display:block;animation:fadeUp .5s ease}

/* Camera */
.cam{border:2px dashed rgba(59,130,246,.15);border-radius:14px;transition:all .4s cubic-bezier(.16,1,.3,1)}
.cam:hover{border-color:rgba(59,130,246,.4);background:rgba(59,130,246,.02)}
.cam.ok{border:2px solid #22C55E;box-shadow:0 0 16px rgba(34,197,94,.08)}
.cam-flash{position:absolute;inset:0;background:#fff;animation:camFlash .25s ease forwards;pointer-events:none;border-radius:14px}

/* Credit photo */
.cp{position:relative;overflow:hidden;border-radius:20px}
.cp::after{content:'';position:absolute;inset:0;background:linear-gradient(to top,rgba(5,5,5,.85) 0%,rgba(5,5,5,.2) 50%,transparent 80%)}
.cp img{transition:transform .8s cubic-bezier(.16,1,.3,1)}.cp:hover img{transform:scale(1.06)}

/* Filter/Tab */
.fb.on{background:rgba(59,130,246,.12)!important;color:#fff!important;border-color:rgba(59,130,246,.25)!important}
.tb.on{background:rgba(59,130,246,.1);color:#fff;border-color:rgba(59,130,246,.2)}

/* Request card */
.rc{transition:all .4s cubic-bezier(.16,1,.3,1)}.rc:hover{border-color:rgba(59,130,246,.15);transform:translateX(3px)}

/* Blob */
.blob{animation:morphBlob 10s ease-in-out infinite}

/* Float */
.fy{animation:floatY 4s ease-in-out infinite}

/* Mobile menu */
.mm{transform:translateX(100%);transition:transform .45s cubic-bezier(.16,1,.3,1)}.mm.on{transform:translateX(0)}

/* Moving car */
.mcar{position:fixed;bottom:12px;left:-120px;z-index:50;opacity:.1;animation:carDrive 20s linear infinite;animation-delay:6s}

/* Map dot */
.md{position:absolute;width:6px;height:6px;background:#3B82F6;border-radius:50%}
.md::after{content:'';position:absolute;inset:-3px;border:1.5px solid rgba(59,130,246,.25);border-radius:50%;animation:ripple 2s infinite}

/* Typing dots */
.td span{display:inline-block;width:6px;height:6px;border-radius:50%;background:#3B82F6;animation:dotPulse 1.4s infinite ease-in-out both}
.td span:nth-child(1){animation-delay:-.32s}.td span:nth-child(2){animation-delay:-.16s}

/* Input focus glow */
input:focus,select:focus,textarea:focus{box-shadow:0 0 0 3px rgba(59,130,246,.08)}
</style>
</head>
<body>

<div class="cursor-dot" id="cDot"></div>
<div class="cursor-ring" id="cRing"></div>
<div class="mcar">🚗</div>
<div id="ptcl" class="fixed inset-0 pointer-events-none z-0"></div>

<!-- NAV -->
<nav class="nav fixed top-0 left-0 right-0 z-[100] h-16" id="nav">
  <div class="max-w-7xl mx-auto px-5 h-full flex items-center justify-between">
    <a href="#" onclick="go('home');return false" class="flex items-center gap-2.5 group">
      <div class="w-9 h-9 rounded-xl bg-gradient-to-br from-blue-500 to-blue-700 flex items-center justify-center transition-transform duration-500 group-hover:rotate-12 group-hover:scale-110"><i class="fas fa-car text-white text-sm"></i></div>
      <span class="text-lg font-bold tracking-tight">Ride<span class="text-blue-400">Local</span></span>
    </a>
    <div class="hidden md:flex items-center gap-7">
      <a href="#" onclick="go('home');return false" class="text-[13px] text-neutral-400 hover:text-white transition-colors duration-300 relative group">Home<span class="absolute -bottom-1 left-0 w-0 h-[1.5px] bg-gradient-to-r from-blue-500 to-purple-500 transition-all duration-300 group-hover:w-full"></span></a>
      <a href="#" onclick="go('cust');return false" class="text-[13px] text-neutral-400 hover:text-white transition-colors duration-300 relative group">Find Drivers<span class="absolute -bottom-1 left-0 w-0 h-[1.5px] bg-gradient-to-r from-blue-500 to-purple-500 transition-all duration-300 group-hover:w-full"></span></a>
      <a href="#" onclick="go('driv');return false" class="text-[13px] text-neutral-400 hover:text-white transition-colors duration-300 relative group">Driver Portal<span class="absolute -bottom-1 left-0 w-0 h-[1.5px] bg-gradient-to-r from-blue-500 to-purple-500 transition-all duration-300 group-hover:w-full"></span></a>
    </div>
    <div class="flex items-center gap-2">
      <button onclick="togNotif()" class="relative w-10 h-10 rounded-xl gl flex items-center justify-center text-neutral-400 hover:text-white transition-all duration-300" id="nBell"><i class="fas fa-bell text-sm"></i><span class="nb" id="nBadge" style="display:none">0</span></button>
      <button onclick="togMM()" class="md:hidden w-10 h-10 rounded-xl gl flex items-center justify-center text-white"><i class="fas fa-bars"></i></button>
    </div>
  </div>
</nav>

<!-- Notif Panel -->
<div id="nPanel" class="fixed top-16 right-3 w-80 z-[99] gl-s rounded-2xl overflow-hidden shadow-2xl" style="display:none">
  <div class="p-4 border-b border-white/5 flex items-center justify-between">
    <h3 class="text-sm font-bold">Notifications</h3>
    <button onclick="clrNotif()" class="text-[10px] text-blue-400 hover:underline">Clear All</button>
  </div>
  <div id="nList" class="max-h-80 overflow-y-auto p-2"><p class="text-xs text-neutral-600 text-center py-8"><i class="fas fa-bell-slash text-xl block mb-2"></i>Nothing yet</p></div>
</div>

<!-- Mobile Menu -->
<div id="mMenu" class="mm fixed top-0 right-0 bottom-0 w-72 z-[101] gl-s">
  <div class="p-6">
    <button onclick="togMM()" class="text-white text-xl mb-8 hover:rotate-90 transition-transform duration-300 block"><i class="fas fa-times"></i></button>
    <div class="flex flex-col gap-1">
      <a href="#" onclick="go('home');togMM();return false" class="text-neutral-300 hover:text-white hover:bg-white/5 py-3 px-4 rounded-xl transition-all duration-300">Home</a>
      <a href="#" onclick="go('cust');togMM();return false" class="text-neutral-300 hover:text-white hover:bg-white/5 py-3 px-4 rounded-xl transition-all duration-300">Find Drivers</a>
      <a href="#" onclick="go('driv');togMM();return false" class="text-neutral-300 hover:text-white hover:bg-white/5 py-3 px-4 rounded-xl transition-all duration-300">Driver Portal</a>
    </div>
  </div>
</div>

<!-- ===== HOME ===== -->
<div id="pg-home" class="pg on">
  <section class="relative min-h-screen flex items-center justify-center pt-16 overflow-hidden">
    <div class="absolute inset-0">
      <div class="blob absolute top-[20%] left-[15%] w-[480px] h-[480px] bg-blue-500/[.06] blur-[100px]"></div>
      <div class="blob absolute bottom-[20%] right-[15%] w-[420px] h-[420px] bg-purple-500/[.05] blur-[90px]" style="animation-delay:-5s"></div>
      <svg class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[580px] h-[580px] opacity-[.035]" style="animation:spin 45s linear infinite"><circle cx="290" cy="290" r="270" fill="none" stroke="#3B82F6" stroke-width="1" stroke-dasharray="8 14"/></svg>
      <svg class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[400px] h-[400px] opacity-[.05]" style="animation:spinR 28s linear infinite"><circle cx="200" cy="200" r="180" fill="none" stroke="#A855F7" stroke-width="1" stroke-dasharray="4 10"/></svg>
      <div class="absolute inset-0 opacity-[.025]" style="background-image:linear-gradient(rgba(59,130,246,.4) 1px,transparent 1px),linear-gradient(90deg,rgba(59,130,246,.4) 1px,transparent 1px);background-size:70px 70px"></div>
    </div>
    <div class="relative z-10 max-w-7xl mx-auto px-5 text-center">
      <div style="animation:fadeDown .7s cubic-bezier(.16,1,.3,1) .15s both">
        <div class="inline-flex items-center gap-2.5 px-4 py-2 rounded-full gl mb-8">
          <span class="st-on"></span>
          <span class="text-[11px] font-medium text-neutral-300">24 Drivers Online</span>
          <span class="w-1.5 h-1.5 rounded-full bg-blue-400" style="animation:glowPulse 2s ease infinite"></span>
        </div>
      </div>
      <h1 class="text-5xl md:text-7xl lg:text-[5.2rem] font-black tracking-tighter leading-[.92] mb-7" style="animation:fadeUp .9s cubic-bezier(.16,1,.3,1) .3s both">
        Your Local<br><span class="gt-shimmer">Ride Partner</span>
      </h1>
      <p class="text-neutral-400 text-sm md:text-base max-w-lg mx-auto mb-11 leading-relaxed" style="animation:fadeUp .9s cubic-bezier(.16,1,.3,1) .5s both">Connect with trusted local drivers instantly. See their info, car photos, and prices before you ride.</p>
      <div class="flex flex-col sm:flex-row items-center justify-center gap-3 mb-16" style="animation:fadeUp .9s cubic-bezier(.16,1,.3,1) .7s both">
        <button onclick="go('cust')" class="bp px-9 h-[52px] rounded-2xl text-sm font-semibold flex items-center gap-2.5"><span><i class="fas fa-search"></i> Find a Driver</span></button>
        <button onclick="go('driv')" class="bs px-9 h-[52px] rounded-2xl text-sm font-semibold flex items-center gap-2.5"><i class="fas fa-id-badge"></i> Join as Driver</button>
      </div>
      <div class="grid grid-cols-3 gap-6 max-w-md mx-auto" style="animation:fadeUp .9s cubic-bezier(.16,1,.3,1) .9s both">
        <div class="text-center"><div class="text-2xl md:text-3xl font-black"><span class="ctr" data-t="500">0</span>+</div><div class="text-[9px] text-neutral-500 mt-1 uppercase tracking-widest">Drivers</div></div>
        <div class="text-center"><div class="text-2xl md:text-3xl font-black"><span class="ctr" data-t="12000">0</span>+</div><div class="text-[9px] text-neutral-500 mt-1 uppercase tracking-widest">Rides</div></div>
        <div class="text-center"><div class="text-2xl md:text-3xl font-black"><span class="ctr" data-t="4.9">0</span>★</div><div class="text-[9px] text-neutral-500 mt-1 uppercase tracking-widest">Rating</div></div>
      </div>
      <div class="mt-14" style="animation:floatY 2.5s ease-in-out infinite;animation-delay:2s">
        <div class="w-5 h-9 rounded-full border border-neutral-700/50 flex items-start justify-center pt-1.5 mx-auto"><div class="w-1 h-2 rounded-full bg-blue-400/60"></div></div>
      </div>
    </div>
  </section>

  <div class="divider max-w-6xl mx-auto"></div>

  <!-- Two Portals -->
  <section class="py-24 md:py-32 relative">
    <div class="max-w-6xl mx-auto px-5">
      <div class="text-center mb-16">
        <p class="rv text-[10px] font-bold uppercase tracking-[.25em] text-blue-400 mb-3">Two Portals</p>
        <h2 class="rv d1 text-3xl md:text-4xl font-black tracking-tight">Choose Your <span class="gt">Path</span></h2>
      </div>
      <div class="grid md:grid-cols-2 gap-6 max-w-4xl mx-auto">
        <div class="rv d2 gl rounded-3xl p-9 text-center group cursor-pointer relative overflow-hidden hover:border-blue-500/15 transition-all duration-600" onclick="go('cust')">
          <div class="absolute top-0 left-0 w-full h-[2px] bg-gradient-to-r from-blue-500 to-cyan-400 origin-left scale-x-0 group-hover:scale-x-100 transition-transform duration-700"></div>
          <div class="w-20 h-20 rounded-2xl bg-blue-500/[.06] flex items-center justify-center mx-auto mb-7 group-hover:scale-110 group-hover:bg-blue-500/[.12] transition-all duration-500 fy"><i class="fas fa-user text-blue-400 text-3xl"></i></div>
          <h3 class="text-xl font-bold mb-2">For Customers</h3>
          <p class="text-[13px] text-neutral-500 leading-relaxed mb-7">Search drivers, view car photos, compare prices, send requests & get notified.</p>
          <div class="flex flex-wrap justify-center gap-1.5 mb-7">
            <span class="px-2.5 py-1 rounded-lg bg-blue-500/[.06] text-blue-400 text-[9px] font-medium">Search</span>
            <span class="px-2.5 py-1 rounded-lg bg-blue-500/[.06] text-blue-400 text-[9px] font-medium">Photos</span>
            <span class="px-2.5 py-1 rounded-lg bg-blue-500/[.06] text-blue-400 text-[9px] font-medium">Requests</span>
            <span class="px-2.5 py-1 rounded-lg bg-blue-500/[.06] text-blue-400 text-[9px] font-medium">Notifications</span>
          </div>
          <span class="bp inline-flex items-center gap-2 px-7 py-2.5 rounded-xl text-sm font-semibold"><span>Enter <i class="fas fa-arrow-right text-xs"></i></span></span>
        </div>
        <div class="rv d3 gl rounded-3xl p-9 text-center group cursor-pointer relative overflow-hidden hover:border-green-500/15 transition-all duration-600" onclick="go('driv')">
          <div class="absolute top-0 left-0 w-full h-[2px] bg-gradient-to-r from-green-500 to-emerald-400 origin-left scale-x-0 group-hover:scale-x-100 transition-transform duration-700"></div>
          <div class="w-20 h-20 rounded-2xl bg-green-500/[.06] flex items-center justify-center mx-auto mb-7 group-hover:scale-110 group-hover:bg-green-500/[.12] transition-all duration-500 fy" style="animation-delay:.6s"><i class="fas fa-car text-green-400 text-3xl"></i></div>
          <h3 class="text-xl font-bold mb-2">For Drivers</h3>
          <p class="text-[13px] text-neutral-500 leading-relaxed mb-7">Register with camera photos, set prices, receive requests & contact customers.</p>
          <div class="flex flex-wrap justify-center gap-1.5 mb-7">
            <span class="px-2.5 py-1 rounded-lg bg-green-500/[.06] text-green-400 text-[9px] font-medium">Register</span>
            <span class="px-2.5 py-1 rounded-lg bg-green-500/[.06] text-green-400 text-[9px] font-medium">Camera</span>
            <span class="px-2.5 py-1 rounded-lg bg-green-500/[.06] text-green-400 text-[9px] font-medium">Pricing</span>
            <span class="px-2.5 py-1 rounded-lg bg-green-500/[.06] text-green-400 text-[9px] font-medium">Accept</span>
          </div>
          <span class="bgo inline-flex items-center gap-2 px-7 py-2.5 rounded-xl text-sm font-semibold"><i class="fas fa-arrow-right text-xs"></i> Enter</span>
        </div>
      </div>
    </div>
  </section>

  <div class="divider max-w-6xl mx-auto"></div>

  <!-- How it Works -->
  <section class="py-24 md:py-32">
    <div class="max-w-6xl mx-auto px-5">
      <div class="text-center mb-16">
        <p class="rv text-[10px] font-bold uppercase tracking-[.25em] text-blue-400 mb-3">Simple Process</p>
        <h2 class="rv d1 text-3xl md:text-4xl font-black tracking-tight">How It <span class="gt">Works</span></h2>
      </div>
      <div class="grid md:grid-cols-4 gap-5 max-w-4xl mx-auto relative">
        <div class="hidden md:block absolute top-14 left-[14%] right-[14%] h-px bg-gradient-to-r from-blue-500/20 via-purple-500/15 to-blue-500/20"></div>
        <div class="rv d1 gl rounded-2xl p-5 text-center relative group hover:bg-white/[.02] transition-all duration-500">
          <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-7 h-7 rounded-full bg-gradient-to-br from-blue-500 to-blue-700 text-[10px] font-bold flex items-center justify-center shadow-lg shadow-blue-500/20">1</div>
          <div class="w-12 h-12 rounded-xl bg-blue-500/[.07] flex items-center justify-center mx-auto mb-3 group-hover:scale-110 transition-transform duration-400"><i class="fas fa-search text-blue-400"></i></div>
          <h3 class="font-bold text-sm mb-1">Browse</h3>
          <p class="text-[11px] text-neutral-500 leading-relaxed">View drivers near you</p>
        </div>
        <div class="rv d2 gl rounded-2xl p-5 text-center relative group hover:bg-white/[.02] transition-all duration-500">
          <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-7 h-7 rounded-full bg-gradient-to-br from-blue-600 to-purple-600 text-[10px] font-bold flex items-center justify-center shadow-lg shadow-purple-500/20">2</div>
          <div class="w-12 h-12 rounded-xl bg-purple-500/[.07] flex items-center justify-center mx-auto mb-3 group-hover:scale-110 transition-transform duration-400"><i class="fas fa-id-card text-purple-400"></i></div>
          <h3 class="font-bold text-sm mb-1">Check</h3>
          <p class="text-[11px] text-neutral-500 leading-relaxed">Car photos & prices</p>
        </div>
        <div class="rv d3 gl rounded-2xl p-5 text-center relative group hover:bg-white/[.02] transition-all duration-500">
          <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-7 h-7 rounded-full bg-gradient-to-br from-purple-500 to-pink-600 text-[10px] font-bold flex items-center justify-center shadow-lg shadow-pink-500/20">3</div>
          <div class="w-12 h-12 rounded-xl bg-pink-500/[.07] flex items-center justify-center mx-auto mb-3 group-hover:scale-110 transition-transform duration-400"><i class="fas fa-paper-plane text-pink-400"></i></div>
          <h3 class="font-bold text-sm mb-1">Request</h3>
          <p class="text-[11px] text-neutral-500 leading-relaxed">Send your ride details</p>
        </div>
        <div class="rv d4 gl rounded-2xl p-5 text-center relative group hover:bg-white/[.02] transition-all duration-500">
          <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-7 h-7 rounded-full bg-gradient-to-br from-pink-500 to-red-500 text-[10px] font-bold flex items-center justify-center shadow-lg shadow-red-500/20">4</div>
          <div class="w-12 h-12 rounded-xl bg-red-500/[.07] flex items-center justify-center mx-auto mb-3 group-hover:scale-110 transition-transform duration-400"><i class="fas fa-car-side text-red-400"></i></div>
          <h3 class="font-bold text-sm mb-1">Ride</h3>
          <p class="text-[11px] text-neutral-500 leading-relaxed">Driver arrives at door</p>
        </div>
      </div>
    </div>
  </section>

  <div class="divider max-w-6xl mx-auto"></div>

  <!-- Credits -->
  <section class="py-24 md:py-32 relative overflow-hidden">
    <div class="blob absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[450px] h-[450px] bg-blue-500/[.03] blur-[100px]" style="animation-delay:-3s"></div>
    <svg class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[480px] h-[480px] opacity-[.03]" style="animation:spin 35s linear infinite"><circle cx="240" cy="240" r="220" fill="none" stroke="#3B82F6" stroke-width=".5" stroke-dasharray="5 10"/></svg>
    <div class="max-w-6xl mx-auto px-5 relative z-10">
      <div class="text-center mb-14">
        <p class="rv text-[10px] font-bold uppercase tracking-[.25em] text-blue-400 mb-3">The Creator</p>
        <h2 class="rv d1 text-3xl md:text-4xl font-black tracking-tight">Built With <span class="gt-shimmer">Passion</span></h2>
      </div>
      <div class="rv d2 max-w-xl mx-auto">
        <div class="gl-s rounded-3xl p-7 md:p-10 relative overflow-hidden" style="border:1.5px solid rgba(59,130,246,.12);background-size:200% 200%;animation:borderRun 6s ease infinite,background 6s ease infinite;background-image:linear-gradient(135deg,rgba(12,12,12,.88),rgba(20,20,40,.88),rgba(12,12,12,.88))">
          <div class="absolute top-0 left-0 w-20 h-20 border-t-2 border-l-2 border-blue-500/15 rounded-tl-3xl"></div>
          <div class="absolute bottom-0 right-0 w-20 h-20 border-b-2 border-r-2 border-blue-500/15 rounded-br-3xl"></div>
          <div class="absolute top-3 right-4 opacity-[.06]"><i class="fas fa-quote-right text-5xl text-blue-400"></i></div>
          <div class="flex flex-col md:flex-row items-center gap-7">
            <div class="cp w-44 h-52 md:w-52 md:h-60 flex-shrink-0 fy">
              <img src="https://z-cdn-media.chatglm.cn/files/625443de-3cea-4316-9edb-29d097f6ca0f.png?auth_key=1875055532-3d77bea0862f43d38c73bb9a6eb44ca7-0-503b5f4f42bd98bb42d7e3b1d12623c0" class="w-full h-full object-cover" alt="Rudra Pratap Rai">
            </div>
            <div class="text-center md:text-left flex-1">
              <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-blue-500/[.06] text-blue-400 text-[9px] font-bold uppercase tracking-[.2em] mb-4 border border-blue-500/10"><i class="fas fa-crown text-yellow-400 text-[8px]"></i> Founder & Developer</div>
              <h3 class="text-2xl md:text-3xl font-black mb-1">Rudra Pratap Rai</h3>
              <p class="text-blue-400 text-sm font-medium mb-4">Full Stack Developer & Designer</p>
              <p class="text-neutral-400 text-[13px] leading-relaxed mb-5">The sole creator of RideLocal — from concept to code. Every pixel, animation, and feature crafted with dedication.</p>
              <div class="grid grid-cols-3 gap-2 mb-5">
                <div class="text-center py-2.5 rounded-xl bg-white/[.02] border border-white/[.04] hover:border-blue-500/15 transition-all duration-300"><i class="fas fa-code text-blue-400 mb-0.5"></i><p class="text-[9px] text-neutral-500">100% Code</p></div>
                <div class="text-center py-2.5 rounded-xl bg-white/[.02] border border-white/[.04] hover:border-purple-500/15 transition-all duration-300"><i class="fas fa-palette text-purple-400 mb-0.5"></i><p class="text-[9px] text-neutral-500">Full Design</p></div>
                <div class="text-center py-2.5 rounded-xl bg-white/[.02] border border-white/[.04] hover:border-red-500/15 transition-all duration-300"><i class="fas fa-heart text-red-400 mb-0.5"></i><p class="text-[9px] text-neutral-500">With Love</p></div>
              </div>
            </div>
          </div>
          <div class="mt-7 pt-5 border-t border-white/[.04] text-center">
            <p class="text-[11px] text-neutral-500 leading-relaxed"><span class="text-neutral-300 font-medium">Full Credit & Copyright</span> — This entire website is exclusively created by <span class="text-blue-400 font-semibold">Rudra Pratap Rai</span>. All rights reserved.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <footer class="border-t border-white/[.03] py-8"><div class="max-w-6xl mx-auto px-5 text-center"><p class="text-[10px] text-neutral-600">© 2025 RideLocal · Created by <span class="text-blue-400/50">Rudra Pratap Rai</span></p></div></footer>
</div>

<!-- ===== CUSTOMER PAGE ===== -->
<div id="pg-cust" class="pg">
  <div class="pt-20 pb-28 min-h-screen">
    <div class="max-w-6xl mx-auto px-5">
      <div class="text-center mb-8">
        <button onclick="go('home')" class="text-[11px] text-neutral-500 hover:text-white mb-3 inline-flex items-center gap-1 transition-all duration-300"><i class="fas fa-arrow-left text-[9px]"></i> Home</button>
        <h1 class="text-2xl md:text-3xl font-black tracking-tight mb-1">Find Your <span class="gt">Driver</span></h1>
        <p class="text-neutral-500 text-[13px]">Browse, check photos, compare, request</p>
      </div>
      <div class="max-w-xl mx-auto mb-7">
        <div class="gl rounded-xl p-1 flex items-center gap-1.5 focus-within:border-blue-500/15 transition-all duration-300">
          <div class="flex-1 flex items-center gap-2.5 px-3.5"><i class="fas fa-search text-neutral-600 text-sm"></i><input type="text" id="cSearch" oninput="doSearch()" placeholder="Name, car, city, or plate..." class="w-full bg-transparent py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none"></div>
          <button onclick="doSearch()" class="bp px-5 py-2.5 rounded-lg text-sm font-medium"><span>Search</span></button>
        </div>
      </div>
      <div class="flex flex-wrap items-center justify-center gap-1.5 mb-8">
        <button onclick="filt('all')" class="fb on px-3.5 py-1.5 rounded-lg text-[11px] font-medium gl transition-all duration-300" data-f="all">All</button>
        <button onclick="filt('sedan')" class="fb px-3.5 py-1.5 rounded-lg text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-f="sedan">Sedan</button>
        <button onclick="filt('suv')" class="fb px-3.5 py-1.5 rounded-lg text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-f="suv">SUV</button>
        <button onclick="filt('hatchback')" class="fb px-3.5 py-1.5 rounded-lg text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-f="hatchback">Hatchback</button>
        <button onclick="filt('luxury')" class="fb px-3.5 py-1.5 rounded-lg text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-f="luxury">Luxury</button>
        <select id="cSort" onchange="doSearch()" class="bg-white/[.02] border border-white/[.05] rounded-lg px-2.5 py-1.5 text-[10px] text-neutral-400 focus:outline-none ml-1"><option value="any">Sort: Any</option><option value="lo">Price: Low</option><option value="hi">Price: High</option></select>
      </div>
      <div id="cGrid" class="grid md:grid-cols-2 lg:grid-cols-3 gap-5"></div>
      <div id="cNone" class="text-center py-16" style="display:none"><i class="fas fa-search text-4xl text-neutral-800 mb-3 block"></i><p class="text-neutral-600 text-sm">No drivers found</p></div>
    </div>
  </div>
</div>

<!-- ===== DRIVER PAGE ===== -->
<div id="pg-driv" class="pg">
  <div class="pt-20 pb-28 min-h-screen">
    <div class="max-w-6xl mx-auto px-5">
      <div class="text-center mb-7">
        <button onclick="go('home')" class="text-[11px] text-neutral-500 hover:text-white mb-3 inline-flex items-center gap-1 transition-all duration-300"><i class="fas fa-arrow-left text-[9px]"></i> Home</button>
        <h1 class="text-2xl md:text-3xl font-black tracking-tight mb-1">Driver <span class="gt">Portal</span></h1>
        <p class="text-neutral-500 text-[13px]">Register, upload photos, manage requests</p>
      </div>
      <div class="flex items-center justify-center gap-1.5 mb-8">
        <button onclick="dTab('reg')" class="tb on px-4 py-2 rounded-xl text-[11px] font-medium gl transition-all duration-300" data-t="reg"><i class="fas fa-user-plus mr-1"></i>Register</button>
        <button onclick="dTab('prof')" class="tb px-4 py-2 rounded-xl text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-t="prof"><i class="fas fa-id-card mr-1"></i>Profile</button>
        <button onclick="dTab('req')" class="tb px-4 py-2 rounded-xl text-[11px] font-medium gl text-neutral-400 transition-all duration-300" data-t="req"><i class="fas fa-inbox mr-1"></i>Requests <span id="dRB" class="ml-0.5 px-1 py-0.5 rounded-full bg-gradient-to-r from-red-500 to-orange-500 text-white text-[8px] font-bold" style="display:none">0</span></button>
      </div>

      <!-- Register -->
      <div id="dt-reg" class="dt">
        <div class="max-w-2xl mx-auto">
          <div class="gl-s rounded-2xl p-6 md:p-8 relative overflow-hidden">
            <div class="absolute top-0 right-0 w-32 h-32 bg-green-500/[.02] rounded-full blur-[50px]"></div>
            <h2 class="text-lg font-bold mb-6 relative z-10 flex items-center gap-2"><i class="fas fa-camera text-green-400"></i> Registration with Car Photos</h2>
            <form id="dForm" onsubmit="submitDr(event)" class="relative z-10 space-y-4">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Name *</label><input type="text" id="dN" required placeholder="Full name" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Phone *</label><input type="tel" id="dP" required placeholder="+91 XXXXX XXXXX" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              </div>
              <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">City *</label><input type="text" id="dC" required placeholder="Lucknow, Gomti Nagar" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              <div class="divider my-1"></div>
              <p class="text-[9px] font-bold text-neutral-500 uppercase tracking-[.2em]"><i class="fas fa-car mr-1 text-blue-400/60"></i>Car Info</p>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Model *</label><input type="text" id="dM" required placeholder="Honda City" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Year *</label><input type="number" id="dY" required placeholder="2022" min="2000" max="2025" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              </div>
              <div class="grid grid-cols-3 gap-3">
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Type *</label><select id="dT" required class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500/30 transition-all appearance-none" style="background-image:url('data:image/svg+xml;charset=UTF-8,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%2210%22 height=%2210%22 viewBox=%220 0 10 10%22%3E%3Cpath fill=%22%23737373%22 d=%22M5 7L1 3h8z%22/%3E%3C/svg%3E');background-repeat:no-repeat;background-position:right 10px center"><option value="" class="bg-neutral-900">Type</option><option value="hatchback" class="bg-neutral-900">Hatchback</option><option value="sedan" class="bg-neutral-900">Sedan</option><option value="suv" class="bg-neutral-900">SUV</option><option value="luxury" class="bg-neutral-900">Luxury</option></select></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Color *</label><input type="text" id="dCo" required placeholder="White" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Plate *</label><input type="text" id="dPl" required placeholder="UP-32-XX-XXXX" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              </div>
              <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Experience *</label><input type="text" id="dE" required placeholder="5 years" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              <div class="divider my-1"></div>
              <p class="text-[9px] font-bold text-neutral-500 uppercase tracking-[.2em]"><i class="fas fa-rupee-sign mr-1 text-green-400/60"></i>Pricing</p>
              <div class="grid grid-cols-3 gap-3">
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Per Km ₹ *</label><input type="number" id="dKm" required placeholder="8" min="1" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Base ₹ *</label><input type="number" id="dBs" required placeholder="50" min="0" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
                <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Min ₹ *</label><input type="number" id="dMn" required placeholder="150" min="0" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all duration-300"></div>
              </div>
              <div class="divider my-1"></div>
              <p class="text-[9px] font-bold text-neutral-500 uppercase tracking-[.2em]"><i class="fas fa-camera mr-1 text-blue-400/60"></i>Photos (tap to capture)</p>
              <div id="camGrid" class="grid grid-cols-2 sm:grid-cols-4 gap-3"></div>
              <button type="submit" class="bgo w-full py-3.5 rounded-2xl text-sm font-bold mt-2"><i class="fas fa-check-circle mr-1"></i> Register as Driver</button>
            </form>
          </div>
        </div>
      </div>

      <!-- Profile -->
      <div id="dt-prof" class="dt" style="display:none"><div class="max-w-2xl mx-auto"><div id="dProf" class="gl-s rounded-2xl p-7"><p class="text-neutral-600 text-sm text-center py-10"><i class="fas fa-user-slash text-2xl block mb-2"></i>Register first</p></div></div></div>

      <!-- Requests -->
      <div id="dt-req" class="dt" style="display:none"><div class="max-w-2xl mx-auto"><div id="dReqs"><p class="text-neutral-600 text-sm text-center py-10"><i class="fas fa-inbox text-2xl block mb-2"></i>No requests yet</p></div></div></div>
    </div>
  </div>
</div>

<!-- MODALS -->
<div id="mReq" class="mo" onclick="if(event.target===this)clM('mReq')">
  <div class="mc gl-s rounded-2xl p-7 w-full max-w-md mx-4">
    <div class="flex items-center justify-between mb-5">
      <h3 class="text-base font-bold"><i class="fas fa-paper-plane text-blue-400 mr-1.5"></i>Send Request</h3>
      <button onclick="clM('mReq')" class="w-7 h-7 rounded-lg gl flex items-center justify-center text-neutral-500 hover:text-white hover:rotate-90 transition-all duration-300"><i class="fas fa-times text-xs"></i></button>
    </div>
    <div id="mReqInfo" class="flex items-center gap-3 mb-5 p-2.5 rounded-xl bg-white/[.02] border border-white/[.04]"></div>
    <form onsubmit="sendReq(event)"><input type="hidden" id="rDid">
      <div class="space-y-3">
        <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Your Name *</label><input type="text" id="rN" required placeholder="Name" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all"></div>
        <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Phone *</label><input type="tel" id="rPh" required placeholder="+91 XXXXX XXXXX" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all"></div>
        <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Pickup *</label><div class="relative"><i class="fas fa-circle text-green-400 text-[5px] absolute left-3.5 top-1/2 -translate-y-1/2"></i><input type="text" id="rPu" required placeholder="From where?" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl pl-7 pr-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all"></div></div>
        <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Drop *</label><div class="relative"><i class="fas fa-map-marker-alt text-red-400 text-[7px] absolute left-3.5 top-1/2 -translate-y-1/2"></i><input type="text" id="rDr" required placeholder="To where?" class="w-full bg-white/[.02] border border-white/[.05] rounded-xl pl-7 pr-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all"></div></div>
        <div><label class="text-[10px] font-semibold text-neutral-400 mb-1 block uppercase tracking-wider">Message</label><textarea id="rMsg" rows="2" placeholder="Special requests..." class="w-full bg-white/[.02] border border-white/[.05] rounded-xl px-3.5 py-2.5 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-blue-500/30 transition-all resize-none"></textarea></div>
        <button type="submit" class="bp w-full py-3 rounded-2xl text-sm font-semibold"><span class="flex items-center justify-center gap-2"><i class="fas fa-paper-plane"></i>Send Request</span></button>
      </div>
    </form>
  </div>
</div>

<div id="mView" class="mo" onclick="if(event.target===this)clM('mView')">
  <div class="mc gl-s rounded-2xl w-full max-w-lg mx-4 overflow-hidden max-h-[90vh] overflow-y-auto"><div id="mViewC"></div></div>
</div>

<div id="mCont" class="mo" onclick="if(event.target===this)clM('mCont')">
  <div class="mc gl-s rounded-2xl p-7 w-full max-w-sm mx-4">
    <div class="flex items-center justify-between mb-5">
      <h3 class="text-base font-bold"><i class="fas fa-phone-alt text-green-400 mr-1.5"></i>Contact</h3>
      <button onclick="clM('mCont')" class="w-7 h-7 rounded-lg gl flex items-center justify-center text-neutral-500 hover:text-white hover:rotate-90 transition-all duration-300"><i class="fas fa-times text-xs"></i></button>
    </div>
    <div id="mContC"></div>
  </div>
</div>

<div id="toasts"></div>
<video id="camVid" style="display:none" autoplay playsinline></video>

<script>
// ===== SAFE HTML =====
function esc(s){if(!s)return'';const d=document.createElement('div');d.textContent=s;return d.innerHTML}

// ===== DATA =====
let notifs=[],regDr=[],reqs=[],photos={};
const CAMS=[{k:'front',l:'Front View *',ic:'fa-car',cap:'environment'},{k:'side',l:'Side View *',ic:'fa-car-side',cap:'environment'},{k:'interior',l:'Interior',ic:'fa-couch',cap:'environment'},{k:'selfie',l:'Your Photo *',ic:'fa-user-circle',cap:'user'}];
const SD=[
  {id:'d1',name:'Rajesh Kumar',phone:'+91 98765 43210',city:'Lucknow, Gomti Nagar',model:'Honda City',year:'2022',type:'sedan',color:'White',plate:'UP-32-AB-1234',exp:'5 years',km:8,base:50,min:150,trips:2340,rate:4.9,photo:'https://picsum.photos/seed/driver1face/200/200.jpg',cp:['https://picsum.photos/seed/sedan1/600/400.jpg','https://picsum.photos/seed/sedan1s/600/400.jpg','https://picsum.photos/seed/sedan1i/600/400.jpg']},
  {id:'d2',name:'Amit Singh',phone:'+91 87654 32109',city:'Lucknow, Hazratganj',model:'Hyundai Creta',year:'2023',type:'suv',color:'Black',plate:'UP-32-CD-5678',exp:'8 years',km:12,base:80,min:200,trips:5120,rate:4.8,photo:'https://picsum.photos/seed/driver2face/200/200.jpg',cp:['https://picsum.photos/seed/suvcar2/600/400.jpg','https://picsum.photos/seed/suv2s/600/400.jpg','https://picsum.photos/seed/suv2i/600/400.jpg']},
  {id:'d3',name:'Vikram Yadav',phone:'+91 76543 21098',city:'Lucknow, Aliganj',model:'Maruti Swift',year:'2021',type:'hatchback',color:'Red',plate:'UP-32-EF-9012',exp:'3 years',km:6,base:30,min:100,trips:1890,rate:4.7,photo:'https://picsum.photos/seed/driver3face/200/200.jpg',cp:['https://picsum.photos/seed/hatch3/600/400.jpg','https://picsum.photos/seed/hat3s/600/400.jpg','https://picsum.photos/seed/hat3i/600/400.jpg']},
  {id:'d4',name:'Suresh Verma',phone:'+91 65432 10987',city:'Lucknow, Indira Nagar',model:'Toyota Fortuner',year:'2024',type:'luxury',color:'Pearl White',plate:'UP-32-GH-3456',exp:'12 years',km:18,base:150,min:400,trips:8450,rate:5.0,photo:'https://picsum.photos/seed/driver4face/200/200.jpg',cp:['https://picsum.photos/seed/luxcar4/600/400.jpg','https://picsum.photos/seed/lux4s/600/400.jpg','https://picsum.photos/seed/lux4i/600/400.jpg']},
  {id:'d5',name:'Pradeep Mishra',phone:'+91 54321 09876',city:'Lucknow, Kanpur Road',model:'Hyundai Verna',year:'2023',type:'sedan',color:'Grey',plate:'UP-32-IJ-7890',exp:'6 years',km:9,base:60,min:180,trips:3780,rate:4.8,photo:'https://picsum.photos/seed/driver5face/200/200.jpg',cp:['https://picsum.photos/seed/sedan5/600/400.jpg','https://picsum.photos/seed/sed5s/600/400.jpg','https://picsum.photos/seed/sed5i/600/400.jpg']},
  {id:'d6',name:'Manoj Tiwari',phone:'+91 43210 98765',city:'Lucknow, Aminabad',model:'Wagon R',year:'2020',type:'hatchback',color:'Blue',plate:'UP-32-KL-2345',exp:'2 years',km:5,base:25,min:80,trips:980,rate:4.6,photo:'https://picsum.photos/seed/driver6face/200/200.jpg',cp:['https://picsum.photos/seed/hat6/600/400.jpg','https://picsum.photos/seed/hat6s/600/400.jpg','https://picsum.photos/seed/hat6i/600/400.jpg']}
];
function load(){try{const a=localStorage.getItem('rl_d');if(a)regDr=JSON.parse(a);const b=localStorage.getItem('rl_r');if(b)reqs=JSON.parse(b)}catch(e){}}
function save(){try{localStorage.setItem('rl_d',JSON.stringify(regDr));localStorage.setItem('rl_r',JSON.stringify(reqs))}catch(e){}}
load();
function allDr(){return[...SD,...regDr]}

// ===== CURSOR =====
const cD=document.getElementById('cDot'),cR=document.getElementById('cRing');
let mx=0,my=0,rx=0,ry=0;
if(window.matchMedia('(pointer:fine)').matches){
  document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cD.style.left=mx-3+'px';cD.style.top=my-3+'px'});
  !function loop(){rx+=(mx-rx)*.15;ry+=(my-ry)*.15;cR.style.left=rx+'px';cR.style.top=ry+'px';requestAnimationFrame(loop)}();
  document.addEventListener('mouseover',e=>{if(e.target.closest('a,button,input,select,textarea,.cam'))cR.classList.add('hover')});
  document.addEventListener('mouseout',e=>{if(e.target.closest('a,button,input,select,textarea,.cam'))cR.classList.remove('hover')});
}else{cD.style.display='none';cR.style.display='none'}

// ===== PARTICLES =====
!function(){const c=document.getElementById('ptcl');for(let i=0;i<18;i++){const p=document.createElement('div');p.className='particle';p.style.cssText=`position:absolute;border-radius:50%;pointer-events:none;width:${Math.random()*2+.5}px;height:${Math.random()*2+.5}px;left:${Math.random()*100}%;bottom:-10px;background:${Math.random()>.5?'rgba(59,130,246,.25)':'rgba(168,85,247,.18)'};animation:floatUp ${Math.random()*18+12}s linear ${Math.random()*10}s infinite`;c.appendChild(p)}}();

// ===== SCROLL REVEAL =====
const rvObs=new IntersectionObserver(es=>{es.forEach(e=>{if(e.isIntersecting)e.target.classList.add('on')})},{threshold:.06,rootMargin:'0px 0px -30px 0px'});
function rvInit(){document.querySelectorAll('.rv,.rv-l,.rv-r,.rv-s').forEach(el=>rvObs.observe(el))}
rvInit();

// ===== COUNTERS =====
let ctrDone=false;
const ctrObs=new IntersectionObserver(es=>{es.forEach(e=>{if(e.isIntersecting&&!ctrDone){ctrDone=true;document.querySelectorAll('.ctr').forEach(c=>{const t=parseFloat(c.dataset.t),dc=t%1!==0,dur=2000,st=performance.now();!function u(n){const p=Math.min((n-st)/dur,1),v=1-Math.pow(1-p,4);c.textContent=dc?(v*t).toFixed(1):Math.floor(v*t).toLocaleString();p<1&&requestAnimationFrame(u)}(st)});ctrObs.disconnect()}})},{threshold:.4});
document.querySelectorAll('.ctr').forEach(c=>ctrObs.observe(c));

// ===== NAV =====
window.addEventListener('scroll',()=>document.getElementById('nav').classList.toggle('scrolled',scrollY>30),{passive:true});

// ===== MOBILE =====
function togMM(){document.getElementById('mMenu').classList.toggle('on')}
document.addEventListener('click',e=>{if(!e.target.closest('#mMenu')&&!e.target.closest('button[onclick*="togMM"]')&&document.getElementById('mMenu').classList.contains('on'))togMM()});

// ===== MODALS =====
function opM(id){document.getElementById(id).classList.add('on');document.body.style.overflow='hidden'}
function clM(id){document.getElementById(id).classList.remove('on');document.body.style.overflow=''}

// ===== TOAST =====
function toast(msg,type='info'){const c=document.getElementById('toasts'),t=document.createElement('div');const cl={success:'border-green-500/15 bg-green-500/[.06]',error:'border-red-500/15 bg-red-500/[.06]',info:'border-blue-500/15 bg-blue-500/[.06]'};const ic={success:'fa-check-circle text-green-400',error:'fa-exclamation-circle text-red-400',info:'fa-info-circle text-blue-400'};t.className='toast gl rounded-2xl '+cl[type];t.innerHTML='<div class="flex items-center gap-2.5"><i class="fas '+ic[type]+' text-sm"></i><span class="text-[13px]">'+esc(msg)+'</span></div>';c.appendChild(t);setTimeout(()=>{t.classList.add('out');setTimeout(()=>t.remove(),350)},4000)}

// ===== NOTIFICATIONS =====
function addN(title,body,type='info'){notifs.unshift({id:Date.now(),title,body,type,time:new Date().toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'}),read:false});updN()}
function updN(){const b=document.getElementById('nBadge'),u=notifs.filter(n=>!n.read).length;if(u>0){b.style.display='flex';b.textContent=u}else b.style.display='none';const l=document.getElementById('nList');if(!notifs.length){l.innerHTML='<p class="text-xs text-neutral-600 text-center py-8"><i class="fas fa-bell-slash text-lg block mb-2"></i>Nothing yet</p>';return}l.innerHTML=notifs.slice(0,10).map((n,i)=>'<div class="p-2.5 rounded-xl mb-0.5 '+(n.read?'opacity-30':'')+' hover:bg-white/[.02] transition-all duration-300" style="animation:notifIn .35s cubic-bezier(.16,1,.3,1) '+(i*.04)+'s both"><div class="flex items-start gap-2.5"><div class="w-7 h-7 rounded-lg '+(n.type==='success'?'bg-green-500/10':'bg-blue-500/10')+' flex items-center justify-center flex-shrink-0"><i class="fas '+(n.type==='success'?'fa-check text-green-400':'fa-bell text-blue-400')+' text-[9px]"></i></div><div class="flex-1 min-w-0"><p class="text-[11px] font-semibold">'+esc(n.title)+'</p><p class="text-[10px] text-neutral-500 truncate">'+esc(n.body)+'</p><p class="text-[8px] text-neutral-600 mt-0.5">'+esc(n.time)+'</p></div></div></div>').join('')}
function togNotif(){const p=document.getElementById('nPanel');p.style.display=p.style.display==='none'?'block':'none';notifs.forEach(n=>n.read=true);setTimeout(updN,400)}
function clrNotif(){notifs=[];updN()}
document.addEventListener('click',e=>{if(!e.target.closest('#nPanel')&&!e.target.closest('#nBell'))document.getElementById('nPanel').style.display='none'});

// ===== PAGE NAV =====
function go(p){document.querySelectorAll('.pg').forEach(x=>x.classList.remove('on'));document.getElementById('pg-'+p).classList.add('on');window.scrollTo({top:0,behavior:'smooth'});document.getElementById('nPanel').style.display='none';if(p==='cust')renderCust();if(p==='driv'){updBadge();const s=localStorage.getItem('rl_mp');if(s)renderProf(JSON.parse(s))}}

// ===== CAMERA GRID (build without nested template literals) =====
function buildCams(){const g=document.getElementById('camGrid');g.innerHTML='';CAMS.forEach(c=>{const d=document.createElement('div');d.innerHTML='<label class="text-[9px] font-semibold text-neutral-500 mb-1.5 block text-center uppercase tracking-wider">'+esc(c.l)+'</label><div class="cam relative bg-white/[.01] rounded-xl h-32 flex flex-col items-center justify-center cursor-pointer group" id="cam-'+c.k+'" onclick="openCam(\''+c.k+'\')"><div id="cam-'+c.k+'-ph" class="text-center transition-opacity duration-300"><i class="fas '+c.ic+' text-xl text-neutral-700 group-hover:text-blue-400 transition-colors duration-300 mb-1 block"></i><p class="text-[8px] text-neutral-700 group-hover:text-neutral-400 transition-colors">Tap to capture</p></div><img id="cam-'+c.k+'-pv" class="absolute inset-0 w-full h-full object-cover rounded-xl" style="display:none" alt=""><input type="file" id="cam-'+c.k+'-f" accept="image/*" capture="'+c.cap+'" onchange="upCam(\''+c.k+'\',event)" class="hidden"><button type="button" id="cam-'+c.k+'-rt" onclick="event.stopPropagation();retCam(\''+c.k+'\')" class="absolute bottom-1.5 right-1.5 w-6 h-6 rounded-lg bg-red-500/80 hover:bg-red-500 flex items-center justify-center text-white text-[9px] transition-all duration-200 hover:scale-110" style="display:none"><i class="fas fa-redo"></i></button></div>';g.appendChild(d)})}
buildCams();

function openCam(k){document.getElementById('cam-'+k+'-f').click()}
function upCam(k,e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=function(ev){photos[k]=ev.target.result;const pv=document.getElementById('cam-'+k+'-pv'),ph=document.getElementById('cam-'+k+'-ph'),rt=document.getElementById('cam-'+k+'-rt'),cm=document.getElementById('cam-'+k);pv.src=ev.target.result;pv.style.display='block';ph.style.display='none';rt.style.display='flex';cm.classList.add('ok');const fl=document.createElement('div');fl.className='cam-flash';cm.appendChild(fl);setTimeout(()=>fl.remove(),250)};r.readAsDataURL(f)}
function retCam(k){photos[k]=null;document.getElementById('cam-'+k+'-pv').style.display='none';document.getElementById('cam-'+k+'-ph').style.display='block';document.getElementById('cam-'+k+'-rt').style.display='none';document.getElementById('cam-'+k).classList.remove('ok');document.getElementById('cam-'+k+'-f').value=''}

// ===== DRIVER REG =====
function submitDr(e){e.preventDefault();if(!photos.front||!photos.side||!photos.selfie){toast('Capture Front, Side & Your Photo first','error');return}const d={id:'d'+Date.now(),name:document.getElementById('dN').value,phone:document.getElementById('dP').value,city:document.getElementById('dC').value,model:document.getElementById('dM').value,year:document.getElementById('dY').value,type:document.getElementById('dT').value,color:document.getElementById('dCo').value,plate:document.getElementById('dPl').value,exp:document.getElementById('dE').value,km:parseInt(document.getElementById('dKm').value),base:parseInt(document.getElementById('dBs').value),min:parseInt(document.getElementById('dMn').value),trips:0,rate:0,photo:photos.selfie,cp:[photos.front,photos.side,photos.interior||photos.front]};regDr.push(d);save();localStorage.setItem('rl_mp',JSON.stringify(d));document.getElementById('dForm').reset();photos={};CAMS.forEach(c=>retCam(c.k));toast('Registered! Profile is live.','success');addN('Registered','Your profile is now visible to customers.','success');renderProf(d);dTab('prof')}

// ===== DRIVER PROFILE =====
function renderProf(d){if(!d){document.getElementById('dProf').innerHTML='<p class="text-neutral-600 text-sm text-center py-10"><i class="fas fa-user-slash text-xl block mb-2"></i>Not registered</p>';return}document.getElementById('dProf').innerHTML='<div class="flex items-center gap-2 mb-6"><span class="st-on"></span><span class="text-[11px] text-green-400 font-medium">Online — Visible</span></div><div class="flex flex-col sm:flex-row items-center gap-5 mb-6"><img src="'+esc(d.photo)+'" class="w-20 h-20 rounded-2xl object-cover ring-2 ring-green-500/15" alt=""><div class="text-center sm:text-left"><h3 class="text-xl font-black">'+esc(d.name)+'</h3><p class="text-[11px] text-neutral-500">'+esc(d.phone)+' · '+esc(d.city)+'</p><p class="text-[11px] text-neutral-500">'+esc(d.exp)+' · '+esc(d.plate)+'</p></div></div><div class="grid grid-cols-2 sm:grid-cols-4 gap-2 mb-6">'+[{l:'Car',v:d.model},{l:'Rate',v:'₹'+d.km+'/km'},{l:'Base',v:'₹'+d.base},{l:'Trips',v:d.trips}].map(x=>'<div class="text-center py-2.5 rounded-xl bg-white/[.02] border border-white/[.03]"><p class="text-[9px] text-neutral-500 uppercase tracking-wider">'+x.l+'</p><p class="text-sm font-bold mt-0.5">'+esc(x.v)+'</p></div>').join('')+'</div><p class="text-[9px] font-bold text-neutral-500 uppercase tracking-[.2em] mb-2"><i class="fas fa-images mr-1 text-blue-400/60"></i>Photos</p><div class="grid grid-cols-3 gap-2 mb-6">'+d.cp.map((p,i)=>'<div class="rounded-xl overflow-hidden h-24 border border-white/[.03]"><img src="'+esc(p)+'" class="w-full h-full object-cover hover:scale-110 transition-transform duration-500" alt="Car '+(i+1)+'"></div>').join('')+'</div><div class="flex gap-2"><button onclick="dTab(\'req\')" class="bp flex-1 py-2.5 rounded-xl text-[11px] font-medium"><span class="flex items-center justify-center gap-1.5"><i class="fas fa-inbox"></i>Requests</span></button><button onclick="delProf()" class="brd px-4 py-2.5 rounded-xl text-[11px] font-medium"><i class="fas fa-trash"></i></button></div>'}
function delProf(){if(!confirm('Delete profile?'))return;const s=localStorage.getItem('rl_mp');if(s){const d=JSON.parse(s);regDr=regDr.filter(x=>x.id!==d.id);save()}localStorage.removeItem('rl_mp');document.getElementById('dProf').innerHTML='<p class="text-neutral-600 text-sm text-center py-10"><i class="fas fa-user-slash text-xl block mb-2"></i>Deleted</p>';toast('Profile deleted','info')}

// ===== DRIVER TABS =====
function dTab(t){document.querySelectorAll('.dt').forEach(x=>x.style.display='none');document.getElementById('dt-'+t).style.display='block';document.querySelectorAll('.tb').forEach(b=>{b.classList.remove('on');b.classList.add('text-neutral-400')});const btn=document.querySelector('.tb[data-t="'+t+'"]');if(btn){btn.classList.add('on');btn.classList.remove('text-neutral-400')}if(t==='prof'){const s=localStorage.getItem('rl_mp');if(s)renderProf(JSON.parse(s))}if(t==='req')renderReqs()}

// ===== DRIVER REQUESTS =====
function updBadge(){const s=localStorage.getItem('rl_mp');if(!s){document.getElementById('dRB').style.display='none';return}const d=JSON.parse(s),p=reqs.filter(r=>r.did===d.id&&r.st==='pending').length,b=document.getElementById('dRB');if(p>0){b.style.display='inline';b.textContent=p}else b.style.display='none'}
function renderReqs(){const s=localStorage.getItem('rl_mp'),c=document.getElementById('dReqs');if(!s){c.innerHTML='<p class="text-neutral-600 text-sm text-center py-10">Register first</p>';return}const d=JSON.parse(s),mr=reqs.filter(r=>r.did===d.id);if(!mr.length){c.innerHTML='<p class="text-neutral-600 text-sm text-center py-10"><i class="fas fa-inbox text-xl block mb-2"></i>No requests</p>';return}c.innerHTML=mr.slice().reverse().map((r,i)=>{const sc=r.st==='pending'?'bg-yellow-500/10 text-yellow-400 border-yellow-500/15':r.st==='accepted'?'bg-green-500/10 text-green-400 border-green-500/15':'bg-red-500/10 text-red-400 border-red-500/15';let act='';if(r.st==='pending')act='<div class="flex gap-2 mt-3"><button onclick="hReq(\''+r.id+'\',\'accepted\',\''+esc(r.cn)+'\',\''+esc(r.cp)+'\')" class="bgo flex-1 py-2 rounded-xl text-[11px] font-medium"><i class="fas fa-check mr-1"></i>Accept</button><button onclick="hReq(\''+r.id+'\',\'rejected\',\''+esc(r.cn)+'\',\''+esc(r.cp)+'\')" class="brd flex-1 py-2 rounded-xl text-[11px] font-medium"><i class="fas fa-times mr-1"></i>Reject</button></div>';else if(r.st==='accepted')act='<button onclick="showCont(\''+esc(r.cn)+'\',\''+esc(r.cp)+'\',\'customer\')" class="bp w-full py-2 rounded-xl text-[11px] font-medium mt-3"><span><i class="fas fa-phone-alt mr-1"></i>Call '+esc(r.cn)+'</span></button>';return'<div class="rc gl rounded-xl p-4 mb-3 border border-transparent" style="animation:cardIn .4s cubic-bezier(.16,1,.3,1) '+(i*.06)+'s both"><div class="flex items-start justify-between mb-2"><div><p class="font-bold text-sm">'+esc(r.cn)+'</p><p class="text-[10px] text-neutral-500">'+esc(r.cp)+'</p></div><span class="px-2 py-0.5 rounded-full text-[9px] font-bold border '+sc+'">'+r.st.toUpperCase()+'</span></div><div class="flex items-center gap-2 text-[11px] text-neutral-400 mb-1"><i class="fas fa-circle text-green-400 text-[4px]"></i>'+esc(r.pu)+' <i class="fas fa-arrow-right text-[7px] text-neutral-600 mx-1"></i> <i class="fas fa-map-marker-alt text-red-400 text-[7px]"></i>'+esc(r.dr)+'</div>'+(r.msg?'<p class="text-[10px] text-neutral-500 italic border-l-2 border-blue-500/15 pl-2 mb-1">"'+esc(r.msg)+'"</p>':'')+'<p class="text-[8px] text-neutral-600">'+esc(r.time)+'</p>'+act+'</div>'}).join('');updBadge()}
function hReq(rid,st,cn,cp){const r=reqs.find(x=>x.id===rid);if(r)r.st=st;save();renderReqs();if(st==='accepted'){toast('Accepted! Contact '+cn,'success');addN('Accepted','Ride with '+cn+' accepted.','success');showCont(cn,cp,'customer')}else{toast('Rejected '+cn+"'s request",'info');addN('Rejected','Rejected '+cn+"'s request.",'info')}}

// ===== CUSTOMER RENDER =====
function renderCust(list){const dr=list||allDr(),g=document.getElementById('cGrid'),nr=document.getElementById('cNone');if(!dr.length){g.innerHTML='';nr.style.display='block';return}nr.style.display='none';g.innerHTML=dr.map((d,i)=>{const pc=d.km<=6?'bg-blue-500/10 text-blue-400 border-blue-500/15':d.km<=10?'bg-green-500/10 text-green-400 border-green-500/15':d.km<=15?'bg-purple-500/10 text-purple-400 border-purple-500/15':'bg-yellow-500/10 text-yellow-400 border-yellow-500/15';return'<div class="dc gl rounded-2xl overflow-hidden" data-type="'+d.type+'" style="animation:cardIn .45s cubic-bezier(.16,1,.3,1) '+(i*.06)+'s both"><div class="h-44 relative overflow-hidden cursor-pointer group" onclick="viewDr(\''+d.id+'\')"><img src="'+esc(d.cp[0])+'" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt="" loading="lazy"><div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div><div class="absolute top-2.5 left-2.5 flex items-center gap-1.5 px-2 py-0.5 rounded-full gl text-[9px] font-medium"><span class="st-on" style="width:5px;height:5px"></span>Online</div><div class="absolute top-2.5 right-2.5 px-2 py-0.5 rounded-full '+pc+' text-[9px] font-bold border">₹'+d.km+'/km</div><div class="absolute bottom-2.5 left-2.5"><p class="text-white font-bold text-sm">'+esc(d.model)+'</p><p class="text-neutral-300 text-[9px]">'+esc(d.color)+' · '+d.type[0].toUpperCase()+d.type.slice(1)+' · '+esc(d.year)+'</p></div><div class="absolute bottom-2.5 right-2.5 flex items-center gap-0.5 bg-black/40 px-1.5 py-0.5 rounded-md"><i class="fas fa-images text-white text-[7px]"></i><span class="text-[8px] text-white">'+d.cp.length+'</span></div></div><div class="p-4"><div class="flex items-start justify-between mb-3"><div class="flex items-center gap-2.5"><img src="'+esc(d.photo)+'" class="w-9 h-9 rounded-full object-cover ring-1.5 ring-blue-500/15" alt="" loading="lazy"><div><p class="font-bold text-[13px]">'+esc(d.name)+'</p><p class="text-[9px] text-neutral-500">'+esc(d.exp)+' · '+esc(d.city)+'</p></div></div><div class="flex items-center gap-0.5 text-yellow-400 text-[11px]">'+(d.rate>0?'<i class="fas fa-star"></i>'+d.rate:'<span class="text-neutral-600 text-[9px]">New</span>')+'</div></div><div class="grid grid-cols-3 gap-1.5 mb-3">'+[{l:'Trips',v:d.trips.toLocaleString()},{l:'Base',v:'₹'+d.base},{l:'Min',v:'₹'+d.min}].map(x=>'<div class="text-center py-1.5 rounded-lg bg-white/[.015] border border-white/[.03]"><p class="text-[8px] text-neutral-500">'+x.l+'</p><p class="text-[11px] font-bold">'+x.v+'</p></div>').join('')+'</div><div class="flex gap-1.5"><button onclick="openReq(\''+d.id+'\')" class="bp flex-1 py-2 rounded-xl text-[11px] font-medium"><span>Request</span></button><button onclick="viewDr(\''+d.id+'\')" class="bs w-9 h-9 rounded-xl flex items-center justify-center text-[11px]"><i class="fas fa-eye"></i></button><button onclick="showCont(\''+esc(d.name)+'\',\''+esc(d.phone)+'\',\'driver\')" class="bs w-9 h-9 rounded-xl flex items-center justify-center text-[11px]"><i class="fas fa-phone-alt"></i></button></div></div></div>'}).join('')}

// ===== SEARCH/FILTER =====
let curFilt='all';
function filt(t){curFilt=t;document.querySelectorAll('.fb').forEach(b=>{b.classList.remove('on');b.classList.add('text-neutral-400');if(b.dataset.f===t){b.classList.add('on');b.classList.remove('text-neutral-400')}});doSearch()}
function doSearch(){const q=document.getElementById('cSearch').value.toLowerCase().trim(),s=document.getElementById('cSort').value;let d=allDr();if(curFilt!=='all')d=d.filter(x=>x.type===curFilt);if(q)d=d.filter(x=>x.name.toLowerCase().includes(q)||x.model.toLowerCase().includes(q)||x.city.toLowerCase().includes(q)||x.type.includes(q)||x.plate.toLowerCase().includes(q));if(s==='lo')d.sort((a,b)=>a.km-b.km);if(s==='hi')d.sort((a,b)=>b.km-a.km);renderCust(d)}

// ===== VIEW DRIVER DETAIL =====
function viewDr(id){const d=allDr().find(x=>x.id===id);if(!d)return;document.getElementById('mViewC').innerHTML='<div class="h-52 relative overflow-hidden"><img src="'+esc(d.cp[0])+'" class="w-full h-full object-cover" alt=""><div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/25 to-transparent"></div><button onclick="clM(\'mView\')" class="absolute top-3 right-3 w-8 h-8 rounded-xl gl flex items-center justify-center text-white text-sm hover:rotate-90 transition-transform duration-300"><i class="fas fa-times"></i></button><div class="absolute bottom-4 left-4 right-4 flex items-end justify-between"><div><p class="text-white font-black text-lg">'+esc(d.model)+'</p><p class="text-neutral-300 text-[11px]">'+esc(d.color)+' · '+d.type[0].toUpperCase()+d.type.slice(1)+' · '+esc(d.year)+'</p></div><div class="px-2.5 py-1 rounded-full bg-blue-500/10 text-blue-400 text-[11px] font-bold border border-blue-500/15">₹'+d.km+'/km</div></div></div><div class="p-5"><div class="flex items-center gap-3.5 mb-5"><img src="'+esc(d.photo)+'" class="w-14 h-14 rounded-2xl object-cover ring-1.5 ring-blue-500/15" alt=""><div class="flex-1"><h3 class="font-black text-base">'+esc(d.name)+'</h3><p class="text-[11px] text-neutral-500">'+esc(d.exp)+' · '+esc(d.plate)+'</p><p class="text-[11px] text-neutral-500"><i class="fas fa-map-marker-alt mr-0.5"></i>'+esc(d.city)+'</p>'+(d.rate>0?'<div class="flex items-center gap-0.5 mt-0.5"><i class="fas fa-star text-yellow-400 text-[10px]"></i><span class="text-[10px] text-neutral-400 ml-0.5">'+d.rate+'</span></div>':'<span class="text-[10px] text-neutral-600">New driver</span>')+'</div></div><div class="grid grid-cols-4 gap-1.5 mb-5">'+[{l:'Trips',v:d.trips.toLocaleString()},{l:'Per Km',v:'₹'+d.km},{l:'Base',v:'₹'+d.base},{l:'Min',v:'₹'+d.min}].map(x=>'<div class="text-center py-2 rounded-xl bg-white/[.015] border border-white/[.03]"><p class="text-[8px] text-neutral-500 uppercase">'+x.l+'</p><p class="text-[12px] font-bold mt-0.5">'+x.v+'</p></div>').join('')+'</div><p class="text-[9px] font-bold text-neutral-500 uppercase tracking-[.2em] mb-2"><i class="fas fa-images mr-1 text-blue-400/60"></i>Photos ('+d.cp.length+')</p><div class="flex gap-1.5 overflow-x-auto pb-1.5 mb-5 -mx-0.5 px-0.5">'+d.cp.map((p,i)=>'<img src="'+esc(p)+'" class="w-24 h-16 rounded-xl object-cover flex-shrink-0 border border-white/[.03] hover:border-blue-500/25 hover:scale-105 transition-all duration-300 cursor-pointer" alt="Car '+(i+1)+'" onclick="try{this.requestFullscreen()}catch(e){}">').join('')+'</div><div class="space-y-1.5 mb-5">'+[{ic:'fa-shield-alt text-green-400',t:'Verified Driver'},{ic:'fa-id-card text-blue-400',t:'Valid License'},{ic:'fa-file-alt text-purple-400',t:'RC & Insurance'},{ic:'fa-snowflake text-cyan-400',t:'AC Available'}].map(x=>'<div class="flex items-center gap-2 text-[11px] text-neutral-400"><i class="fas '+x.ic+' w-3.5 text-center text-[10px]"></i>'+x.t+'</div>').join('')+'</div><div class="flex gap-1.5"><button onclick="clM(\'mView\');openReq(\''+d.id+'\')" class="bp flex-1 py-2.5 rounded-2xl text-sm font-semibold"><span class="flex items-center justify-center gap-1.5"><i class="fas fa-paper-plane"></i>Request</span></button><button onclick="clM(\'mView\');showCont(\''+esc(d.name)+'\',\''+esc(d.phone)+'\',\'driver\')" class="bs px-4 py-2.5 rounded-2xl text-sm font-medium"><i class="fas fa-phone-alt"></i></button></div></div>';opM('mView')}

// ===== RIDE REQUEST =====
function openReq(did){const d=allDr().find(x=>x.id===did);if(!d)return;document.getElementById('rDid').value=did;document.getElementById('mReqInfo').innerHTML='<img src="'+esc(d.photo)+'" class="w-9 h-9 rounded-full object-cover ring-1.5 ring-blue-500/15" alt=""><div class="flex-1"><p class="font-bold text-[13px]">'+esc(d.name)+'</p><p class="text-[9px] text-neutral-500">'+esc(d.model)+' · ₹'+d.km+'/km</p></div>';opM('mReq')}
function sendReq(e){e.preventDefault();const did=document.getElementById('rDid').value,d=allDr().find(x=>x.id===did),r={id:'r'+Date.now(),did:did,dn:d?d.name:'Unknown',cn:document.getElementById('rN').value,cp:document.getElementById('rPh').value,pu:document.getElementById('rPu').value,dr:document.getElementById('rDr').value,msg:document.getElementById('rMsg').value,st:'pending',time:new Date().toLocaleString()};reqs.push(r);save();clM('mReq');e.target.reset();toast('Request sent to '+r.dn+'!','success');addN('Sent','Ride to '+r.dn+': '+r.pu+' → '+r.dr,'info');setTimeout(()=>addN('Notified',r.dn+' has been notified.','info'),1500)}

// ===== CONTACT =====
function showCont(n,p,r){const l=r==='customer'?'Customer':'Driver';document.getElementById('mContC').innerHTML='<div class="text-center mb-5"><div class="w-14 h-14 rounded-2xl bg-green-500/[.06] flex items-center justify-center mx-auto mb-2 fy"><i class="fas fa-user text-green-400 text-xl"></i></div><h4 class="font-black">'+esc(n)+'</h4><p class="text-[9px] text-neutral-500 uppercase tracking-wider">'+l+'</p></div><div class="space-y-2 mb-5"><a href="tel:'+esc(p)+'" class="bgo w-full py-3 rounded-2xl text-sm font-medium flex items-center justify-center gap-2"><i class="fas fa-phone-alt"></i>Call</a><a href="https://wa.me/'+p.replace(/\D/g,'')+'" target="_blank" class="w-full py-3 rounded-2xl text-sm font-medium flex items-center justify-center gap-2" style="background:linear-gradient(135deg,#25D366,#128C7E)"><i class="fab fa-whatsapp text-lg"></i>WhatsApp</a><a href="sms:'+esc(p)+'" class="bs w-full py-3 rounded-2xl text-sm font-medium flex items-center justify-center gap-2"><i class="fas fa-comment-alt"></i>SMS</a></div><div class="p-3 rounded-xl bg-white/[.02] border border-white/[.03] text-center"><p class="text-[9px] text-neutral-500 uppercase tracking-wider mb-0.5">Phone</p><p class="text-sm font-mono font-bold text-green-400">'+esc(p)+'</p></div>';opM('mCont')}

// ===== INIT =====
renderCust();updN();
</script>
</body>
</html>
