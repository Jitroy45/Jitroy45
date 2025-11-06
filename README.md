<!-- LOKI | Electrical Engineer Portfolio -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>LOKI</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500&display=swap');
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      background:#000; color:#eee; font-family:'JetBrains Mono',monospace;
      line-height:1.6; padding:2rem; min-height:100vh;
    }
    .container { max-width:960px; margin:auto; }
    h1 { font-size:2rem; font-weight:400; text-align:center; margin:1.5rem 0; }
    h3 { font-size:1.1rem; font-weight:300; text-align:center; color:#aaa; margin-bottom:2rem; }
    hr { border:none; border-top:1px solid #333; margin:2.5rem 0; }
    section { margin-bottom:3rem; }
    .grid { display:grid; grid-template-columns:1fr 1fr; gap:1.5rem; }
    @media(max-width:640px){ .grid{grid-template-columns:1fr;} }
    .card { background:#111; padding:1.2rem; border:1px solid #222; border-radius:4px; }
    .card h4 { color:#0f0; font-size:0.95rem; margin-bottom:0.5rem; }
    .line { height:1px; background:linear-gradient(90deg,#0f0 0%,#0f0 50%,transparent 100%); margin:0.8rem 0; }
    pre { background:#080808; padding:1rem; border-radius:4px; overflow-x:auto; font-size:0.85rem; border:1px solid #222; }
    .plot { width:100%; height:180px; background:#080808; border:1px solid #222; border-radius:4px; position:relative; overflow:hidden; }
    .plot svg { width:100%; height:100%; }
    footer { text-align:center; color:#555; font-size:0.8rem; margin-top:4rem; }
    a { color:#0f8; text-decoration:none; }
    a:hover { text-decoration:underline; }
  </style>
</head>
<body>
<div class="container">

<h1>LOKI</h1>
<h3>Power Systems • Renewable Integration • Electromagnetic Design</h3>

<hr>

<section>
<div class="grid">
  <div class="card">
    <h4>Grid Stability</h4>
    <div class="line"></div>
    <div class="plot" id="plot1"></div>
  </div>
  <div class="card">
    <h4>PV Yield Forecast</h4>
    <div class="line"></div>
    <div class="plot" id="plot2"></div>
  </div>
</div>
</section>

<section>
<div class="grid">
  <div class="card">
    <h4>PMLSM Thrust Ripple</h4>
    <div class="line"></div>
    <pre>% FEMM + MATLAB
femm.mi_addmaterial('NdFeB',1.2,1.2,1.049e6);
% → Ripple < 1.2%</pre>
  </div>
  <div class="card">
    <h4>Grid-Forming MPC</h4>
    <div class="line"></div>
    <pre>A = [0 -ω; ω 0]; B = [1/L; 0];
mpcobj.Weights.Output = [10 10];</pre>
  </div>
</div>
</section>

<hr>

<footer>
  <a href="lokenathroy2003@gmail.com">contact</a> • 
  <a href="https://github.com/Jitroy45">github</a> • 
</footer>

</div>

<script>
// Minimal line plot engine
function drawPlot(id, data, color='#0f0') {
  const canvas = document.getElementById(id);
  const svg = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
  svg.setAttribute('viewBox', '0 0 100 30');
  canvas.appendChild(svg);

  const path = document.createElementNS('http://www.w3.org/2000/svg', 'path');
  let d = 'M0,15';
  data.forEach((y,i) => d += ` L${i*(100/(data.length-1))},${15-y*12}`);
  path.setAttribute('d', d);
  path.setAttribute('stroke', color);
  path.setAttribute('stroke-width', '1.2');
  path.setAttribute('fill', 'none');
  path.setAttribute('stroke-linecap', 'round');
  svg.appendChild(path);
}

// Simulate real-time data
setInterval(() => {
  const grid = Array.from({length:50}, () => 0.5 + Math.sin(Date.now()/1000)*0.1 + Math.random()*0.05);
  const pv = Array.from({length:50}, (_,i) => Math.max(0, Math.sin(i/15)*0.8 + 0.2 + Math.random()*0.1));
  document.getElementById('plot1').innerHTML=''; 
  document.getElementById('plot2').innerHTML='';
  drawPlot('plot1', grid, '#0f8');
  drawPlot('plot2', pv, '#0f0');
}, 1200);

window.onload = () => {
  drawPlot('plot1', Array(50).fill(0.5), '#0f8');
  drawPlot('plot2', Array(50).fill(0.3), '#0f0');
};
</script>
</body>
</html>
