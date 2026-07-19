[picking-rate-calculator.html](https://github.com/user-attachments/files/30160659/picking-rate-calculator.html)
<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>피킹률 계산기 · 잼비의 첫 재테크</title>
<meta name="description" content="내 카드가 진짜로 돌려주는 비율, 피킹률을 계산해보세요. 카드 3장까지 비교할 수 있어요.">
<link rel="preconnect" href="https://cdn.jsdelivr.net">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css">
<style>
:root{
  --ink:#1B1310;
  --ink-2:#4A3B33;
  --muted:#958174;
  --paper:#FFF1DF;
  --card:#FFFFFF;
  --line:#E9D7C4;
  --orange:#FF6B18;
  --orange-deep:#C64B0A;
  --orange-wash:#FFE3CC;
  --mint:#0B8F63;
  --alert:#D42B2B;
  --shadow:0 1px 0 rgba(27,19,16,.06), 0 12px 32px -18px rgba(27,19,16,.45);
  --r:14px;
}
*{box-sizing:border-box}
html,body{margin:0;padding:0}
body{
  background:var(--paper);
  color:var(--ink);
  font-family:"Pretendard Variable",Pretendard,-apple-system,BlinkMacSystemFont,"Apple SD Gothic Neo","Malgun Gothic",sans-serif;
  font-size:16px;line-height:1.6;
  -webkit-font-smoothing:antialiased;
  background-image:radial-gradient(circle at 1px 1px, rgba(198,75,10,.07) 1px, transparent 0);
  background-size:22px 22px;
}
.wrap{max-width:1060px;margin:0 auto;padding:28px 20px 72px}

/* ── header ── */
header{margin-bottom:26px}
.eyebrow{
  display:inline-flex;align-items:center;gap:7px;
  font-size:12px;font-weight:700;letter-spacing:.14em;
  color:var(--orange-deep);background:var(--orange-wash);
  padding:6px 12px;border-radius:999px;
}
h1{
  font-size:clamp(30px,6.2vw,46px);line-height:1.12;
  font-weight:800;letter-spacing:-.035em;margin:14px 0 8px;
}
h1 em{font-style:normal;color:var(--orange);}
.sub{color:var(--ink-2);max-width:46ch;margin:0;font-size:15px}

/* ── card tabs ── */
.tabs{display:flex;gap:8px;margin:26px 0 0;flex-wrap:wrap;align-items:center}
.tab{
  appearance:none;border:1.5px solid var(--line);background:var(--card);
  color:var(--ink-2);font:inherit;font-size:14px;font-weight:700;
  padding:9px 16px;border-radius:999px;cursor:pointer;
  transition:transform .12s ease, border-color .12s ease, color .12s ease;
  display:flex;align-items:center;gap:8px;
}
.tab:hover{transform:translateY(-1px)}
.tab[aria-selected="true"]{border-color:var(--orange);color:var(--orange-deep);background:var(--orange-wash)}
.tab .dot{width:7px;height:7px;border-radius:50%;background:var(--line)}
.tab[aria-selected="true"] .dot{background:var(--orange)}
.tab-rate{font-variant-numeric:tabular-nums;font-size:12px;color:var(--muted)}
.tab[aria-selected="true"] .tab-rate{color:var(--orange-deep)}
.tab-add{border-style:dashed;color:var(--muted)}
.tab-del{
  appearance:none;border:0;background:none;font:inherit;color:var(--muted);
  cursor:pointer;font-size:13px;padding:9px 6px;text-decoration:underline;text-underline-offset:3px;
}

/* ── layout ── */
.grid{display:grid;grid-template-columns:1fr 400px;gap:20px;margin-top:18px;align-items:start}
@media(max-width:880px){.grid{grid-template-columns:1fr}}
.panel{background:var(--card);border:1px solid var(--line);border-radius:var(--r);box-shadow:var(--shadow)}
.panel-pad{padding:22px}

/* ── form ── */
fieldset{border:0;margin:0;padding:0}
fieldset + fieldset{margin-top:24px;padding-top:22px;border-top:1px dashed var(--line)}
legend{
  font-size:12px;font-weight:800;letter-spacing:.1em;color:var(--muted);
  padding:0;margin-bottom:4px;
}
legend .hint{display:block;font-size:12.5px;font-weight:500;letter-spacing:0;color:var(--muted);margin-top:5px;line-height:1.5}
.field{display:flex;align-items:center;gap:12px;padding:9px 0}
.field label{flex:1;font-size:14.5px;color:var(--ink-2)}
.field .note{display:block;font-size:12px;color:var(--muted);margin-top:1px}
.money{position:relative;flex:0 0 168px}
.money input{
  width:100%;font:inherit;font-size:15px;font-weight:700;
  font-variant-numeric:tabular-nums;text-align:right;
  padding:10px 34px 10px 12px;border:1.5px solid var(--line);border-radius:9px;
  background:#FFFDFA;color:var(--ink);
}
.money input:focus{outline:2.5px solid var(--orange);outline-offset:1px;border-color:transparent}
.money input::-webkit-outer-spin-button,.money input::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}
.money .unit{
  position:absolute;right:12px;top:50%;transform:translateY(-50%);
  font-size:13px;color:var(--muted);pointer-events:none;font-weight:600;
}
.money.minus input{color:var(--alert)}
input[type=text].cardname{
  width:100%;font:inherit;font-size:17px;font-weight:800;letter-spacing:-.02em;
  padding:11px 13px;border:1.5px solid var(--line);border-radius:9px;background:#FFFDFA;
}
input[type=text].cardname:focus{outline:2.5px solid var(--orange);outline-offset:1px;border-color:transparent}

/* ── result ── */
.result{position:sticky;top:20px}
.gauge{padding:24px 22px 20px;text-align:center;border-bottom:1px dashed var(--line)}
.gauge-label{font-size:12px;font-weight:800;letter-spacing:.12em;color:var(--muted)}
.big{
  font-size:clamp(56px,15vw,76px);font-weight:800;letter-spacing:-.05em;line-height:1;
  font-variant-numeric:tabular-nums;margin:8px 0 2px;color:var(--orange);
  transition:color .3s ease;
}
.big.neg{color:var(--alert)}
.big .pct{font-size:.42em;font-weight:700;margin-left:2px}
.gauge-track{height:9px;border-radius:99px;background:var(--orange-wash);overflow:hidden;margin:16px 0 0;position:relative}
.gauge-fill{height:100%;width:0;background:var(--orange);border-radius:99px;transition:width .5s cubic-bezier(.22,1,.36,1)}
.gauge-fill.neg{background:var(--alert)}
.gauge-scale{display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-top:6px;font-variant-numeric:tabular-nums}

.stamp-row{padding:18px 22px;display:flex;align-items:center;gap:14px}
.stamp{
  flex:0 0 auto;border:2.5px solid currentColor;border-radius:8px;
  padding:7px 13px;font-weight:800;font-size:15px;letter-spacing:.03em;
  transform:rotate(-4deg);opacity:.92;
}
.stamp.pop{animation:pop .35s cubic-bezier(.34,1.56,.64,1)}
@keyframes pop{0%{transform:rotate(-4deg) scale(.6);opacity:0}100%{transform:rotate(-4deg) scale(1);opacity:.92}}
.verdict-text{font-size:14px;color:var(--ink-2);line-height:1.5}

/* ── receipt ── */
.receipt{padding:18px 22px 22px;border-top:1px dashed var(--line);background:#FFFDFA;border-radius:0 0 var(--r) var(--r)}
.receipt h3{font-size:12px;font-weight:800;letter-spacing:.12em;color:var(--muted);margin:0 0 12px}
.line{display:flex;justify-content:space-between;gap:10px;font-size:14px;padding:5px 0;color:var(--ink-2)}
.line span:last-child{font-variant-numeric:tabular-nums;font-weight:700;color:var(--ink);white-space:nowrap}
.line.minus span:last-child{color:var(--alert)}
.line.total{border-top:1.5px solid var(--ink);margin-top:9px;padding-top:11px;font-weight:800;font-size:15px;color:var(--ink)}
.compare{
  margin-top:16px;padding:14px;border-radius:10px;background:var(--orange-wash);
  font-size:13.5px;line-height:1.6;color:var(--ink-2)
}
.compare b{color:var(--orange-deep)}
.compare .vs{display:flex;justify-content:space-between;margin-bottom:8px;font-variant-numeric:tabular-nums}
.compare .vs em{font-style:normal;font-size:12px;color:var(--muted);display:block}
.compare .vs strong{font-size:20px;font-weight:800;letter-spacing:-.03em}

.actions{display:flex;gap:8px;margin-top:14px}
.btn{
  appearance:none;border:1.5px solid var(--ink);background:var(--ink);color:#fff;
  font:inherit;font-size:14px;font-weight:700;padding:11px 14px;border-radius:9px;
  cursor:pointer;flex:1;transition:transform .12s ease,opacity .12s ease;
}
.btn:hover{transform:translateY(-1px)}
.btn.ghost{background:transparent;color:var(--ink);border-color:var(--line)}

/* ── read table ── */
.read{margin-top:20px}
.read table{width:100%;border-collapse:collapse;font-size:14px;background:var(--card)}
.read caption{text-align:left;font-size:12px;font-weight:800;letter-spacing:.12em;color:var(--muted);padding:0 0 10px}
.read th,.read td{text-align:left;padding:11px 14px;border-bottom:1px solid var(--line)}
.read th{font-size:12px;color:var(--muted);font-weight:700;background:#FFFAF3}
.read td:first-child{font-weight:800;font-variant-numeric:tabular-nums;white-space:nowrap}
.read tr[data-on="1"] td{background:var(--orange-wash)}
.read tr:last-child td{border-bottom:0}

.note-box{
  margin-top:20px;padding:18px 20px;border-radius:var(--r);
  border:1.5px solid var(--line);background:var(--card);font-size:14.5px;line-height:1.7;color:var(--ink-2)
}
.note-box strong{color:var(--ink)}
.note-box .who{font-size:12px;font-weight:800;letter-spacing:.1em;color:var(--orange-deep);display:block;margin-bottom:8px}

footer{margin-top:34px;font-size:13px;color:var(--muted);text-align:center;line-height:1.7}

.toast{
  position:fixed;left:50%;bottom:26px;transform:translate(-50%,14px);
  background:var(--ink);color:#fff;padding:12px 20px;border-radius:999px;
  font-size:14px;font-weight:600;opacity:0;pointer-events:none;transition:.24s ease;z-index:9;
}
.toast.show{opacity:1;transform:translate(-50%,0)}
.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);white-space:nowrap}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="wrap">

<header>
  <span class="eyebrow">잼비의 첫 재테크 · 실행 키트 03</span>
  <h1>이 카드, 나한테<br>진짜 <em>얼마나</em> 돌려줄까?</h1>
  <p class="sub">카드사가 말하는 혜택 말고, 연회비랑 실적 채우느라 쓴 돈까지 빼고 남는 진짜 비율. 3장까지 나란히 비교할 수 있어요.</p>
</header>

<div class="tabs" role="tablist" id="tabs"></div>

<div class="grid">

  <!-- 입력 -->
  <section class="panel panel-pad" aria-label="카드 정보 입력">
    <fieldset>
      <legend>카드<span class="sr">이름과 연간 결제액</span></legend>
      <div style="padding:9px 0">
        <input type="text" class="cardname" id="name" placeholder="카드 이름 (예: 주력카드)" maxlength="20">
      </div>
      <div class="field">
        <label for="spend">연간 결제액<span class="note">이 카드로 1년 동안 긁은 총액</span></label>
        <div class="money"><input type="number" id="spend" inputmode="numeric" min="0" step="10000" placeholder="0"><span class="unit">원</span></div>
      </div>
    </fieldset>

    <fieldset>
      <legend>받은 것
        <span class="hint">지난 1년 기준으로 적어요. 기억이 안 나면 카드사 앱 → 이용실적/혜택 내역에서 확인할 수 있어요.</span>
      </legend>
      <div class="field">
        <label for="cash">할인 · 캐시백<span class="note">청구할인, 즉시할인 합계</span></label>
        <div class="money"><input type="number" id="cash" inputmode="numeric" min="0" step="1000" placeholder="0"><span class="unit">원</span></div>
      </div>
      <div class="field">
        <label for="point">적립 포인트<span class="note">현금 가치로 환산해서</span></label>
        <div class="money"><input type="number" id="point" inputmode="numeric" min="0" step="1000" placeholder="0"><span class="unit">원</span></div>
      </div>
      <div class="field">
        <label for="perk">부가서비스<span class="note">라운지, 영화, 커피 등 실제로 쓴 것만</span></label>
        <div class="money"><input type="number" id="perk" inputmode="numeric" min="0" step="1000" placeholder="0"><span class="unit">원</span></div>
      </div>
    </fieldset>

    <fieldset>
      <legend>빼야 할 것
        <span class="hint">여기를 안 빼면 피킹률이 실제보다 높게 나와요. 계산이 어긋나는 건 대부분 아래 두 번째 칸 때문이에요.</span>
      </legend>
      <div class="field">
        <label for="fee">연회비<span class="note">국내 + 해외 겸용 합산</span></label>
        <div class="money minus"><input type="number" id="fee" inputmode="numeric" min="0" step="1000" placeholder="0"><span class="unit">원</span></div>
      </div>
      <div class="field">
        <label for="waste">실적 채우려고 쓴 돈<span class="note">그 카드가 아니었으면 안 썼을 지출</span></label>
        <div class="money minus"><input type="number" id="waste" inputmode="numeric" min="0" step="1000" placeholder="0"><span class="unit">원</span></div>
      </div>
    </fieldset>
  </section>

  <!-- 결과 -->
  <aside class="result">
    <div class="panel">
      <div class="gauge">
        <div class="gauge-label">진짜 피킹률</div>
        <div class="big" id="big">0.00<span class="pct">%</span></div>
        <div class="gauge-track"><div class="gauge-fill" id="fill"></div></div>
        <div class="gauge-scale"><span>0%</span><span>1.5%</span><span>3%+</span></div>
      </div>

      <div class="stamp-row">
        <div class="stamp" id="stamp" style="color:var(--muted)">입력 대기</div>
        <p class="verdict-text" id="verdict">연간 결제액부터 넣어주세요.</p>
      </div>

      <div class="receipt">
        <h3>계산 내역</h3>
        <div class="line"><span>할인 · 캐시백</span><span id="r-cash">0원</span></div>
        <div class="line"><span>적립 포인트</span><span id="r-point">0원</span></div>
        <div class="line"><span>부가서비스</span><span id="r-perk">0원</span></div>
        <div class="line minus"><span>연회비</span><span id="r-fee">0원</span></div>
        <div class="line minus"><span>실적 채우려 쓴 돈</span><span id="r-waste">0원</span></div>
        <div class="line total"><span>순혜택</span><span id="r-net">0원</span></div>

        <div class="compare">
          <div class="vs">
            <div><em>카드사가 말하는 피킹률</em><strong id="r-gross">0.00%</strong></div>
            <div style="text-align:right"><em>연회비·실적 빼면</em><strong id="r-real" style="color:var(--orange-deep)">0.00%</strong></div>
          </div>
          <span id="gapmsg">두 숫자의 차이가 그동안 안 보이던 비용이에요.</span>
        </div>

        <div class="actions">
          <button class="btn" id="copy">결과 복사</button>
          <button class="btn ghost" id="reset">이 카드 비우기</button>
        </div>
      </div>
    </div>
  </aside>
</div>

<div class="read">
  <table>
    <caption>피킹률 읽는 법</caption>
    <thead><tr><th style="width:110px">피킹률</th><th>이럴 땐 이렇게</th></tr></thead>
    <tbody>
      <tr data-band="0"><td>0% 미만</td><td>혜택보다 비용이 커요. 연회비부터 확인하고 해지를 검토하세요</td></tr>
      <tr data-band="1"><td>0 ~ 0.5%</td><td>거의 없는 수준이에요. 체크카드가 더 나을 수 있어요</td></tr>
      <tr data-band="2"><td>0.5 ~ 1.5%</td><td>평범해요. 실적 맞추느라 쓰는 돈이 있다면 손해예요</td></tr>
      <tr data-band="3"><td>1.5 ~ 3%</td><td>잘 쓰고 있어요. 그대로 유지</td></tr>
      <tr data-band="4"><td>3% 이상</td><td>최적화 완료. 이 카드에 지출을 몰아주세요</td></tr>
    </tbody>
  </table>
</div>

<div class="note-box">
  <span class="who">잼비 한마디</span>
  저는 제 주력 카드 피킹률이 <strong>0.4%</strong>였어요. 연회비 빼니까 거의 본전이더라고요.
  분명 혜택 보려고 만든 카드인데, 막상 쓸 땐 매번 조건을 까먹고 그냥 긁었거든요.<br><br>
  그러니까 카드를 바꿀지 말지 고민하기 전에 <strong>숫자부터 구해보세요.</strong>
  생각보다 혜택이 적어서 결정이 쉬워질 수도 있어요.
</div>

<footer>
  피킹률 = (할인 + 포인트 + 부가서비스 − 연회비 − 실적용 지출) ÷ 연간 결제액 × 100<br>
  잼비의 첫 재테크 실행 키트 · 03. 신용카드 vs 체크카드
</footer>

</div>

<div class="toast" id="toast">결과를 복사했어요</div>

<script>
(function(){
  var FIELDS = ['name','spend','cash','point','perk','fee','waste'];
  var cards = [blank('주력카드')];
  var active = 0;

  function blank(n){ return {name:n||'',spend:'',cash:'',point:'',perk:'',fee:'',waste:''}; }
  function num(v){ var n = parseFloat(v); return isFinite(n) ? n : 0; }
  function won(n){
    var s = Math.round(Math.abs(n)).toLocaleString('ko-KR');
    return (n < 0 ? '-' : '') + s + '원';
  }

  function calc(c){
    var spend = num(c.spend);
    var gain  = num(c.cash) + num(c.point) + num(c.perk);
    var cost  = num(c.fee) + num(c.waste);
    var net   = gain - cost;
    return {
      spend: spend, gain: gain, cost: cost, net: net,
      gross: spend > 0 ? gain / spend * 100 : 0,
      real:  spend > 0 ? net  / spend * 100 : 0,
      ready: spend > 0
    };
  }

  function band(r){
    if (r < 0)   return {i:0, label:'해지 검토', color:'var(--alert)', msg:'혜택보다 비용이 커요. 유지할 이유를 찾기 어려운 상태예요.'};
    if (r < 0.5) return {i:1, label:'교체 검토', color:'var(--alert)', msg:'혜택이 거의 없는 수준이에요. 체크카드 쪽이 나을 수 있어요.'};
    if (r < 1.5) return {i:2, label:'평범',      color:'var(--muted)', msg:'나쁘진 않지만 특별하지도 않아요. 실적 조건을 다시 보세요.'};
    if (r < 3)   return {i:3, label:'유지',      color:'var(--mint)',  msg:'잘 쓰고 있어요. 이대로 가면 돼요.'};
    return              {i:4, label:'최적화 완료', color:'var(--mint)', msg:'훌륭해요. 이 카드에 지출을 몰아주는 게 이득이에요.'};
  }

  var $ = function(id){ return document.getElementById(id); };

  function renderTabs(){
    var t = $('tabs'); t.innerHTML = '';
    cards.forEach(function(c,i){
      var r = calc(c);
      var b = document.createElement('button');
      b.className = 'tab'; b.type = 'button';
      b.setAttribute('role','tab');
      b.setAttribute('aria-selected', i === active ? 'true' : 'false');
      b.innerHTML = '<span class="dot"></span>' +
        '<span>' + (c.name ? esc(c.name) : '카드 ' + (i+1)) + '</span>' +
        (r.ready ? '<span class="tab-rate">' + r.real.toFixed(2) + '%</span>' : '');
      b.onclick = function(){ active = i; render(); };
      t.appendChild(b);
    });
    if (cards.length < 3){
      var add = document.createElement('button');
      add.className = 'tab tab-add'; add.type = 'button';
      add.textContent = '+ 카드 추가';
      add.onclick = function(){ cards.push(blank('')); active = cards.length - 1; render(); focusName(); };
      t.appendChild(add);
    }
    if (cards.length > 1){
      var del = document.createElement('button');
      del.className = 'tab-del'; del.type = 'button';
      del.textContent = '이 카드 삭제';
      del.onclick = function(){
        cards.splice(active,1);
        active = Math.max(0, active - 1);
        render();
      };
      t.appendChild(del);
    }
  }

  function esc(s){ return String(s).replace(/[&<>"]/g, function(m){
    return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[m]; }); }

  function focusName(){ var el = $('name'); if (el) el.focus(); }

  function renderInputs(){
    var c = cards[active];
    FIELDS.forEach(function(f){ $(f).value = c[f]; });
  }

  function renderResult(){
    var c = cards[active], r = calc(c), b = band(r.real);

    var big = $('big');
    big.innerHTML = (r.ready ? r.real.toFixed(2) : '0.00') + '<span class="pct">%</span>';
    big.classList.toggle('neg', r.real < 0);

    var pct = Math.max(0, Math.min(100, r.real / 3 * 100));
    var fill = $('fill');
    fill.style.width = (r.ready ? pct : 0) + '%';
    fill.classList.toggle('neg', r.real < 0);

    var stamp = $('stamp');
    if (r.ready){
      if (stamp.textContent !== b.label){
        stamp.classList.remove('pop'); void stamp.offsetWidth; stamp.classList.add('pop');
      }
      stamp.textContent = b.label;
      stamp.style.color = b.color;
      $('verdict').textContent = b.msg;
    } else {
      stamp.textContent = '입력 대기';
      stamp.style.color = 'var(--muted)';
      $('verdict').textContent = '연간 결제액부터 넣어주세요.';
    }

    $('r-cash').textContent  = won(num(c.cash));
    $('r-point').textContent = won(num(c.point));
    $('r-perk').textContent  = won(num(c.perk));
    $('r-fee').textContent   = won(-num(c.fee));
    $('r-waste').textContent = won(-num(c.waste));
    $('r-net').textContent   = won(r.net);

    $('r-gross').textContent = r.gross.toFixed(2) + '%';
    $('r-real').textContent  = r.real.toFixed(2) + '%';

    var gap = r.gross - r.real;
    $('gapmsg').innerHTML = !r.ready
      ? '두 숫자의 차이가 그동안 안 보이던 비용이에요.'
      : (gap < 0.01
        ? '연회비도 낭비지출도 없네요. 이 카드는 광고 그대로예요.'
        : '차이 <b>' + gap.toFixed(2) + '%p</b> · 연 <b>' + won(r.cost) + '</b>이 그동안 안 보이던 비용이에요.');

    var rows = document.querySelectorAll('.read tbody tr');
    for (var i = 0; i < rows.length; i++){
      rows[i].setAttribute('data-on', (r.ready && +rows[i].dataset.band === b.i) ? '1' : '0');
    }
  }

  function render(){ renderTabs(); renderInputs(); renderResult(); }

  FIELDS.forEach(function(f){
    $(f).addEventListener('input', function(e){
      cards[active][f] = e.target.value;
      renderResult();
      if (f === 'name' || f === 'spend') renderTabs();
    });
  });

  $('reset').onclick = function(){
    cards[active] = blank(cards[active].name);
    render();
  };

  $('copy').onclick = function(){
    var c = cards[active], r = calc(c), b = band(r.real);
    var txt = [
      '[' + (c.name || '내 카드') + '] 피킹률 계산 결과',
      '연간 결제액 ' + won(r.spend),
      '순혜택 ' + won(r.net),
      '카드사 기준 ' + r.gross.toFixed(2) + '% → 진짜 피킹률 ' + r.real.toFixed(2) + '%',
      '판정: ' + b.label,
      '',
      '잼비의 첫 재테크 · 피킹률 계산기'
    ].join('\n');

    var done = function(){
      var t = $('toast'); t.classList.add('show');
      setTimeout(function(){ t.classList.remove('show'); }, 1800);
    };
    if (navigator.clipboard && navigator.clipboard.writeText){
      navigator.clipboard.writeText(txt).then(done, fallback);
    } else { fallback(); }

    function fallback(){
      var ta = document.createElement('textarea');
      ta.value = txt; ta.style.position = 'fixed'; ta.style.opacity = '0';
      document.body.appendChild(ta); ta.select();
      try { document.execCommand('copy'); done(); } catch(e){}
      document.body.removeChild(ta);
    }
  };

  render();
})();
</script>
</body>
</html>
