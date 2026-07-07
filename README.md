[candle-game_1.html](https://github.com/user-attachments/files/29725571/candle-game_1.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>잼비의 빵빵한 캔들 심리 🍞</title>
<link rel="preconnect" href="https://cdn.jsdelivr.net">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.css">
<style>
  :root{
    --bg:#fdf1de; --card:#fffaf1; --line:#f0e3cd;
    --ink:#3a2c18; --muted:#8a7654; --faint:#b4a385;
    --up:#e5423b; --down:#2f6bf0; --flat:#9a8f7c;
    --bread:#f0b357; --bread-dk:#d98b2b; --bread-soft:#fbe6c4;
    --ok:#2fae66; --no:#e5675b;
    --shadow:0 10px 30px rgba(120,80,20,.13);
  }
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
  html,body{background:var(--bg)}
  body{
    font-family:'Pretendard',system-ui,sans-serif;color:var(--ink);
    line-height:1.5;padding:20px 15px 44px;max-width:440px;margin:0 auto;
    min-height:100vh;
  }
  .wrap{animation:fade .35s ease}
  @keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
  @keyframes pop{0%{transform:scale(.9)}60%{transform:scale(1.04)}100%{transform:scale(1)}}
  @keyframes bob{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}
  .bob{animation:bob 2.4s ease-in-out infinite}

  .eyebrow{display:inline-block;font-size:12px;font-weight:800;letter-spacing:.03em;
    color:var(--bread-dk);background:var(--bread-soft);padding:5px 12px;border-radius:100px}
  h1{font-size:27px;font-weight:800;letter-spacing:-.02em;line-height:1.22;margin-top:12px}
  h1 .pt{color:var(--bread-dk)}
  .lead{color:var(--muted);font-size:14.5px;margin-top:10px}

  .mascot{width:150px;margin:6px auto 2px;display:block}
  .mascot.sm{width:96px}

  .card{background:var(--card);border:1px solid var(--line);border-radius:22px;
    box-shadow:var(--shadow);padding:20px}

  .btn{display:block;width:100%;border:none;cursor:pointer;font-family:inherit;
    font-weight:800;font-size:16px;padding:15px;border-radius:16px;
    background:var(--bread);color:#4a3410;box-shadow:0 4px 0 var(--bread-dk);
    transition:transform .06s, box-shadow .06s;letter-spacing:-.01em}
  .btn:active{transform:translateY(3px);box-shadow:0 1px 0 var(--bread-dk)}
  .btn.ghost{background:var(--card);color:var(--muted);box-shadow:none;border:1px solid var(--line)}

  /* intro */
  .intro{text-align:center}
  .rules{text-align:left;background:var(--bread-soft);border-radius:16px;padding:14px 16px;
    margin:18px 0;font-size:13.5px;color:#6b5121;line-height:1.7}
  .rules b{color:var(--bread-dk)}

  /* quiz */
  .top{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
  .crumbs{display:flex;gap:4px;flex-wrap:wrap;max-width:230px}
  .crumb{width:8px;height:8px;border-radius:50%;background:var(--line);transition:background .2s}
  .crumb.on{background:var(--bread)}
  .qcount{font-size:13px;font-weight:800;color:var(--muted)}
  .qcard{text-align:center}
  .qcard svg.chart{width:120px;height:auto;margin:2px auto 0;display:block}
  .qtext{font-size:18px;font-weight:800;margin:14px 4px 4px;letter-spacing:-.01em;line-height:1.4}
  .qtip{font-size:12.5px;color:var(--faint);margin-bottom:16px}
  .opts{display:flex;flex-direction:column;gap:10px}
  .opt{width:100%;text-align:left;border:1.5px solid var(--line);background:#fff;border-radius:14px;
    padding:14px 15px;font-family:inherit;font-size:14.5px;font-weight:600;color:var(--ink);
    cursor:pointer;transition:transform .06s,border-color .12s,background .12s;line-height:1.4}
  .opt:hover{border-color:var(--bread)}
  .opt:active{transform:scale(.98)}
  .opt.picked{border-color:var(--bread-dk);background:var(--bread-soft)}

  /* result */
  .res{text-align:center}
  .grade{font-size:23px;font-weight:800;margin-top:6px;letter-spacing:-.02em}
  .score{font-size:15px;color:var(--muted);margin-top:4px}
  .score b{color:var(--bread-dk);font-size:19px}
  .review{margin-top:20px;display:flex;flex-direction:column;gap:12px;text-align:left}
  .rv{border:1px solid var(--line);border-radius:16px;padding:14px 15px;background:#fff}
  .rv-head{display:flex;align-items:center;gap:8px;font-size:14px;font-weight:800}
  .rv-head .n{width:22px;height:22px;border-radius:50%;display:grid;place-items:center;
    font-size:12px;color:#fff;flex:0 0 auto}
  .rv-head .n.ok{background:var(--ok)} .rv-head .n.no{background:var(--no)}
  .rv-ans{font-size:13px;margin-top:8px;color:var(--muted);line-height:1.55}
  .rv-ans .correct{color:var(--ok);font-weight:800}
  .rv-ans .mine{color:var(--no);font-weight:700}
  .rv-exp{font-size:13px;margin-top:7px;color:var(--ink);background:var(--bread-soft);
    border-radius:11px;padding:9px 11px;line-height:1.55}
  .cta-row{margin-top:20px;display:flex;flex-direction:column;gap:10px}

  .sign{text-align:center;font-size:12px;color:var(--faint);margin-top:22px;line-height:1.6}
  .sign b{color:var(--muted)}
</style>
</head>
<body>
<div id="app"></div>

<script>
/* ---------- bread mascot ---------- */
function bread(mood){
  const mouths={
    hi:'M50,64 Q60,73 70,64',
    think:'M55,67 Q60,64 65,67',
    happy:'M48,62 Q60,76 72,62',
    meh:'M53,68 H67',
    sad:'M50,71 Q60,64 70,71'
  };
  const brows = mood==='think' ? '<line x1="42" y1="47" x2="50" y2="49" stroke="#b6741f" stroke-width="2.5" stroke-linecap="round"/><line x1="78" y1="47" x2="70" y2="49" stroke="#b6741f" stroke-width="2.5" stroke-linecap="round"/>' : '';
  const steam = (mood==='happy') ? '<path d="M60,10 q4,-6 0,-11" stroke="#e0c79a" stroke-width="2.4" fill="none" stroke-linecap="round"/>' : '';
  return `<svg class="mascot bob" viewBox="0 0 120 100" xmlns="http://www.w3.org/2000/svg" aria-label="빵 캐릭터">
    ${steam}
    <path d="M15,86 L15,54 Q15,18 60,18 Q105,18 105,54 L105,86 Q105,91 100,91 L20,91 Q15,91 15,86 Z"
      fill="var(--bread)" stroke="var(--bread-dk)" stroke-width="3"/>
    <path d="M22,40 Q60,26 98,40" stroke="#e0982f" stroke-width="2.4" fill="none" opacity=".5"/>
    <circle cx="35" cy="70" r="7" fill="#f6c98a" opacity=".8"/>
    <circle cx="85" cy="70" r="7" fill="#f6c98a" opacity=".8"/>
    ${brows}
    <circle cx="47" cy="56" r="4" fill="#4a3410"/>
    <circle cx="73" cy="56" r="4" fill="#4a3410"/>
    <circle cx="48.5" cy="54.5" r="1.3" fill="#fff"/>
    <circle cx="74.5" cy="54.5" r="1.3" fill="#fff"/>
    <path d="${mouths[mood]}" stroke="#4a3410" stroke-width="3" fill="none" stroke-linecap="round"/>
  </svg>`;
}

/* ---------- candle drawing ---------- */
function candleSVG(o,c,h,l){
  const W=120,H=220,pad=14,cx=W/2,hw=24;
  const y=p=>pad+(100-p)/100*(H-2*pad);
  const doji=Math.abs(c-o)<3;
  const col=doji?'var(--flat)':(c>o?'var(--up)':'var(--down)');
  const bt=y(Math.max(o,c)),bb=y(Math.min(o,c)),bh=Math.max(3,bb-bt);
  return `<svg class="chart" viewBox="0 0 ${W} ${H}" xmlns="http://www.w3.org/2000/svg">
    <line x1="${cx}" y1="${y(h)}" x2="${cx}" y2="${bt}" stroke="${col}" stroke-width="3.2"/>
    <line x1="${cx}" y1="${bb}" x2="${cx}" y2="${y(l)}" stroke="${col}" stroke-width="3.2"/>
    <rect x="${cx-hw}" y="${bt}" width="${hw*2}" height="${bh}" rx="4"
      fill="${doji?'#fff':col}" stroke="${col}" stroke-width="${doji?3.2:0}"/>
  </svg>`;
}

/* ---------- questions ---------- */
const QS=[
 {c:[15,85,88,12], q:'몸통 빵빵한 빨강 캔들! 🔥', tip:'꼬리는 거의 없고 몸통이 길어',
  opts:['사자 세력 압승! 하루종일 사는 힘이 셌어','팔자가 이겨서 다들 던졌어','아무도 관심 없어서 조용했어'],
  a:0, exp:'장대양봉이야. 몸통이 길고 빨강 → 매수세가 압도적. 강한 상승 에너지 🔥'},

 {c:[68,76,80,15], q:'아래꼬리가 길쭉~ 이 캔들 심리는? 🔨', tip:'몸통은 작고 아래로 꼬리가 길어',
  opts:['밑에서 빠졌다가 사주는 힘이 받쳐줬어 (반등 신호)','위에서 실컷 팔리고 끝났어','하루종일 떨어지기만 했어'],
  a:0, exp:'긴 아래꼬리 = 저점에서 매수세 유입. 바닥권 "망치형"은 반등 신호로 읽혀 🔨'},

 {c:[50,50,74,26], q:'시가·종가가 딱 붙은 십자 캔들. 지금 시장은? ✝️', tip:'몸통이 거의 없어',
  opts:['사자·팔자 팽팽, 방향 고민 중 (전환 신호)','무조건 내일 오른다는 뜻','무조건 내일 내린다는 뜻'],
  a:0, exp:'도지야. 힘겨루기가 팽팽하다는 뜻이고 추세 전환 신호로 자주 등장 ✨ (방향을 확정하진 않아!)'},

 {c:[30,38,88,24], q:'위꼬리가 쭉 뻗은 캔들. 무슨 심리? ☄️', tip:'몸통은 작고 위로 꼬리가 길어',
  opts:['위로 올랐다가 팔려서 밀려 내려왔어 (하락 신호)','상승세가 계속 강하게 이어져','거래가 하나도 없었어'],
  a:0, exp:'긴 위꼬리 = 고점에서 매도세 등장. 고점권 "유성형"은 하락 신호 ☄️'},

 {c:[85,18,88,15], q:'몸통 빵빵한 파랑 캔들! 🥶', tip:'꼬리는 거의 없고 몸통이 길어',
  opts:['팔자 세력 압승! 하루종일 파는 힘이 셌어','사자가 이겨서 쭉 올랐어','시가랑 종가가 똑같았어'],
  a:0, exp:'장대음봉이야. 몸통 길고 파랑 → 매도세가 압도적. 하락 압력이 셈 🥶'},

 {c:[30,68,75,25], q:'이 빨간 캔들이 알려주는 사실은? 🍅', tip:'한국 주식 색깔 개념 문제!',
  opts:['종가가 시가보다 높게 끝났다','종가가 시가보다 낮게 끝났다','아무 일도 없었다'],
  a:0, exp:'한국은 오르면 빨강(양봉)! 빨강 = 종가가 시가보다 위 = 그날 올라서 끝났다는 뜻이야 (미국은 반대라 헷갈리지 말자) 🇰🇷'},

 {c:[38,58,84,34], q:'올랐는데 위꼬리가 달렸네? 🤔', tip:'빨간 몸통 + 제법 긴 위꼬리',
  opts:['오르긴 했지만 위에서 파는 힘도 나왔어','완벽하게 강한 상승이야','하루종일 내리기만 했어'],
  a:0, exp:'양봉인데 위꼬리가 길면 = 올랐지만 고점에선 매도세가 나왔다는 뜻. 100% 강세는 아니고 살짝 부담이 있는 신호 ⚠️'},

 {c:[62,42,66,15], q:'내렸는데 아래꼬리가 길어! 무슨 심리? 💙', tip:'파란 몸통 + 제법 긴 아래꼬리',
  opts:['내렸지만 밑에서 받쳐주는 힘이 있었어','완전히 무너진 폭락이야','거래가 하나도 없었어'],
  a:0, exp:'음봉인데 아래꼬리가 길면 = 떨어졌지만 저점에선 사주는 힘이 있었다는 뜻. 하락세가 조금 누그러지는 신호 🌱'},

 {c:[46,54,80,20], q:'몸통 쪼끄맣고 꼬리는 위아래로! 🌀', tip:'몸통 작고 위·아래 꼬리 둘 다 있어',
  opts:['사자·팔자 힘겨루기, 시장이 눈치보는 중','강한 상승이 확정됐어','강한 하락이 확정됐어'],
  a:0, exp:'"팽이형(스피닝탑)"이야. 위아래로 흔들렸지만 결국 제자리 → 방향을 못 정하고 관망하는 심리 👀'},

 {c:[28,31,86,27], q:'위로 쭉 갔다가 바닥에서 끝났어! 🪦', tip:'몸통이 맨 아래, 위꼬리만 길~게',
  opts:['위로 올랐다가 몽땅 밀려 내려왔어 (하락 경고)','저점에서 반등했어','하루종일 올랐어'],
  a:0, exp:'"비석도지"야. 고점을 찍고 종가가 다시 바닥으로 → 매도세가 압도한 하락 경고 신호 🪦'},

 {c:[71,74,77,16], q:'밑까지 갔다가 위에서 끝났어! 🐝', tip:'몸통이 맨 위, 아래꼬리만 길~게',
  opts:['저점 찍고 다시 다 회복했어 (반등 기대)','고점에서 팔렸어','계속 떨어졌어'],
  a:0, exp:'"잠자리도지"야. 저점을 찍고 종가가 다시 위로 → 매수세가 받쳐준 반등 기대 신호 🐝'},

 {c:[30,60,78,22], q:'캔들의 "몸통(네모)"이 나타내는 건? 📏', tip:'개념 문제! 네모 부분 말이야',
  opts:['시가와 종가 사이','고가와 저가 사이','거래량'],
  a:0, exp:'몸통(네모)은 시가~종가 사이야. 몸통이 길수록 그날 방향의 힘이 셌다는 뜻! 꼬리는 별개로 고가·저가를 나타내 📏'},

 {c:[40,55,85,36], q:'"위꼬리(윗그림자)"가 나타내는 건? 🕯️', tip:'몸통 위로 삐져나온 선!',
  opts:['그날 고가까지 올라갔던 흔적','그날 거래한 사람 수','다음 날 시가'],
  a:0, exp:'위꼬리는 그날 "고가"까지 찍었다가 다시 내려온 흔적이야. 길수록 위에서 밀렸다는 뜻! (아래꼬리는 저가 흔적) 🕯️'},

 {c:[50,50,86,14], q:'위아래로 크게 흔들렸는데 제자리! 😵', tip:'몸통 거의 없고 위·아래 꼬리 둘 다 길~어',
  opts:['크게 출렁였지만 방향은 못 정했어','조용히 살짝 올랐어','거래가 없었어'],
  a:0, exp:'"롱레그 도지"야. 위아래로 크게 싸웠는데 결국 시가=종가 → 변동성은 크지만 방향은 미궁 🌪️ 전환 신호로도 봐'},

 {c:[30,60,82,15], q:'마지막 문제! 캔들 하나에 담긴 가격 4개는? 🍞', tip:'양봉·음봉 공통 기본 개념',
  opts:['시가 · 고가 · 저가 · 종가','상한가 · 하한가 · 평균가 · 거래량','오전가 · 오후가 · 종가 · 예상가'],
  a:0, exp:'정답! 캔들 하나엔 시가(시작)·고가(제일 높았던)·저가(제일 낮았던)·종가(마감) 4개가 담겨있어. 이게 캔들의 전부야 🎓🍞'},
];

/* ---------- state ---------- */
let qi=0, picks=[];
const app=document.getElementById('app');

function intro(){
  app.innerHTML=`<div class="wrap intro">
    <span class="eyebrow">잼비의 자료나눔 · 미니게임</span>
    <h1>빵빵이의 <span class="pt">캔들 심리</span><br>맞히기 🍞</h1>
    ${bread('hi')}
    <p class="lead">캔들 ${QS.length}개를 보여줄게 칭구들!<br>이 캔들 속 <b>시장의 속마음</b>이 뭘지 골라봐 👀</p>
    <div class="rules">
      🍞 <b>총 ${QS.length}문제</b>, 캔들 심리를 골라줘<br>
      🤫 정답은 <b>중간에 안 알려줌</b> — 끝까지 감으로!<br>
      🎉 <b>마지막에 한 번에 공개</b> + 빵 심리 등급 발표
    </div>
    <button class="btn" onclick="start()">빵빵이랑 시작하기 →</button>
    <p class="sign"><b>캔들은 참고용이지 정답이 아니야</b><br>투자 판단은 언제나 내 몫 💛</p>
  </div>`;
}

function start(){ qi=0; picks=[]; question(); }

function question(){
  const Q=QS[qi];
  const crumbs=QS.map((_,i)=>`<span class="crumb ${i<=qi?'on':''}"></span>`).join('');
  app.innerHTML=`<div class="wrap">
    <div class="top">
      <div class="crumbs">${crumbs}</div>
      <div class="qcount">🍞 ${qi+1} / ${QS.length}</div>
    </div>
    <div class="card qcard">
      ${candleSVG(...Q.c)}
      <div class="qtext">${Q.q}</div>
      <div class="qtip">${Q.tip}</div>
      <div class="opts">
        ${Q.opts.map((o,i)=>`<button class="opt" data-i="${i}">${o}</button>`).join('')}
      </div>
    </div>
  </div>`;
  app.querySelectorAll('.opt').forEach(b=>{
    b.addEventListener('click',()=>{
      app.querySelectorAll('.opt').forEach(x=>x.classList.remove('picked'));
      b.classList.add('picked');
      picks[qi]=+b.dataset.i;
      setTimeout(()=>{ qi++; qi<QS.length ? question() : result(); },360);
    });
  });
}

function result(){
  const score=picks.filter((p,i)=>p===QS[i].a).length;
  let mood,grade;
  if(score===15){mood='happy';grade='캔들 심리 마스터 빵빵이 👑';}
  else if(score>=11){mood='happy';grade='노릇노릇 잘 구워진 빵 🥐';}
  else if(score>=6){mood='hi';grade='제법인데? 반쯤 구워졌어 🍞';}
  else if(score>=1){mood='meh';grade='아직 반죽 단계 🫓 다시 구워보자';}
  else {mood='sad';grade='밀가루 상태 😅 첨부터 다시!';}

  const review=QS.map((Q,i)=>{
    const ok=picks[i]===Q.a;
    const mineTxt = ok ? '' : `<br><span class="mine">내 선택: ${Q.opts[picks[i]]}</span>`;
    return `<div class="rv">
      <div class="rv-head"><span class="n ${ok?'ok':'no'}">${ok?'✓':'✕'}</span> ${i+1}번 문제</div>
      <div class="rv-ans"><span class="correct">정답: ${Q.opts[Q.a]}</span>${mineTxt}</div>
      <div class="rv-exp">${Q.exp}</div>
    </div>`;
  }).join('');

  app.innerHTML=`<div class="wrap res">
    <span class="eyebrow">🎉 결과 공개</span>
    ${bread(mood)}
    <div class="grade">${grade}</div>
    <div class="score">${QS.length}문제 중 <b>${score}개</b> 정답!</div>
    <div class="review">${review}</div>
    <div class="cta-row">
      <button class="btn" onclick="start()">🍞 다시 굽기 (재도전)</button>
      <button class="btn ghost" onclick="intro()">처음으로</button>
    </div>
    <p class="sign"><b>캔들은 시장 심리를 읽는 힌트일 뿐</b><br>투자 판단은 언제나 내 몫이야 💛<br>— 잼비 @jam._bi</p>
  </div>`;
  window.scrollTo({top:0,behavior:'smooth'});
}

intro();
</script>
</body>
</html>
