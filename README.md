<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trainer's Odyssey - Ultimate Pokémon Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Exo+2:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #FF0000;
            --secondary: #3B4CCA;
            --accent: #FFDE00;
            --dark: #0A0E27;
            --darker: #050711;
            --light: #F5F5F5;
            --electric: #F7D02C;
            --fire: #F08030;
            --water: #6890F0;
            --grass: #78C850;
            --card-bg: rgba(255, 255, 255, 0.05);
            --glow: 0 0 20px rgba(255, 0, 0, 0.3);
        }

        body {
            font-family: 'Exo 2', sans-serif;
            background: var(--darker);
            color: var(--light);
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* Animated Background */
        .bg-pattern {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(circle at 20% 50%, rgba(255, 0, 0, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(59, 76, 202, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 40% 20%, rgba(255, 222, 0, 0.05) 0%, transparent 50%);
            animation: bgFloat 20s ease-in-out infinite;
        }

        @keyframes bgFloat {
            0%, 100% { transform: translate(0, 0); }
            50% { transform: translate(-20px, 20px); }
        }

        /* Header */
        header {
            background: linear-gradient(135deg, var(--dark) 0%, rgba(59, 76, 202, 0.2) 100%);
            border-bottom: 3px solid var(--primary);
            position: sticky;
            top: 0;
            z-index: 1000;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        nav {
            max-width: 1400px;
            margin: 0 auto;
            padding: 1.5rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .logo {
            font-family: 'Press Start 2P', cursive;
            font-size: 1.4rem;
            color: var(--accent);
            text-shadow: 3px 3px 0 var(--primary);
            letter-spacing: 2px;
            animation: pulse 2s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
            align-items: center;
            flex-wrap: wrap;
        }

        .nav-links a {
            color: var(--light);
            text-decoration: none;
            font-weight: 600;
            position: relative;
            transition: all 0.3s;
            text-transform: uppercase;
            font-size: 0.9rem;
            letter-spacing: 1px;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent);
            transition: width 0.3s;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .admin-btn {
            background: linear-gradient(135deg, var(--primary), #CC0000);
            padding: 0.6rem 1.5rem;
            border-radius: 25px;
            border: 2px solid var(--accent);
            cursor: pointer;
            font-weight: 700;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(255, 0, 0, 0.3);
        }

        .admin-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 25px rgba(255, 0, 0, 0.5);
        }

        /* Hero Section */
        .hero {
            padding: 6rem 2rem;
            text-align: center;
            background: linear-gradient(180deg, transparent, var(--dark));
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.1) 0%, transparent 70%);
            animation: heroRotate 30s linear infinite;
        }

        @keyframes heroRotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .hero h1 {
            font-family: 'Press Start 2P', cursive;
            font-size: 3rem;
            color: var(--accent);
            text-shadow: 
                4px 4px 0 var(--primary),
                -2px -2px 0 var(--secondary),
                0 0 30px rgba(255, 222, 0, 0.5);
            margin-bottom: 1.5rem;
            position: relative;
            z-index: 1;
            animation: slideIn 1s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .hero p {
            font-size: 1.3rem;
            color: var(--light);
            max-width: 700px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
            animation: slideIn 1s ease-out 0.2s backwards;
        }

        /* Main Content */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 4rem 2rem;
        }

        .section-title {
            font-family: 'Press Start 2P', cursive;
            font-size: 2rem;
            color: var(--accent);
            text-shadow: 3px 3px 0 var(--primary);
            margin-bottom: 3rem;
            text-align: center;
            position: relative;
            display: inline-block;
            left: 50%;
            transform: translateX(-50%);
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 60%;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--accent), transparent);
        }

        /* Grid Layouts */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .card {
            background: var(--card-bg);
            border: 2px solid rgba(255, 222, 0, 0.2);
            border-radius: 15px;
            padding: 2rem;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(10px);
        }

        .card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255, 222, 0, 0.1) 0%, transparent 70%);
            opacity: 0;
            transition: opacity 0.3s;
        }

        .card:hover::before {
            opacity: 1;
        }

        .card:hover {
            transform: translateY(-10px);
            border-color: var(--accent);
            box-shadow: 0 10px 40px rgba(255, 222, 0, 0.2), var(--glow);
        }

        .card h3 {
            color: var(--accent);
            font-size: 1.5rem;
            margin-bottom: 1rem;
            font-weight: 700;
        }

        .card p {
            color: rgba(245, 245, 245, 0.8);
            line-height: 1.8;
        }

        .card-tag {
            display: inline-block;
            background: var(--primary);
            color: white;
            padding: 0.3rem 1rem;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-top: 1rem;
        }

        /* Buttons */
        .btn {
            display: inline-block;
            padding: 0.8rem 2rem;
            background: linear-gradient(135deg, var(--secondary), #2a3ba8);
            color: white;
            text-decoration: none;
            border-radius: 25px;
            font-weight: 600;
            transition: all 0.3s;
            border: 2px solid transparent;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(59, 76, 202, 0.4);
            border-color: var(--accent);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), #CC0000);
        }

        .btn-primary:hover {
            box-shadow: 0 5px 20px rgba(255, 0, 0, 0.4);
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--dark);
            border: 3px solid var(--accent);
            border-radius: 20px;
            padding: 3rem;
            max-width: 800px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            box-shadow: 0 0 50px rgba(255, 222, 0, 0.3);
            animation: modalSlide 0.3s ease-out;
        }

        @keyframes modalSlide {
            from { opacity: 0; transform: scale(0.9) translateY(-20px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        .close-modal {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: var(--primary);
            border: none;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.5rem;
            font-weight: bold;
            transition: all 0.3s;
        }

        .close-modal:hover {
            transform: rotate(90deg);
            background: #CC0000;
        }

        /* Form Styles */
        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            color: var(--accent);
            font-weight: 600;
            margin-bottom: 0.5rem;
            text-transform: uppercase;
            font-size: 0.9rem;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 222, 0, 0.3);
            border-radius: 10px;
            color: var(--light);
            font-family: 'Exo 2', sans-serif;
            font-size: 1rem;
            transition: all 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(255, 222, 0, 0.2);
        }

        .form-group textarea {
            min-height: 120px;
            resize: vertical;
        }

        /* Video Embed */
        .video-container {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: 15px;
            margin: 2rem 0;
            border: 3px solid var(--accent);
        }

        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        /* Social Links */
        .social-links {
            display: flex;
            gap: 1.5rem;
            justify-content: center;
            margin-top: 2rem;
        }

        .social-links a {
            width: 60px;
            height: 60px;
            background: var(--card-bg);
            border: 2px solid var(--accent);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            font-size: 1.5rem;
        }

        .social-links a:hover {
            transform: translateY(-5px) rotate(5deg);
            box-shadow: 0 5px 20px rgba(255, 222, 0, 0.3);
            background: var(--accent);
            color: var(--dark);
        }

        /* Filter Section */
        .filters {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            flex-wrap: wrap;
            justify-content: center;
        }

        .filter-btn {
            padding: 0.6rem 1.5rem;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 222, 0, 0.3);
            border-radius: 25px;
            color: var(--light);
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 600;
        }

        .filter-btn.active,
        .filter-btn:hover {
            background: var(--accent);
            color: var(--dark);
            border-color: var(--accent);
        }

        /* Admin Panel */
        .admin-panel {
            background: linear-gradient(135deg, rgba(255, 0, 0, 0.1), rgba(59, 76, 202, 0.1));
            border: 3px solid var(--primary);
            border-radius: 20px;
            padding: 2rem;
            margin-top: 2rem;
        }

        .admin-actions {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            margin-top: 1rem;
        }

        /* Walkthrough specific */
        .game-header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            padding: 3rem 2rem;
            border-radius: 20px;
            margin-bottom: 3rem;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .game-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg"><circle cx="10" cy="10" r="2" fill="rgba(255,255,255,0.1)"/></svg>');
            opacity: 0.3;
        }

        .game-header h2 {
            font-family: 'Press Start 2P', cursive;
            font-size: 2.5rem;
            color: var(--accent);
            text-shadow: 3px 3px 0 rgba(0, 0, 0, 0.5);
            position: relative;
        }

        .walkthrough-nav {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            margin: 2rem 0;
        }

        .walkthrough-part {
            flex: 1;
            min-width: 250px;
            background: var(--card-bg);
            border: 2px solid rgba(255, 222, 0, 0.2);
            border-radius: 15px;
            padding: 1.5rem;
            cursor: pointer;
            transition: all 0.3s;
        }

        .walkthrough-part:hover {
            border-color: var(--accent);
            transform: translateY(-5px);
            box-shadow: 0 5px 20px rgba(255, 222, 0, 0.2);
        }

        /* Footer */
        footer {
            background: var(--darker);
            border-top: 3px solid var(--primary);
            padding: 3rem 2rem;
            text-align: center;
            margin-top: 4rem;
        }

        footer p {
            color: rgba(245, 245, 245, 0.6);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 1.8rem;
            }

            .section-title {
                font-size: 1.5rem;
            }

            .logo {
                font-size: 1rem;
            }

            .nav-links {
                gap: 1rem;
            }

            .grid {
                grid-template-columns: 1fr;
            }
        }

        /* Loading Animation */
        .loading {
            text-align: center;
            padding: 2rem;
            color: var(--accent);
            font-size: 1.2rem;
            animation: pulse 1.5s ease-in-out infinite;
        }

        /* Success Message */
        .success-msg {
            background: linear-gradient(135deg, rgba(120, 200, 80, 0.2), rgba(78, 200, 80, 0.1));
            border: 2px solid var(--grass);
            color: var(--grass);
            padding: 1rem;
            border-radius: 10px;
            margin: 1rem 0;
            text-align: center;
            font-weight: 600;
        }

        .error-msg {
            background: linear-gradient(135deg, rgba(255, 0, 0, 0.2), rgba(200, 0, 0, 0.1));
            border: 2px solid var(--primary);
            color: var(--primary);
            padding: 1rem;
            border-radius: 10px;
            margin: 1rem 0;
            text-align: center;
            font-weight: 600;
        }

        /* Type badges for Pokemon */
        .type-badge {
            display: inline-block;
            padding: 0.4rem 1rem;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            margin: 0.2rem;
            text-transform: uppercase;
        }

        .type-fire { background: var(--fire); color: white; }
        .type-water { background: var(--water); color: white; }
        .type-grass { background: var(--grass); color: white; }
        .type-electric { background: var(--electric); color: var(--dark); }

        /* Search Bar */
        .search-container {
            max-width: 600px;
            margin: 2rem auto;
            position: relative;
        }

        .search-input {
            width: 100%;
            padding: 1rem 3rem 1rem 1.5rem;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 222, 0, 0.3);
            border-radius: 30px;
            color: var(--light);
            font-size: 1rem;
            transition: all 0.3s;
        }

        .search-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 20px rgba(255, 222, 0, 0.2);
        }

        .search-icon {
            position: absolute;
            right: 1.5rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--accent);
            font-size: 1.2rem;
        }
    </style>
<base target="_blank">
</head>
<body>
    <div class="bg-pattern"></div>

    <!-- Header -->
    <header>
        <nav>
            <div class="logo">TRAINER'S ODYSSEY</div>
            <ul class="nav-links">
                <li><a href="#home" onclick="showSection('home')">Home</a></li>
                <li><a href="#walkthroughs" onclick="showSection('walkthroughs')">Walkthroughs</a></li>
                <li><a href="#romhacks" onclick="showSection('romhacks')">ROM Hacks</a></li>
                <li><a href="#pokedex" onclick="showSection('pokedex')">Pokédex</a></li>
                <li><a href="#guides" onclick="showSection('guides')">Guides</a></li>
                <li><a href="#myromhacks" onclick="showSection('myromhacks')">My ROM Hacks</a></li>
                <li><a href="#videos" onclick="showSection('videos')">Videos</a></li>
                <li><a href="#about" onclick="showSection('about')">About</a></li>
                <li><button class="admin-btn" onclick="showAdminLogin()">Admin</button></li>
            </ul>
        </nav>
    </header>

    <!-- Main Content -->
    <main id="app-content">
        <!-- Home Section -->
        <section id="home" class="active-section">
            <div class="hero">
                <h1>TRAINER'S ODYSSEY</h1>
                <p>Your Ultimate Destination for Pokémon Walkthroughs, ROM Hacks, and Legendary Adventures</p>
            </div>

            <div class="container">
                <h2 class="section-title">Latest Updates</h2>
                <div id="latest-content" class="grid">
                    <!-- Dynamic content will be loaded here -->
                </div>

                <h2 class="section-title" style="margin-top: 4rem;">Featured Videos</h2>
                <div class="grid">
                    <div class="card">
                        <h3>Pokémon Ash Gray Series</h3>
                        <div class="video-container">
                            <iframe src="https://www.youtube.com/embed/videoseries?list=PLYourPlaylistID" frameborder="0" allowfullscreen></iframe>
                        </div>
                        <p>Follow along as we experience the Pokémon world through Ash's journey!</p>
                    </div>
                    <div class="card">
                        <h3>Latest PSP Gameplay</h3>
                        <div class="video-container">
                            <iframe src="https://www.youtube.com/embed/videoseries?list=PLYourPlaylistID" frameborder="0" allowfullscreen></iframe>
                        </div>
                        <p>Check out the newest handheld gaming content including Naruto and Dragon Ball Z!</p>
                    </div>
                </div>

                <h2 class="section-title" style="margin-top: 4rem;">Connect With Me</h2>
                <div class="social-links">
                    <a href="https://youtube.com/@trainersodyssey323" target="_blank" title="Trainer's Odyssey YouTube">
                        <span>▶</span>
                    </a>
                    <a href="https://youtube.com/@handholdhavoc" target="_blank" title="Handhold Havoc YouTube">
                        <span>🎮</span>
                    </a>
                    <a href="https://www.instagram.com/pokebattle_reels" target="_blank" title="Instagram">
                        <span>📷</span>
                    </a>
                </div>
            </div>
        </section>

        <!-- Walkthroughs Section -->
        <section id="walkthroughs" class="hidden-section">
            <div class="container">
                <h2 class="section-title">Pokémon Walkthroughs</h2>
                
                <div class="search-container">
                    <input type="text" class="search-input" id="walkthrough-search" placeholder="Search walkthroughs...">
                    <span class="search-icon">🔍</span>
                </div>

                <div class="filters">
                    <button class="filter-btn active" onclick="filterWalkthroughs('all')">All Games</button>
                    <button class="filter-btn" onclick="filterWalkthroughs('official')">Official Games</button>
                    <button class="filter-btn" onclick="filterWalkthroughs('romhack')">ROM Hacks</button>
                </div>

                <div id="walkthroughs-grid" class="grid">
                    <!-- Walkthroughs will be loaded here -->
                </div>

                <div id="admin-walkthrough-panel" style="display: none;">
                    <div class="admin-panel">
                        <h3 style="color: var(--accent); margin-bottom: 1rem;">Add New Walkthrough</h3>
                        <button class="btn btn-primary" onclick="showAddWalkthroughModal()">+ Add Game Walkthrough</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- ROM Hacks Hub -->
        <section id="romhacks" class="hidden-section">
            <div class="container">
                <h2 class="section-title">ROM Hacks Hub</h2>
                <p style="text-align: center; max-width: 800px; margin: 0 auto 3rem; color: rgba(245, 245, 245, 0.8);">
                    Discover incredible fan-made Pokémon adventures with unique stories, regions, and gameplay mechanics!
                </p>

                <div class="filters">
                    <button class="filter-btn active" onclick="filterRomHacks('all')">All Hacks</button>
                    <button class="filter-btn" onclick="filterRomHacks('kanto')">Kanto</button>
                    <button class="filter-btn" onclick="filterRomHacks('johto')">Johto</button>
                    <button class="filter-btn" onclick="filterRomHacks('hoenn')">Hoenn</button>
                    <button class="filter-btn" onclick="filterRomHacks('difficulty-easy')">Easy</button>
                    <button class="filter-btn" onclick="filterRomHacks('difficulty-hard')">Hard</button>
                </div>

                <div id="romhacks-grid" class="grid">
                    <!-- ROM hacks will be loaded here -->
                </div>
            </div>
        </section>

        <!-- Pokédex Section -->
        <section id="pokedex" class="hidden-section">
            <div class="container">
                <h2 class="section-title">National Pokédex</h2>
                
                <div class="search-container">
                    <input type="text" class="search-input" id="pokedex-search" placeholder="Search Pokémon by name or number...">
                    <span class="search-icon">🔍</span>
                </div>

                <div class="filters">
                    <button class="filter-btn active" onclick="filterPokedex('all')">All</button>
                    <button class="filter-btn" onclick="filterPokedex('gen1')">Gen 1</button>
                    <button class="filter-btn" onclick="filterPokedex('gen2')">Gen 2</button>
                    <button class="filter-btn" onclick="filterPokedex('gen3')">Gen 3</button>
                    <button class="filter-btn" onclick="filterPokedex('gen4')">Gen 4</button>
                    <button class="filter-btn" onclick="filterPokedex('gen5')">Gen 5</button>
                </div>

                <div id="pokedex-grid" class="grid">
                    <!-- Pokémon entries will be loaded here -->
                </div>
            </div>
        </section>

        <!-- Guides Section -->
        <section id="guides" class="hidden-section">
            <div class="container">
                <h2 class="section-title">Guides & Tips</h2>
                
                <div id="guides-grid" class="grid">
                    <!-- Guides will be loaded here -->
                </div>
            </div>
        </section>

        <!-- My ROM Hacks Section -->
        <section id="myromhacks" class="hidden-section">
            <div class="container">
                <h2 class="section-title">My ROM Hacks</h2>
                <p style="text-align: center; max-width: 800px; margin: 0 auto 3rem; color: rgba(245, 245, 245, 0.8);">
                    Check out my custom Pokémon ROM hacks! Download patches, read dev logs, and experience unique adventures I've created.
                </p>

                <div id="myromhacks-grid" class="grid">
                    <!-- My ROM hacks will be loaded here -->
                </div>

                <div id="admin-myromhacks-panel" style="display: none;">
                    <div class="admin-panel">
                        <h3 style="color: var(--accent); margin-bottom: 1rem;">Manage Your ROM Hacks</h3>
                        <button class="btn btn-primary" onclick="showAddMyRomHackModal()">+ Add New ROM Hack</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Videos Section -->
        <section id="videos" class="hidden-section">
            <div class="container">
                <h2 class="section-title">Video Gallery</h2>

                <div class="game-header" style="margin-bottom: 3rem;">
                    <h2>YouTube Channels</h2>
                </div>

                <div class="grid">
                    <div class="card">
                        <h3>🎮 Handhold Havoc</h3>
                        <p>PSP gameplay including Naruto Ultimate Ninja Impact, Dragon Ball Z, God of War, GTA Vice City Stories, and more!</p>
                        <div style="margin-top: 1.5rem;">
                            <a href="https://youtube.com/@handholdhavoc" target="_blank" class="btn">Visit Channel</a>
                        </div>
                    </div>

                    <div class="card">
                        <h3>⚡ Trainer's Odyssey</h3>
                        <p>Pokémon walkthroughs including Ash Gray, FireRed, Ruby, Sword & Shield GBA, and Hearth ROM hack!</p>
                        <div style="margin-top: 1.5rem;">
                            <a href="https://youtube.com/@trainersodyssey323" target="_blank" class="btn">Visit Channel</a>
                        </div>
                    </div>
                </div>

                <h2 class="section-title" style="margin-top: 4rem;">Latest Playlists</h2>
                <div id="playlists-grid" class="grid">
                    <!-- Playlists will be loaded here -->
                </div>
            </div>
        </section>

        <!-- About Section -->
        <section id="about" class="hidden-section">
            <div class="container">
                <h2 class="section-title">About Trainer's Odyssey</h2>
                
                <div class="card" style="max-width: 900px; margin: 0 auto; padding: 3rem;">
                    <h3>Welcome, Trainers!</h3>
                    <p style="font-size: 1.1rem; line-height: 2; margin-top: 1.5rem;">
                        Trainer's Odyssey is your ultimate destination for comprehensive Pokémon walkthroughs, ROM hack showcases, 
                        and gaming content. I've dedicated this platform to helping trainers navigate through official Pokémon games 
                        and discover incredible fan-made adventures.
                    </p>
                    <p style="font-size: 1.1rem; line-height: 2; margin-top: 1.5rem;">
                        From detailed episode-by-episode walkthroughs with embedded YouTube videos to in-depth guides on items, 
                        legendaries, and optimal strategies, this site is built for both casual players and hardcore enthusiasts. 
                        I also create my own ROM hacks, which you can find in the dedicated section!
                    </p>
                    <p style="font-size: 1.1rem; line-height: 2; margin-top: 1.5rem;">
                        Beyond Pokémon, my Handhold Havoc channel features PSP gameplay from classics like Naruto, Dragon Ball Z, 
                        God of War, and more. Join me on this gaming odyssey!
                    </p>

                    <div style="margin-top: 2rem; padding-top: 2rem; border-top: 2px solid rgba(255, 222, 0, 0.3);">
                        <h3 style="margin-bottom: 1rem;">Get in Touch</h3>
                        <div class="social-links" style="justify-content: flex-start;">
                            <a href="https://youtube.com/@trainersodyssey323" target="_blank">▶</a>
                            <a href="https://youtube.com/@handholdhavoc" target="_blank">🎮</a>
                            <a href="https://www.instagram.com/pokebattle_reels" target="_blank">📷</a>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Admin Login Modal -->
    <div id="admin-login-modal" class="modal">
        <div class="modal-content">
            <button class="close-modal" onclick="closeModal('admin-login-modal')">&times;</button>
            <h2 style="color: var(--accent); font-family: 'Press Start 2P', cursive; font-size: 1.5rem; margin-bottom: 2rem; text-align: center;">Admin Login</h2>
            
            <form onsubmit="adminLogin(event)">
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" id="admin-password" required>
                </div>
                <div id="login-message"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 1rem;">Login</button>
            </form>
        </div>
    </div>

    <!-- Add Walkthrough Modal -->
    <div id="add-walkthrough-modal" class="modal">
        <div class="modal-content">
            <button class="close-modal" onclick="closeModal('add-walkthrough-modal')">&times;</button>
            <h2 style="color: var(--accent); font-family: 'Press Start 2P', cursive; font-size: 1.3rem; margin-bottom: 2rem;">Add New Walkthrough</h2>
            
            <form onsubmit="addWalkthrough(event)">
                <div class="form-group">
                    <label>Game Title</label>
                    <input type="text" id="wt-title" required>
                </div>
                <div class="form-group">
                    <label>Game Type</label>
                    <select id="wt-type" required>
                        <option value="official">Official Game</option>
                        <option value="romhack">ROM Hack</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea id="wt-description" required></textarea>
                </div>
                <div class="form-group">
                    <label>Cover Image URL (optional)</label>
                    <input type="url" id="wt-image">
                </div>
                <div id="add-walkthrough-message"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 1rem;">Add Walkthrough</button>
            </form>
        </div>
    </div>

    <!-- Add Walkthrough Part Modal -->
    <div id="add-part-modal" class="modal">
        <div class="modal-content">
            <button class="close-modal" onclick="closeModal('add-part-modal')">&times;</button>
            <h2 style="color: var(--accent); font-family: 'Press Start 2P', cursive; font-size: 1.3rem; margin-bottom: 2rem;">Add Walkthrough Part</h2>
            
            <form onsubmit="addWalkthroughPart(event)">
                <input type="hidden" id="part-game-id">
                <div class="form-group">
                    <label>Part Title (e.g., "Part 1: Pallet Town to Pewter City")</label>
                    <input type="text" id="part-title" required>
                </div>
                <div class="form-group">
                    <label>YouTube Video URL</label>
                    <input type="url" id="part-video" required>
                </div>
