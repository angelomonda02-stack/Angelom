<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Angelom — Social</title>
<meta name="description" content="Angelom — your social space" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#f4f6fb;
    --card:#ffffff;
    --muted:#6b7280;
    --brand-deep:#0b3b6f; /* deep blue inspired by image */
    --brand-pink:#ff5aa3; /* pink accent inspired by image */
    --accent:#1877f2;
    --radius:12px;
    --shadow: 0 10px 30px rgba(15,23,42,0.08);
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:"Inter",system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    background:linear-gradient(180deg,var(--bg), #eef3fb 60%);
    color:#0f172a;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    line-height:1.45;
  }

  /* Top nav */
  header.topbar{
    display:flex;
    align-items:center;
    gap:16px;
    padding:14px 20px;
    background:linear-gradient(90deg,var(--brand-deep), #04305a);
    color:white;
  }
  .logo-wrap{ display:flex; gap:12px; align-items:center; cursor:pointer }
  .site-title{ font-weight:700; letter-spacing:0.2px}
  .nav-actions{ margin-left:auto; display:flex; gap:10px; align-items:center }
  .btn{ background:transparent; border:1px solid rgba(255,255,255,0.18); color:white; padding:8px 12px; border-radius:10px; cursor:pointer; font-weight:700 }
  .btn.ghost{ background:rgba(255,255,255,0.06) }

  /* Layout */
  .wrap{ width:min(1150px,96%); margin:22px auto; display:grid; grid-template-columns: 300px 1fr 320px; gap:18px; align-items:start; }
  @media (max-width:1100px){ .wrap{ grid-template-columns: 1fr; } .right-col, .left-col { order: 2 } .main-col { order: 1 } }

  /* Cards */
  .card{ background:var(--card); border-radius:var(--radius); box-shadow:var(--shadow); padding:14px; }
  .profile{ display:flex; gap:12px; align-items:center }
  .avatar{ width:64px; height:64px; border-radius:12px; background:linear-gradient(180deg,#fff,#eee); display:flex; align-items:center; justify-content:center; font-weight:800; color:var(--brand-deep); font-size:22px }

  /* Composer */
  .composer textarea{ width:100%; min-height:82px; padding:12px; border-radius:10px; border:1px solid #e8edf6; resize:vertical; font-size:14px; }
  .composer .row{ display:flex; justify-content:space-between; align-items:center; margin-top:10px; gap:8px }
  .small{ font-size:13px; color:var(--muted) }

  /* Feed */
  .feed{ display:flex; flex-direction:column; gap:14px }
  .post{ display:block; border-radius:12px; background:var(--card); padding:12px; box-shadow:var(--shadow) }
  .post .post-head{ display:flex; gap:12px; align-items:center }
  .post .post-media{ margin-top:10px; border-radius:10px; overflow:hidden; background:#f6f8fc }
  .post img{ width:100%; height:auto; display:block }

  /* Interactions */
  .actions{ display:flex; gap:8px; margin-top:10px }
  .pill{ padding:6px 10px; border-radius:999px; background:#f1f5fb; font-weight:700; cursor:pointer; border:1px solid #eef3fb }

  /* Right column small widgets */
  .trending { display:flex; flex-direction:column; gap:10px }
  .trend-item{ display:flex; justify-content:space-between; gap:8px; align-items:center; padding:8px; border-radius:8px; background:linear-gradient(180deg,#fff,#fbfcff); border:1px solid #f0f4fb }

  footer{ text-align:center; color:var(--muted); padding:30px 10px; margin-top:30px }

  /* Inputs */
  input[type="text"], input[type="email"]{ padding:10px 12px; border-radius:8px; border:1px solid #e6e9ee; width:100% }

  /* tiny */
  .muted{ color:var(--muted) }
  .hide{ display:none }
</style>
</head>
<body>

<header class="topbar" role="banner">
  <div class="logo-wrap" onclick="window.scrollTo({top:0,behavior:'smooth'})" aria-label="Angelom home">
    <!-- SVG logo built from image colors (deep blue + pink) -->
    <svg width="56" height="56" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" role="img">
      <defs>
        <linearGradient id="g1" x1="0" x2="1" y1="0" y2="1">
          <stop offset="0" stop-color="#0b3b6f"/>
          <stop offset="1" stop-color="#04305a"/>
        </linearGradient>
      </defs>
      <rect rx="12" ry="12" width="64" height="64" fill="url(#g1)"/>
      <!-- stylized 'A' mark with pink accent -->
      <path d="M20 44 L32 16 L44 44 Z" fill="white" opacity="0.95"/>
      <circle cx="48" cy="16" r="8" fill="#ff5aa3"/>
      <circle cx="48" cy="16" r="4.8" fill="white" opacity="0.12"/>
    </svg>

    <div>
      <div class="site-title" style="font-size:16px">Angelom</div>
      <div style="font-size:12px; opacity:0.95">Your social space</div>
    </div>
  </div>

  <div class="nav-actions" role="navigation" aria-label="Top actions">
    <button class="btn ghost" id="btn-login">Log in</button>
    <button class="btn" id="btn-signup">Create account</button>
  </div>
</header>

<main class="wrap" role="main">
  <!-- Left column: profile / shortcuts -->
  <aside class="left-col card" style="position:sticky; top:18px; height:max-content">
    <div class="profile">
      <div class="avatar" id="miniAvatar">A</div>
      <div>
        <div id="miniName" style="font-weight:800">Guest</div>
        <div class="small" id="miniHandle">@guest</div>
      </div>
    </div>

    <hr style="margin:12px 0; border:none; border-top:1px dashed #eef3fb"/>

    <div>
      <div style="font-weight:700; margin-bottom:8px">Quick Links</div>
      <div style="display:flex; flex-direction:column; gap:8px">
        <button class="pill" onclick="showSection('feed')">Home</button>
        <button class="pill" onclick="showSection('profile')">Profile</button>
        <button class="pill" onclick="showSection('notifications')">Notifications</button>
      </div>
    </div>

    <hr style="margin:12px 0; border:none; border-top:1px dashed #eef3fb"/>

    <div>
      <div style="font-weight:700; margin-bottom:8px">About Angelom</div>
      <div class="small">A simple, privacy-first social feed — demo site. Customize features or connect a backend to make it live.</div>
    </div>
  </aside>

  <!-- Main column: composer + feed -->
  <section class="main-col">
    <div class="card composer" aria-label="Create post">
      <div style="display:flex; gap:12px; align-items:flex-start">
        <div class="avatar" style="width:56px;height:56px" id="composerAvatar">A</div>
        <div style="flex:1">
          <textarea id="postText" placeholder="What's happening?" aria-label="Write a post"></textarea>
          <div class="row" style="margin-top:8px; display:flex; gap:8px; align-items:center; justify-content:space-between">
            <div style="display:flex; gap:8px; align-items:center">
              <input id="postImage" type="text" placeholder="Optional image URL" style="width:360px">
              <button class="pill" id="attachExample" title="Insert sample image">Sample image</button>
            </div>
            <div style="display:flex; gap:8px">
              <div class="small" id="charCount">0 / 1000</div>
              <button class="btn" id="postBtn">Post</button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div style="height:14px"></div>

    <div class="feed card" id="feed" aria-live="polite" aria-label="Feed">
      <!-- Posts will be injected here -->
    </div>
  </section>

  <!-- Right column: widgets -->
  <aside class="right-col" style="position:sticky; top:18px">
    <div class="card trending">
      <div style="display:flex; justify-content:space-between; align-items:center">
        <div style="font-weight:800">Trending</div>
        <small class="muted">Now</small>
      </div>
      <div class="trend-item"><div>#community</div><div class="small muted">2.1k</div></div>
      <div class="trend-item"><div>#design</div><div class="small muted">860</div></div>
      <div class="trend-item"><div>#shoplocal</div><div class="small muted">430</div></div>
    </div>

    <div style="height:12px"></div>

    <div class="card">
      <div style="font-weight:800">Who to follow</div>
      <div style="display:flex; gap:8px; margin-top:10px; align-items:center">
        <div style="width:46px; height:46px; border-radius:10px; background:linear-gradient(180deg,#fff,#f2f6ff); display:flex; align-items:center; justify-content:center; font-weight:800">MJ</div>
        <div style="flex:1">
          <div style="font-weight:700">Maya Joy</div>
          <div class="small muted">@mayaj</div>
        </div>
        <button class="pill" onclick="followDemo()">Follow</button>
      </div>
    </div>

  </aside>
</main>

<footer>
  © <span id="year"></span> Angelom · Demo social site
</footer>

<!-- Simple modal for login/signup -->
<div id="authModal" class="hide" style="position:fixed; inset:0; display:flex; align-items:center; justify-content:center; background:rgba(5,8,18,0.45); z-index:40;">
  <div style="width:420px; background:white; border-radius:12px; padding:18px; box-shadow:0 30px 60px rgba(2,6,23,0.25)">
    <h3 id="authTitle">Create account</h3>
    <div style="display:flex; flex-direction:column; gap:8px">
      <input id="authName" type="text" placeholder="Full name">
      <input id="authHandle" type="text" placeholder="Handle (no @)">
      <input id="authEmail" type="email" placeholder="Email (demo)">
      <div style="display:flex; gap:8px; justify-content:flex-end; margin-top:8px">
        <button class="btn" id="authCancel">Cancel</button>
        <button class="btn" id="authSave">Save</button>
      </div>
    </div>
  </div>
</div>

<script>
/* ====================
   Tiny front-end app
   - Uses localStorage to persist users & posts
   - Demo-only: no backend, no auth security
   ==================== */

const STORAGE_KEYS = {
  USER: 'angelom_user_v1',
  POSTS: 'angelom_posts_v1'
};

// default demo posts
const DEFAULT_POSTS = [
  {
    id: 't1',
    author: { name: 'Angelom Team', handle: 'angelom' },
    text: 'Welcome to Angelom — your demo social space! 🌟',
    image: '',
    createdAt: Date.now() - 1000 * 60 * 60 * 24
  },
  {
    id: 't2',
    author: { name: 'Design Club', handle: 'designclub' },
    text: 'Share your creative work and tag #design to get featured.',
    image: 'https://images.unsplash.com/photo-1508921912186-1d1a45ebb3c1?w=1200&q=80&auto=format&fit=crop',
    createdAt: Date.now() - 1000 * 60 * 60 * 6
  }
];

// simple helpers
function uid(prefix='id'){ return prefix + '-' + Math.random().toString(36).slice(2,9); }
function loadJSON(key, fallback){ try{ return JSON.parse(localStorage.getItem(key)) || fallback }catch(e){ return fallback } }
function saveJSON(key, v){ localStorage.setItem(key, JSON.stringify(v)) }

let currentUser = loadJSON(STORAGE_KEYS.USER, null);
let posts = loadJSON(STORAGE_KEYS.POSTS, DEFAULT_POSTS);

// DOM refs
const feedEl = document.getElementById('feed');
const postBtn = document.getElementById('postBtn');
const postText = document.getElementById('postText');
const postImage = document.getElementById('postImage');
const charCount = document.getElementById('charCount');
const composerAvatar = document.getElementById('composerAvatar');
const miniAvatar = document.getElementById('miniAvatar');
const miniName = document.getElementById('miniName');
const miniHandle = document.getElementById('miniHandle');
const btnLogin = document.getElementById('btn-login');
const btnSignup = document.getElementById('btn-signup');
const authModal = document.getElementById('authModal');
const authTitle = document.getElementById('authTitle');
const authName = document.getElementById('authName');
const authHandle = document.getElementById('authHandle');
const authEmail = document.getElementById('authEmail');
const authCancel = document.getElementById('authCancel');
const authSave = document.getElementById('authSave');
const attachExample = document.getElementById('attachExample');

document.getElementById('year').textContent = new Date().getFullYear();

/* ===== init view based on user ===== */
function refreshUserUI(){
  if(currentUser){
    composerAvatar.textContent = currentUser.name ? currentUser.name[0].toUpperCase() : 'A';
    miniAvatar.textContent = currentUser.name ? currentUser.name[0].toUpperCase() : 'A';
    miniName.textContent = currentUser.name || 'You';
    miniHandle.textContent = '@' + (currentUser.handle || 'you');
    btnLogin.textContent = 'Log out';
    btnSignup.textContent = 'Profile';
  } else {
    composerAvatar.textContent = 'A';
    miniAvatar.textContent = 'A';
    miniName.textContent = 'Guest';
    miniHandle.textContent = '@guest';
    btnLogin.textContent = 'Log in';
    btnSignup.textContent = 'Create account';
  }
}

/* ===== render feed ===== */
function renderFeed(){
  feedEl.innerHTML = '';
  if(!posts.length){
    feedEl.innerHTML = '<div class="muted" style="padding:20px">No posts yet — be the first!</div>';
    return;
  }
  // show newest first
  posts.slice().sort((a,b)=> b.createdAt - a.createdAt).forEach(p=>{
    const post = document.createElement('article');
    post.className = 'post';
    post.innerHTML = `
      <div class="post-head">
        <div style="width:44px; height:44px; border-radius:10px; display:flex; align-items:center; justify-content:center; font-weight:800; background:linear-gradient(180deg,#fff,#f2f6ff)">${escapeHtml(p.author.name[0]||'A')}</div>
        <div style="flex:1">
          <div style="display:flex; gap:8px; align-items:center">
            <div style="font-weight:800">${escapeHtml(p.author.name)}</div>
            <div class="small muted">@${escapeHtml(p.author.handle)}</div>
            <div class="small muted" style="margin-left:auto">${timeAgo(p.createdAt)}</div>
          </div>
          <div style="margin-top:6px">${escapeHtml(p.text)}</div>
        </div>
      </div>
      ${p.image ? `<div class="post-media"><img loading="lazy" src="${escapeHtml(p.image)}" alt="Post image"></div>` : ''}
      <div class="actions">
        <div class="pill" onclick="likePost('${p.id}')">Like</div>
        <div class="pill" onclick="replyPost('${p.id}')">Reply</div>
        <div class="pill" onclick="sharePost('${p.id}')">Share</div>
      </div>
    `;
    feedEl.appendChild(post);
  });
}

/* ===== post interactions (local only) ===== */
function likePost(id){
  alert('Like (demo) — implement backend to store likes.');
}
function replyPost(id){
  const text = prompt('Write a reply (demo):');
  if(text) alert('Reply (demo) — would post: ' + text);
}
function sharePost(id){
  const p = posts.find(x=>x.id===id);
  if(!p) return;
  const shareUrl = location.href + '#post-' + id;
  navigator.clipboard?.writeText(shareUrl).then(()=> alert('Post link copied to clipboard (demo).'));
}

/* ===== create post ===== */
postText.addEventListener('input', ()=>{
  const len = postText.value.length;
  charCount.textContent = `${len} / 1000`;
});

postBtn.addEventListener('click', ()=>{
  if(!currentUser){
    openAuth('signup');
    return;
  }
  const txt = postText.value.trim();
  if(!txt && !postImage.value.trim()){
    alert('Write something or add an image.');
    return;
  }
  const p = {
    id: uid('post'),
    author: { name: currentUser.name, handle: currentUser.handle },
    text: txt,
    image: postImage.value.trim() || '',
    createdAt: Date.now()
  };
  posts.push(p);
  saveJSON(STORAGE_KEYS.POSTS, posts);
  postText.value = '';
  postImage.value = '';
  charCount.textContent = '0 / 1000';
  renderFeed();
});

/* ===== auth modal logic (demo) ===== */
btnLogin.addEventListener('click', ()=>{
  if(currentUser){
    // log out
    if(confirm('Log out?')){
      currentUser = null;
      localStorage.removeItem(STORAGE_KEYS.USER);
      refreshUserUI();
    }
  } else {
    openAuth('login');
  }
});
btnSignup.addEventListener('click', ()=>{
  if(currentUser){
    alert('Profile (demo): ' + JSON.stringify(currentUser));
    return;
  }
  openAuth('signup');
});

function openAuth(mode='signup'){
  authModal.classList.remove('hide');
  authTitle.textContent = mode === 'signup' ? 'Create account' : 'Log in (demo)';
  authName.value = '';
  authHandle.value = '';
  authEmail.value = '';
  authSave.dataset.mode = mode;
}
authCancel.addEventListener('click', ()=> authModal.classList.add('hide'));
authSave.addEventListener('click', ()=>{
  const mode = authSave.dataset.mode;
  const name = authName.value.trim();
  const handle = authHandle.value.trim().replace(/\s+/g,'').toLowerCase();
  if(!name || !handle){ alert('Please provide name and handle'); return; }
  currentUser = { name, handle, email: authEmail.value.trim() };
  saveJSON(STORAGE_KEYS.USER, currentUser);
  authModal.classList.add('hide');
  refreshUserUI();
});

/* ===== utilities ===== */
function escapeHtml(s){ if(!s) return ''; return s.replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;').replaceAll('"','&quot;'); }
function saveJSON(k,v){ localStorage.setItem(k, JSON.stringify(v)); }
function loadJSON(k, fallback){ try{ return JSON.parse(localStorage.getItem(k)) || fallback }catch(e){ return fallback } }
function timeAgo(ts){
  const s = Math.floor((Date.now() - ts) / 1000);
  if(s < 60) return s + 's';
  if(s < 3600) return Math.floor(s/60) + 'm';
  if(s < 86400) return Math.floor(s/3600) + 'h';
  return Math.floor(s/86400) + 'd';
}

/* ===== small helpers ===== */
window.showSection = function(name){
  alert('Demo navigation: ' + name + ' (no separate pages).');
};
window.followDemo = function(){ alert('Followed (demo)'); };

/* ===== sample image filler ===== */
attachExample.addEventListener('click', ()=>{
  postImage.value = 'https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=1200&q=80&auto=format&fit=crop';
});

/* ===== init ===== */
refreshUserUI();
renderFeed();
saveJSON(STORAGE_KEYS.POSTS, posts);

/* expose in console for debugging */
window.Angelom = {
  getUser: ()=> currentUser,
  getPosts: ()=> posts,
  reset: ()=> { localStorage.removeItem(STORAGE_KEYS.USER); localStorage.removeItem(STORAGE_KEYS.POSTS); location.reload(); }
};

</script>
</body>
</html>
