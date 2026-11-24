# <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
<meta name="theme-color" content="#0b0508" />
<title>mumbi</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,500;0,700;1,500&family=Lora:ital,wght@0,400;0,500;1,400&family=Great+Vibes&family=Caveat:wght@500&display=swap" rel="stylesheet">
<style>
:root{
  --black:#0b0508;
  --pink:#e8a4b8;
  --rose:#c9567a;
  --parch:#efe0c2;
  --parch2:#e4d0a8;
  --choc:#3b2418;
  --burg:#7a1f33;
  --gold:#b8913f;
  --paper-noise:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='220' height='220'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 .38  0 0 0 0 .24  0 0 0 0 .1  0 0 0 .16 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
[hidden]{display:none!important}
html{scroll-behavior:smooth}
body{
  font-family:'Lora',Georgia,serif;color:var(--choc);
  background:radial-gradient(ellipse at 50% 0%,#2a0f1a 0%,#120609 45%,var(--black) 100%) fixed;
  min-height:100dvh;overflow-x:hidden;
}
#snow{position:fixed;inset:0;width:100%;height:100%;pointer-events:none;z-index:1}

/* ---------- shared paper look ---------- */
.paper{
  background-color:var(--parch);background-image:var(--paper-noise);
  box-shadow:0 18px 40px rgba(0,0,0,.55),inset 0 0 60px rgba(120,80,30,.18);
  border-radius:14px;
}
.script{font-family:'Great Vibes',cursive;font-weight:400}
.small-caps{font-size:.72rem;letter-spacing:.38em;text-transform:uppercase}

/* ---------- buttons ---------- */
.btn{
  font-family:'Playfair Display',serif;font-weight:500;letter-spacing:.3em;text-transform:uppercase;font-size:.8rem;
  color:var(--parch);background:linear-gradient(180deg,#8d2640,var(--burg));cursor:pointer;
  border:1px solid var(--gold);border-radius:999px;padding:13px 40px;
  box-shadow:0 6px 16px rgba(0,0,0,.4);transition:transform .25s,box-shadow .25s,filter .25s;
}
.btn:hover{transform:translateY(-2px);filter:brightness(1.1)}
.btn:active{transform:scale(.98)}
.btn.line{background:none;color:var(--burg);border-color:var(--burg);box-shadow:none}

/* ================= FRONT PAGE ================= */
#front{
  position:relative;z-index:2;min-height:100dvh;display:flex;align-items:center;justify-content:center;padding:28px 16px;
  transition:opacity .9s ease;
}
#front.leave{opacity:0}
.stationery{
  width:min(440px,100%);padding:38px 26px 30px;text-align:center;position:relative;
}
.stationery::before{content:"";position:absolute;inset:10px;border:1px solid rgba(184,145,63,.65);border-radius:9px;pointer-events:none}
.stationery::after{content:"";position:absolute;inset:15px;border:1px solid rgba(184,145,63,.3);border-radius:6px;pointer-events:none}
.eyebrow{color:var(--burg)}
.title{font-family:'Playfair Display',serif;font-style:italic;font-weight:500;font-size:clamp(2rem,8vw,2.7rem);margin-top:14px;color:var(--choc)}
.recipient{font-size:clamp(3.4rem,15vw,5rem);line-height:1;color:var(--rose);margin:2px 0 8px}
.intro{font-style:italic;font-size:1rem;line-height:1.6;max-width:320px;margin:0 auto}
.signature-sm{font-size:1.9rem;color:var(--burg);margin-top:16px}

/* envelope */
.env-stage{margin:34px auto 26px;width:min(290px,72vw);height:min(190px,47vw);position:relative}
.envelope{position:absolute;inset:0}
.env-back{position:absolute;inset:0;background:#d6bd92;border-radius:4px;box-shadow:0 14px 26px rgba(0,0,0,.4)}
.env-paper{position:absolute;left:7%;right:7%;top:8%;height:80%;background-color:#f6ead0;background-image:var(--paper-noise);
  border-radius:3px;z-index:1;transition:transform 1.1s cubic-bezier(.25,.8,.25,1) .55s;
  display:flex;align-items:center;justify-content:center;color:var(--burg);font-size:1.6rem}
.env-front{position:absolute;inset:0;z-index:2;pointer-events:none;border-radius:4px;
  background:
   linear-gradient(to top right,transparent 49.5%,#cbb084 50%) left/50% 100% no-repeat,
   linear-gradient(to top left,transparent 49.5%,#cbb084 50%) right/50% 100% no-repeat,
   linear-gradient(180deg,transparent 40%,#d2b88c 41%) bottom/100% 100% no-repeat;
  clip-path:polygon(0 0,50% 52%,100% 0,100% 100%,0 100%)}
.env-flap{position:absolute;left:0;right:0;top:0;height:56%;z-index:4;transform-origin:top;
  background:linear-gradient(180deg,#c8ac7c,#bd9f6c);clip-path:polygon(0 0,100% 0,50% 100%);
  transition:transform .9s ease,z-index 0s .45s;filter:drop-shadow(0 3px 3px rgba(0,0,0,.25))}
.seal{
  position:absolute;left:50%;top:51%;transform:translate(-50%,-50%);z-index:6;width:56px;height:56px;
  border-radius:48% 52% 50% 50% / 52% 48% 52% 48%;
  background:radial-gradient(circle at 35% 30%,#b8344f,#7a1630 60%,#4d0c1e);
  box-shadow:0 3px 7px rgba(0,0,0,.55),inset 0 0 0 4px rgba(0,0,0,.14),inset 0 0 0 5px rgba(255,200,210,.18);
  display:flex;align-items:center;justify-content:center;
  font-family:'Playfair Display',serif;font-weight:700;font-size:1.5rem;color:#e7c777;text-shadow:0 1px 1px rgba(0,0,0,.6);
  transition:opacity .4s;
}
.envelope.open .env-flap{transform:rotateX(180deg);z-index:0}
.envelope.open .seal{opacity:0}
.envelope.open .env-paper{transform:translateY(-52%)}

/* ================= SITE (after open) ================= */
#site{position:relative;z-index:2;opacity:0;transition:opacity .9s ease;padding-top:64px}
#site.in{opacity:1}
nav{
  position:fixed;top:0;left:0;right:0;z-index:20;display:flex;align-items:center;justify-content:space-between;gap:10px;
  padding:10px 14px;background:rgba(11,5,8,.82);backdrop-filter:blur(8px);border-bottom:1px solid rgba(184,145,63,.35);
}
nav button,nav a{
  font-family:'Playfair Display',serif;letter-spacing:.14em;font-size:.72rem;text-transform:uppercase;color:var(--pink);
  background:none;border:none;text-decoration:none;cursor:pointer;padding:6px 4px;
}
nav .links{display:flex;gap:10px;flex-wrap:wrap;justify-content:flex-end}
nav a:hover,nav button:hover{color:#fff}

section.block{padding:54px 16px;display:flex;flex-direction:column;align-items:center}
.sec-title{font-family:'Playfair Display',serif;font-style:italic;color:var(--pink);font-size:clamp(1.5rem,6vw,2rem);text-align:center;margin-bottom:6px}
.sec-sub{color:#b9a79a;font-size:.9rem;font-style:italic;text-align:center;margin-bottom:26px}

.reveal{opacity:0;transform:translateY(22px);transition:opacity 1s ease,transform 1s ease}
.reveal.visible{opacity:1;transform:none}

/* letter */
.letter{width:min(620px,100%);padding:44px 30px 36px;position:relative}
.letter::before{content:"";position:absolute;inset:10px;border:1px solid rgba(184,145,63,.45);border-radius:9px;pointer-events:none}
.letter .date{font-style:italic;font-size:.9rem;color:#7b5a42;text-align:right;margin-bottom:18px}
.letter h2{font-family:'Playfair Display',serif;font-weight:500;font-size:1.5rem;margin-bottom:16px;color:var(--burg)}
.letter p{font-size:1.06rem;line-height:1.85;margin-bottom:14px}
.letter .closing{margin-top:22px}
.sign{font-size:2.6rem;color:var(--burg);line-height:1.1;margin-top:2px}

/* cards */
.cards{display:flex;flex-direction:column;gap:22px;width:min(520px,100%)}
.card{padding:0;overflow:hidden;transition:box-shadow .3s,transform 1s ease,opacity 1s ease}
.card:nth-child(odd){transform:rotate(-.8deg)}
.card:nth-child(even){transform:rotate(.8deg)}
.card.visible:nth-child(odd){transform:rotate(-.8deg)}
.card.visible:nth-child(even){transform:rotate(.8deg)}
.card:not(.reveal):hover{box-shadow:0 22px 44px rgba(0,0,0,.6),inset 0 0 60px rgba(120,80,30,.18)}
.card-head{
  width:100%;display:flex;align-items:center;gap:14px;text-align:left;cursor:pointer;
  background:none;border:none;padding:20px 22px;color:var(--choc);font-family:inherit;
}
.card-num{font-family:'Playfair Display',serif;font-style:italic;color:var(--gold);font-size:1.7rem;min-width:30px}
.card-title{font-family:'Playfair Display',serif;font-size:1.2rem;font-weight:500}
.card-hint{display:block;font-style:italic;font-size:.82rem;color:#7b5a42;margin-top:2px}
.chev{margin-left:auto;color:var(--burg);transition:transform .4s;font-size:1.1rem}
.card.open .chev{transform:rotate(180deg)}
.card-body{display:grid;grid-template-rows:0fr;transition:grid-template-rows .6s ease}
.card.open .card-body{grid-template-rows:1fr}
.card-body>div{overflow:hidden}
.card-inner{padding:0 24px 24px;border-top:1px dashed rgba(122,31,51,.3);margin:0 22px;padding:18px 2px 22px}
.card-inner p{line-height:1.8;font-size:1.02rem;margin-bottom:10px}
.card-inner .ps{font-family:'Caveat',cursive;font-size:1.4rem;color:var(--burg)}
.mini-sign{font-size:2rem;color:var(--burg);margin-top:4px}

/* polaroid */
.polaroid{
  background:#faf5e9;padding:14px 14px 22px;width:min(320px,86vw);transform:rotate(-2.2deg);position:relative;
  box-shadow:0 20px 40px rgba(0,0,0,.6),0 0 0 1px rgba(0,0,0,.05);border-radius:3px;
}
.polaroid.visible{transform:rotate(-2.2deg)}
.polaroid::before{content:"";position:absolute;top:-14px;left:50%;width:96px;height:28px;transform:translateX(-50%) rotate(2deg);
  background:rgba(216,190,120,.55);box-shadow:0 1px 3px rgba(0,0,0,.25)}
.photo-wrap{aspect-ratio:1/1;background:#2a1a1a;position:relative;overflow:hidden}
.photo-wrap img{width:100%;height:100%;object-fit:cover;display:block;filter:sepia(.18) contrast(1.03)}
.photo-missing{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;justify-content:center;gap:8px;text-align:center;padding:16px;
  color:#d9c3a0;font-style:italic;font-size:.95rem;background:#2b1b1d}
.polaroid .cap{font-family:'Caveat',cursive;font-size:1.6rem;text-align:center;color:var(--choc);margin-top:14px;line-height:1.2}

/* final */
.final{width:min(560px,100%);padding:42px 28px 36px;text-align:center;position:relative}
.final::before{content:"";position:absolute;inset:10px;border:1px solid rgba(184,145,63,.45);border-radius:9px;pointer-events:none}
.rose{width:96px;height:auto;margin:0 auto 14px;display:block}
.final p.msg{font-style:italic;font-size:1.12rem;line-height:1.85;margin-bottom:22px}
.final .sincerely{font-size:1rem;margin-bottom:2px}
.final .name-sign{font-size:2.7rem;color:var(--burg);line-height:1.1}
.final .actions{margin-top:26px;display:flex;justify-content:center}
footer{text-align:center;color:#8c7a6d;font-size:.78rem;letter-spacing:.2em;padding:6px 0 40px;font-style:italic}

@media (prefers-reduced-motion:reduce){*{transition-duration:.01s!important;animation:none!important}html{scroll-behavior:auto}}
</style>
</head>
<body>
<canvas id="snow"></canvas>

<!-- ===================== FRONT PAGE ===================== -->
<main id="front">
  <div class="stationery paper">
    <div class="eyebrow small-caps">A Personal Letter</div>
    <h1 class="title">for her</h1>
    <div class="recipient script">Mumbi</div>
    <p class="intro">Some words are better written than spoken. I have a little something for you.</p>

    <div class="env-stage">
      <div class="envelope" id="envelope">
        <div class="env-back"></div>
        <div class="env-paper">♡</div>
        <div class="env-front"></div>
        <div class="env-flap"></div>
        <div class="seal">M</div>
      </div>
    </div>

    <button class="btn" id="openBtn">Open</button>
    <div class="signature-sm script">Modix</div>
  </div>
</main>

<!-- ===================== LETTER SITE ===================== -->
<div id="site" hidden>
  <nav>
    <button id="backBtn" aria-label="Back to the envelope">← Back</button>
    <div class="links">
      <a href="#letter">Letter</a>
      <a href="#cards">Cards</a>
      <a href="#photo">Photo</a>
      <a href="#end">End</a>
    </div>
  </nav>

  <!-- LETTER -->
  <section class="block" id="letter">
    <article class="letter paper reveal">
      <div class="date">Christmas, with love</div>
      <h2>My dearest Mumbi,</h2>
      <p>I tried to say this out loud a few times, and the words kept coming out smaller than I meant them. So I decided to write them down instead, the old-fashioned way.</p>
      <p>Thank you for the way you make ordinary days feel softer. For your kindness, your laugh, and the quiet ways you show up for the people you care about. Being around you makes me want to be a better person.</p>
      <p>This isn't a grand gesture. It's a small gift made with a lot of thought, and I hope it makes you smile, even for a moment.</p>
      <p class="closing">Merry Christmas, Mumbi. You are special to me.</p>
      <div class="sign script">Modix</div>
    </article>
  </section>

  <!-- MEMORY CARDS -->
  <section class="block" id="cards">
    <h2 class="sec-title reveal">Three little things</h2>
    <p class="sec-sub reveal">Tap a card to open it</p>

    <div class="cards">
      <article class="card paper reveal" data-delay="0">
        <button class="card-head" aria-expanded="false">
          <span class="card-num">I</span>
          <span><span class="card-title">A Few Words</span><span class="card-hint">a message from Modix</span></span>
          <span class="chev">⌄</span>
        </button>
        <div class="card-body"><div><div class="card-inner">
          <p>If I could keep only one thing from this year, it would be the moments with you. They're the ones I replay when I'm tired, and they never fail to help.</p>
          <p>Thank you for being you. Never change that part of yourself.</p>
          <div class="mini-sign script">Modix</div>
        </div></div></div>
      </article>

      <article class="card paper reveal" data-delay="1">
        <button class="card-head" aria-expanded="false">
          <span class="card-num">II</span>
          <span><span class="card-title">A Little Memory</span><span class="card-hint">a photograph, kept safe</span></span>
          <span class="chev">⌄</span>
        </button>
        <div class="card-body"><div><div class="card-inner">
          <p id="memoryCaption"></p>
          <button class="btn line" id="seePhoto" style="margin-top:8px;padding:10px 26px;font-size:.7rem">See the photograph ↓</button>
        </div></div></div>
      </article>

      <article class="card paper reveal" data-delay="2">
        <button class="card-head" aria-expanded="false">
          <span class="card-num">III</span>
          <span><span class="card-title">One Last Thing</span><span class="card-hint">a final surprise</span></span>
          <span class="chev">⌄</span>
        </button>
        <div class="card-body"><div><div class="card-inner">
          <p>Whatever the new year brings, I hope you always know that someone is cheering for you, quietly and proudly, and that I'm so glad you're in my life.</p>
          <p class="ps">P.S. You're smiling right now, aren't you? 🎄</p>
        </div></div></div>
      </article>
    </div>
  </section>

  <!-- PHOTO -->
  <section class="block" id="photo">
    <h2 class="sec-title reveal">A little memory</h2>
    <p class="sec-sub reveal">Kept just for you</p>
    <figure class="polaroid reveal">
      <div class="photo-wrap">
        <img id="photoImg" src="mumbi.jpg" alt="A memory of Mumbi" />
        <div class="photo-missing" id="photoMissing">
          <span style="font-size:2rem">📷</span>
          <span>Add your photo by uploading<br><b>mumbi.jpg</b> to the repository</span>
        </div>
      </div>
      <figcaption class="cap" id="photoCaption"></figcaption>
    </figure>
  </section>

  <!-- FINAL -->
  <section class="block" id="end">
    <div class="final paper reveal">
      <svg class="rose" viewBox="0 0 120 190" xmlns="http://www.w3.org/2000/svg" aria-label="A small rose">
        <path d="M60 98 C57 130 63 156 60 184" stroke="#4a6340" stroke-width="4" fill="none" stroke-linecap="round"/>
        <path d="M60 148 C42 146 30 132 27 120 C45 118 58 128 60 148 Z" fill="#587349"/>
        <path d="M61 160 C78 158 90 146 94 135 C76 132 63 142 61 160 Z" fill="#4a6340"/>
        <circle cx="60" cy="56" r="40" fill="#5f1426"/>
        <path d="M24 56 C22 32 46 14 60 18 C78 14 98 32 96 56 C98 80 78 98 60 96 C42 98 22 80 24 56 Z" fill="#7a1f33"/>
        <path d="M34 56 C34 38 48 28 60 30 C74 28 86 40 86 56 C86 74 72 86 60 84 C46 86 34 74 34 56 Z" fill="#963049"/>
        <path d="M44 56 C44 44 52 38 60 40 C70 38 76 46 76 56 C76 66 68 74 60 72 C52 74 44 66 44 56 Z" fill="#b3435f"/>
        <path d="M52 56 C52 49 56 46 61 47 C67 47 69 52 68 57 C66 63 58 64 55 60" stroke="#e9a3b6" stroke-width="2.4" fill="none" stroke-linecap="round"/>
        <path d="M30 40 C42 28 78 26 90 42" stroke="#e9b8c4" stroke-width="1.2" fill="none" opacity=".45"/>
        <path d="M28 72 C40 88 80 90 92 70" stroke="#e9b8c4" stroke-width="1.2" fill="none" opacity=".35"/>
      </svg>
      <p class="msg">If you ever wonder whether someone took a moment to make something special for you, remember this little corner of the internet.</p>
      <div class="sincerely">Yours sincerely,</div>
      <div class="name-sign script">Modix ❤️</div>
      <div class="actions"><button class="btn line" id="restartBtn">Read it again</button></div>
    </div>
  </section>

  <footer>made with love</footer>
</div>

<script>
/* =========================================================
   EDIT THESE TWO LINES
   - PHOTO:   the image file you upload next to index.html
   - CAPTION: the little handwritten line under the photo
   ========================================================= */
const PHOTO   = 'mumbi.jpg';
const CAPTION = 'A moment worth keeping';

const $  = (s, r=document) => r.querySelector(s);
const $$ = (s, r=document) => [...r.querySelectorAll(s)];

/* ---------- Subtle snowfall ---------- */
const cv = $('#snow'), cx = cv.getContext('2d');
let W, H, flakes = [];
function mkFlake(any){
  return {x:Math.random()*W, y:any?Math.random()*H:-8, r:Math.random()*1.7+.6,
          v:Math.random()*.55+.2, p:Math.random()*6.28, a:Math.random()*.4+.2,
          pink:Math.random()<.3};
}
function resize(){
  const d = Math.min(window.devicePixelRatio || 1, 2);
  W = innerWidth; H = innerHeight;
  cv.width = W*d; cv.height = H*d; cx.setTransform(d,0,0,d,0,0);
  flakes = Array.from({length:Math.min(60, Math.round(W*H/17000))}, () => mkFlake(true));
}
function tick(){
  cx.clearRect(0,0,W,H);
  for(const f of flakes){
    f.p += .012; f.y += f.v; f.x += Math.sin(f.p)*.28;
    if(f.y > H+8) Object.assign(f, mkFlake(false));
    cx.beginPath();
    cx.fillStyle = f.pink ? `rgba(232,164,184,${f.a})` : `rgba(255,255,255,${f.a})`;
    cx.arc(f.x, f.y, f.r, 0, 6.283); cx.fill();
  }
  requestAnimationFrame(tick);
}
addEventListener('resize', resize); resize(); tick();

/* ---------- Photo + captions ---------- */
const photoImg = $('#photoImg'), photoMissing = $('#photoMissing');
photoImg.src = PHOTO;
function showMissing(){ photoImg.style.display = 'none'; photoMissing.style.display = 'flex'; }
photoImg.addEventListener('error', showMissing);
if(photoImg.complete && photoImg.naturalWidth === 0) showMissing();
$('#photoCaption').textContent = CAPTION;
$('#memoryCaption').textContent = CAPTION + ' — kept safe, just for you.';

/* ---------- Scroll reveal ---------- */
const reveals = $$('.reveal');
reveals.forEach(el => {
  const d = el.dataset.delay;
  if(d !== undefined) el.style.transitionDelay = (d * 0.18) + 's';
});
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if(e.isIntersecting){ e.target.classList.add('visible'); io.unobserve(e.target); }
  });
}, {threshold:.15, rootMargin:'0px 0px -6% 0px'});
function armReveals(){
  reveals.forEach(el => { el.classList.remove('visible'); io.observe(el); });
}

/* ---------- Opening the envelope ---------- */
const front = $('#front'), site = $('#site'), env = $('#envelope'), openBtn = $('#openBtn');
let busy = false;

openBtn.addEventListener('click', () => {
  if(busy) return; busy = true;
  env.classList.add('open');
  openBtn.textContent = 'Opening…';
  setTimeout(() => front.classList.add('leave'), 2300);
  setTimeout(() => {
    front.hidden = true;
    site.hidden = false;
    window.scrollTo(0, 0);
    armReveals();
    requestAnimationFrame(() => requestAnimationFrame(() => site.classList.add('in')));
  }, 3250);
});

/* ---------- Back to the envelope ---------- */
function goBack(){
  site.classList.remove('in');
  setTimeout(() => {
    site.hidden = true;
    closeAllCards();
    front.hidden = false;
    env.classList.remove('open');
    openBtn.textContent = 'Open';
    window.scrollTo(0, 0);
    requestAnimationFrame(() => requestAnimationFrame(() => {
      front.classList.remove('leave');
      busy = false;
    }));
  }, 700);
}
$('#backBtn').addEventListener('click', goBack);
$('#restartBtn').addEventListener('click', goBack);

/* ---------- Memory cards ---------- */
function setCard(card, open){
  card.classList.toggle('open', open);
  $('.card-head', card).setAttribute('aria-expanded', open);
}
function closeAllCards(){ $$('.card').forEach(c => setCard(c, false)); }
$$('.card').forEach(card => {
  $('.card-head', card).addEventListener('click', () => setCard(card, !card.classList.contains('open')));
});

/* ---------- Jump to photo from card II ---------- */
$('#seePhoto').addEventListener('click', () => {
  $('#photo').scrollIntoView({behavior:'smooth', block:'center'});
});
</script>
</body>
</html>