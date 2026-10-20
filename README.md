<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>自我建构量表测试</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: -apple-system, "Segoe UI", "Microsoft YaHei", "PingFang SC", sans-serif;
    background: linear-gradient(to bottom, #ffffff, #fafafa);
    color: #0f172a; min-height: 100vh; line-height: 1.7;
  }
  .wrap { max-width: 640px; margin: 0 auto; padding: 48px 16px 80px; }

  /* ---------- 说明页 ---------- */
  .center { text-align: center; }
  .badge {
    display: inline-block; background: #f1f5f9; color: #334155;
    font-size: 12px; padding: 4px 14px; border-radius: 999px; margin-bottom: 14px;
    border: 1px solid #e2e8f0;
  }
  h1 { font-size: 34px; letter-spacing: -0.5px; margin-bottom: 8px; }
  .sub { color: #64748b; font-size: 17px; }
  .card {
    background: #fff; border: 1px solid #e2e8f0; border-radius: 14px;
    padding: 26px; margin-top: 26px; box-shadow: 0 1px 3px rgba(15,23,42,.06);
  }
  .card h2 { font-size: 18px; margin-bottom: 2px; }
  .card .desc { color: #64748b; font-size: 13px; margin-bottom: 14px; }
  .intro-body { text-align: left; font-size: 14.5px; }
  .intro-body p { margin-bottom: 12px; }
  .scale-row { display: flex; flex-wrap: wrap; gap: 6px; justify-content: center; padding: 8px 0 14px; }
  .scale-chip {
    font-size: 11.5px; border: 1px solid #e2e8f0; border-radius: 999px;
    padding: 3px 10px; color: #475569; background: #fff; white-space: nowrap;
  }
  ul.tips { list-style: disc; padding-left: 22px; color: #64748b; font-size: 13.5px; }
  ul.tips li { margin-bottom: 6px; }
  .btn {
    display: inline-flex; align-items: center; justify-content: center; gap: 6px;
    border: none; cursor: pointer; border-radius: 10px;
    background: #0f172a; color: #fff; font-size: 16px; font-weight: 600;
    padding: 12px 32px; transition: opacity .15s; font-family: inherit;
  }
    .btn:hover { opacity: .85; }
  .btn:disabled { background: #cbd5e1; cursor: not-allowed; }
  .btn.outline { background: #fff; color: #334155; border: 1.5px solid #cbd5e1; }
  .btn.block { width: 100%; margin-top: 16px; }
  .footnote { font-size: 12px; color: #94a3b8; text-align: center; margin-top: 24px; line-height: 1.9; }
  .ind { color: #4f46e5; font-weight: 600; }
  .int { color: #f43f5e; font-weight: 600; }

  /* ---------- 答题页 ---------- */
  .meta-row { display: flex; justify-content: space-between; font-size: 13.5px; color: #64748b; margin-bottom: 6px; }
  .meta-row b { color: #0f172a; }
  .progress-outer { height: 8px; background: #e2e8f0; border-radius: 999px; overflow: hidden; }
  .progress-inner { height: 100%; background: #0f172a; border-radius: 999px; width: 0; transition: width .25s; }
  .q-card {
    background: #fff; border: 1px solid #e2e8f0; border-radius: 14px;
    padding: 34px 30px; margin-top: 22px; min-height: 320px;
    display: flex; flex-direction: column;
    box-shadow: 0 1px 3px rgba(15,23,42,.06);
    animation: fadeSlide .3s ease;
  }
  @keyframes fadeSlide { from { opacity: 0; transform: translateX(14px); } to { opacity: 1; transform: none; } }
  .q-step { font-size: 12px; font-weight: 600; color: #94a3b8; margin-bottom: 12px; }
  .q-text { font-size: 21px; font-weight: 500; line-height: 1.6; margin-bottom: 34px; }
  .q-bottom { margin-top: auto; }
  .likert-ends { display: flex; justify-content: space-between; font-size: 12px; color: #94a3b8; margin: 0 2px 6px; }
  .opts { display: flex; justify-content: space-between; gap: 8px; }
  .opt {
    flex: 1; max-width: 54px; aspect-ratio: 1; border: 2px solid #e2e8f0; border-radius: 12px;
    background: #fff; font-size: 16px; font-weight: 600; color: #475569; cursor: pointer;
    transition: all .12s; font-family: inherit;
  }
  .opt:hover { border-color: #94a3b8; }
  .opt.on {
    background: #0f172a; border-color: #0f172a; color: #fff;
    transform: scale(1.1); box-shadow: 0 3px 10px rgba(15,23,42,.3);
  }
  .q-sel-label { text-align: center; font-size: 12px; color: #64748b; margin-top: 12px; min-height: 18px; }
  .nav-row { display: flex; justify-content: space-between; margin-top: 22px; }
  .quiz-hint { text-align: center; font-size: 12px; color: #94a3b8; margin-top: 10px; }

  /* ---------- 结果页 ---------- */
  .result-head .badge { margin-bottom: 12px; }
  .result-title { font-size: 28px; font-weight: 700; margin-bottom: 4px; }
  .score-row { display: flex; justify-content: center; gap: 30px; font-size: 14px; margin-top: 12px; flex-wrap: wrap; }
  .score-row b { font-size: 17px; }
  .chart-box { width: 100%; }
  .chart-box canvas { display: block; width: 100%; }
  .chart-note { font-size: 12px; color: #94a3b8; text-align: center; margin-top: 6px; }
  .advice p { font-size: 14px; margin-bottom: 12px; line-height: 1.8; }
  .note { background: #f8fafc; border-radius: 10px; padding: 14px 16px; font-size: 12px; color: #64748b; line-height: 1.8; margin-top: 6px; }
  @media (max-width: 480px) {
    h1 { font-size: 27px; }
    .q-text { font-size: 18px; }
    .q-card { padding: 26px 20px; }
  }
</style>
</head>
<body>
<div class="wrap">

  <!-- 说明页 -->
  <div id="page-intro">
    <div class="center">
      <span class="badge">滑铁卢大学 2008 年修订版 · 中文版</span>
      <h1>自我建构量表测试</h1>
      <div class="sub">Self-Construal Scale · 独立型 vs 互依型</div>
    </div>
    <div class="card intro-body">
      <h2>测试说明</h2>
      <div class="desc">开始前请仔细阅读</div>
      <p>本量表共 <b>24 题</b>，测量自我建构的两个维度：<span class="ind">独立型</span>（重视独特、自主与自我表达）与 <span class="int">互依型</span>（重视关系、和谐与群体归属）。</p>
      <p>每题只需点选一个数字（1–7 分），表示你对这句话的同意程度：</p>
      <div class="scale-row">
        <span class="scale-chip">1 非常不同意</span><span class="scale-chip">2 不同意</span>
        <span class="scale-chip">3 有点不同意</span><span class="scale-chip">4 既不同意也不赞同</span>
        <span class="scale-chip">5 有点同意</span><span class="scale-chip">6 同意</span>
        <span class="scale-chip">7 非常同意</span>
      </div>
      <ul class="tips">
        <li>请按<b>真实感受</b>作答，而不是"理想中的自己"。</li>
        <li>没有对错之分，请回答所有题目。</li>
        <li>题目逐题呈现，点选后会自动进入下一题，也可以返回修改。</li>
        <li>大约需要 3–5 分钟，完成后可查看维度图与个性化建议。</li>
      </ul>
      <button class="btn block" onclick="showQuiz()">开始测试</button>
    </div>
    <div class="footnote">
      来源：Singelis (1994)；Grossmann &amp; Na (2008) 修订版，滑铁卢大学智慧与心理文化实验室。<br>
      中文版为研究者翻译，尚未经独立的信效度验证，结果仅供自我探索参考。
    </div>
  </div>

  <!-- 答题页 -->
  <div id="page-quiz" style="display:none;">
    <div class="meta-row">
      <span>第 <b id="q-now">1</b> / 24 题</span>
      <span>已作答 <b id="q-count">0</b> 题</span>
    </div>
    <div class="progress-outer"><div class="progress-inner" id="progress"></div></div>

    <div class="q-card" id="q-card">
      <div class="q-step" id="q-step"></div>
      <div class="q-text" id="q-text"></div>
      <div class="q-bottom">
        <div class="likert-ends"><span>非常不同意</span><span>非常同意</span></div>
        <div class="opts" id="q-opts"></div>
        <div class="q-sel-label" id="q-sel-label">&nbsp;</div>
      </div>
    </div>

    <div class="nav-row">
      <button class="btn outline" id="btn-prev" onclick="goPrev()">← 上一题</button>
      <button class="btn" id="btn-next" onclick="goNext()" disabled>下一题 →</button>
    </div>
    <div class="quiz-hint" id="quiz-hint">点选 1–7 分后自动进入下一题</div>
  </div>

  <!-- 结果页 -->
  <div id="page-result" style="display:none;">
    <div class="card center result-head">
      <span class="badge">你的测试结果</span>
      <div class="result-title" id="cat-title"></div>
      <div class="sub" id="cat-sub" style="margin-bottom:4px;"></div>
      <div class="score-row">
        <span>独立型均分：<b class="ind" id="ind-score"></b> / 7</span>
        <span>互依型均分：<b class="int" id="int-score"></b> / 7</span>
      </div>
    </div>

    <div class="card">
      <h2>自我建构维度图</h2>
      <div class="desc">两个维度的均分对比（量表范围 1–7，中点为 4）</div>
      <div class="chart-box"><canvas id="radarChart" height="300"></canvas></div>
      <div class="chart-box" style="margin-top:16px;"><canvas id="barChart" height="210"></canvas></div>
      <div class="chart-note">虚线为量表中点（4 分）：条形越过中点表示该倾向较明显</div>
    </div>

    <div class="card">
      <h2>独立性与互依性占比</h2>
      <div class="desc">以两个维度均分的相对比例计算（独立 + 互依 = 100%）</div>
      <div class="chart-box"><canvas id="pieChart" height="300"></canvas></div>
    </div>

    <div class="card advice">
      <h2>结果解读与建议</h2>
      <div class="desc">简单分类以量表中点 4 分为参考，并非正式分界值</div>
      <div id="advice-list"></div>
      <div class="note">说明：两个维度可以同时较高或较低，不应合并成单一总分；正式统计分析应保留两个连续得分。若任一均分恰好为 4 分，记为该维度中性，不强行归类。中文版尚未经独立的信效度验证，结果仅供自我探索参考。</div>
      <button class="btn outline block" onclick="location.reload()">↻ 重新测试</button>
    </div>

    <div class="footnote">
      Source page: https://uwaterloo.ca/wisdom-and-culture-lab/measures<br>
      Singelis, T. M. (1994). The measurement of independent and interdependent self-construals.<br>
      Personality and Social Psychology Bulletin, 20(5), 580–591.
    </div>
  </div>

</div>

<script>
/* ================= 量表数据 ================= */
var QUESTIONS = [
  { text: '我喜欢在很多方面保持独特，与他人不同。', dim: 'ind' },
  { text: '即使我非常不同意群体成员的意见，我也会避免争论。', dim: 'int' },
  { text: '不管别人怎么看，我都按自己的方式做事。', dim: 'ind' },
  { text: '我尊重谦虚的人。', dim: 'int' },
  { text: '我觉得以独立自主的方式行事很重要。', dim: 'ind' },
  { text: '为了我所在群体的利益，我愿意牺牲自己的利益。', dim: 'int' },
  { text: '我宁愿直接说"不"，也不愿冒着被误解的风险。', dim: 'ind' },
  { text: '拥有丰富的想象力对我很重要。', dim: 'ind' },
  { text: '我觉得自己的命运与周围人的命运紧密相连。', dim: 'int' },
  { text: '与刚认识的人相处时，我更愿意直接、坦率地表达。', dim: 'ind' },
  { text: '与他人合作让我感觉很好。', dim: 'int' },
  { text: '被单独表扬或奖励时，我感到自在。', dim: 'ind' },
  { text: '如果我的兄弟姐妹失败了，我会觉得自己有责任。', dim: 'int' },
  { text: '我常觉得我与他人的关系比我个人的成就更重要。', dim: 'int' },
  { text: '在会议上发言对我来说不成问题。', dim: 'ind' },
  { text: '无论和谁在一起，我的表现都一样。', dim: 'ind' },
  { text: '我的快乐取决于周围人的快乐。', dim: 'int' },
  { text: '如果一个群体需要我，即使我在其中并不开心，我也会留下来。', dim: 'int' },
  { text: '我会努力做对自己最有利的事，不管这会如何影响他人。', dim: 'ind' },
  { text: '对我来说，尊重群体做出的决定很重要。', dim: 'int' },
  { text: '独立于他人的个人身份对我非常重要。', dim: 'ind' },
  { text: '对我来说，维持群体内部的和谐很重要。', dim: 'int' },
  { text: '我在家里和在其他场合的表现一样。', dim: 'ind' },
  { text: '即使我更想做别的事，我通常也会顺从他人的意愿。', dim: 'int' }
];
var LIKERT = ['非常不同意','不同意','有点不同意','既不同意也不赞同','有点同意','同意','非常同意'];
var MID = 4;
var IND = '#4f46e5', INT = '#f43f5e';
var answers = new Array(24); // 0 表示未作答
var idx = 0;
var finished = false;

var CATEGORY = {
  'ind-dom': { title: '独立倾向较明显', color: IND, sub: '你更重视独特的自我、自主选择与直接表达', advice: [
    '你的自我建构以独立性为主：你重视个人独特性和自主决策，乐于坦率表达自己的观点，行为方式相对稳定、不太随场合改变。',
    '优势：独立判断让你在需要创新和坚持立场的场合表现出色；你不太容易被群体压力左右。',
    '建议：在保持独立主见的同时，可以有意识地练习倾听与共情——在团队决策前多问一句"大家怎么看"，会让你的直接表达更容易被接受。',
    '注意：直接说"不"固然高效，但在高互依文化（如东亚）的语境中，适度照顾对方的感受能减少不必要的摩擦。' ] },
  'int-dom': { title: '互依倾向较明显', color: INT, sub: '你更重视关系和谐、群体利益与他人的感受', advice: [
    '你的自我建构以互依性为主：你看重与他人的关系，愿意为群体利益做出让步，敏感于周围人的情绪，并把和谐看得很重要。',
    '优势：你在协作、维系关系和融入团队方面表现出色，是群体中可靠的"粘合剂"。',
    '建议：适度练习表达个人需求与边界——适当地说"不"、争取单独的认可，不会伤害关系，反而能让他人更了解真实的你。',
    '注意：过度压抑自己的意愿去迁就他人，长期来看可能造成疲惫或隐性不满，记得把"照顾自己"也放进待办清单。' ] },
  'both-high': { title: '两种倾向均较明显', color: '#7c3aed', sub: '你兼具独立与互依的双重自我，情境灵活度高', advice: [
    '你的独立性与互依性得分都高于中点，属于"双重自我建构"：你既能坚持自我、独立行事，也重视关系与群体和谐。',
    '优势：这种灵活的自我让你能在不同情境中切换自如——该表达时坦率直言，该协作时体贴配合。',
    '建议：留意两种倾向偶尔产生的内心拉扯（"我想做自己" vs "我不想让大家难堪"），提前想清楚自己的底线和优先级，可以减少决策时的内耗。',
    '这也常见于跨文化经历丰富或双文化背景的人群，是一种适应优势。' ] },
  'both-low': { title: '两种倾向均不明显', color: '#64748b', sub: '你的两个维度都低于中点，自我建构相对平缓', advice: [
    '你在独立性和互依性两个维度上的得分都低于中点，说明这些陈述与你的自我描述匹配度不高。',
    '可能的原因：你对这类概括性陈述本身不太认同，或者你的自我建构更多由其他维度（如具体角色、价值观）定义。',
    '建议：不必强行归入某一类型——可以结合具体生活场景回顾自己的行为：在需要坚持的场合和需要配合的场合，你分别是怎么做的？',
    '如果你的多数回答落在"既不同意也不赞同"附近，说明你倾向于审慎看待这类自我标签，这本身也是一种特点。' ] },
  'neutral': { title: '中性 / 边界情况', color: '#d97706', sub: '至少一个维度的均分恰好落在量表中点（4 分）', advice: [
    '有一个维度的均分恰好等于 4 分（量表中点），按照量表说明，这记为该维度中性，不强行归类。',
    '建议：关注你的两个具体均分（而不是分类标签），看看哪个维度更接近你的真实感受。',
    '正式的统计分析应保留两个连续得分，而非简单分类——本页下方的均分和图表比标签更有参考价值。' ] }
};

/* ================= 答题流程 ================= */
function showQuiz() {
  document.getElementById('page-intro').style.display = 'none';
  document.getElementById('page-quiz').style.display = 'block';
  idx = 0;
  for (var i = 0; i < 24; i++) if (!answers[i]) { idx = i; break; }
  renderQ();
  window.scrollTo(0, 0);
}

function answeredCount() {
  var n = 0;
  for (var i = 0; i < 24; i++) if (answers[i]) n++;
  return n;
}

function renderQ() {
  var q = QUESTIONS[idx];
  // 重建卡片以触发入场动画
  var card = document.getElementById('q-card');
  card.style.animation = 'none';
  void card.offsetWidth;
  card.style.animation = '';
  document.getElementById('q-step').textContent = '第 ' + (idx + 1) + ' 题 · 共 24 题';
  document.getElementById('q-text').textContent = q.text;
  var opts = document.getElementById('q-opts');
  opts.innerHTML = '';
  for (var v = 1; v <= 7; v++) {
    var b = document.createElement('button');
    b.className = 'opt' + (answers[idx] === v ? ' on' : '');
    b.textContent = v;
    b.title = v + ' ' + LIKERT[v - 1];
    (function (val, btn) {
      btn.onclick = function () { pick(val, btn); };
    })(v, b);
    opts.appendChild(b);
  }
  updateSelLabel();
  document.getElementById('q-now').textContent = idx + 1;
  var n = answeredCount();
  document.getElementById('q-count').textContent = n;
  document.getElementById('progress').style.width = (n / 24 * 100) + '%';
  document.getElementById('btn-prev').disabled = (idx === 0);
  var nextBtn = document.getElementById('btn-next');
  var hint = document.getElementById('quiz-hint');
  if (idx === 23) {
    nextBtn.textContent = '查看结果 →';
    nextBtn.disabled = (n < 24);
    hint.textContent = (n < 24) ? '还有 ' + (24 - n) + ' 题未作答，全部完成后才能查看结果' : '已完成全部作答，可以查看结果了';
  } else {
    nextBtn.textContent = '下一题 →';
    nextBtn.disabled = !answers[idx];
    hint.textContent = '点选 1–7 分后自动进入下一题';
  }
}

function updateSelLabel() {
  var el = document.getElementById('q-sel-label');
  el.textContent = answers[idx] ? answers[idx] + ' · ' + LIKERT[answers[idx] - 1] : ' ';
}

function pick(v, btn) {
  answers[idx] = v;
  var opts = btn.parentNode.children;
  for (var i = 0; i < opts.length; i++) opts[i].classList.remove('on');
  btn.classList.add('on');
  updateSelLabel();
  document.getElementById('q-count').textContent = answeredCount();
  document.getElementById('progress').style.width = (answeredCount() / 24 * 100) + '%';
  if (idx === 23) {
    var nextBtn = document.getElementById('btn-next');
    nextBtn.disabled = (answeredCount() < 24);
    document.getElementById('quiz-hint').textContent = (answeredCount() < 24)
      ? '还有 ' + (24 - answeredCount()) + ' 题未作答，全部完成后才能查看结果'
      : '已完成全部作答，可以查看结果了';
  } else {
    document.getElementById('btn-next').disabled = false;
    setTimeout(function () { goNext(); }, 280);
  }
}

function goPrev() {
  if (idx > 0) { idx--; renderQ(); }
  window.scrollTo(0, 0);
}

function goNext() {
  if (idx === 23) {
    if (answeredCount() === 24) showResult();
    return;
  }
  if (idx < 23) { idx++; renderQ(); }
  window.scrollTo(0, 0);
}

/* ================= 计分与分类 ================= */
function computeScores() {
  var ind = 0, int = 0, ni = 0, nt = 0;
  for (var i = 0; i < 24; i++) {
    if (QUESTIONS[i].dim === 'ind') { ind += answers[i]; ni++; }
    else { int += answers[i]; nt++; }
  }
  return { ind: ind / ni, int: int / nt };
}

function classify(s) {
  if (s.ind > MID && s.int < MID) return 'ind-dom';
  if (s.int > MID && s.ind < MID) return 'int-dom';
  if (s.ind > MID && s.int > MID) return 'both-high';
  if (s.ind < MID && s.int < MID) return 'both-low';
  return 'neutral';
}

/* ================= 结果展示 ================= */
function showResult() {
  finished = true;
  var s = computeScores();
  var cat = CATEGORY[classify(s)];
  document.getElementById('page-quiz').style.display = 'none';
  document.getElementById('page-result').style.display = 'block';
  document.getElementById('cat-title').textContent = cat.title;
  document.getElementById('cat-title').style.color = cat.color;
  document.getElementById('cat-sub').textContent = cat.sub;
  document.getElementById('ind-score').textContent = s.ind.toFixed(2);
  document.getElementById('int-score').textContent = s.int.toFixed(2);
  document.getElementById('advice-list').innerHTML =
    cat.advice.map(function (p) { return '<p>' + p + '</p>'; }).join('');
  drawAll(s);
  window.scrollTo(0, 0);
}

/* 高清画布：按容器宽度 × DPR 缩放，保证图表完整显示 */
function ctx2d(id) {
  var c = document.getElementById(id);
  var dpr = window.devicePixelRatio || 1;
  var w = c.parentNode.clientWidth || 600;
  var h = parseInt(c.getAttribute('height'), 10);
  c.width = w * dpr;
  c.height = h * dpr;
  c.style.height = h + 'px';
  var ctx = c.getContext('2d');
  ctx.scale(dpr, dpr);
  return { ctx: ctx, w: w, h: h };
}

function drawAll(s) {
  drawRadar(s);
  drawBar(s);
  drawPie(s);
}

window.addEventListener('resize', function () {
  if (finished) drawAll(computeScores());
});

/* 雷达图（两轴：独立 ↑ / 互依 ↓，网格 0–7） */
function drawRadar(s) {
  var r = ctx2d('radarChart'), ctx = r.ctx, W = r.w, H = r.h;
  ctx.clearRect(0, 0, W, H);
  var cx = W / 2, cy = H / 2 + 6;
  var R = Math.min(W / 2 - 66, H / 2 - 42);
  if (R < 60) R = 60;
  var data = [ { label: '独立型', val: s.ind, color: IND, ang: -Math.PI / 2 },
               { label: '互依型', val: s.int, color: INT, ang: Math.PI / 2 } ];
  var i, g;
  for (g = 1; g <= 7; g++) {
    ctx.beginPath(); ctx.arc(cx, cy, R * g / 7, 0, Math.PI * 2);
    ctx.strokeStyle = g === MID ? '#cbd5e1' : '#e8edf3';
    ctx.setLineDash(g === MID ? [4, 4] : []);
    ctx.stroke();
  }
  ctx.setLineDash([]);
  data.forEach(function (d) {
    ctx.beginPath();
    ctx.moveTo(cx, cy);
    ctx.lineTo(cx + R * Math.cos(d.ang), cy + R * Math.sin(d.ang));
    ctx.strokeStyle = '#cbd5e1'; ctx.stroke();
  });
  ctx.beginPath();
  ctx.moveTo(cx, cy);
  data.forEach(function (d) {
    var rr = R * d.val / 7;
    ctx.lineTo(cx + rr * Math.cos(d.ang), cy + rr * Math.sin(d.ang));
  });
  ctx.closePath();
  ctx.fillStyle = 'rgba(79,70,229,.20)'; ctx.fill();
  ctx.strokeStyle = IND; ctx.lineWidth = 2; ctx.stroke(); ctx.lineWidth = 1;
  data.forEach(function (d) {
    var rr = R * d.val / 7;
    var px = cx + rr * Math.cos(d.ang), py = cy + rr * Math.sin(d.ang);
    ctx.beginPath(); ctx.arc(px, py, 5, 0, Math.PI * 2);
    ctx.fillStyle = d.color; ctx.fill();
    ctx.strokeStyle = '#fff'; ctx.stroke();
    ctx.fillStyle = '#334155'; ctx.font = 'bold 14px sans-serif';
    ctx.textAlign = 'center';
    var ly = d.ang < 0 ? cy - R - 12 : cy + R + 20;
    ctx.fillText(d.label, cx, ly);
    ctx.font = '12px sans-serif'; ctx.fillStyle = d.color;
    ctx.fillText(d.val.toFixed(2) + ' / 7', cx, ly + 16);
  });
  ctx.font = '10px sans-serif'; ctx.fillStyle = '#cbd5e1'; ctx.textAlign = 'left';
  ctx.fillText('7', cx + R + 4, cy + 3);
  ctx.fillText('中点 4', cx + R * MID / 7 + 4, cy - 6);
}

/* 横向条形图（带中点参考线） */
function drawBar(s) {
  var r = ctx2d('barChart'), ctx = r.ctx, W = r.w, H = r.h;
  ctx.clearRect(0, 0, W, H);
  var padL = 62, padR = 16, padT = 12, padB = 26;
  var plotW = W - padL - padR, rowH = (H - padT - padB) / 2;
  var data = [ { label: '独立型', val: s.ind, color: IND },
               { label: '互依型', val: s.int, color: INT } ];
  var t;
  ctx.font = '10px sans-serif'; ctx.textAlign = 'center';
  for (t = 0; t <= 7; t++) {
    var x = padL + plotW * t / 7;
    ctx.strokeStyle = '#eef2f6';
    ctx.beginPath(); ctx.moveTo(x, padT); ctx.lineTo(x, H - padB); ctx.stroke();
    ctx.fillStyle = '#b6c2cf'; ctx.fillText(String(t), x, H - padB + 15);
  }
  var mx = padL + plotW * MID / 7;
  ctx.strokeStyle = '#94a3b8'; ctx.setLineDash([5, 4]);
  ctx.beginPath(); ctx.moveTo(mx, padT - 2); ctx.lineTo(mx, H - padB); ctx.stroke();
  ctx.setLineDash([]);
  data.forEach(function (d, i) {
    var y = padT + rowH * i + rowH / 2 - 15;
    var bw = Math.max(plotW * d.val / 7, 2);
    ctx.fillStyle = d.color;
    rounded(ctx, padL, y, bw, 30, 6); ctx.fill();
    ctx.fillStyle = '#334155'; ctx.font = '13px sans-serif'; ctx.textAlign = 'right';
    ctx.fillText(d.label, padL - 10, y + 20);
    ctx.fillStyle = '#fff'; ctx.font = 'bold 12px sans-serif'; ctx.textAlign = 'left';
    ctx.fillText(d.val.toFixed(2), padL + 8, y + 20);
    ctx.fillStyle = '#64748b'; ctx.font = '11px sans-serif';
    var tag = d.val > MID ? '▲ 高于中点' : (d.val < MID ? '▼ 低于中点' : '＝ 中点');
    ctx.fillText(tag, Math.min(padL + bw + 8, W - 70), y + 20);
  });
}

function rounded(ctx, x, y, w, h, rad) {
  ctx.beginPath();
  ctx.moveTo(x + rad, y);
  ctx.arcTo(x + w, y, x + w, y + h, rad);
  ctx.arcTo(x + w, y + h, x, y + h, rad);
  ctx.arcTo(x, y + h, x, y, rad);
  ctx.arcTo(x, y, x + w, y, rad);
  ctx.closePath();
}

/* 环形占比图（标签放在环内两侧，避免溢出） */
function drawPie(s) {
  var r = ctx2d('pieChart'), ctx = r.ctx, W = r.w, H = r.h;
  ctx.clearRect(0, 0, W, H);
  var cx = W / 2, cy = H / 2;
  var R = Math.min(W, H) / 2 - 26;
  if (R < 70) R = 70;
  var ir = R * 0.6;
  var total = s.ind + s.int;
  var segs = [ { pct: s.ind / total, color: IND, name: '独立性', val: s.ind },
               { pct: s.int / total, color: INT, name: '互依性', val: s.int } ];
  var gap = 0.05, start = -Math.PI / 2;
  segs.forEach(function (seg) {
    var a0 = start + gap / 2, a1 = start + seg.pct * Math.PI * 2 - gap / 2;
    ctx.beginPath();
    ctx.arc(cx, cy, R, a0, a1);
    ctx.arc(cx, cy, ir, a1, a0, true);
    ctx.closePath();
    ctx.fillStyle = seg.color; ctx.fill();
    var mid = (a0 + a1) / 2;
    var lr = (R + ir) / 2;
    ctx.fillStyle = '#fff';
    ctx.font = 'bold ' + Math.max(12, R * 0.13) + 'px sans-serif';
    ctx.textAlign = 'center';
    ctx.fillText(Math.round(seg.pct * 100) + '%', cx + lr * Math.cos(mid), cy + lr * Math.sin(mid) + 4);
    start += seg.pct * Math.PI * 2;
  });
  // 环内中心说明
  ctx.fillStyle = '#334155'; ctx.font = 'bold 13px sans-serif'; ctx.textAlign = 'center';
  ctx.fillText('自我建构占比', cx, cy - 4);
  ctx.fillStyle = '#94a3b8'; ctx.font = '11px sans-serif';
  ctx.fillText('按均分相对比例', cx, cy + 14);
  // 底部图例（两行居中，避免小屏溢出）
  ctx.textAlign = 'center'; ctx.font = '12px sans-serif';
  var ly1 = H - 32, ly2 = H - 14;
  ctx.fillStyle = IND;
  ctx.fillRect(cx - 118, ly1 - 9, 12, 12);
  ctx.fillStyle = '#334155';
  ctx.fillText('独立性 ' + Math.round(segs[0].pct * 100) + '%（均分 ' + segs[0].val.toFixed(2) + '）', cx + 8, ly1 + 2);
  ctx.fillStyle = INT;
  ctx.fillRect(cx - 118, ly2 - 9, 12, 12);
  ctx.fillStyle = '#334155';
  ctx.fillText('互依性 ' + Math.round(segs[1].pct * 100) + '%（均分 ' + segs[1].val.toFixed(2) + '）', cx + 8, ly2 + 2);
}
</script>
</body>
</html>
