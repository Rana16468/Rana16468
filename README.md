import { useState, useEffect, useRef } from "react";

const USERNAME = "Rana16468";
const GH = `https://api.github.com/users/${USERNAME}`;
const GH_REPOS = `https://api.github.com/users/${USERNAME}/repos?per_page=100&sort=updated`;
const AVATAR = `https://avatars.githubusercontent.com/u/149747260?v=4`;

const TECH_STACK = {
  Frontend: ["React","Next.js","TypeScript","JavaScript","Tailwind","SASS","MUI","Figma"],
  Backend: ["Node.js","Express","NestJS","GraphQL","Prisma"],
  Databases: ["MongoDB","MySQL","PostgreSQL","Firebase","Redis"],
  "Cloud & DevOps": ["AWS","GCP","Docker","Kubernetes","Git","GitHub"],
};

const LANG_COLORS = {
  TypeScript:"#3178C6", JavaScript:"#F7DF1E", HTML:"#E34F26",
  CSS:"#1572B6", Python:"#3776AB", Java:"#ED8B00", Vue:"#42b883",
  Shell:"#89e051", Dart:"#00B4AB", "C++":"#9C033A", C:"#A8B9CC",
  CMake:"#888", SCSS:"#c6538c", Other:"#666",
};

const SOCIALS = [
  { label:"LinkedIn", url:"https://www.linkedin.com/in/ali-mohammad-sohel-rana/", icon:"in", color:"#0A66C2" },
  { label:"Facebook", url:"https://www.facebook.com/amsohel.rana.90", icon:"f", color:"#1877F2" },
  { label:"Portfolio", url:"https://my-portfolio-chi-rust-66.vercel.app/", icon:"↗", color:"#FFD700" },
  { label:"Email", url:"mailto:rana16-468@diu.edu.bd", icon:"@", color:"#EA4335" },
];

const GOALS = [
  { text:"Learning GraphQL & Advanced Next.js patterns", status:"wip" },
  { text:"Contract-based web application development", status:"wip" },
  { text:"Collaborate with Programming Hero Team", status:"plan" },
  { text:"Open source contributions & mentoring", status:"plan" },
  { text:"Publishing technical blog articles", status:"plan" },
];

const ARTICLES = [
  "Building Scalable Apps with Next.js and GraphQL",
  "Advanced React Patterns for Better Code Organization",
  "MongoDB vs PostgreSQL: Choosing the Right Database",
  "Deploying Full-Stack Applications to the Cloud",
];

export default function App() {
  const [user, setUser] = useState(null);
  const [repos, setRepos] = useState([]);
  const [langs, setLangs] = useState({});
  const [loading, setLoading] = useState(true);
  const [tab, setTab] = useState("overview");
  const canvasRef = useRef(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const [uRes, rRes] = await Promise.all([
          fetch(GH), fetch(GH_REPOS)
        ]);
        const userData = await uRes.json();
        const repoData = await rRes.json();
        setUser(userData);
        setRepos(Array.isArray(repoData) ? repoData : []);
        const langMap = {};
        repoData.forEach(r => {
          if (r.language) langMap[r.language] = (langMap[r.language] || 0) + 1;
        });
        setLangs(langMap);
      } catch (e) {
        console.error(e);
      } finally {
        setLoading(false);
      }
    }
    fetchData();
  }, []);

  useEffect(() => {
    if (!canvasRef.current) return;
    drawActivity(canvasRef.current);
  }, [repos]);

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
        ctx.roundRect(x, y, cell, cell, 2);
        ctx.fill();
      }
    }
  }

  const totalLangs = Object.values(langs).reduce((a, b) => a + b, 0);
  const topLangs = Object.entries(langs)
    .sort((a, b) => b[1] - a[1])
    .slice(0, 7)
    .map(([name, count]) => ({
      name, count,
      pct: Math.round((count / totalLangs) * 100),
      color: LANG_COLORS[name] || LANG_COLORS.Other
    }));

  const pinnedRepos = repos
    .filter(r => !r.fork)
    .sort((a, b) => b.stargazers_count - a.stargazers_count || new Date(b.updated_at) - new Date(a.updated_at))
    .slice(0, 6);

  const totalStars = repos.reduce((s, r) => s + r.stargazers_count, 0);
  const totalForks = repos.reduce((s, r) => s + r.forks_count, 0);

  const s = {
    root: {
      minHeight:"100vh", background:"#0D1B2A",
      fontFamily:"'Syne', 'Segoe UI', sans-serif", color:"#E8EFF8",
      padding:"0 0 40px",
    },
    hero: {
      background:"linear-gradient(180deg,#0f2035 0%,#0D1B2A 100%)",
      borderBottom:"1px solid #1E3048", padding:"32px 24px 0",
      position:"relative", overflow:"hidden",
    },
    heroGlow: {
      position:"absolute", top:"-60px", right:"-60px",
      width:"300px", height:"300px", borderRadius:"50%",
      background:"radial-gradient(circle,rgba(255,215,0,0.06),transparent 70%)",
      pointerEvents:"none",
    },
    heroTop: { display:"flex", alignItems:"flex-start", gap:"20px", marginBottom:"20px" },
    avatar: {
      width:"80px", height:"80px", borderRadius:"50%",
      border:"3px solid #FFD700", objectFit:"cover", flexShrink:0,
    },
    name: { fontSize:"22px", fontWeight:"800", letterSpacing:"-0.5px", lineHeight:1.2 },
    handle: { fontSize:"12px", color:"#FFD700", fontFamily:"'JetBrains Mono',monospace", marginTop:"3px" },
    bio: { fontSize:"12px", color:"#A8BCCF", marginTop:"6px", lineHeight:1.6, maxWidth:"440px" },
    metaRow: { display:"flex", flexWrap:"wrap", gap:"10px", marginTop:"10px", fontSize:"11px", color:"#5C7A99" },
    statusBadge: {
      display:"inline-flex", alignItems:"center", gap:"5px",
      background:"#0d2a1a", border:"1px solid #1a4a2a",
      padding:"3px 10px", borderRadius:"20px", fontSize:"10px",
      color:"#00E5A0", marginBottom:"10px",
    },
    statusDot: {
      width:"6px", height:"6px", borderRadius:"50%", background:"#00E5A0",
      animation:"pulse 2s infinite",
    },
    socialRow: { display:"flex", gap:"8px", flexWrap:"wrap", marginTop:"14px", paddingBottom:"0" },
    slink: {
      padding:"5px 13px", borderRadius:"20px", fontSize:"11px",
      border:"1px solid #1E3048", color:"#A8BCCF",
      textDecoration:"none", cursor:"pointer",
      background:"#111E2E", transition:"border-color 0.2s",
    },
    tabs: {
      display:"flex", gap:"0", borderBottom:"1px solid #1E3048",
      marginTop:"20px", paddingLeft:"24px",
    },
    tab: {
      padding:"10px 18px", fontSize:"12px", cursor:"pointer",
      border:"none", background:"transparent", color:"#5C7A99",
      borderBottom:"2px solid transparent", transition:"all 0.2s",
      fontFamily:"'Syne',sans-serif", fontWeight:"600",
    },
    tabActive: {
      color:"#FFD700", borderBottomColor:"#FFD700",
    },
    body: { padding:"20px 16px 0", maxWidth:"760px", margin:"0 auto" },
    card: {
      background:"#111E2E", border:"1px solid #1E3048",
      borderRadius:"14px", padding:"18px", marginBottom:"14px",
    },
    cardTitle: {
      fontSize:"10px", textTransform:"uppercase", letterSpacing:"1.4px",
      color:"#5C7A99", marginBottom:"14px", fontWeight:"700",
    },
    grid2: { display:"grid", gridTemplateColumns:"1fr 1fr", gap:"14px", marginBottom:"14px" },
    grid3: { display:"grid", gridTemplateColumns:"repeat(3,1fr)", gap:"12px", marginBottom:"14px" },
    bigNum: { fontFamily:"'JetBrains Mono',monospace", fontSize:"28px", fontWeight:"700", lineHeight:1 },
    numLabel: { fontSize:"10px", color:"#A8BCCF", marginTop:"5px", textTransform:"uppercase", letterSpacing:"0.8px" },
    numSub: { fontSize:"9px", color:"#5C7A99", marginTop:"2px", fontFamily:"'JetBrains Mono',monospace" },
    repoCard: {
      background:"#1B2B44", border:"1px solid #1E3048",
      borderRadius:"10px", padding:"14px",
    },
    repoName: { fontSize:"12px", fontWeight:"700", color:"#4FC3F7", marginBottom:"5px",
      whiteSpace:"nowrap", overflow:"hidden", textOverflow:"ellipsis" },
    repoDesc: { fontSize:"10px", color:"#A8BCCF", marginBottom:"8px", lineHeight:1.4,
      display:"-webkit-box", WebkitLineClamp:2, WebkitBoxOrient:"vertical", overflow:"hidden" },
    repoMeta: { display:"flex", alignItems:"center", gap:"8px", fontSize:"10px", color:"#5C7A99" },
    langDot: { width:"8px", height:"8px", borderRadius:"50%" },
    statRow: {
      display:"flex", alignItems:"center", justifyContent:"space-between",
      padding:"7px 0", borderBottom:"1px solid #1E3048",
    },
    statK: { display:"flex", alignItems:"center", gap:"7px", fontSize:"12px", color:"#A8BCCF" },
    statV: { fontFamily:"'JetBrains Mono',monospace", fontSize:"13px", fontWeight:"600", color:"#E8EFF8" },
    pill: {
      background:"#1B2B44", border:"1px solid #1E3048",
      borderRadius:"20px", padding:"4px 12px", fontSize:"11px",
      color:"#A8BCCF", fontFamily:"'JetBrains Mono',monospace",
    },
    pillHot: { borderColor:"#cc9900", color:"#FFD700" },
    goalRow: { display:"flex", alignItems:"flex-start", gap:"10px", marginBottom:"10px", fontSize:"12px", color:"#A8BCCF" },
    goalIcon: {
      width:"18px", height:"18px", borderRadius:"4px",
      display:"flex", alignItems:"center", justifyContent:"center",
      fontSize:"10px", flexShrink:0, marginTop:"1px",
    },
  };

  if (loading) return (
    <div style={{...s.root, display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center", minHeight:"300px"}}>
      <div style={{width:"48px", height:"48px", border:"3px solid #1E3048", borderTopColor:"#FFD700",
        borderRadius:"50%", animation:"spin 0.8s linear infinite", marginBottom:"16px"}} />
      <div style={{fontSize:"13px", color:"#5C7A99", fontFamily:"'JetBrains Mono',monospace"}}>
        Fetching @{USERNAME} from GitHub...
      </div>
      <style>{`@keyframes spin{to{transform:rotate(360deg)}} @keyframes pulse{0%,100%{opacity:1}50%{opacity:0.4}}`}</style>
    </div>
  );

  return (
    <div style={s.root}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Syne:wght@400;600;700;800&display=swap');
        @keyframes spin{to{transform:rotate(360deg)}}
        @keyframes pulse{0%,100%{opacity:1}50%{opacity:0.4}}
        @keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
        *{box-sizing:border-box;margin:0;padding:0}
        a{text-decoration:none}
        .repo-card:hover{border-color:#FFD700!important;transition:border-color 0.2s}
        .tab-btn:hover{color:#A8BCCF!important}
        .slink:hover{border-color:#FFD700!important;color:#FFD700!important}
      `}</style>

      {/* HERO */}
      <div style={s.hero}>
        <div style={s.heroGlow} />
        <div style={{maxWidth:"760px", margin:"0 auto"}}>
          <div style={s.statusBadge}>
            <span style={s.statusDot}/>
            🎯 Focusing — Active on GitHub
          </div>
          <div style={s.heroTop}>
            <img src={AVATAR} alt={USERNAME} style={s.avatar}
              onError={e => { e.target.style.display="none"; }} />
            <div>
              <div style={s.name}>{user?.name || "Ali Mohammad Sohel Rana"}</div>
              <div style={s.handle}>@{user?.login || USERNAME}</div>
              <div style={s.bio}>{user?.bio || "BSC graduate in CIS · Passionate Full Stack Developer from Thakurgoan, Bangladesh 🇧🇩"}</div>
              <div style={s.metaRow}>
                <span>🎓 Daffodil International University</span>
                <span>📍 {user?.location || "Thakurgoan, Bangladesh"}</span>
                <span>👥 {user?.followers || 5} followers · {user?.following || 10} following</span>
                <span>📦 {user?.public_repos || 75} public repos</span>
              </div>
            </div>
          </div>
          <div style={s.socialRow}>
            {SOCIALS.map(s2 => (
              <a key={s2.label} href={s2.url} target="_blank" rel="noreferrer"
                className="slink" style={s.slink}>
                {s2.label} ↗
              </a>
            ))}
            <a href={`https://github.com/${USERNAME}`} target="_blank" rel="noreferrer"
              className="slink" style={{...s.slink, borderColor:"#cc9900", color:"#FFD700"}}>
              GitHub ↗
            </a>
          </div>
          <div style={s.tabs}>
            {["overview","repos","stack","goals"].map(t => (
              <button key={t} className="tab-btn" onClick={() => setTab(t)}
                style={{...s.tab, ...(tab===t ? s.tabActive : {})}}>
                {t.charAt(0).toUpperCase()+t.slice(1)}
              </button>
            ))}
          </div>
        </div>
      </div>

      {/* BODY */}
      <div style={s.body}>

        {tab === "overview" && (
          <div style={{animation:"fadeIn 0.3s ease"}}>

            {/* STATS ROW */}
            <div style={{...s.grid3, marginTop:"20px"}}>
              {[
                {val: user?.public_repos || 75, label:"Repositories", sub:"public", color:"#00E5A0", border:"#1e3d20"},
                {val: totalStars || 0, label:"Total Stars", sub:"across all repos", color:"#FFD700", border:"#2a1a0a"},
                {val: totalForks || 0, label:"Total Forks", sub:"across all repos", color:"#4FC3F7", border:"#1e2e3a"},
              ].map(item => (
                <div key={item.label} style={{...s.card, textAlign:"center", borderColor:item.border, padding:"14px"}}>
                  <div style={{...s.bigNum, color:item.color}}>{item.val}</div>
                  <div style={s.numLabel}>{item.label}</div>
                  <div style={s.numSub}>{item.sub}</div>
                </div>
              ))}
            </div>

            {/* STATS + LANGS */}
            <div style={s.grid2}>
              <div style={s.card}>
                <div style={s.cardTitle}>GitHub Stats</div>
                {[
                  {k:"📦 Public Repos", v: user?.public_repos || 75},
                  {k:"👥 Followers", v: user?.followers || 5},
                  {k:"🔗 Following", v: user?.following || 10},
                  {k:"⭐ Stars Earned", v: totalStars},
                  {k:"🔀 Forks", v: totalForks},
                  {k:"🎯 Status", v:"Focusing", vc:"#00E5A0"},
                ].map((row, i, arr) => (
                  <div key={row.k} style={{...s.statRow, ...(i===arr.length-1?{borderBottom:"none"}:{})}}>
                    <span style={s.statK}>{row.k}</span>
                    <span style={{...s.statV, ...(row.vc?{color:row.vc}:{})}}>{row.v}</span>
                  </div>
                ))}
              </div>

              <div style={s.card}>
                <div style={s.cardTitle}>Top Languages</div>
                {topLangs.length > 0 ? (
                  <>
                    <div style={{height:"8px", borderRadius:"4px", overflow:"hidden", display:"flex", marginBottom:"14px"}}>
                      {topLangs.map(l => (
                        <span key={l.name} style={{width:`${l.pct}%`, background:l.color}} />
                      ))}
                    </div>
                    {topLangs.map(l => (
                      <div key={l.name} style={{display:"flex", alignItems:"center", gap:"7px", marginBottom:"7px"}}>
                        <span style={{...s.langDot, background:l.color}} />
                        <span style={{fontSize:"11px", color:"#A8BCCF", flex:1}}>{l.name}</span>
                        <span style={{fontSize:"11px", fontFamily:"'JetBrains Mono',monospace", color:"#E8EFF8", fontWeight:"600"}}>{l.pct}%</span>
                      </div>
                    ))}
                  </>
                ) : (
                  <div style={{fontSize:"12px", color:"#5C7A99"}}>Loading language data...</div>
                )}
              </div>
            </div>

            {/* ACTIVITY */}
            <div style={s.card}>
              <div style={s.cardTitle}>Contribution Activity (2025–2026)</div>
              <canvas ref={canvasRef} width={52*(12+3)} height={7*(12+3)} style={{width:"100%", borderRadius:"4px"}} />
              <div style={{display:"flex", justifyContent:"space-between", fontSize:"9px", color:"#5C7A99", marginTop:"6px", fontFamily:"'JetBrains Mono',monospace"}}>
                <span>Jan 2025</span><span>Apr 2025</span><span>Jul 2025</span><span>Oct 2025</span><span>Apr 2026</span>
              </div>
            </div>

            {/* PINNED REPOS */}
            <div style={s.card}>
              <div style={s.cardTitle}>Top Repositories</div>
              <div style={{display:"grid", gridTemplateColumns:"repeat(auto-fill,minmax(200px,1fr))", gap:"10px"}}>
                {pinnedRepos.map(r => (
                  <a key={r.id} href={r.html_url} target="_blank" rel="noreferrer"
                    className="repo-card" style={s.repoCard}>
                    <div style={s.repoName}>{r.name}</div>
                    <div style={s.repoDesc}>{r.description || "No description"}</div>
                    <div style={s.repoMeta}>
                      {r.language && <><span style={{...s.langDot, background:LANG_COLORS[r.language]||"#888"}} /><span>{r.language}</span></>}
                      <span>⭐ {r.stargazers_count}</span>
                      <span>🍴 {r.forks_count}</span>
                    </div>
                  </a>
                ))}
              </div>
            </div>
          </div>
        )}

        {tab === "repos" && (
          <div style={{animation:"fadeIn 0.3s ease", marginTop:"20px"}}>
            <div style={s.card}>
              <div style={s.cardTitle}>{repos.filter(r=>!r.fork).length} Original Repos · {repos.filter(r=>r.fork).length} Forks</div>
              <div style={{display:"grid", gridTemplateColumns:"repeat(auto-fill,minmax(220px,1fr))", gap:"10px"}}>
                {repos.filter(r=>!r.fork).sort((a,b)=>new Date(b.updated_at)-new Date(a.updated_at)).map(r => (
                  <a key={r.id} href={r.html_url} target="_blank" rel="noreferrer"
                    className="repo-card" style={s.repoCard}>
                    <div style={s.repoName}>{r.name}</div>
                    <div style={s.repoDesc}>{r.description || "No description"}</div>
                    <div style={s.repoMeta}>
                      {r.language && <><span style={{...s.langDot, background:LANG_COLORS[r.language]||"#888"}} /><span>{r.language}</span></>}
                      <span>⭐ {r.stargazers_count}</span>
                      {r.topics?.length > 0 && <span style={{color:"#4FC3F7"}}>#{r.topics[0]}</span>}
                    </div>
                  </a>
                ))}
              </div>
            </div>
          </div>
        )}

        {tab === "stack" && (
          <div style={{animation:"fadeIn 0.3s ease", marginTop:"20px"}}>
            {Object.entries(TECH_STACK).map(([cat, techs]) => (
              <div key={cat} style={s.card}>
                <div style={s.cardTitle}>{cat}</div>
                <div style={{display:"flex", flexWrap:"wrap", gap:"7px"}}>
                  {techs.map(t => (
                    <span key={t} style={{...s.pill, ...(["React","Next.js","GraphQL","Node.js","TypeScript"].includes(t)?s.pillHot:{})}}>
                      {t}
                    </span>
                  ))}
                </div>
              </div>
            ))}
            <div style={s.card}>
              <div style={s.cardTitle}>About Me</div>
              <pre style={{fontFamily:"'JetBrains Mono',monospace", fontSize:"11px", color:"#A8BCCF",
                background:"#0D1B2A", padding:"14px", borderRadius:"8px", overflowX:"auto", lineHeight:1.7}}>
{`const aliMohammad = {
  name:       "Ali Mohammad Sohel Rana",
  location:   "Bangladesh 🇧🇩",
  education:  "Daffodil International University",
  role:       "Full Stack Developer",
  work:       "Contract-based Application Development",
  learning:   ["GraphQL", "Next.js", "Advanced React Patterns"],
  askMeAbout: ["React", "Next.js", "Node.js", "GraphQL"],
  funFact:    "I debug with console.log and I'm not ashamed! 😄",
};`}
              </pre>
            </div>
          </div>
        )}

        {tab === "goals" && (
          <div style={{animation:"fadeIn 0.3s ease", marginTop:"20px"}}>
            <div style={s.card}>
              <div style={s.cardTitle}>Goals & Learning</div>
              {GOALS.map((g, i) => (
                <div key={i} style={s.goalRow}>
                  <div style={{...s.goalIcon,
                    background: g.status==="wip"?"#2a1a0a":g.status==="done"?"#0d2a1a":"#1B2B44",
                    color: g.status==="wip"?"#FFA116":g.status==="done"?"#00E5A0":"#5C7A99",
                    border: `1px solid ${g.status==="wip"?"#4a3010":g.status==="done"?"#1a4a2a":"#1E3048"}`,
                  }}>
                    {g.status==="wip"?"⟳":g.status==="done"?"✓":"○"}
                  </div>
                  {g.text}
                </div>
              ))}
            </div>
            <div style={s.card}>
              <div style={s.cardTitle}>Upcoming Blog Articles</div>
              {ARTICLES.map((a, i) => (
                <div key={i} style={{...s.statRow, ...(i===ARTICLES.length-1?{borderBottom:"none"}:{})}}>
                  <span style={{fontSize:"12px", color:"#A8BCCF"}}>{a}</span>
                  <span style={{fontSize:"10px", color:"#FFA116", background:"#2a1a0a",
                    border:"1px solid #4a3010", padding:"2px 8px", borderRadius:"10px", flexShrink:0}}>
                    Coming Soon
                  </span>
                </div>
              ))}
            </div>
            <div style={s.card}>
              <div style={s.cardTitle}>Connect With Me</div>
              <div style={{display:"grid", gridTemplateColumns:"1fr 1fr", gap:"10px"}}>
                {[
                  {label:"LinkedIn", val:"ali-mohammad-sohel-rana", url:"https://www.linkedin.com/in/ali-mohammad-sohel-rana/"},
                  {label:"Facebook", val:"amsohel.rana.90", url:"https://www.facebook.com/amsohel.rana.90"},
                  {label:"Email", val:"rana16-468@diu.edu.bd", url:"mailto:rana16-468@diu.edu.bd"},
                  {label:"Portfolio", val:"my-portfolio-chi-rust-66.vercel.app", url:"https://my-portfolio-chi-rust-66.vercel.app/"},
                ].map(c => (
                  <a key={c.label} href={c.url} target="_blank" rel="noreferrer"
                    style={{background:"#1B2B44", border:"1px solid #1E3048", borderRadius:"12px",
                      padding:"12px 14px", display:"flex", flexDirection:"column", gap:"3px", textDecoration:"none"}}>
                    <span style={{fontSize:"10px", color:"#5C7A99", textTransform:"uppercase", letterSpacing:"0.8px"}}>{c.label}</span>
                    <span style={{fontSize:"11px", color:"#4FC3F7", whiteSpace:"nowrap", overflow:"hidden", textOverflow:"ellipsis"}}>{c.val}</span>
                  </a>
                ))}
              </div>
            </div>
          </div>
        )}

      </div>
    </div>
  );
}
