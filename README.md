<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Walkthroughs - Trainer's Odyssey</title>
<script>
    // Runs immediately, before first paint, to prevent white flash / wrong theme flash
    (function() {
        var savedTheme = localStorage.getItem('to_theme') || 'dark';
        document.documentElement.setAttribute('data-theme', savedTheme);
        document.documentElement.style.background = savedTheme === 'light' ? '#f2ede3' : '#050711';
    })();
</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Exo+2:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<style>

        * { margin:0; padding:0; box-sizing:border-box; }

        :root[data-theme="dark"] {
            --primary:#FF0000; --secondary:#3B4CCA; --accent:#FFDE00;
            --bg:#050711; --bg2:#0A0E27; --text:#F5F5F5; --text-dim: rgba(245,245,245,0.75);
            --card-bg: rgba(255,255,255,0.06); --border: rgba(255,222,0,0.25);
            --nav-bg: rgba(10,14,39,0.85); --overlay: rgba(3,5,15,0.72);
            --fire:#F08030; --water:#6890F0; --grass:#78C850; --electric:#F7D02C;
        }
        :root[data-theme="light"] {
            --primary:#D8232A; --secondary:#2E4BC6; --accent:#B8860B;
            --bg:#f2ede3; --bg2:#ffffff; --text:#1a1a2e; --text-dim: rgba(26,26,46,0.75);
            --card-bg: rgba(255,255,255,0.65); --border: rgba(184,134,11,0.35);
            --nav-bg: rgba(242,237,227,0.88); --overlay: rgba(242,237,227,0.78);
            --fire:#D9622B; --water:#3B6FD1; --grass:#4B9E3F; --electric:#C99A00;
        }

        html { background: var(--bg); }

        body {
            font-family:'Exo 2', sans-serif;
            background: var(--bg);
            color: var(--text);
            overflow-x:hidden;
            line-height:1.6;
            min-height:100vh;
            transition: color 0.3s ease;
        }

        /* Blurred background photo, fixed behind everything */
        .bg-photo {
            position:fixed; inset:-30px; z-index:-3;
            background-image:url('pokemon-bg.png');
            background-size:cover;
            background-position:center;
            filter:blur(9px) saturate(1.1);
            transform:scale(1.06);
        }
        .bg-overlay {
            position:fixed; inset:0; z-index:-2;
            background: var(--overlay);
        }
        .bg-pattern {
            position:fixed; inset:0; z-index:-1;
            background:
                radial-gradient(circle at 20% 50%, rgba(255,0,0,0.10) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(59,76,202,0.10) 0%, transparent 50%),
                radial-gradient(circle at 40% 20%, rgba(255,222,0,0.06) 0%, transparent 50%);
            animation: bgFloat 20s ease-in-out infinite;
        }
        @keyframes bgFloat { 0%,100%{transform:translate(0,0);} 50%{transform:translate(-20px,20px);} }

        /* Page loader - prevents blank white flash while assets settle */
        #page-loader {
            position:fixed; inset:0; z-index:9999;
            background: var(--bg);
            display:flex; align-items:center; justify-content:center;
            transition: opacity 0.4s ease, visibility 0.4s ease;
        }
        #page-loader.hide { opacity:0; visibility:hidden; pointer-events:none; }
        .loader-mark {
            font-family:'Press Start 2P', cursive;
            color:var(--accent);
            font-size:1rem;
            animation:pulse 1.1s ease-in-out infinite;
            text-shadow:3px 3px 0 var(--primary);
        }
        @keyframes pulse { 0%,100%{transform:scale(1);opacity:0.8;} 50%{transform:scale(1.08);opacity:1;} }

        /* Fixed header */
        header {
            position:fixed; top:0; left:0; right:0; z-index:1000;
            background: var(--nav-bg);
            border-bottom:3px solid var(--primary);
            backdrop-filter: blur(10px);
            box-shadow:0 4px 30px rgba(0,0,0,0.35);
        }
        nav {
            max-width:1400px; margin:0 auto; padding:1.1rem 2rem;
            display:flex; justify-content:space-between; align-items:center;
            flex-wrap:wrap; gap:1rem;
        }
        .logo {
            font-family:'Press Start 2P', cursive; font-size:1.1rem;
            color: var(--accent); text-shadow:3px 3px 0 var(--primary);
            letter-spacing:2px; white-space:nowrap;
            text-decoration:none;
        }
        .nav-links { display:flex; gap:1.6rem; list-style:none; align-items:center; flex-wrap:wrap; }
        .nav-links a {
            color:var(--text); text-decoration:none; font-weight:600; position:relative;
            transition:all 0.3s; text-transform:uppercase; font-size:0.82rem; letter-spacing:1px;
        }
        .nav-links a::after {
            content:''; position:absolute; bottom:-5px; left:0; width:0; height:2px;
            background:var(--accent); transition:width 0.3s;
        }
        .nav-links a:hover::after, .nav-links a.active::after { width:100%; }
        .nav-links a.active { color:var(--accent); }

        .theme-toggle {
            display:flex; align-items:center; gap:0.4rem;
            background:rgba(128,128,128,0.15);
            border:2px solid var(--border);
            border-radius:25px; padding:0.3rem; cursor:pointer;
        }
        .theme-toggle button {
            background:none; border:none; color:var(--text); font-size:1.1rem;
            padding:0.3rem 0.6rem; border-radius:20px; cursor:pointer; transition:all 0.25s;
        }
        .theme-toggle button.active { background:var(--accent); color:var(--bg2); }

        .admin-btn {
            background:linear-gradient(135deg, var(--primary), #a80000);
            padding:0.55rem 1.4rem; border-radius:25px; border:2px solid var(--accent);
            cursor:pointer; font-weight:700; transition:all 0.3s; color:#fff;
            box-shadow:0 4px 15px rgba(255,0,0,0.25); font-size:0.85rem;
        }
        .admin-btn:hover { transform:translateY(-2px); box-shadow:0 6px 25px rgba(255,0,0,0.45); }

        /* Push content below fixed nav */
        main { padding-top:92px; }

        .hero {
            padding:5rem 2rem 3rem; text-align:center; position:relative; overflow:hidden;
        }
        .hero h1 {
            font-family:'Press Start 2P', cursive; font-size:clamp(1.6rem, 5vw, 2.6rem);
            color:var(--accent);
            text-shadow:4px 4px 0 var(--primary), -2px -2px 0 var(--secondary);
            margin-bottom:1.3rem;
        }
        .hero p { font-size:1.15rem; color:var(--text-dim); max-width:700px; margin:0 auto; }

        .container { max-width:1400px; margin:0 auto; padding:3rem 2rem; }

        .section-title {
            font-family:'Press Start 2P', cursive; font-size:1.6rem; color:var(--accent);
            text-shadow:3px 3px 0 var(--primary); margin-bottom:2.5rem; text-align:center;
            position:relative;
        }

        .grid { display:grid; grid-template-columns:repeat(auto-fill, minmax(300px,1fr)); gap:2rem; margin-top:2rem; }

        .card {
            background:var(--card-bg); border:2px solid var(--border); border-radius:15px;
            padding:2rem; transition:all 0.3s; backdrop-filter:blur(10px);
        }
        .card:hover { transform:translateY(-8px); border-color:var(--accent); box-shadow:0 10px 40px rgba(255,222,0,0.15); }
        .card h3 { color:var(--accent); font-size:1.35rem; margin-bottom:0.8rem; }
        .card p { color:var(--text-dim); line-height:1.8; }

        .article-block { background:var(--card-bg); border:2px solid var(--border); border-radius:15px; padding:2.2rem; margin-bottom:2.5rem; }
        .article-block h3 { color:var(--accent); font-size:1.4rem; margin-bottom:1rem; }
        .article-block h4 { color:var(--secondary); font-size:1.1rem; margin:1.2rem 0 0.5rem; }
        .article-block p { color:var(--text-dim); line-height:1.85; margin-bottom:0.8rem; }
        .article-block ul, .article-block ol { color:var(--text-dim); line-height:1.85; padding-left:1.5rem; margin-bottom:0.8rem; }
        .article-block li { margin-bottom:0.4rem; }
        .article-block strong { color:var(--text); }
        .rights-note { font-size:0.8rem; color:var(--text-dim); font-style:italic; margin-top:0.8rem; padding-top:0.8rem; border-top:1px solid var(--border); }

        .card-tag {
            display:inline-block; background:var(--primary); color:white; padding:0.3rem 1rem;
            border-radius:20px; font-size:0.8rem; font-weight:600; margin-top:0.8rem;
        }

        .btn {
            display:inline-block; padding:0.75rem 1.8rem; background:linear-gradient(135deg, var(--secondary), #2a3ba8);
            color:white; text-decoration:none; border-radius:25px; font-weight:600; transition:all 0.3s;
            border:2px solid transparent; text-transform:uppercase; letter-spacing:1px; cursor:pointer; font-size:0.85rem;
        }
        .btn:hover { transform:translateY(-3px); box-shadow:0 5px 20px rgba(59,76,202,0.35); border-color:var(--accent); }
        .btn-primary { background:linear-gradient(135deg, var(--primary), #a80000); }
        .btn-primary:hover { box-shadow:0 5px 20px rgba(255,0,0,0.35); }

        .modal {
            display:none; position:fixed; inset:0; background:rgba(0,0,0,0.85); z-index:2000;
            justify-content:center; align-items:center; backdrop-filter:blur(5px);
        }
        .modal.active { display:flex; }
        .modal-content {
            background:var(--bg2); border:3px solid var(--accent); border-radius:20px; padding:2.5rem;
            max-width:800px; width:90%; max-height:85vh; overflow-y:auto; position:relative;
            box-shadow:0 0 50px rgba(255,222,0,0.25); color:var(--text);
        }
        .close-modal {
            position:absolute; top:1rem; right:1rem; background:var(--primary); border:none; color:#fff;
            width:38px; height:38px; border-radius:50%; cursor:pointer; font-size:1.4rem; font-weight:bold;
        }

        .form-group { margin-bottom:1.4rem; }
        .form-group label { display:block; color:var(--accent); font-weight:600; margin-bottom:0.5rem; text-transform:uppercase; font-size:0.85rem; }
        .form-group input, .form-group textarea, .form-group select {
            width:100%; padding:0.75rem; background:rgba(128,128,128,0.1); border:2px solid var(--border);
            border-radius:10px; color:var(--text); font-family:'Exo 2', sans-serif; font-size:1rem;
        }
        .form-group textarea { min-height:110px; resize:vertical; }

        .video-container { position:relative; padding-bottom:56.25%; height:0; overflow:hidden; border-radius:15px; margin:1.5rem 0; border:3px solid var(--accent); }
        .video-container iframe { position:absolute; top:0; left:0; width:100%; height:100%; }

        .social-links { display:flex; gap:1.3rem; justify-content:center; margin-top:2rem; flex-wrap:wrap; }
        .social-links a {
            width:56px; height:56px; background:var(--card-bg); border:2px solid var(--accent); border-radius:50%;
            display:flex; align-items:center; justify-content:center; transition:all 0.3s; font-size:1.4rem; text-decoration:none;
        }
        .social-links a:hover { transform:translateY(-5px) rotate(5deg); background:var(--accent); }

        .filters { display:flex; gap:1rem; margin-bottom:2rem; flex-wrap:wrap; justify-content:center; }
        .filter-btn {
            padding:0.55rem 1.4rem; background:rgba(128,128,128,0.1); border:2px solid var(--border);
            border-radius:25px; color:var(--text); cursor:pointer; transition:all 0.3s; font-weight:600; font-size:0.85rem;
        }
        .filter-btn.active, .filter-btn:hover { background:var(--accent); color:var(--bg2); border-color:var(--accent); }

        .admin-panel { background:linear-gradient(135deg, rgba(255,0,0,0.08), rgba(59,76,202,0.08)); border:3px solid var(--primary); border-radius:20px; padding:2rem; margin-top:2rem; }

        .game-header {
            background:linear-gradient(135deg, var(--primary), var(--secondary)); padding:2.5rem 2rem;
            border-radius:20px; margin-bottom:2.5rem; text-align:center;
        }
        .game-header h2 { font-family:'Press Start 2P', cursive; font-size:1.8rem; color:var(--accent); text-shadow:3px 3px 0 rgba(0,0,0,0.4); }

        footer {
            border-top:3px solid var(--primary); padding:2.5rem 2rem; text-align:center; margin-top:3rem;
            background:var(--nav-bg);
        }
        footer p { color:var(--text-dim); font-size:0.9rem; }

        .success-msg { background:rgba(120,200,80,0.18); border:2px solid var(--grass); color:var(--grass); padding:1rem; border-radius:10px; margin:1rem 0; text-align:center; font-weight:600; }
        .error-msg { background:rgba(255,0,0,0.18); border:2px solid var(--primary); color:var(--primary); padding:1rem; border-radius:10px; margin:1rem 0; text-align:center; font-weight:600; }

        .type-badge { display:inline-block; padding:0.35rem 0.9rem; border-radius:20px; font-size:0.8rem; font-weight:700; margin:0.2rem; text-transform:uppercase; color:#fff; }
        .type-normal{background:#A8A878;} .type-fire{background:#F08030;} .type-water{background:#6890F0;}
        .type-electric{background:#F8D030; color:#1a1a2e;} .type-grass{background:#78C850;} .type-ice{background:#98D8D8; color:#1a1a2e;}
        .type-fighting{background:#C03028;} .type-poison{background:#A040A0;} .type-ground{background:#E0C068; color:#1a1a2e;}
        .type-flying{background:#A890F0;} .type-psychic{background:#F85888;} .type-bug{background:#A8B820;}
        .type-rock{background:#B8A038;} .type-ghost{background:#705898;} .type-dragon{background:#7038F8;}
        .type-dark{background:#705848;} .type-steel{background:#B8B8D0; color:#1a1a2e;} .type-fairy{background:#EE99AC; color:#1a1a2e;}

        .search-container { max-width:600px; margin:2rem auto; position:relative; }
        .search-input { width:100%; padding:1rem 3rem 1rem 1.5rem; background:rgba(128,128,128,0.1); border:2px solid var(--border); border-radius:30px; color:var(--text); font-size:1rem; }
        .search-icon { position:absolute; right:1.5rem; top:50%; transform:translateY(-50%); color:var(--accent); }

        @media (max-width:768px) {
            .hero p{font-size:1rem;}
            .nav-links{gap:0.9rem; width:100%; justify-content:center;}
            main{padding-top:130px;}
        }

</style>
</head>

<body>

<div id="page-loader"><div class="loader-mark">LOADING TRAINER'S ODYSSEY...</div></div>
<div class="bg-photo"></div>
<div class="bg-overlay"></div>
<div class="bg-pattern"></div>

<header>
<nav>
    <a href="index.html" class="logo">TRAINER'S ODYSSEY</a>
    <ul class="nav-links">
        <li><a href="index.html" class="">Home</a></li>
<li><a href="walkthroughs.html" class="active">Walkthroughs</a></li>
<li><a href="romhacks.html" class="">ROM Hacks</a></li>
<li><a href="pokedex.html" class="">Pokédex</a></li>
<li><a href="guides.html" class="">Guides</a></li>
<li><a href="my-romhacks.html" class="">My ROM Hacks</a></li>
<li><a href="videos.html" class="">Videos</a></li>
<li><a href="about.html" class="">About</a></li>

        <li>
            <div class="theme-toggle" id="theme-toggle">
                <button id="btn-dark" onclick="setTheme('dark')" title="Dark theme">🌙</button>
                <button id="btn-light" onclick="setTheme('light')" title="Light theme">☀️</button>
            </div>
        </li>
        <li><button class="admin-btn" onclick="showAdminLogin()">Admin</button></li>
    </ul>
</nav>
</header>

<main>

<div class="container">
    <h2 class="section-title">Pokémon Walkthroughs</h2>
    <div class="search-container">
        <input type="text" class="search-input" id="walkthrough-search" placeholder="Search walkthroughs...">
        <span class="search-icon">🔍</span>
    </div>
    <div class="filters">
        <button class="filter-btn active" onclick="filterWalkthroughs('all', event)">All Games</button>
        <button class="filter-btn" onclick="filterWalkthroughs('official', event)">Official Games</button>
        <button class="filter-btn" onclick="filterWalkthroughs('romhack', event)">ROM Hacks</button>
    </div>
    <div id="walkthroughs-grid" class="grid"></div>
    <div id="admin-walkthrough-panel" style="display:none;">
        <div class="admin-panel">
            <h3 style="color:var(--accent); margin-bottom:1rem;">Add New Walkthrough</h3>
            <button class="btn btn-primary" onclick="showAddWalkthroughModal()">+ Add Game Walkthrough</button>
        </div>
    </div>
</div>

</main>

<footer>
    <p>&copy; 2024 Trainer's Odyssey. All rights reserved. Pokémon is a trademark of Nintendo, Game Freak, and The Pokémon Company.</p>
    <div class="social-links" style="margin-top:1.2rem;">
        <a href="https://youtube.com/@trainersodyssey323" target="_blank">▶</a>
        <a href="https://youtube.com/@handholdhavoc" target="_blank">🎮</a>
        <a href="https://www.instagram.com/pokebattle_reels" target="_blank">📷</a>
    </div>
</footer>


<div id="add-walkthrough-modal" class="modal">
    <div class="modal-content">
        <button class="close-modal" onclick="closeModal('add-walkthrough-modal')">&times;</button>
        <h2 style="color:var(--accent); font-family:'Press Start 2P', cursive; font-size:1.2rem; margin-bottom:2rem;">Add New Walkthrough</h2>
        <form onsubmit="addWalkthrough(event)">
            <div class="form-group"><label>Game Title</label><input type="text" id="wt-title" required></div>
            <div class="form-group"><label>Game Type</label>
                <select id="wt-type" required>
                    <option value="official">Official Game</option>
                    <option value="romhack">ROM Hack</option>
                </select>
            </div>
            <div class="form-group"><label>Description</label><textarea id="wt-description" required></textarea></div>
            <div class="form-group"><label>Cover Image URL (optional)</label><input type="url" id="wt-image"></div>
            <div id="add-walkthrough-message"></div>
            <button type="submit" class="btn btn-primary" style="width:100%; margin-top:1rem;">Add Walkthrough</button>
        </form>
    </div>
</div>

<div id="add-part-modal" class="modal">
    <div class="modal-content">
        <button class="close-modal" onclick="closeModal('add-part-modal')">&times;</button>
        <h2 style="color:var(--accent); font-family:'Press Start 2P', cursive; font-size:1.2rem; margin-bottom:2rem;">Add Walkthrough Part</h2>
        <form onsubmit="addWalkthroughPart(event)">
            <input type="hidden" id="part-game-id">
            <div class="form-group"><label>Part Title (e.g. "Part 1: Pallet Town to Pewter City")</label><input type="text" id="part-title" required></div>
            <div class="form-group"><label>YouTube Video URL</label><input type="url" id="part-video" required></div>
            <div class="form-group"><label>Written Guide</label><textarea id="part-content" required style="min-height:180px;"></textarea></div>
            <div class="form-group"><label>Key Items & Tips</label><textarea id="part-tips"></textarea></div>
            <div id="add-part-message"></div>
            <button type="submit" class="btn btn-primary" style="width:100%; margin-top:1rem;">Add Part</button>
        </form>
    </div>
</div>

<div id="walkthrough-detail-modal" class="modal">
    <div class="modal-content" style="max-width:1100px;">
        <button class="close-modal" onclick="closeModal('walkthrough-detail-modal')">&times;</button>
        <div id="walkthrough-detail-content"></div>
    </div>
</div>


<div id="admin-login-modal" class="modal">
    <div class="modal-content">
        <button class="close-modal" onclick="closeModal('admin-login-modal')">&times;</button>
        <h2 style="color:var(--accent); font-family:'Press Start 2P', cursive; font-size:1.3rem; margin-bottom:2rem; text-align:center;">Admin Login</h2>
        <form onsubmit="adminLogin(event)">
            <div class="form-group">
                <label>Password</label>
                <input type="password" id="admin-password" required>
            </div>
            <div id="login-message"></div>
            <button type="submit" class="btn btn-primary" style="width:100%; margin-top:1rem;">Login</button>
        </form>
    </div>
</div>

<script>

    // Theme handling
    function setTheme(theme) {
        localStorage.setItem('to_theme', theme);
        document.documentElement.setAttribute('data-theme', theme);
        updateThemeButtons();
    }
    function updateThemeButtons() {
        var theme = localStorage.getItem('to_theme') || 'dark';
        var dark = document.getElementById('btn-dark');
        var light = document.getElementById('btn-light');
        if (dark && light) {
            dark.classList.toggle('active', theme === 'dark');
            light.classList.toggle('active', theme === 'light');
        }
    }
    updateThemeButtons();

    // Hide loader once page is ready (also acts as min-flash-free load)
    window.addEventListener('load', function() {
        var loader = document.getElementById('page-loader');
        if (loader) {
            setTimeout(function(){ loader.classList.add('hide'); }, 150);
        }
    });
    // Fallback in case 'load' fires slowly on some assets
    document.addEventListener('DOMContentLoaded', function() {
        setTimeout(function() {
            var loader = document.getElementById('page-loader');
            if (loader) loader.classList.add('hide');
        }, 900);
    });

    const ADMIN_PASSWORD = 'pokemon2024';
    let isAdmin = (sessionStorage.getItem('to_isAdmin') === 'true');

    function showAdminLogin() {
        var m = document.getElementById('admin-login-modal');
        if (m) m.classList.add('active');
    }
    function closeModal(id) {
        var m = document.getElementById(id);
        if (m) m.classList.remove('active');
    }
    function adminLogin(event) {
        event.preventDefault();
        const password = document.getElementById('admin-password').value;
        const messageDiv = document.getElementById('login-message');
        if (password === ADMIN_PASSWORD) {
            isAdmin = true;
            sessionStorage.setItem('to_isAdmin', 'true');
            messageDiv.innerHTML = '<div class="success-msg">Login successful! Admin features enabled.</div>';
            setTimeout(() => {
                closeModal('admin-login-modal');
                if (typeof onAdminEnabled === 'function') onAdminEnabled();
            }, 800);
        } else {
            messageDiv.innerHTML = '<div class="error-msg">Incorrect password!</div>';
        }
    }
    if (isAdmin && typeof onAdminEnabled === 'function') {
        document.addEventListener('DOMContentLoaded', onAdminEnabled);
    }


    if (!localStorage.getItem('walkthroughs')) {
        localStorage.setItem('walkthroughs', JSON.stringify([
{"id": 1, "title": "Pokémon FireRed", "type": "official", "description": "Complete walkthrough of Pokémon FireRed with detailed guides, item locations, and strategies.", "image": "", "parts": [{"id": 101, "title": "Part 1: Pallet Town & Your First Pokémon", "videoUrl": "#", "content": "This is the walkthrough for Pokémon FireRed and LeafGreen.<br><br>Contents · Introduction<br><br>Pallet Town:<br><br>Home · 2F · 1F<br><br>Oak Appears!<br><br>Professor Oak's Lab:<br><br>Rival Battle 1 · Introduction<br><br>After a brief cutscene, press the A Button or Start on the title screen. The player is shown a list of controls in order of importance, then with a mission statement from the games' developers. Afterward, the researcher of the Kanto region, Professor Oak, appears on screen and explains a few basics.<br><br>Firstly, Professor Oak asks you to choose your gender and then select a name (7 characters long). Using the Control Pad will allow you to move the cursor and the Select Button to move through three pages of upper-case letters, lower-case letters, and other characters. On this screen, if you press the A Button will select a letter whereas pressing the B Button will delete the previous one. When you are done, press Start or select OK in the bottom-right corner.<br><br>Next, Professor Oak introduces his grandson, who happens to be your rival. The professor is having trouble remembering the boy's name and asks if you might know. Choose his name from a list of preset names or select a new one. With that done, you are transported into the world of Pokémon to begin your adventure!<br><br>Default Names · Pokémon FireRed Pokémon LeafGreen · Rival Green, Gary, Kaz, Toru · Player: Red, Ash, Kene, Geki · Pallet Town<br><br>Your journey begins in Pallet Town, in the southwest part of the Kanto region. It is a rather small, quaint town with only three buildings. The western house belongs to you and Mom, while the eastern one is home to your rival and his sister. The large building to the south is Professor Oak's Laboratory. The north part of town leads to the tall grasses of Route 1, and the waters to the south open up to Route 21.<br><br>Available Pokémon .<br><br>Bulbasaur Charmander Squirtle Grass Poison Fire Water Ivysaur Charmeleon Wartortle Grass Poison Fire Water Venusaur Charizard Blastoise Grass Poison Fire Flying Water<br><br>Pokémon Games Location Levels · Bulbasaur | FR: LG | First Partner | 5 | One · Charmander | FR:LG | First Partner | 5 | One · Squirtle | FR:LG | First Partner | 5 | One · Items · Item Location Games<br><br>Potion |Home; retrievable from the player's PC |FR LG<br><br>Later visit<br><br>Pokédex |Oak's Lab; from Professor Oak, after he<br><br>|receives his parcel |FR LG<br><br>Poké BalL ×5 |Oak's Lab; from Professor Oak, after<br><br>|obtaining the Pokédex |FR LG<br><br>Town Map |Blue's house; from Daisy, after obtaining<br><br>|the Pokédex |FR LG · Home · 2F<br><br>Your journey begins in your bedroom, with you standing in front of your Nintendo Entertainment System. Now that you can control your character, the various buttons and their effects are as follows:<br><br>Input Effect(s)<br><br>+Control Pad Moves character; moves cursor in a menu<br><br>A Button Interact with people and the environment; select menu options<br><br>B Button Cancel a selection; exit a menu · Start Opens the main menu · Select Sort items; use a registered item · L Button, R Button Activates the Help System<br><br>The PC in the corner can be used as store items your item storage and check Mailbox.<br><br>Your Bag has three pockets: one for Items, one for Key Items, and one for Poké Balls. Each pocket can hold up to 42 different items and up to 999 of each item. If a pocket becomes full, it would be necessary to use or discard some items before obtaining anything new. The PC can hold up to 30 different items from the Items pocket. Deposit Item and Withdraw Item allow for moving items between inventory and storage. It seems as though there is already an item in storage, so select Withdraw Item and choose the Potion to add to your Bag. Press the B Button to close the menus and return to your bedroom. To save the game, press Start to open the main menu, select Save, and then Yes. When the menu disappears, your progress is saved and it is safe to exit the game.<br><br>Mail is a type of held item. You may leave a note on each piece of Mail when giving one to one of your Pokémon. This message can be sent to other Trainers by trading Pokémon. When taking a piece of Mail from a Pokémon, you may choose to place it in their Bag or send it to their Mailbox. You can store it in the Mailbox to preserve the original message.<br><br>You can go downstairs by stepping on the stairs in the northeast corner of the room.<br><br>1F<br><br>Your Mom is sitting at the table and tells you that Professor Oak has been looking for you. To leave the house, step on the floor mat along the south wall and press down on the +Control Pad.<br><br>Oak Appears!<br><br>Exit the house. Pallet Town has only a few places to explore, and Professor Oak is nowhere to be found. Head for the tall grass on the north side of town. Suddenly, the professor appears! He scolds you for trying to venture off on your own, as it can be dangerous without a Pokémon of your own for defense against wild Pokémon. He will take you to his lab.<br><br>Professor Oak's Lab<br><br>Inside his lab Blue is already waiting and gives you the choice of your very first Pokémon. Each has its advantages and disadvantages, so simply choose the one that you like the best.<br><br>Name|<br><br>Bulbasaur Charmander Squirtle Grass Poison Fire Water Ivysaur Charmeleon Wartortle Grass Poison Fire Water Venusaur Charizard Blastoise Grass Poison Fire Flying Water<br><br>Bulbasaur |Squirtle| Charmander · Typing: Grass:Poison |Water| Fire · Ability: Overgrow |Torrent Blaze · Ivysaur Wartortle Charmeleon · Venusaur Blaistoise Charizard · Typing: Fire/Flying<br><br>Once you are done selecting a Pokémon, you can nickname it if you like. Your rival will pick next and choose the one that has a type advantage over your Pokémon. As you try to leave, he will challenge you to a Pokémon battle!<br><br>Rival Battle 1<br><br>As you and rival, Professor Oak defines the basics. When battling another trainer, one Pokemon is sent at a time, both Pokemon are at Level 5 written next to the name of pokemon. Below it is the green health bar which shows your Pokemon's remaining HP. You can win a battle by lowering your health of your Opponent Pokemon to 0. Winning a battle gives you experience points that will level up your Pokémon and it will eventually evolve.<br><br>Choosing Fight shows you the attacks you can against your opponent. Each of the Pokémon will have two moves. The first move can damage your opponent and the other one lowers it stats. You can restore your Pokémon to full health when low on health. You can also buy potions from the Poke Mart to heal your Pokémon on the go.<br><br>If you choose Bulbasaur<br><br>If the player chose Bulbasaur:<br><br>Rival · Blue · Professor Oak's Laboratory · FireRed and LeafGreen · Reward: $80 · Charmander♂ Lv.5<br><br>Type:<br><br>Fire<br><br>Ability:<br><br>Blaze<br><br>Held item:<br><br>None · Scratch · Normal · Growl · Normal<br><br>If the player chose Charmander:<br><br>Rival · Blue · Professor Oak's Laboratory · FireRed and LeafGreen · Reward: $80 · Squirtle♂ Lv.5<br><br>Type:<br><br>Water<br><br>Ability:<br><br>Torrent<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal<br><br>If the player chose Squirtle:<br><br>Rival · Blue · Professor Oak's Laboratory · FireRed and LeafGreen · Reward: $80 · Bulbasaur♂ Lv.5<br><br>Types:<br><br>Grass · Poison<br><br>Ability:<br><br>Overgrow<br><br>Held item:<br><br>None · Tackle · Normal · Growl · Normal<br><br>You earn $80 in prizes after defeating Blue after which he leaves. He makes a joke about his sister having two maps and telling her not to lend you one before leaving. Your chosen Pokémon will grow to Level 6. Exit the laboratory and head to Route 1.", "tips": ""}, {"id": 102, "title": "Part 2: Route 1, Viridian City, Viridian Forest & Pewter Gym", "videoUrl": "#", "content": "Contents Tab (Make it collapsing and expanding tab)<br><br>Route 1:<br><br>Free Potion<br><br>Viridian City:<br><br>Pokémon Center · Poke Mart · Special Delivery · Pokémon Academy<br><br>Pallet Town:<br><br>Oak's Lab · Blue's House · Viridian City<br><br>Route 22:<br><br>Rival Battle 2 · Route 2 (West)<br><br>Introduction:<br><br>Route 1:<br><br>It is a quaint, country road that is north of Viridian City from Pallet Town. Path 1 from Pokémon includes ledges so the player must travel through the tall grass. It is not possible to catch Pokémon yet, but it is a good place to gain experience and level up your Pokémon.<br><br>You can catch the following pokemon here:<br><br>Free Sample:<br><br>Talk to the guy on the south side of the route, near the signpost. He works at the Poke Mart in Viridian City and gives you a potion as a free sample.<br><br>Items Item · Location · Games · Oak's Parcel · Poké Mart; from the shopkeeper · FR LG · Potion<br><br>Near the city's north exit, west of the small tree<br><br>FR LG · Later visit · Teachy TV<br><br>From the old man who demonstrates how to catch a Pokémon<br><br>FR LG · TM26 (Earthquake) · From the Gym Leader, after defeating him<br><br>Viridian City:<br><br>It is tiny, city that is surrounded by green all year round. It is situated between Route 1 to the south, Route 2 to the north, and Route 22 to the west.<br><br>Pokémon Center:<br><br>The first building is the Pokémon Center. It is useful for healing your Pokémon any time they are low on health and removing status conditions. You can use the PC to store Pokémon that you don't want to keep in your active party. There are 30 boxes so there's plenty of space. There's withdraw and deposit option for quickly leaving and taking Pokémon. The item option allows you to take the item each Pokémon is holding while in storage.<br><br>Poke Mart:<br><br>Poké Mart · Poké Ball · $200 · Potion · $300 · Antidote · $100 · Parlyz Heal · $200<br><br>It is located to the right of the Pokémon Center. You can buy different items such as Poke ball, Potion, Antidote, and Paralyze heal. More items become available as you progress through the game.<br><br>Special Delivery: As soon as you enter the mart, the shopkeeper asks you if you are from Pallet Town and hands over Professor Oak's package to you. He asks you to give it to him. You can't buy anything yet.<br><br>Pokémon Academy:<br><br>It teaches different basic knowledge regarding Pokémon to inexperienced or new trainers. The blackboards describe the five different status conditions and their effects:<br><br>Ailment Effect(s) BRN Burn Attack drops to 50%; inflicts damage equal to 1/8 of maximum HP every turn FRZ Freeze Cannot move until thawed PAR Paralysis Speed drops to 25%; cannot attack 1/4 of the time PSN Poison Inflicts damage equal to 1/8 of maximum HP every turn; loses 1 HP for every five steps taken outside of battle SLP Sleep Cannot move for one to six turns<br><br>Prof Oak's Lab:<br><br>As soon you deliver Oak's parcel to him, your rival Blue appears. The Professor gives you and your rival a pokedex which records data on a pokemon when it is caught. He asks you and your rival to go and complete the pokedex since he can't in his old age. He also gives you five pokeballs to help you catch pokemon as part of that filling the pokedex.<br><br>Blue's House:<br><br>Talk to his sister Daisy to receive a town map.<br><br>Kanto Region Map<br><br>Viridian City:<br><br>When you reach Viridian City again, talk to the old guy who will be up now that he has had his coffee. He notices you have a pokedex and gives you a demonstration of how to catch a Pokémon. Afterwards he gives you the Teachy TV which contains video explaining basics of being a trainer. Use it if you don't understand anything.<br><br>You can head either to Route or Route 22.<br><br>Route 22:<br><br>It is not fully unlocked yet. There's a few different Pokémon available such as:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Rattata · FR · LG · Grass · 2-5 · 45% · Mankey · FR · LG · Grass · 2-5 · 45% · Spearow · FR · LG · Grass · 3, 5 · 10%<br><br>However, Blue appears and challenges you to a battle. His team is as follows:<br><br>If the player chose Bulbasaur:<br><br>Rival · Blue · Route 22 · FireRed and LeafGreen · Reward: $144 · Pidgey♂ Lv.9<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Sand-Attack · Ground · Gust · Flying · Charmander♂ Lv.9<br><br>Type:<br><br>Fire<br><br>Ability:<br><br>Blaze<br><br>Held item:<br><br>None · Scratch · Normal · Growl · Normal<br><br>If the player chose Charmander:<br><br>Rival · Blue · Route 22 · FireRed and LeafGreen · Reward: $144 · Pidgey♂ Lv.9<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Sand-Attack · Ground · Gust · Flying · Squirtle♂ Lv.9<br><br>Type:<br><br>Water<br><br>Ability:<br><br>Torrent<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal<br><br>If the player chose Squirtle:<br><br>Rival · Blue · Route 22 · FireRed and LeafGreen · Reward: $144 · Pidgey♂ Lv.9<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Sand-Attack · Ground · Gust · Flying · Bulbasaur♂ Lv.9<br><br>Types:<br><br>Grass · Poison<br><br>Ability:<br><br>Overgrow<br><br>Held item:<br><br>None · Tackle · Normal · Growl · Normal<br><br>Heal up your Pokémon at the PC after the battle regardless of the outcome. Stock up on some potions and repels at the Poke Mart. Head to Route 2 then.<br><br>Route 2:<br><br>You can find the following Pokémon’s here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Pidgey · FR · LG · Grass · 2-5 · 45% · Rattata · FR · LG · Grass · 2-5 · 45% · Caterpie · FR · LG · Grass · 4-5 · 5% · Weedle · FR · LG · Grass · 4-5 · 5%<br><br>Additionally, players can encounter a Mr. Mime through an in-game trade with a trainer who requests an Abra. Items such as Ether, Paralyze Heal, and HM05 Flash can be found on the route.<br><br>(Note that HM05 Flash and Mr Mime can only be acquired when the player has the HM Cut. Abra is also not available in the grass until you reach Cerulean City).<br><br>The player enters Viridian Forest next. You can find the following Pokémon here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Caterpie · FR · LG · Grass · 3-5 · 40% · Weedle · FR · LG · Grass · 3-5 · 40% · Metapod · FR · LG · Grass · 4-6 · 10% · Kakuna · FR · LG · Grass · 4-6 · 10% · Metapod · FR · LG · Grass · 5 · 5% · Kakuna · FR · LG · Grass · 5 · 5% · Pikachu · FR · LG · Grass · 3, 5 · 5%<br><br>You can find the following items as well:<br><br>Items Item · Location · Games · Poké Ball<br><br>Dead-end grassy path northwest of the south entrance<br><br>FR LG · Antidote ×2<br><br>• West side of the lone tree near the south entrance (hidden)<br><br>• Northeast area of the forest, past a Trainer Tips sign<br><br>FR LG · Potion ×3<br><br>• Tall grass patch, east of the southern entrance<br><br>• Dead-end path southeast of the north exit<br><br>• In front of Bug Catcher Sammy near the north exit (hidden)<br><br>FR LG<br><br>Head towards the tall grass on the left and go north then. The bug catchers will have the following Pokémon:<br><br>Trainer Pokemon Rewards Bug Catcher Rick · Weedle♂ · Lv.6 · No item · Caterpie♂ · Lv.6 · No item · $ 72 Bug Catcher Doug · Weedle♂ · Lv.7 · No item · Kakuna♂ · Lv.7 · No item · Weedle♂ · Lv.7 · No item · $ 84 Bug Catcher Anthony · Caterpie♂ · Lv.7 · No item · Caterpie♂ · Lv.8 · No item · $ 96 Bug Catcher Charlie · Metapod♂ · Lv.7 · No item · Caterpie♂ · Lv.7 · No item · Metapod♂ · Lv.7 · No item · $ 84 Bug Catcher Sammy · Weedle♂ · Lv.9 · No item · $ 108<br><br>Step into the walkway between and exit through the other end to reach Route 2. Diglett Cave is on the right, but it can be accessed when you have the HM01 Cut.<br><br>Pewter City:<br><br>There’s a few things you can do here.<br><br>You can visit the Pewter Museum of Science. The fee is $50. It contains fossils of ancient Pokémon like Kabutops and Omastar. It has a replica model of a rocket.<br><br>Head to the Gym to challenge Brock then. If you don’t feel like walking to the Gym, talk to the boy blocking the way ahead. He will take you to the front of the Pewter Gym.<br><br>There’s only one trainer in the Gym apart from from Brock. Their teams is as follows:<br><br>Pewter Gym · Trainers Trainer · Pokémon · Camper Liam Reward: $220 · Geodude♂ · Lv.10 · No item · Sandshrew♂ · Lv.11 · No item · Leader · Brock · Pewter Gym · FireRed and LeafGreen · Reward: $1,400 · Geodude♂ Lv.12<br><br>Types:<br><br>Rock · Ground<br><br>Ability:<br><br>Rock Head<br><br>Held item:<br><br>None · Tackle · Normal · Defense Curl · Normal · Onix♂ Lv.14<br><br>Types:<br><br>Rock · Ground<br><br>Ability:<br><br>Rock Head<br><br>Held item:<br><br>None · Tackle · Normal · Bind · Normal · Rock Tomb · Rock<br><br>After winning against Brock, he praises your skill and hands you the Boulder Badge. He also gives you TM39: Rock Tomb. Exit the gym afterwards and heal up. Stock up on potions, antidotes, paralyze heal, repels and a few escape ropes. Next step is to head East then towards Route 3.", "tips": ""}, {"id": 103, "title": "Part 3: Route 3, Mt. Moon, Cerulean City & Cerulean Gym", "videoUrl": "#", "content": "Route 3<br><br>An aide of Prof 0ak will show up as soon as you head East saying your mom sent you running shoes and a letter attached to the shoe that says: Love Mom. There are a bunch of trainers on the way to Mt Moon with the following teams:<br><br>Trainers Trainer · Pokémon · Lass Janice Reward: $144 · Pidgey♀ · Lv.9 · No item · Pidgey♀ · Lv.9 · No item · Bug Catcher Colton Reward: $120 · Caterpie♂ · Lv.10 · No item · Weedle♂ · Lv.10 · No item · Caterpie♂ · Lv.10 · No item · Youngster Ben Reward: $176 · Rattata♂ · Lv.11 · No item · Ekans♂ · Lv.11 · No item · Bug Catcher Greg Reward: $108 · Weedle♂ · Lv.9 · No item · Kakuna♂ · Lv.9 · No item · Caterpie♂ · Lv.9 · No item · Metapod♂ · Lv.9 · No item · Youngster Calvin Reward: $224 · Spearow♂ · Lv.14 · No item · Lass Sally Reward: $160 · Rattata♀ · Lv.10 · No item · Nidoran♀ · Lv.10 · No item · Bug Catcher James Reward: $132 · Caterpie♂ · Lv.11 · No item · Metapod♂ · Lv.11 · No item · Lass Robin Reward: $224 · Jigglypuff♀ · Lv.14 · No item<br><br>You can find the following Pokémon here:<br><br>Available Pokémon Pokémon · Games · Location Levels · Rate · Spearow · FR · Grass · 6-8 · 35% · Pidgey · FR · Grass · 6-7 · 30% · Nidoran♂ · FR · Grass · 6-7 · 14% · Jigglypuff · FR · Grass · 3, 5, 7 · 10% · Mankey · FR · Grass · 7 · 10% · Nidoran♀ · FR · Grass · 6 · 1%<br><br>Once you are done with all the trainers, keep going and head North. There’s a Pokemon Center up ahead so heal up. Once you are prepared, enter Mt. Moon.<br><br>Mt Moon:<br><br>Mt. Moon is a famous cave located between Pewter City and Cerulean City. It is known for its Moon Stones, Clefairy sightings, wild Pokémon, and ancient fossils hidden within its depths.<br><br>Mt Moon 1F · Mt Moon B1F · Mt Moon B2F<br><br>After entering Mt. Moon from Route 3, head through the cave while battling the trainers along the way. Early in the cave, you will face various trainers such as nerds, bug catchers, several hikers and Team Rocket Grunts.<br><br>Continue through the first floor (1F) and descend to B1F using the available staircases. In the lower section, battle the trainers and Team Rocket members while collecting items along the paths. Eventually, make your way back up through the appropriate staircase to 1F.<br><br>Continue toward the northeastern section of the cave, where you will encounter more Team Rocket Grunts and a Super Nerd. After defeating them, proceed to the fossil area and choose between the Dome Fossil and Helix Fossil.<br><br>From the fossil area, follow the remaining path toward the cave's exit. Continue through the final section until you reach the entrance leading to Route 4. From there, Cerulean City is just ahead.<br><br>The player will find the following trainers here.<br><br>Trainers 1F · Trainer · Pokémon · Bug Catcher Kent トモミチ Tomomichi Reward: $132 · Weedle♂ · Lv.11 · No item · Kakuna♂ · Lv.11 · No item · Lass Iris ナホ Naho Reward: $224 · Clefairy♀ · Lv.14 · No item · Super Nerd Jovan キミタカ Kimitaka Reward: $264 · Magnemite · Lv.11 · No item · Voltorb · Lv.11 · No item · Bug Catcher Robby ノリオ Norio Reward: $120 · Caterpie♂ · Lv.10 · No item · Metapod♂ · Lv.10 · No item · Caterpie♂ · Lv.10 · No item · Lass Miriam ルリ Ruri Reward: $176 · Oddish♀ · Lv.11 · No item · Bellsprout♀ · Lv.11 · No item · Youngster Josh タロウ Tarô Reward: $160 · Rattata♂ · Lv.10 · No item · Rattata♂ · Lv.10 · No item · Zubat♂ · Lv.10 · No item · Hiker Marcos カツト Katsuto Reward: $360 · Geodude♂ · Lv.10 · No item · Geodude♂ · Lv.10 · No item · Onix♂ · Lv.10 · No item<br><br>Once you reach B2F, you will find mostly Team Rocket members with a few scientists like follows:<br><br>B2F Trainer · Pokémon · Team Rocket Grunt Reward: $352 · Sandshrew♂ · Lv.11 · No item · Rattata♂ · Lv.11 · No item · Zubat♂ · Lv.11 · No item · Team Rocket Grunt Reward: $352 · Zubat♂ · Lv.11 · No item · Ekans♂ · Lv.11 · No item · Team Rocket Grunt Reward: $416 · Rattata♂ · Lv.13 · No item · Sandshrew♂ · Lv.13 · No item · Team Rocket Grunt Reward: $416 · Rattata♂ · Lv.13 · No item · Zubat♂ · Lv.13 · No item · Super Nerd Miguel ミツハル Mitsuharu Reward: $288 · Grimer♂ · Lv.12 · No item · Voltorb · Lv.12 · No item · Koffing♂ · Lv.12 · No item<br><br>Here’s the list of pokemon you will find on the various floors:<br><br>Available Pokémon 1F · Pokémon · Games · Location · Levels · Rate · Zubat · FR · LG · Cave · 7-10 · 69% · Geodude · FR · LG · Cave · 7-9 · 25% · Paras · FR · LG · Cave · 8 · 5% · Clefairy · FR · LG · Cave · 8 · 1% · B1F Pokémon · Games · Location · Levels · Rate · Paras · FR · LG · Cave · 5-10 · 100% · B2F Pokémon · Games · Location · Levels · Rate · Zubat · FR · LG · Cave · 8-11 · 49% · Geodude · FR · LG · Cave · 9-10 · 30% · Paras · FR · LG · Cave · 10, 12 · 15% · Clefairy · FR · LG · Cave · 10, 12 · 6% · Items Item · Location · Games · 1F · TM09 (Bullet Seed) · In the chamber to the west of the entrance · FR LG · Parlyz Heal · In the chamber to the west of the entrance · FR LG · Potion<br><br>Southeast area, on the opposite side of the wall from the entrance<br><br>FR LG · Rare Candy · Southeast corner, east of Super Nerd Jovan · FR LG · Escape Rope · East-central area · FR LG · Moon Stone · Northwest corner · FR LG<br><br>B1F TinyMushroom ×3 • Via the first ladder on 1F; on the second rock from the east of the four arranged west-east (hidden recurring item; group B and C)<br><br>• Via the second ladder on 1F; on the rock in the northeast corner (hidden recurring item; group B and C)<br><br>• Via the northwest ladder on B2F; on a rock in the northeast corner (hidden recurring item; group B and C) FR LG Big Mushroom ×3 • Via the first ladder on 1F; on the two reachable rocks northwest of the ladder to B2F (×2) (hidden recurring item; group C)<br><br>• Via the third ladder on 1F; on the southernmost rock (hidden recurring item; group C) FR LG<br><br>B2F Star Piece South; accessible via the first ladder found on 1F FR LG TM46 (Thief) Northeast; accessible via the second ladder found on 1F FR LG Ether Northeast; accessible via the second ladder found on 1F, on a rock (hidden) FR LG Moon Stone Main chamber; southeast of the stairway near the fossils, on a rock (hidden) FR LG Revive Main chamber; north of the ladder in the center of the floor FR LG Dome Fossil Main chamber; choice between the two Fossils, after defeating the Super Nerd on the northwest platform FR LG Helix Fossil Antidote Southwest of the ladder in the northwest corner FR LG<br><br>Cerulean City<br><br>Cerulean City is a peaceful, water-themed city in northern Kanto, surrounded by rivers and waterways. Its bright blue buildings, open streets, and scenic waterfront give it a clean and lively appearance.<br><br>There are a few things that be of help to you.<br><br>To the north north-east, an old man. If you provide him with required quantity of Berry, he can concoct several types of medicines. When you visit him for the first time, he will give you the Powder Jar. It can store all berry power concocted by the old man.<br><br>Berry Powder · EnergyPowder · 50 units · Energy Root · 80 units · Heal Powder · 50 units · Revival Herb · 300 units · Protein · 1,000 units · Iron · 1,000 units · Carbos · 1,000 units · Calcium · 1,000 units · Zinc · 1,000 units · HP Up · 1,000 units · PP Up · 3,000 units<br><br>Next is the bike shop however the bike is just too expensive. You can obtain it right now.<br><br>The next step should head to trainer bridge (Route 24) where your rival will engage you in battle once again. Although you can head to the Gym first if you like.<br><br>If the player chose Bulbasaur:<br><br>Rival · Blue · Cerulean City · FireRed and LeafGreen · Reward: $288 · Pidgeotto♂ Lv.17<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Abra♂ Lv.16<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Rattata♂ Lv.15<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Charmander♂ Lv.18<br><br>Type:<br><br>Fire<br><br>Ability:<br><br>Blaze<br><br>Held item:<br><br>None · Scratch · Normal · Growl · Normal · Ember · Fire · Metal Claw · Steel<br><br>If the player chose Charmander:<br><br>Rival · Blue · Cerulean City · FireRed and LeafGreen · Reward: $288 · Pidgeotto♂ Lv.17<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Abra♂ Lv.16<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Rattata♂ Lv.15<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Squirtle♂ Lv.18<br><br>Type:<br><br>Water<br><br>Ability:<br><br>Torrent<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Withdraw · Water · Water Gun · Water<br><br>If the player chose Squirtle:<br><br>Rival · Blue · Cerulean City · FireRed and LeafGreen · Reward: $288 · Pidgeotto♂ Lv.17<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Abra♂ Lv.16<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Rattata♂ Lv.15<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Bulbasaur♂ Lv.18<br><br>Types:<br><br>Grass · Poison<br><br>Ability:<br><br>Overgrow<br><br>Held item:<br><br>None · Sleep Powder · Grass · PoisonPowder · Poison · Vine Whip · Grass · Leech Seed · Grass<br><br>After the battle, your rival mentions he visited a famous poke maniac named Bill who invented the Pokémon storage system. He says the usual things about what is going to do next and leaves briefly. He comes back and gives you the Fame Checkers saying he doesn’t want it and exits for good finally. Next are the five trainers on the bridge.<br><br>Route 24 extends further to route 25 leading towards Bill’s house and Cape Brink. Defeat the five trainers on the bridge for a reward.<br><br>Trainers Trainer · Pokémon · Nugget Bridge · Bug Catcher Cale Reward: $120 · Caterpie♂ · Lv.10 · No item · Weedle♂ · Lv.10 · No item · Metapod♂ · Lv.10 · No item · Kakuna♂ · Lv.10 · No item · Lass Ali Reward: $192 · Pidgey♀ · Lv.12 · No item · Oddish♀ · Lv.12 · No item · Bellsprout♀ · Lv.12 · No item · Youngster Timmy Reward: $224 · Sandshrew♂ · Lv.14 · No item · Ekans♂ · Lv.14 · No item · Lass Reli Reward: $256 · Nidoran♂ · Lv.16 · No item · Nidoran♀ · Lv.16 · No item · Camper Ethan Reward: $360 · Mankey♂ · Lv.18 · No item · Team Rocket Grunt Reward: $480 · Ekans♂ · Lv.15 · No item · Zubat♂ · Lv.15 · No item<br><br>The TR Grunt will make you an offer to join TR however the game makes it its choice to reject him by itself.<br><br>Grassy area · Camper Shane Reward: $280 · Rattata♂ · Lv.14 · No item · Ekans♂ · Lv.14 · No item<br><br>Here are the pokemon you can catch here.<br><br>Available Pokémon Pokémon · Location · Levels · Rate · Oddish · FR · Grass · 12-14 · 25% · Caterpie · FR · Grass · 7 · 20% · Weedle · FR · Grass · 7 · 20% · Pidgey · FR · Grass · 11, 13 · 15% · Abra · FR · Grass · 8, 10, 12 · 15% · Kakuna · FR · Grass · 8 · 4% · Metapod · FR · Grass · 8 · 1%<br><br>Progress towards Route 25. There are a god number of trainers here as well, perfect for levelling up.<br><br>Trainers Trainer · Pokémon · Hiker Franklin Reward: $540 · Machop♂ · Lv.15 · No item · Geodude♂ · Lv.15 · No item · Hiker Wayne Reward: $612 · Onix♂ · Lv.17 · No item · Youngster Joey Reward: $240 · Rattata♂ · Lv.15 · No item · Spearow♂ · Lv.15 · No item · Youngster Dan Reward: $272 · Slowpoke♂ · Lv.17 · No item · Picnicker Kelsey Reward: $300 · Nidoran♂ · Lv.15 · No item · Nidoran♀ · Lv.15 · No item · Hiker Nob Reward: $468 · Geodude♂ · Lv.13 · No item · Geodude♂ · Lv.13 · No item · Machop♂ · Lv.13 · No item · Geodude♂ · Lv.13 · No item · Camper Flint Reward: $280 · Rattata♂ · Lv.14 · No item · Ekans♂ · Lv.14 · No item · Youngster Chad Reward: $224 · Ekans♂ · Lv.14 · No item · Sandshrew♂ · Lv.14 · No item · Lass Haley Reward: $208 · Oddish♀ · Lv.13 · No item · Pidgey♀ · Lv.13 · No item · Oddish♀ · Lv.13 · No item<br><br>After you are done with battling the trainers, head to Cape Brink. There is nothing outside the cottage except a couple who don’t battle. Enter the cottage. Once you are inside, you will see that Bill has turned into a clefairy by merging his cells with it. He asks you to go to his computer and help him turn back to human. Once he is back to human form, talk to him. He asks you if you came to see his eeveelution collection. He hands you the SS Anne Ticket, a ship in Vermillion City. Head over to Cerulean City and heal up. Head to the gym then. The experience points from the route 24 and 25 battles will hopefully make it easier to win.<br><br>The Cerulean Gym is a pure water type Gym. It has 4 trainers excluding Misty, the gym leader. It is swimming pool mainly that’s been turned into a Gym. The Gym trainers have the following teams:<br><br>Cerulean Gym · Trainer · Pokémon · Swimmer Luis Reward: $64 · Horsea♂ · Lv.16 · No item · Shellder♂ · Lv.16 · No item · Picnicker Diana Reward: $380 · Goldeen♀ · Lv.19 · No item · Leader · Misty · Cerulean Gym · FireRed and LeafGreen · Reward: $2,100 · Staryu Lv.18<br><br>Type:<br><br>Water<br><br>Ability:<br><br>Natural Cure<br><br>Held item:<br><br>None · Tackle · Normal · Harden · Normal · Recover · Normal · Water Pulse · Water · Starmie Lv.21<br><br>Types:<br><br>Water · Psychic<br><br>Ability:<br><br>Natural Cure<br><br>Held item:<br><br>None · Rapid Spin · Normal · Swift · Normal · Recover · Normal · Water Pulse · Water<br><br>After you defeat her, she gives you the Cascade Badge along with the TM03 Water Pulse. The Cascade Badge allows people up to level 30 to obey you and allows you to use HMO1 Cut outside of battle too. Exit the Gym after winning and heal up.", "tips": ""}, {"id": 104, "title": "Part 4: Route 5, S.S. Anne & Vermilion Gym", "videoUrl": "#", "content": "Route 5:<br><br>Route 5 is located between Cerulean City and Saffron City. The first Underground Path begins and runs southward underneath Saffron City leading the player to route 6.<br><br>Route 5<br><br>Here are the Pokémon available here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Pidgey · FR · LG · Grass · 13, 15-16 · 40% · Meowth · FR · LG · Grass · 10, 12, 14, 16 · 35% · Oddish · FR · LG · Grass · 13, 15-16 · 25% · Bellsprout · FR · LG · Grass · 13, 15-16 · 25%<br><br>The nearby house is the Pokémon Day Care. The player can hand over one pokemon to the old day for care. The pokemon will gain exp points for every step taken by the player. He may teach your deposited pokemon moves that you may not like. He will charge $100 for returning the pokemon and $100 for every level raised.<br><br>Take the underground path and go through the tunnel to reach route 6. Route 6 leads to Vermillion City. It has several trainers, good for levelling up.<br><br>Here are the pokemon available here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Pidgey · FR · LG · Grass · 13, 15-16 · 40% · Meowth · FR · LG · Grass · 10, 12, 14, 16 · 35% · Oddish · FR · LG · Grass · 13, 15-16 · 25% · Bellsprout · FR · LG · Grass · 13, 15-16 · 25% · Trainers Trainer · Pokémon · Bug Catcher Keigo Reward: $192 · Weedle♂ · Lv.16 · No item · Caterpie♂ · Lv.16 · No item · Weedle♂ · Lv.16 · No item · Camper Ricky Reward: $400 · Squirtle♂ · Lv.20 · No item · Picnicker Nancy Reward: $320 · Rattata♀ · Lv.16 · No item · Pikachu♀ · Lv.16 · No item · Bug Catcher Elijah Reward: $240 · Butterfree♂ · Lv.20 · No item · Picnicker Isabelle Reward: $320 · Pidgey♀ · Lv.16 · No item · Pidgey♀ · Lv.16 · No item · Pidgey♀ · Lv.16 · No item · Camper Jeff Reward: $320 · Spearow♂ · Lv.16 · No item · Raticate♂ · Lv.16 · No item<br><br>Head to Vermillion City after defeating them and heal up at the PC. There are a few things to do here including SS. Anne, or Vermillion Gym.<br><br>Vermillion CIty<br><br>First head to the Pokémon Fan Club and listen to the Chairman talk about Rapidash. He will give you a Bike Voucher for listening to him. Exchange it for the bike later at Cerulean Bike Shop.<br><br>Head to the Vermillion Harbour and have your ticket flashed. Enter SS. Anne then.<br><br>Head downstairs and grab the following items:<br><br>B1F:<br><br>This part of the ship leads to a dead-end with five cabins. Inspect the trash can by the stairs for a Hyper Potion. Visit the room at the far right to get a Super Potion and the middle room to get an Ether. TM44 (Rest) the fourth room from the stairs, then head back up to the main floor.<br><br>1F:<br><br>Go through the hallway around to the front of the ship and enter the second cabin from the left. After defeating Youngster Tyler, continue towards the kitchen. Pick up the Great Ball in the corner and inspect the three trash cans for any forgotten items. Leave the kitchen and climb the nearest stairs to reach the upper floor.<br><br>2F:<br><br>2F<br><br>The closest doorway leads to the deck of the ship, where two Sailors will challenge you to a battle. Enter the second cabin from the left to battle Fisherman Dale, Gentleman Brooks, and get a Stardust. You can visit the fourth room to battle either Lass Dawn or Gentleman Lamar.<br><br>As soon as you head towards the captain’s room at the back of the ship, Blue exist his room.<br><br>He will talk about Cut Master simply being an old man and will challenge you to battle as usual.<br><br>He has the following team:<br><br>If the player chose Bulbasaur:<br><br>Rival · Blue · S.S. Anne · FireRed and LeafGreen · Reward: $720 · Pidgeotto♂ Lv.19<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Raticate♂ Lv.16<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Hyper Fang · Normal · Kadabra♂ Lv.18<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Confusion · Psychic · Disable · Normal · Kinesis · Psychic · Charmeleon♂ Lv.20<br><br>Type:<br><br>Fire<br><br>Ability:<br><br>Blaze<br><br>Held item:<br><br>None · Scratch · Normal · Growl · Normal · Ember · Fire · Metal Claw · Steel<br><br>If the player chose Charmander:<br><br>Rival · Blue · S.S. Anne · FireRed and LeafGreen · Reward: $720 · Pidgeotto♂ Lv.19<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Raticate♂ Lv.16<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Hyper Fang · Normal · Kadabra♂ Lv.18<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Confusion · Psychic · Disable · Normal · Kinesis · Psychic · Wartortle♂ Lv.20<br><br>Type:<br><br>Water<br><br>Ability:<br><br>Torrent<br><br>Held item:<br><br>None · Bite · Dark · Bubble · Water · Withdraw · Water · Water Gun · Water<br><br>If the player chose Squirtle:<br><br>Rival · Blue · S.S. Anne · FireRed and LeafGreen · Reward: $720 · Pidgeotto♂ Lv.19<br><br>Types:<br><br>Normal · Flying<br><br>Ability:<br><br>Keen Eye<br><br>Held item:<br><br>None · Tackle · Normal · Gust · Flying · Sand-Attack · Ground · Quick Attack · Normal · Raticate♂ Lv.16<br><br>Type:<br><br>Normal<br><br>Ability:<br><br>Guts<br><br>Held item:<br><br>None · Tackle · Normal · Tail Whip · Normal · Quick Attack · Normal · Hyper Fang · Normal · Kadabra♂ Lv.18<br><br>Type:<br><br>Psychic<br><br>Ability:<br><br>Synchronize<br><br>Held item:<br><br>None · Teleport · Psychic · Confusion · Psychic · Disable · Normal · Kinesis · Psychic · Ivysaur♂ Lv.20<br><br>Types:<br><br>Grass · Poison<br><br>Ability:<br><br>Overgrow<br><br>Held item:<br><br>None · Sleep Powder · Grass · PoisonPowder · Poison · Vine Whip · Grass · Leech Seed · Grass<br><br>He taunts you once more before leaving. Head upstairs. The captain will be seasick. Talk to him and rub his back to make him well. He gives you HM01 Cut. Exit the ship then. SS. Anne will leave as soon as you exit. Heal up at the PC and teach one of your pokemon cut (the HM Bot if you have one).<br><br>Vermillion Gym:<br><br>Head to the Vermillion Gym then. It specializes in electric types. Rely on using ground types preferably Diglett from the Diglett Cave.<br><br>Vermilion Gym · Trainers Trainer · Pokémon · Sailor Dwayne Reward: $672 · Pikachu♂ · Lv.21 · No item · Pikachu♂ · Lv.21 · No item · Engineer Baily Reward: $1008 · Voltorb · Lv.21 · No item · Magnemite · Lv.21 · No item · Gentleman Tucker Reward: $1656 · Pikachu♂ · Lv.23 · No item<br><br>Take on the gym trainers and talk to the ones standing near the electric locks to get hints about opening them. Try pressing A on each trash, as soon as you open the first electric lock, press the adjacent can. If you click the wrong can, the puzzle will reset.<br><br>Make all preparations including healing up, buying potions and paralyze heal. Challenge Lt Surge to a battle.<br><br>Leader · Lt. Surge · Vermilion Gym · FireRed and LeafGreen · Reward: $2,400 · Voltorb Lv.21<br><br>Type:<br><br>Electric<br><br>Ability:<br><br>Soundproof<br><br>Held item:<br><br>None · Shock Wave · Electric · Tackle · Normal · Screech · Normal · SonicBoom · Normal · Pikachu♂ Lv.18<br><br>Type:<br><br>Electric<br><br>Ability:<br><br>Static<br><br>Held item:<br><br>None · Shock Wave · Electric · Thunder Wave · Electric · Quick Attack · Normal · Double Team · Normal · Raichu♂ Lv.24<br><br>Type:<br><br>Electric<br><br>Ability:<br><br>Static<br><br>Held item:<br><br>None · Shock Wave · Electric · Thunder Wave · Electric · Quick Attack · Normal · Double Team · Normal<br><br>If you manage to win, Lt Surge will hand you the Thunder Badge increasing the speed of your Pokémon overall. You are all done here now.", "tips": ""}, {"id": 105, "title": "Part 5: Route 11, Diglett's Cave, Route 9 & Route 10", "videoUrl": "#", "content": "Route 11 is located between Vermillion City and Route 12 to the east. The southeastern entrance of Diglett’s Cave and leads back to Route 2.<br><br>Here are the following trainers here:<br><br>Trainers · Youngster Eddie Reward: $336 · Ekans♂ · Lv.21 · No item · Gamer Hugo Reward: $1296 · Poliwag♂ · Lv.18 · No item · Horsea♂ · Lv.18 · No item · Engineer Bernie Reward: $864 · Magnemite · Lv.18 · No item · Magnemite · Lv.18 · No item · Magneton · Lv.18 · No item · Youngster Dave Reward: $288 · Nidoran♂ · Lv.18 · No item · Nidorino♂ · Lv.18 · No item · Youngster Dillon Reward: $304 · Sandshrew♂ · Lv.19 · No item · Zubat♂ · Lv.19 · No item · Gamer Jasper Reward: $1296 · Bellsprout♂ · Lv.18 · No item · Oddish♂ · Lv.18 · No item · Engineer Braxton Reward: $1008 · Magnemite · Lv.21 · No item · Gamer Darian Reward: $1296 · Growlithe♂ · Lv.18 · No item · Vulpix♀ · Lv.18 · No item · Youngster Yasu Reward: $272 · Rattata♂ · Lv.17 · No item · Rattata♂ · Lv.17 · No item · Raticate♂ · Lv.17 · No item · Gamer Dirk Reward: $1296 · Voltorb · Lv.18 · No item · Magnemite · Lv.18 · No item<br><br>You can find the following Pokémon here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Ekans · FR · LG · Grass · 12, 14-15 · 40% · Sandshrew · FR · LG · Grass · 12, 14-15 · 40% · Spearow · FR · LG · Grass · 13, 15, 17 · 35% · Drowzee · FR · LG · Grass · 11, 13, 15 · 25% · Fishing · Magikarp · FR LG · Fishing Old Rod · 5 100% Special Pokémon · Nidorina · FR LG · Trade Nidorino · The same as the traded Pokémon One · Nidorino · FR LG · Trade Nidorina · The same as the traded Pokémon One<br><br>You can find the following items here:<br><br>Items Item · Location · Games · Awakening · Northwest part of the route · FR LG · X Defend · Middle of the route, in a grass patch · FR LG<br><br>Escape Rope On a rock just north of the gate (hidden) FR LG Great Ball South of the gate FR LG Itemfinder In the gate; from Professor Oak's aide, after capturing 30 different species FR LG<br><br>Diglett Cave:<br><br>It is stretched across the whole region connecting route 11 to the east side of route 2. You can only find Diglett and Dugtrio here.<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Diglett · FR · LG · Cave · 15-22 · 95% · Dugtrio · FR · LG · Cave · 29, 31 · 5%<br><br>Route 2:<br><br>This side can be accessed when the player has the HM Cut. The northwestern end of Diglett’s cave emerges here.<br><br>Items Item · Location · Games · HM05 (Flash)<br><br>In the eastern gate; from Oak's aide, after catching at least 10 different species<br><br>FR LG · Ether · South of the gate and the first ledge · FR LG · Parlyz Heal · South of the second ledge · FR LG<br><br>You can visit Pewter City and use cut to get to the employee area of the Museum on the northeast hill. Head back to Cerulean City next. There are two ways to reach Cerulean City now through Mt Moon or Diglett’s Cave. When you are back in Cerulean City, head to the east side of the city and go forward after clearing the small tree.<br><br>Route 9:<br><br>It is a rocky path that connects Cerulean City and Route 10.<br><br>You can battle the following trainers here:<br><br>Trainers Trainer · Pokémon · Picnicker Alicia Reward: $360 · Oddish♀ · Lv.18 · No item · Bellsprout♀ · Lv.18 · No item · Oddish♀ · Lv.18 · No item · Bellsprout♀ · Lv.18 · No item · Hiker Jeremy Reward: $720 · Machop♂ · Lv.20 · No item · Onix♂ · Lv.20 · No item · Camper Chris Reward: $420 · Growlithe♂ · Lv.21 · No item · Charmander♂ · Lv.21 · No item · Bug Catcher Brent Reward: $228 · Beedrill♂ · Lv.19 · No item · Beedrill♂ · Lv.19 · No item · Hiker Alan Reward: $756 · Geodude♂ · Lv.21 · No item · Onix♂ · Lv.21 · No item · Bug Catcher Conner Reward: $240 · Caterpie♂ · Lv.20 · No item · Weedle♂ · Lv.20 · No item · Venonat♂ · Lv.20 · No item · Camper Drew Reward: $380 · Rattata♂ · Lv.19 · No item · Sandshrew♂ · Lv.19 · No item · Ekans♂ · Lv.19 · No item · Sandshrew♂ · Lv.19 · No item · Hiker Brice Reward: $720 · Geodude♂ · Lv.20 · No item · Geodude♂ · Lv.20 · No item · Machop♂ · Lv.20 · No item · Picnicker Caitlin Reward: $460 · Meowth♀ · Lv.23 · No item<br><br>You can find the following Pokémon here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Rattata · FR · LG · Grass · 14, 16-17 · 40% · Spearow · FR · LG · Grass · 13, 16-17 · 35% · Ekans · FR LG · Grass · 11, 13, 15, 17 25% · Sandshrew · FR LG · Grass · 11, 13, 15, 17 25%<br><br>You can find the following items here:<br><br>Items Item · Location · Games · Ether<br><br>On a rock in the northwest part of the route (hidden)<br><br>FR LG · Burn Heal · Southeast corner of the route · FR LG · Chesto Berry<br><br>Northeast part of the route, on the green grass to the west (hidden)<br><br>FR LG · Rare Candy<br><br>Northeast part of the route, one step west and one step south from the corner (hidden)<br><br>FR LG<br><br>Route 10:<br><br>Route 10 links route 9 to Lavender Town in the south. Head through Rock Tunnel to reach Lavender Town. (HM Flash will be useful here).<br><br>You can battle the following trainers:<br><br>Trainers Trainer · Pokémon · Picnicker Heidi Reward: $400 · Pikachu♀ · Lv.20 · No item · Clefairy♀ · Lv.20 · No item · PokéManiac Mark Reward: $1392 Requires Surf · Rhyhorn♂ · Lv.29 · No item · Lickitung♂ · Lv.29 · No item<br><br>You can catch the following Pokemon here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Voltorb · FR · LG · Grass · 14, 16-17 · 40% · Spearow · FR · LG · Grass · 13, 16-17 · 35% · Ekans · FR · LG · Grass · 11, 13, 15, 17 · 25% · Sandshrew · FR · LG · Grass · 11, 13, 15, 17 · 25% · Fishing · Magikarp · FR · LG · Fishing Old Rod · 5 · 100%<br><br>You can find the following items here:<br><br>Items Item · Location · Games · Everstone<br><br>Pokémon Center; from Oak's aide, after catching at least 20 different species<br><br>FR LG · Persim Berry<br><br>Southeast of the Pokémon Center, in the corner of fencing (hidden)<br><br>FR LG · Cheri Berry<br><br>Southwest of the Pokémon Center, on the edge of the dirt patch (hidden)<br><br>FR LG · Super Potion<br><br>One step east of Rock Tunnel's north entrance (hidden, requires Cut)<br><br>FR LG<br><br>Talk to Professor Oak’s aide inside in the Pokémon Center. He will give you the everstone if you have data on 20 different species of Pokémon. It can be handy as unevolved Pokémon learn more moves than evolved Pokémon. Heal up at the PC if needed.", "tips": ""}, {"id": 106, "title": "Part 6: Rock Tunnel, Lavender Town & Routes 7-8", "videoUrl": "#", "content": "Rock Tunnel: 1st Floor<br><br>This cave is full of darkness. Bringing a Pokémon with HM Flash would make it<br><br>easier to go through it.<br><br>1 F (Northeast):<br><br>Here are the trainers you will encounter here:<br><br>Trainers 1F · Trainer · Pokémon · PokéManiac Ashton Reward: $1104 · Cubone♂ · Lv.23 · No item · Slowpoke♂ · Lv.23 · No item · Hiker Lenny Reward: $684 · Geodude♂ · Lv.19 · No item · Machop♂ · Lv.19 · No item · Geodude♂ · Lv.19 · No item · Geodude♂ · Lv.19 · No item · Hiker Oliver Reward: $720 · Onix♂ · Lv.20 · No item · Onix♂ · Lv.20 · No item · Geodude♂ · Lv.20 · No item · Hiker Lucas Reward: $756 · Geodude♂ · Lv.21 · No item · Graveler♂ · Lv.21 · No item · Picnicker Leah Reward: $440 · Bellsprout♀ · Lv.22 · No item · Clefairy♀ · Lv.22 · No item · Picnicker Ariana Reward: $380 · Pidgey♀ · Lv.19 · No item · Rattata♀ · Lv.19 · No item · Rattata♀ · Lv.19 · No item · Bellsprout♀ · Lv.19 · No item · Picnicker Dana Reward: $400 · Meowth♀ · Lv.20 · No item · Oddish♀ · Lv.20 · No item · Pidgey♀ · Lv.20 · No item<br><br>Here are the Pokemon you will find:<br><br>Available Pokémon 1F · Pokémon · Games · Location · Levels · Rate · Geodude · FR · LG · Cave · 15-17 · 35% · Zubat · FR · LG · Cave · 15-16 · 30% · Mankey · FR · LG · Cave · 16-17 · 15% · Machop · FR · LG · Cave · 16-17 · 15% · Onix · FR · LG · Cave · 13, 15 · 5%<br><br>Here are the items you will find:<br><br>Items Item · Location · Games · 1F · Repel · Northeast; east of the cave entrance · FR LG · Escape Rope · West; near the middle of 1F · FR LG · Pearl<br><br>South; west of Picnicker Leah and Picnicker Ariana<br><br>FR LG<br><br>Climb down the ladder in the northeast corner to reach B1F.<br><br>B1F (Southeast):<br><br>B1F<br><br>Here are the trainers you can battle here:<br><br>Trainer Pokémon · PokéManiac Winston Reward: $1200 · Slowpoke♂ · Lv.25 · No item · Picnicker Martha Reward: $440 · Oddish♀ · Lv.22 · No item · Bulbasaur♂ · Lv.22 · No item · PokéManiac Steve Reward: $1056 · Charmander♂ · Lv.22 · No item · Cubone♂ · Lv.22 · No item · Hiker Allen Reward: $900 · Geodude♂ · Lv.25 · No item · Hiker Eric Reward: $720 · Machop♂ · Lv.20 · No item · Onix♂ · Lv.20 · No item · Picnicker Sofia Reward: $420 · Jigglypuff♀ · Lv.21 · No item · Pidgey♀ · Lv.21 · No item · Meowth♀ · Lv.21 · No item · Hiker Dudley Reward: $756 · Geodude♂ · Lv.21 · No item · Geodude♂ · Lv.21 · No item · Graveler♂ · Lv.21 · No item · PokéManiac Cooper Reward: $960 · Slowpoke♂ · Lv.20 · No item · Slowpoke♂ · Lv.20 · No item · Slowpoke♂ · Lv.20 · No item<br><br>Here are the Pokémon you can find here:<br><br>B1F Pokémon · Games · Location · Levels · Rate · Geodude · FR · LG · Cave · 15-17 · 35% · Zubat · FR · LG · Cave · 15-16 · 30% · Mankey · FR · LG · Cave · 16-17 · 15% · Machop · FR · LG · Cave · 17 · 10% · Onix · FR · LG · Cave · 13, 15, 17 · 10%<br><br>Here are the items you can find here:<br><br>B1F Revive Southeast; in the southwest corner of B1F FR LG Max Ether Northwest; north of Picnicker Sofia FR LG<br><br>Head back up 1F.<br><br>Go southeast and enter the nearby ladder.<br><br>Go southwest after reaching B1F. Turn back and head north from where Sofia is standing. Go north and enter the northwest ladder.<br><br>Go south to past the picnickers and continue to the southwest.<br><br>Route 10 (South):<br><br>The southern part of the route is shorter than the north. There are few trainers to battle as well. You can use the eastern exit if you do not want to battle them yet.<br><br>Here are the trainers here:<br><br>Trainers Trainer · Pokémon · Picnicker Carol Reward: $420 · Pidgey♀ · Lv.21 · No item · Pidgeotto♀ · Lv.21 · No item · Hiker Clark Reward: $756 · Geodude♂ · Lv.21 · No item · Onix♂ · Lv.21 · No item · Hiker Trent Reward: $684 · Onix♂ · Lv.19 · No item · Graveler♂ · Lv.19 · No item · PokéManiac Herman Reward: $960 · Cubone♂ · Lv.20 · No item · Slowpoke♂ · Lv.20 · No item<br><br>Lavender Town:<br><br>This town does not have a gym, but it has the Pokémon Tower instead where people go to pay respect the souls of departed Pokémon. The name rater’s house and the Volunteer Pokémon House (VPH) is also located here.<br><br>Upon entering the VPH, one of the volunteers will tell you that Mr. Fuji is at the Pokémon Tower. The top floor of the Pokémon Tower cannot be accessed at this point. Head east.<br><br>Route 8:<br><br>Route 8<br><br>This route links Lavender Town to the east and Saffron City to the east.<br><br>Here are the trainers you can battle here:<br><br>Trainers Trainer · Pokémon · Lass Julia Reward: $352 · Clefairy♀ · Lv.22 · No item · Clefairy♀ · Lv.22 · No item · Gamer Rich Reward: $1728 · Growlithe♂ · Lv.24 · No item · Vulpix♀ · Lv.24 · No item · Super Nerd Glenn Reward: $528 · Grimer♂ · Lv.22 · No item · Muk♂ · Lv.22 · No item · Grimer♂ · Lv.22 · No item · Twins Eli & Anne Reward: $528 · Clefairy♀ · Lv.22 · No item · Jigglypuff♀ · Lv.22 · No item · Lass Paige Reward: $368 · Nidoran♀ · Lv.23 · No item · Nidorina♀ · Lv.23 · No item · Super Nerd Leslie Reward: $624 · Koffing♂ · Lv.26 · No item · Lass Andrea Reward: $384 · Meowth♀ · Lv.24 · No item · Meowth♀ · Lv.24 · No item · Meowth♀ · Lv.24 · No item · Lass Megan Reward: $304 · Pidgey♀ · Lv.19 · No item · Rattata♀ · Lv.19 · No item · Nidoran♂ · Lv.19 · No item · Meowth♀ · Lv.19 · No item · Pikachu♀ · Lv.19 · No item · Biker Jaren Reward: $480 · Grimer♂ · Lv.24 · No item · Grimer♂ · Lv.24 · No item · Biker Ricardo Reward: $460 · Koffing♂ · Lv.22 · No item · Koffing♂ · Lv.22 · No item · Grimer♂ · Lv.23 · No item · Gamer Stan Reward: $1584 · Poliwag♂ · Lv.22 · No item · Poliwag♂ · Lv.22 · No item · Poliwhirl♂ · Lv.22 · No item · Super Nerd Aidan Reward: $480 · Voltorb · Lv.20 · No item · Voltorb · Lv.20 · No item · Magnemite · Lv.20 · No item · Koffing♂ · Lv.20 · No item<br><br>Here are the Pokémon available here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Pidgey · FR · LG · Grass · 18, 20 · 30% · Meowth · FR · LG · Grass · 18, 20 · 30% · Ekans · FR · LG · Grass · 17, 19 · 20% · Sandshrew · FR · LG · Grass · 17, 19 · 20% · Vulpix · FR · LG · Grass · 15-18 · 20% · Growlithe · FR · LG · Grass · 15-18 · 20% · Items Item · Location · Games · Leppa Berry<br><br>Tall grass patch, southeast area (hidden) (requires Cut)<br><br>FR LG · Lum Berry<br><br>Tall grass patch, northwest area (hidden) (requires Cut)<br><br>FR LG · Rawst Berry<br><br>Tall grass patch, northeast area (hidden) (requires Cut)<br><br>FR LG<br><br>Underground Path:<br><br>Saffron City is inaccessible at this point in the game. Instead use the underground path and go where the tunnel leads. Exit the underground path to reach route 7.<br><br>Route 7:<br><br>Route 7<br><br>Route 7 connects Saffron City to the east and Celadon City to the west.<br><br>Here the Pokémon available here:<br><br>Available Pokémon Pokémon · Games · Location · Levels · Rate · Meowth · FR · LG · Grass · 17-20 · 40% · Pidgey · FR · LG · Grass · 19, 22 · 30% · Oddish · FR · LG · Grass · 19, 22 · 20% · Bellsprout · FR · LG · Grass · 19, 22 · 20% · Vulpix · FR · LG · Grass · 18, 20 · 10% · Growlithe · FR · LG · Grass · 18, 20 · 10%", "tips": ""}]}, {"id": 2, "title": "Pokémon Ash Gray", "type": "romhack", "description": "Experience the Pokémon anime through this incredible ROM hack following Ash's journey, starting with Pikachu instead of a traditional starter.", "image": "", "parts": [{"id": 201, "title": "Part 1: Pallet Town and Pikachu", "videoUrl": "#", "content": "Oversleep like Ash did in the show and you're left with the last Pokémon available: a stubborn Pikachu that refuses to enter its Poké Ball at first.<br><br>Early routes recreate anime moments including the Spearow flock chase over the waterfall and meeting the Pokémon Ash famously caught in the anime.", "tips": "Key notes: Pikachu starts unwilling to battle inside its Ball, following you on the overworld map like in the show."}, {"id": 202, "title": "Part 2: Viridian Forest and Brock", "videoUrl": "#", "content": "Viridian Forest plays out with anime-specific encounters, and the Brock fight uses his anime lineup and dialogue rather than the original game's team.<br><br>Expect cutscenes recreating the show's famous beats, including Brock joining your journey afterward.", "tips": "Key notes: Anime-accurate gym teams differ from vanilla FireRed — check current-gen team compositions before fighting."}, {"id": 203, "title": "Part 3: Mt. Moon and Misty", "videoUrl": "#", "content": "Mt. Moon includes the anime's Clefairy cult subplot, and Misty joins as a traveling companion after the Cerulean Gym battle, recreating her anime debut and rivalry with Ash.", "tips": "Key notes: Story-driven content plays out on rails in spots — follow on-screen prompts for anime-exclusive cutscenes."}]}, {"id": 3, "title": "Pokémon Emerald", "type": "official", "description": "Complete Hoenn walkthrough covering both the Petalburg/Rustboro path and the Battle Frontier post-game content.", "image": "", "parts": []}, {"id": 4, "title": "Pokémon Sword and Shield GBA", "type": "romhack", "description": "A GBA-style reimagining of the Galar region's story, gyms, and Pokémon, built for the classic handheld engine.", "image": "", "parts": []}, {"id": 5, "title": "Pokémon Hearth", "type": "romhack", "description": "An original-region ROM hack with its own story, gyms, and cast of characters.", "image": "", "parts": []}
]));
    }

    function onAdminEnabled() {
        var p = document.getElementById('admin-walkthrough-panel');
        if (p) p.style.display = 'block';
    }

    function loadWalkthroughs() {
        const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs') || '[]');
        const grid = document.getElementById('walkthroughs-grid');
        grid.innerHTML = walkthroughs.map(wt => `
            <div class="card walkthrough-card" data-type="${wt.type}">
                ${wt.image ? `<img src="${wt.image}" alt="${wt.title}" style="width:100%; border-radius:10px; margin-bottom:1rem;">` : ''}
                <h3>${wt.title}</h3>
                <span class="card-tag">${wt.type === 'official' ? 'Official Game' : 'ROM Hack'}</span>
                <p>${wt.description}</p>
                <div style="margin-top:1.5rem; display:flex; gap:1rem; flex-wrap:wrap;">
                    <button class="btn" onclick="viewWalkthrough(${wt.id})">View Walkthrough</button>
                    ${isAdmin ? `<button class="btn btn-primary" onclick="showAddPartModal(${wt.id})">+ Add Part</button>` : ''}
                </div>
            </div>
        `).join('');
    }

    function extractYouTubeId(url) {
        const regExp = /^.*((youtu\.be\/)|(v\/)|(\/u\/\w\/)|(embed\/)|(watch\?))\??v?=?([^#&?]*).*/;
        const match = url.match(regExp);
        return (match && match[7] && match[7].length === 11) ? match[7] : null;
    }

    function viewWalkthrough(id) {
        const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs') || '[]');
        const wt = walkthroughs.find(w => w.id === id);
        if (!wt) return;
        const partsHtml = wt.parts.map(part => {
            const videoId = extractYouTubeId(part.videoUrl);
            return `
                <div style="margin-bottom:2rem; border-bottom:1px solid var(--border); padding-bottom:2rem;">
                    <h3 style="color:var(--accent); margin-bottom:1rem;">${part.title}</h3>
                    ${videoId ? `<div class="video-container"><iframe src="https://www.youtube.com/embed/${videoId}" frameborder="0" allowfullscreen></iframe></div>` : ''}
                    <div style="margin-top:1.2rem; color:var(--text-dim); line-height:1.8;">${part.content.replace(/\n/g,'<br>')}</div>
                    ${part.tips ? `<div style="margin-top:1.2rem; padding:1rem; background:rgba(255,222,0,0.1); border-left:3px solid var(--accent); border-radius:5px;"><strong style="color:var(--accent);">💡 Key Tips & Items:</strong><br>${part.tips.replace(/\n/g,'<br>')}</div>` : ''}
                </div>
            `;
        }).join('');
        document.getElementById('walkthrough-detail-content').innerHTML = `
            <div class="game-header"><h2>${wt.title}</h2><p style="margin-top:1rem; font-size:1.05rem; color:#fff;">${wt.description}</p></div>
            ${wt.parts.length > 0 ? partsHtml : '<p style="text-align:center; color:var(--text-dim);">No walkthrough parts added yet.</p>'}
        `;
        document.getElementById('walkthrough-detail-modal').classList.add('active');
    }

    function showAddWalkthroughModal() { document.getElementById('add-walkthrough-modal').classList.add('active'); }

    function addWalkthrough(event) {
        event.preventDefault();
        if (!isAdmin) return;
        const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs') || '[]');
        walkthroughs.push({
            id: Date.now(),
            title: document.getElementById('wt-title').value,
            type: document.getElementById('wt-type').value,
            description: document.getElementById('wt-description').value,
            image: document.getElementById('wt-image').value,
            parts: []
        });
        localStorage.setItem('walkthroughs', JSON.stringify(walkthroughs));
        document.getElementById('add-walkthrough-message').innerHTML = '<div class="success-msg">Walkthrough added successfully!</div>';
        setTimeout(() => { closeModal('add-walkthrough-modal'); loadWalkthroughs(); event.target.reset(); }, 800);
    }

    function showAddPartModal(gameId) {
        document.getElementById('part-game-id').value = gameId;
        document.getElementById('add-part-modal').classList.add('active');
    }

    function addWalkthroughPart(event) {
        event.preventDefault();
        if (!isAdmin) return;
        const gameId = parseInt(document.getElementById('part-game-id').value);
        const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs') || '[]');
        const game = walkthroughs.find(w => w.id === gameId);
        if (game) {
            game.parts.push({
                id: Date.now(),
                title: document.getElementById('part-title').value,
                videoUrl: document.getElementById('part-video').value,
                content: document.getElementById('part-content').value,
                tips: document.getElementById('part-tips').value
            });
            localStorage.setItem('walkthroughs', JSON.stringify(walkthroughs));
            document.getElementById('add-part-message').innerHTML = '<div class="success-msg">Part added successfully!</div>';
            setTimeout(() => { closeModal('add-part-modal'); event.target.reset(); }, 800);
        }
    }

    function filterWalkthroughs(type, evt) {
        document.querySelectorAll('#walkthroughs-grid').forEach(()=>{});
        document.querySelectorAll('.filters .filter-btn').forEach(btn => btn.classList.remove('active'));
        if (evt && evt.target) evt.target.classList.add('active');
        document.querySelectorAll('.walkthrough-card').forEach(card => {
            card.style.display = (type === 'all' || card.dataset.type === type) ? 'block' : 'none';
        });
    }

    document.getElementById('walkthrough-search').addEventListener('input', (e) => {
        const term = e.target.value.toLowerCase();
        document.querySelectorAll('.walkthrough-card').forEach(card => {
            const title = card.querySelector('h3').textContent.toLowerCase();
            const desc = card.querySelector('p').textContent.toLowerCase();
            card.style.display = (title.includes(term) || desc.includes(term)) ? 'block' : 'none';
        });
    });

    loadWalkthroughs();

</script>
</body>
</html>
