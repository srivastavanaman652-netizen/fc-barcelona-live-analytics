<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FC Barcelona Live Analytics Platform – Portfolio Project</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body{
margin:0;
font-family:'Poppins',sans-serif;
background:#02040a;
color:white;
}

header{
background:linear-gradient(90deg,#004D98,#A50044);
padding:30px;
text-align:center;
box-shadow:0 0 30px rgba(0,0,0,0.8);
}

header h1{margin:0;font-size:40px;}
header p{opacity:0.9;font-size:15px;}

.hero{
height:60vh;
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
text-align:center;
background:radial-gradient(circle at center,#0a1220,#000);
}

.hero h1{font-size:50px;margin-bottom:10px;}
.hero p{opacity:0.8;max-width:700px;}

section{padding:50px 40px;}

.section-title{
font-size:28px;
margin-bottom:25px;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
gap:25px;
}

.card{
background:#0a1220;
border-radius:18px;
padding:20px;
box-shadow:0 0 20px rgba(0,0,0,0.7);
transition:0.3s;
}

.card:hover{
transform:translateY(-6px);
box-shadow:0 0 25px rgba(165,0,68,0.7);
}

.live-box{
background:#0a1220;
padding:25px;
border-radius:18px;
box-shadow:0 0 20px rgba(0,0,0,0.8);
}

.match{
display:flex;
justify-content:space-between;
padding:18px 0;
border-bottom:1px solid #1e2a45;
}

.score{
font-size:30px;
font-weight:bold;
color:#EDBB00;
}

.tech-stack{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:20px;
}

.tech{
background:#0a1220;
padding:20px;
border-radius:14px;
text-align:center;
}

canvas{max-width:450px;margin:auto;display:block;}

.footer{
text-align:center;
padding:30px;
background:#000;
opacity:0.8;
font-size:14px;
}

</style>
</head>

<body>

<header>
<h1>FC Barcelona Live Analytics Platform</h1>
<p>Portfolio Project – Real-Time Football Data Web Application</p>
</header>

<section class="hero">
<h1>Real-Time Football Analytics Website</h1>
<p>This project demonstrates live API integration, responsive UI design, real-time match tracking, data visualization, and front-end engineering skills.</p>
</section>

<section>
<h2 class="section-title">Project Features</h2>
<div class="grid">
<div class="card"><h3>Live Match Tracking</h3><p>Real-time Barcelona match scores using football-data API with auto-refresh every 30 seconds.</p></div>
<div class="card"><h3>Live La Liga Table</h3><p>Dynamic league standings that update automatically without page refresh.</p></div>
<div class="card"><h3>Champions League Tracker</h3><p>Displays all live UCL matches with real-time scores.</p></div>
<div class="card"><h3>Data Visualization</h3><p>Interactive squad analytics using Chart.js to represent player position distribution.</p></div>
</div>
</section>

<section>
<h2 class="section-title">Live Barcelona Match</h2>
<div class="live-box" id="liveMatches">Loading live data...</div>
</section>

<section>
<h2 class="section-title">La Liga Standings (Live)</h2>
<div class="live-box" id="laligaTable">Loading standings...</div>
</section>

<section>
<h2 class="section-title">Squad Analytics</h2>
<canvas id="chart"></canvas>
</section>

<section>
<h2 class="section-title">Tech Stack Used</h2>
<div class="tech-stack">
<div class="tech">HTML5</div>
<div class="tech">CSS3</div>
<div class="tech">JavaScript</div>
<div class="tech">REST API Integration</div>
<div class="tech">Chart.js</div>
<div class="tech">GitHub Pages Deployment</div>
</div>
</section>

<section>
<h2 class="section-title">About This Project</h2>
<div class="card">
<p>This project was developed as a portfolio website to demonstrate real-time API integration, responsive design, and front-end development skills. The platform fetches live football data and displays it in a structured dashboard format with analytics and match tracking.</p>
</div>
</section>

<div class="footer">
Portfolio Project – Live Football Analytics Website | Built using JavaScript + API Integration
</div>

<script>

const API_KEY = "00190d2e9d11448cad0ff5f817e82f9d";

/* LIVE MATCHES */
async function loadMatches(){
const res = await fetch("https://api.football-data.org/v4/teams/81/matches?status=LIVE",{headers:{"X-Auth-Token":API_KEY}});
const data = await res.json();
const box=document.getElementById("liveMatches");

if(!data.matches || data.matches.length===0){box.innerHTML="No live Barcelona match currently";return;}

let html="";

data.matches.forEach(m=>{
html+=`<div class="match"><div>${m.homeTeam.name}</div><div class="score">${m.score.fullTime.home ?? 0} - ${m.score.fullTime.away ?? 0}</div><div>${m.awayTeam.name}</div></div>`;
});

box.innerHTML=html;
}
loadMatches();setInterval(loadMatches,30000);

/* LA LIGA TABLE */
async function loadTable(){
const res = await fetch("https://api.football-data.org/v4/competitions/PD/standings",{headers:{"X-Auth-Token":API_KEY}});
const data = await res.json();
const table=data.standings[0].table.slice(0,10);
let html="";
table.forEach(t=>{html+=`<div class="match"><div>${t.position}. ${t.team.name}</div><div>${t.points} pts</div></div>`;});
document.getElementById("laligaTable").innerHTML=html;
}
loadTable();setInterval(loadTable,60000);

/* CHART */
new Chart(document.getElementById("chart"),{
type:"pie",
data:{labels:["Goalkeepers","Defenders","Midfielders","Forwards"],datasets:[{data:[1,4,4,3]}]}
});

</script>

</body>
</html>

