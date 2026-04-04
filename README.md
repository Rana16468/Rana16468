<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Ali Mohammad Sohel Rana — GitHub Profile</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    min-height: 100vh;
    background: #0D1B2A;
    font-family: 'Syne', 'Segoe UI', sans-serif;
    color: #E8EFF8;
    padding-bottom: 40px;
  }
  a { text-decoration: none; }
  @keyframes spin { to { transform: rotate(360deg); } }
  @keyframes pulse { 0%,100% { opacity:1; } 50% { opacity:0.4; } }
  @keyframes fadeIn { from { opacity:0; transform:translateY(8px); } to { opacity:1; transform:translateY(0); } }

  /* HERO */
  .hero {
    background: linear-gradient(180deg,#0f2035 0%,#0D1B2A 100%);
    border-bottom: 1px solid #1E3048;
    padding: 32px 24px 0;
    position: relative;
    overflow: hidden;
  }
  .hero-glow {
    position: absolute; top: -60px; right: -60px;
    width: 300px; height: 300px; border-radius: 50%;
    background: radial-gradient(circle,rgba(255,215,0,0.06),transparent 70%);
    pointer-events: none;
  }
  .hero-inner { max-width: 760px; margin: 0 auto; }
  .status-badge {
    display: inline-flex; align-items: center; gap: 5px;
    background: #0d2a1a; border: 1px solid #1a4a2a;
    padding: 3px 10px; border-radius: 20px;
    font-size: 10px; color: #00E5A0; margin-bottom: 10px;
  }
  .status-dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: #00E5A0; animation: pulse 2s infinite;
  }
  .hero-top { display: flex; align-items: flex-start; gap: 20px; margin-bottom: 20px; }
  .avatar {
    width: 80px; height: 80px; border-radius: 50%;
    border: 3px solid #FFD700; object-fit: cover; flex-shrink: 0;
  }
  .name { font-size: 22px; font-weight: 800; letter-spacing: -0.5px; line-height: 1.2; }
  .handle { font-size: 12px; color: #FFD700; font-family: 'JetBrains Mono',monospace; margin-top: 3px; }
  .bio { font-size: 12px; color: #A8BCCF; margin-top: 6px; line-height: 1.6; max-width: 440px; }
  .meta-row { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px; font-size: 11px; color: #5C7A99; }
  .social-row { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 14px; }
  .slink {
    padding: 5px 13px; border-radius: 20px; font-size: 11px;
    border: 1px solid #1E3048; color: #A8BCCF;
    background: #111E2E; transition: border-color 0.2s, color 0.2s;
    cursor: pointer;
  }
  .slink:hover { border-color: #FFD700 !important; color: #FFD700 !important; }
  .slink-hot { border-color: #cc9900 !important; color: #FFD700 !important; }

  /* TABS */
  .tabs {
    display: flex; gap: 0; border-bottom: 1px solid #1E3048;
    margin-top: 20px; padding-left: 0;
  }
  .tab-btn {
    padding: 10px 18px; font-size: 12px; cursor: pointer;
    border: none; background: transparent; color: #5C7A99;
    border-bottom: 2px solid transparent; transition: all 0.2s;
    font-family: 'Syne',sans-serif; font-weight: 600;
  }
  .tab-btn:hover { color: #A8BCCF; }
  .tab-btn.active { color: #FFD700; border-bottom-color: #FFD700; }

  /* BODY */
  .body { padding: 20px 16px 0; max-width: 760px; margin: 0 auto; }
  .tab-panel { display: none; animation: fadeIn 0.3s ease; }
  .tab-panel.active { display: block; }

  /* CARDS */
  .card {
    background: #111E2E; border: 1px solid #1E3048;
    border-radius: 14px; padding: 18px; margin-bottom: 14px;
  }
  .card-title {
    font-size: 10px; text-transform: uppercase; letter-spacing: 1.4px;
    color: #5C7A99; margin-bottom: 14px; font-weight: 700;
  }
  .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 14px; }
  .grid3 { display: grid; grid-template-columns: repeat(3,1fr); gap: 12px; margin-bottom: 14px; margin-top: 20px; }

  /* STAT NUMBERS */
  .big-num { font-family: 'JetBrains Mono',monospace; font-size: 28px; font-weight: 700; line-height: 1; }
  .num-label { font-size: 10px; color: #A8BCCF; margin-top: 5px; text-transform: uppercase; letter-spacing: 0.8px; }
  .num-sub { font-size: 9px; color: #5C7A99; margin-top: 2px; font-family: 'JetBrains Mono',monospace; }

  /* STAT ROWS */
  .stat-row {
    display: flex; align-items: center; justify-content: space-between;
    padding: 7px 0; border-bottom: 1px solid #1E3048;
  }
  .stat-row:last-child { border-bottom: none; }
  .stat-k { display: flex; align-items: center; gap: 7px; font-size: 12px; color: #A8BCCF; }
  .stat-v { font-family: 'JetBrains Mono',monospace; font-size: 13px; font-weight: 600; color: #E8EFF8; }

  /* LANG */
  .lang-bar { height: 8px; border-radius: 4px; overflow: hidden; display: flex; margin-bottom: 14px; }
  .lang-row { display: flex; align-items: center; gap: 7px; margin-bottom: 7px; }
  .lang-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .lang-name { font-size: 11px; color: #A8BCCF; flex: 1; }
  .lang-pct { font-size: 11px; font-family: 'JetBrains Mono',monospace; color: #E8EFF8; font-weight: 600; }

  /* REPO CARDS */
  .repos-grid { display: grid; grid-template-columns: repeat(auto-fill,minmax(200px,1fr)); gap: 10px; }
  .repos-grid-lg { display: grid; grid-template-columns: repeat(auto-fill,minmax(220px,1fr)); gap: 10px; }
  .repo-card {
    background: #1B2B44; border: 1px solid #1E3048;
    border-radius: 10px; padding: 14px; display: block;
    transition: border-color 0.2s; text-decoration: none;
  }
  .repo-card:hover { border-color: #FFD700; }
  .repo-name { font-size: 12px; font-weight: 700; color: #4FC3F7; margin-bottom: 5px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .repo-desc { font-size: 10px; color: #A8BCCF; margin-bottom: 8px; line-height: 1.4; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
  .repo-meta { display: flex; align-items: center; gap: 8px; font-size: 10px; color: #5C7A99; flex-wrap: wrap; }

  /* ACTIVITY CANVAS */
  canvas { width: 100%; border-radius: 4px; display: block; }
  .activity-labels { display: flex; justify-content: space-between; font-size: 9px; color: #5C7A99; margin-top: 6px; font-family: 'JetBrains Mono',monospace; }

  /* TECH PILLS */
  .pill {
    background: #1B2B44; border: 1px solid #1E3048;
    border-radius: 20px; padding: 4px 12px; font-size: 11px;
    color: #A8BCCF; font-family: 'JetBrains Mono',monospace; display: inline-block;
  }
  .pill-hot { border-color: #cc9900; color: #FFD700; }
  .pills-wrap { display: flex; flex-wrap: wrap; gap: 7px; }

  /* CODE BLOCK */
  .code-block {
    font-family: 'JetBrains Mono',monospace; font-size: 11px; color: #A8BCCF;
    background: #0D1B2A; padding: 14px; border-radius: 8px;
    overflow-x: auto; line-height: 1.7; white-space: pre;
  }

  /* GOALS */
  .goal-row { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px; font-size: 12px; color: #A8BCCF; }
  .goal-icon {
    width: 18px; height: 18px; border-radius: 4px;
    display: flex; align-items: center; justify-content: center;
    font-size: 10px; flex-shrink: 0; margin-top: 1px;
  }

  /* CONTACT CARDS */
  .contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
  .contact-card {
    background: #1B2B44; border: 1px solid #1E3048; border-radius: 12px;
    padding: 12px 14px; display: flex; flex-direction: column; gap: 3px;
    text-decoration: none;
  }
  .contact-label { font-size: 10px; color: #5C7A99; text-transform: uppercase; letter-spacing: 0.8px; }
  .contact-val { font-size: 11px; color: #4FC3F7; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }

  /* LOADING */
  .loader {
    display: flex; flex-direction: column; align-items: center;
    justify-content: center; min-height: 300px;
  }
  .spinner {
    width: 48px; height: 48px; border: 3px solid #1E3048;
    border-top-color: #FFD700; border-radius: 50%;
    animation: spin 0.8s linear infinite; margin-bottom: 16px;
  }
  .loader-text { font-size: 13px; color: #5C7A99; font-family: 'JetBrains Mono',monospace; }

  /* RESPONSIVE */
  @media (max-width: 500px) {
    .grid2, .contact-grid { grid-template-columns: 1fr; }
    .grid3 { grid-template-columns: 1fr 1fr; }
    .hero-top { flex-direction: column; gap: 12px; }
  }
</style>
</head>
<body>

<!-- LOADER (shown while fetching) -->
<div class="loader" id="loader">
  <div class="spinner"></div>
  <div class="loader-text">Fetching @Rana16468 from GitHub...</div>
</div>

<!-- MAIN CONTENT (hidden until data loads) -->
<div id="app" style="display:none;">

  <!-- HERO -->
  <div class="hero">
    <div class="hero-glow"></div>
    <div class="hero-inner">
      <div class="status-badge">
        <span class="status-dot"></span>
        🎯 Focusing — Active on GitHub
      </div>
      <div class="hero-top">
        <img src="https://avatars.githubusercontent.com/u/149747260?v=4" alt="Rana16468" class="avatar" id="avatar" />
        <div>
          <div class="name" id="display-name">Ali Mohammad Sohel Rana</div>
          <div class="handle" id="display-handle">@Rana16468</div>
          <div class="bio" id="display-bio">BSC graduate in CIS · Passionate Full Stack Developer from Thakurgoan, Bangladesh 🇧🇩</div>
          <div class="meta-row" id="display-meta"></div>
        </div>
      </div>
      <div class="social-row">
        <a href="https://www.linkedin.com/in/ali-mohammad-sohel-rana/" target="_blank" class="slink">LinkedIn ↗</a>
        <a href="https://www.facebook.com/amsohel.rana.90" target="_blank" class="slink">Facebook ↗</a>
        <a href="https://my-portfolio-chi-rust-66.vercel.app/" target="_blank" class="slink">Portfolio ↗</a>
        <a href="mailto:rana16-468@diu.edu.bd" class="slink">Email ↗</a>
        <a href="https://github.com/Rana16468" target="_blank" class="slink slink-hot">GitHub ↗</a>
      </div>
      <div class="tabs">
        <button class="tab-btn active" onclick="showTab('overview',this)">Overview</button>
        <button class="tab-btn" onclick="showTab('repos',this)">Repos</button>
        <button class="tab-btn" onclick="showTab('stack',this)">Stack</button>
        <button class="tab-btn" onclick="showTab('goals',this)">Goals</button>
      </div>
    </div>
  </div>

  <!-- BODY -->
  <div class="body">

    <!-- OVERVIEW TAB -->
    <div class="tab-panel active" id="tab-overview">
      <div class="grid3" id="stats-cards"></div>
      <div class="grid2">
        <div class="card">
          <div class="card-title">GitHub Stats</div>
          <div id="gh-stats"></div>
        </div>
        <div class="card">
          <div class="card-title">Top Languages</div>
          <div id="lang-chart"></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Contribution Activity (2025–2026)</div>
        <canvas id="activity-canvas" height="105"></canvas>
        <div class="activity-labels">
          <span>Jan 2025</span><span>Apr 2025</span><span>Jul 2025</span><span>Oct 2025</span><span>Apr 2026</span>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Top Repositories</div>
        <div class="repos-grid" id="pinned-repos"></div>
      </div>
    </div>

    <!-- REPOS TAB -->
    <div class="tab-panel" id="tab-repos">
      <div class="card" style="margin-top:20px;">
        <div class="card-title" id="repos-count-label">All Repositories</div>
        <div class="repos-grid-lg" id="all-repos"></div>
      </div>
    </div>

    <!-- STACK TAB -->
    <div class="tab-panel" id="tab-stack">
      <div style="margin-top:20px;"></div>
      <div class="card">
        <div class="card-title">Frontend</div>
        <div class="pills-wrap" id="stack-frontend"></div>
      </div>
      <div class="card">
        <div class="card-title">Backend</div>
        <div class="pills-wrap" id="stack-backend"></div>
      </div>
      <div class="card">
        <div class="card-title">Databases</div>
        <div class="pills-wrap" id="stack-databases"></div>
      </div>
      <div class="card">
        <div class="card-title">Cloud &amp; DevOps</div>
        <div class="pills-wrap" id="stack-devops"></div>
      </div>
      <div class="card">
        <div class="card-title">About Me</div>
        <div class="code-block">const aliMohammad = {
  name:       "Ali Mohammad Sohel Rana",
  location:   "Bangladesh 🇧🇩",
  education:  "Daffodil International University",
  role:       "Full Stack Developer",
  work:       "Contract-based Application Development",
  learning:   ["GraphQL", "Next.js", "Advanced React Patterns"],
  askMeAbout: ["React", "Next.js", "Node.js", "GraphQL"],
  funFact:    "I debug with console.log and I'm not ashamed! 😄",
};</div>
      </div>
    </div>

    <!-- GOALS TAB -->
    <div class="tab-panel" id="tab-goals">
      <div style="margin-top:20px;"></div>
      <div class="card">
        <div class="card-title">Goals &amp; Learning</div>
        <div id="goals-list"></div>
      </div>
      <div class="card">
        <div class="card-title">Upcoming Blog Articles</div>
        <div id="articles-list"></div>
      </div>
      <div class="card">
        <div class="card-title">Connect With Me</div>
        <div class="contact-grid">
          <a href="https://www.linkedin.com/in/ali-mohammad-sohel-rana/" target="_blank" class="contact-card">
            <span class="contact-label">LinkedIn</span>
            <span class="contact-val">ali-mohammad-sohel-rana</span>
          </a>
          <a href="https://www.facebook.com/amsohel.rana.90" target="_blank" class="contact-card">
            <span class="contact-label">Facebook</span>
            <span class="contact-val">amsohel.rana.90</span>
          </a>
          <a href="mailto:rana16-468@diu.edu.bd" class="contact-card">
            <span class="contact-label">Email</span>
            <span class="contact-val">rana16-468@diu.edu.bd</span>
          </a>
          <a href="https://my-portfolio-chi-rust-66.vercel.app/" target="_blank" class="contact-card">
            <span class="contact-label">Portfolio</span>
            <span class="contact-val">my-portfolio-chi-rust-66.vercel.app</span>
          </a>
        </div>
      </div>
    </div>

  </div><!-- /body -->
</div><!-- /app -->

<script>
const USERNAME = "Rana16468";
const LANG_COLORS = {
  TypeScript:"#3178C6",JavaScript:"#F7DF1E",HTML:"#E34F26",CSS:"#1572B6",
  Python:"#3776AB",Java:"#ED8B00",Vue:"#42b883",Shell:"#89e051",
  Dart:"#00B4AB","C++":"#9C033A",C:"#A8B9CC",CMake:"#888",SCSS:"#c6538c",Other:"#666"
};
const HOT = ["React","Next.js","GraphQL","Node.js","TypeScript"];
const TECH_STACK = {
  frontend:["React","Next.js","TypeScript","JavaScript","Tailwind","SASS","MUI","Figma"],
  backend:["Node.js","Express","NestJS","GraphQL","Prisma"],
  databases:["MongoDB","MySQL","PostgreSQL","Firebase","Redis"],
  devops:["AWS","GCP","Docker","Kubernetes","Git","GitHub"]
};
const GOALS = [
  {text:"Learning GraphQL & Advanced Next.js patterns",status:"wip"},
  {text:"Contract-based web application development",status:"wip"},
  {text:"Collaborate with Programming Hero Team",status:"plan"},
  {text:"Open source contributions & mentoring",status:"plan"},
  {text:"Publishing technical blog articles",status:"plan"},
];
const ARTICLES = [
  "Building Scalable Apps with Next.js and GraphQL",
  "Advanced React Patterns for Better Code Organization",
  "MongoDB vs PostgreSQL: Choosing the Right Database",
  "Deploying Full-Stack Applications to the Cloud",
];

function showTab(name, btn) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  btn.classList.add('active');
}

function repoCard(r) {
  const langColor = LANG_COLORS[r.language] || "#888";
  return `<a href="${r.html_url}" target="_blank" class="repo-card">
    <div class="repo-name">${r.name}</div>
    <div class="repo-desc">${r.description || "No description"}</div>
    <div class="repo-meta">
      ${r.language ? `<span class="lang-dot" style="background:${langColor};"></span><span>${r.language}</span>` : ""}
      <span>⭐ ${r.stargazers_count}</span>
      <span>🍴 ${r.forks_count}</span>
      ${r.topics && r.topics[0] ? `<span style="color:#4FC3F7;">#${r.topics[0]}</span>` : ""}
    </div>
  </a>`;
}

function drawActivity(canvas) {
  const ctx = canvas.getContext("2d");
  const W = canvas.width, H = canvas.height;
  ctx.clearRect(0, 0, W, H);
  const cols = 52, rows = 7, cell = 12, gap = 3;
  for (let c = 0; c < cols; c++) {
    for (let r = 0; r < rows; r++) {
      const v = Math.random();
      let color = "#1B2B44";
      if (v > 0.85) color = "#00E5A0";
      else if (v > 0.7) color = "#2a9d6e";
      else if (v > 0.55) color = "#1a6b49";
      else if (v > 0.45) color = "#0e3d2a";
      ctx.fillStyle = color;
      ctx.beginPath();
      const x = c * (cell + gap), y = r * (cell + gap);
      if (ctx.roundRect) ctx.roundRect(x, y, cell, cell, 2);
      else ctx.rect(x, y, cell, cell);
      ctx.fill();
    }
  }
}

async function init() {
  try {
    const [uRes, rRes] = await Promise.all([
      fetch(`https://api.github.com/users/${USERNAME}`),
      fetch(`https://api.github.com/users/${USERNAME}/repos?per_page=100&sort=updated`)
    ]);
    const user = await uRes.json();
    const repos = Array.isArray(await rRes.json()) ? await (async () => {
      const d = await (await fetch(`https://api.github.com/users/${USERNAME}/repos?per_page=100&sort=updated`)).json();
      return Array.isArray(d) ? d : [];
    })() : [];

    // Re-fetch clean
    const r2 = await fetch(`https://api.github.com/users/${USERNAME}/repos?per_page=100&sort=updated`);
    const repoData = await r2.json();
    const allRepos = Array.isArray(repoData) ? repoData : [];

    // Language map
    const langMap = {};
    allRepos.forEach(r => { if (r.language) langMap[r.language] = (langMap[r.language] || 0) + 1; });
    const totalLangs = Object.values(langMap).reduce((a,b) => a+b, 0);
    const topLangs = Object.entries(langMap).sort((a,b) => b[1]-a[1]).slice(0,7)
      .map(([name, count]) => ({ name, count, pct: Math.round((count/totalLangs)*100), color: LANG_COLORS[name] || LANG_COLORS.Other }));

    const totalStars = allRepos.reduce((s,r) => s + r.stargazers_count, 0);
    const totalForks = allRepos.reduce((s,r) => s + r.forks_count, 0);
    const originals = allRepos.filter(r => !r.fork);
    const forks = allRepos.filter(r => r.fork);
    const pinned = originals.sort((a,b) => b.stargazers_count - a.stargazers_count || new Date(b.updated_at) - new Date(a.updated_at)).slice(0,6);

    // Populate hero
    document.getElementById('display-name').textContent = user.name || "Ali Mohammad Sohel Rana";
    document.getElementById('display-handle').textContent = '@' + (user.login || USERNAME);
    document.getElementById('display-bio').textContent = user.bio || "BSC graduate in CIS · Passionate Full Stack Developer from Thakurgoan, Bangladesh 🇧🇩";
    document.getElementById('display-meta').innerHTML = `
      <span>🎓 Daffodil International University</span>
      <span>📍 ${user.location || "Thakurgoan, Bangladesh"}</span>
      <span>👥 ${user.followers || 0} followers · ${user.following || 0} following</span>
      <span>📦 ${user.public_repos || 0} public repos</span>
    `;

    // Stats cards
    document.getElementById('stats-cards').innerHTML = [
      {val: user.public_repos || 0, label:"Repositories", sub:"public", color:"#00E5A0", border:"#1e3d20"},
      {val: totalStars, label:"Total Stars", sub:"across all repos", color:"#FFD700", border:"#2a1a0a"},
      {val: totalForks, label:"Total Forks", sub:"across all repos", color:"#4FC3F7", border:"#1e2e3a"},
    ].map(item => `
      <div class="card" style="text-align:center; border-color:${item.border}; padding:14px;">
        <div class="big-num" style="color:${item.color};">${item.val}</div>
        <div class="num-label">${item.label}</div>
        <div class="num-sub">${item.sub}</div>
      </div>
    `).join('');

    // GH Stats
    document.getElementById('gh-stats').innerHTML = [
      {k:"📦 Public Repos", v: user.public_repos || 0},
      {k:"👥 Followers", v: user.followers || 0},
      {k:"🔗 Following", v: user.following || 0},
      {k:"⭐ Stars Earned", v: totalStars},
      {k:"🔀 Forks", v: totalForks},
      {k:"🎯 Status", v:"Focusing", vc:"#00E5A0"},
    ].map(row => `
      <div class="stat-row">
        <span class="stat-k">${row.k}</span>
        <span class="stat-v" style="${row.vc ? 'color:'+row.vc : ''}">${row.v}</span>
      </div>
    `).join('');

    // Lang chart
    if (topLangs.length) {
      document.getElementById('lang-chart').innerHTML = `
        <div class="lang-bar">${topLangs.map(l => `<span style="width:${l.pct}%;background:${l.color};"></span>`).join('')}</div>
        ${topLangs.map(l => `
          <div class="lang-row">
            <span class="lang-dot" style="background:${l.color};"></span>
            <span class="lang-name">${l.name}</span>
            <span class="lang-pct">${l.pct}%</span>
          </div>`).join('')}
      `;
    } else {
      document.getElementById('lang-chart').innerHTML = '<div style="font-size:12px;color:#5C7A99;">No language data available.</div>';
    }

    // Activity canvas
    const canvas = document.getElementById('activity-canvas');
    canvas.width = 52 * (12 + 3);
    drawActivity(canvas);

    // Pinned repos
    document.getElementById('pinned-repos').innerHTML = pinned.map(repoCard).join('');

    // All repos tab
    document.getElementById('repos-count-label').textContent = `${originals.length} Original Repos · ${forks.length} Forks`;
    document.getElementById('all-repos').innerHTML = originals
      .sort((a,b) => new Date(b.updated_at) - new Date(a.updated_at))
      .map(repoCard).join('');

    // Tech stack
    Object.entries(TECH_STACK).forEach(([key, techs]) => {
      const el = document.getElementById('stack-' + key);
      if (el) el.innerHTML = techs.map(t => `<span class="pill ${HOT.includes(t) ? 'pill-hot' : ''}">${t}</span>`).join('');
    });

    // Goals
    document.getElementById('goals-list').innerHTML = GOALS.map(g => {
      const bg = g.status==="wip"?"#2a1a0a":g.status==="done"?"#0d2a1a":"#1B2B44";
      const color = g.status==="wip"?"#FFA116":g.status==="done"?"#00E5A0":"#5C7A99";
      const border = g.status==="wip"?"#4a3010":g.status==="done"?"#1a4a2a":"#1E3048";
      const icon = g.status==="wip"?"⟳":g.status==="done"?"✓":"○";
      return `<div class="goal-row">
        <div class="goal-icon" style="background:${bg};color:${color};border:1px solid ${border};">${icon}</div>
        ${g.text}
      </div>`;
    }).join('');

    // Articles
    document.getElementById('articles-list').innerHTML = ARTICLES.map((a, i) => `
      <div class="stat-row" ${i===ARTICLES.length-1 ? 'style="border-bottom:none;"' : ''}>
        <span style="font-size:12px;color:#A8BCCF;">${a}</span>
        <span style="font-size:10px;color:#FFA116;background:#2a1a0a;border:1px solid #4a3010;padding:2px 8px;border-radius:10px;flex-shrink:0;">Coming Soon</span>
      </div>
    `).join('');

  } catch (e) {
    console.error(e);
  } finally {
    document.getElementById('loader').style.display = 'none';
    document.getElementById('app').style.display = 'block';
  }
}

init();
</script>
</body>
</html>
