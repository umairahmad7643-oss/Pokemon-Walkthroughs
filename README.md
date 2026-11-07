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
            transition: transform 0.3s ease;
            will-change: transform;
        }

        /* Slides out of the way when scrolling down; returns on scroll up */
        header.header-hidden {
            transform: translateY(-100%);
            box-shadow: none;
        }

        /* Never hide while the user is interacting with the menu */
        header:focus-within {
            transform: none;
        }

        nav {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0.8rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 0.6rem 1rem;
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
            gap: 1.4rem;
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
            font-size: 0.85rem;
            letter-spacing: 1px;
            white-space: nowrap;
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
            padding: 0.4rem 1.2rem;
            border-radius: 25px;
            border: 2px solid var(--accent);
            color: var(--light);
            font-family: inherit;
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
            pointer-events: none; /* decorative glow must not swallow clicks on card buttons */
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
            pointer-events: none;
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

        /* ===== Walkthrough guide content (FireRed Part 1) ===== */
        .wt-part-wrap {
            background: var(--card-bg);
            border: 2px solid rgba(255, 222, 0, 0.2);
            border-radius: 15px;
            padding: 1.5rem;
            margin-bottom: 2rem;
        }
        .wt-part-wrap > h3 { color: var(--accent); font-size: 1.6rem; margin-bottom: 0.8rem; }
        .wt-guide { color: rgba(245, 245, 245, 0.92); line-height: 1.8; }
        .wt-guide p { margin: 0 0 1rem; }
        .wt-guide a { color: #8fb0ff; text-decoration: underline; text-underline-offset: 2px; }
        .wt-guide a:hover { color: var(--accent); }
        .wt-lead { font-size: 1.1rem; color: var(--accent); font-weight: 600; }
        .wt-h {
            font-family: 'Press Start 2P', cursive;
            font-size: 1.05rem;
            line-height: 1.6;
            color: var(--accent);
            text-shadow: 2px 2px 0 var(--primary);
            margin: 2.5rem 0 1rem;
            scroll-margin-top: 1rem;
        }
        .wt-h2 {
            font-size: 1.25rem;
            font-weight: 800;
            color: var(--accent);
            margin: 1.8rem 0 0.6rem;
            padding-left: 0.7rem;
            border-left: 4px solid var(--primary);
            scroll-margin-top: 1rem;
        }
        .wt-px { image-rendering: pixelated; }
        .wt-icon { width: 32px; height: 32px; flex: none; }

        details.wt-collapse {
            border: 2px solid rgba(255, 222, 0, 0.3);
            border-radius: 12px;
            margin: 1.5rem 0;
            background: rgba(255, 255, 255, 0.03);
        }
        details.wt-collapse > summary {
            cursor: pointer;
            padding: 0.8rem 1.2rem;
            font-weight: 700;
            font-size: 1.1rem;
            color: var(--accent);
            list-style: none;
            display: flex;
            justify-content: space-between;
            align-items: center;
            user-select: none;
        }
        details.wt-collapse > summary::-webkit-details-marker { display: none; }
        details.wt-collapse > summary::after {
            content: '+';
            width: 28px; height: 28px;
            display: inline-flex; align-items: center; justify-content: center;
            border: 2px solid var(--accent);
            border-radius: 50%;
            font-size: 1.1rem;
            line-height: 1;
        }
        details.wt-collapse[open] > summary::after { content: '\2212'; }
        details.wt-collapse > summary:hover { background: rgba(255, 222, 0, 0.08); }
        details.wt-collapse > summary:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }
        .wt-collapse-body { padding: 0.4rem 1.2rem 1.2rem; }

        .wt-toc-list, .wt-toc-list ul { padding-left: 1.4rem; margin: 0; }
        .wt-toc-list li { margin: 0.2rem 0; }

        .wt-table-wrap { overflow-x: auto; margin: 1.2rem 0; }
        .wt-table { border-collapse: collapse; width: 100%; }
        .wt-table.wt-narrow { max-width: 620px; }
        .wt-table caption { text-align: left; color: var(--accent); font-weight: 700; padding-bottom: 0.4rem; }
        .wt-table th, .wt-table td {
            border: 1px solid rgba(255, 222, 0, 0.25);
            padding: 0.5rem 0.8rem;
            text-align: left;
            vertical-align: middle;
        }
        .wt-table thead th { background: rgba(255, 0, 0, 0.25); color: var(--accent); }
        .wt-table tbody th { background: rgba(255, 255, 255, 0.05); color: var(--accent); white-space: nowrap; }
        .wt-game {
            display: inline-block;
            background: var(--secondary);
            color: #fff;
            font-size: 0.75rem;
            font-weight: 700;
            padding: 0.1rem 0.5rem;
            border-radius: 10px;
            margin-right: 0.3rem;
        }
        .wt-item { display: inline-flex; align-items: center; gap: 0.6rem; font-weight: 600; }

        .wt-townrow { display: flex; gap: 1.5rem; align-items: flex-start; flex-wrap: wrap; }
        .wt-townrow p { flex: 1 1 280px; }
        .wt-figure { margin: 0; text-align: center; flex: none; }
        .wt-figure img { max-width: 100%; height: auto; border: 3px solid var(--accent); border-radius: 8px; }
        .wt-figure figcaption { font-weight: 700; color: var(--accent); margin-top: 0.3rem; }

        .wt-starters { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; margin: 1rem 0; }
        .wt-starter {
            text-align: center;
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 222, 0, 0.2);
            border-radius: 12px;
            padding: 1rem;
            display: flex; flex-direction: column; align-items: center; gap: 0.3rem;
        }
        .wt-evos { width: 100%; margin-top: 0.6rem; border-top: 1px dashed rgba(255, 222, 0, 0.3); padding-top: 0.6rem; }
        .wt-evo { display: flex; align-items: center; gap: 0.6rem; text-align: left; margin-bottom: 0.4rem; }
        .wt-evo .type-badge { font-size: 0.7rem; padding: 0.15rem 0.6rem; margin: 0.1rem 0.2rem 0 0; }

        .wt-rivals { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 1rem; margin: 1.2rem 0; }
        .wt-rival { border: 2px solid rgba(255, 222, 0, 0.3); border-radius: 12px; overflow: hidden; background: rgba(255, 255, 255, 0.03); }
        .wt-rival-head { display: flex; align-items: center; gap: 0.6rem; background: rgba(255, 0, 0, 0.25); padding: 0.5rem 0.9rem; }
        .wt-rival-body { padding: 0.9rem; display: flex; flex-direction: column; gap: 1rem; }
        .wt-trainer { display: flex; gap: 0.8rem; flex-wrap: wrap; align-items: flex-start; }
        .wt-trainer dl, .wt-mon dl { margin: 0; font-size: 0.9rem; line-height: 1.5; }
        .wt-trainer dt, .wt-mon dt { color: var(--accent); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.5px; }
        .wt-trainer dd, .wt-mon dd { margin: 0 0 0.3rem; }
        .wt-balls { width: 100%; display: flex; gap: 2px; }
        .wt-mon { display: flex; gap: 0.8rem; flex-wrap: wrap; align-items: flex-start; border-top: 1px dashed rgba(255, 222, 0, 0.3); padding-top: 0.9rem; }
        .wt-moves { list-style: none; padding: 0; margin: 0; width: 100%; display: flex; gap: 0.6rem; flex-wrap: wrap; }
        .wt-moves li { background: rgba(255, 255, 255, 0.06); border-radius: 8px; padding: 0.3rem 0.7rem; font-weight: 600; }
        .wt-moves .type-badge { font-size: 0.65rem; padding: 0.1rem 0.5rem; margin: 0 0 0 0.4rem; }

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

            nav {
                padding: 0.5rem 1rem;
                gap: 0.4rem;
            }

            .logo {
                animation: none;
            }

            .nav-links {
                gap: 1.1rem;
                flex-wrap: nowrap;
                overflow-x: auto;
                width: 100%;
                padding-bottom: 0.4rem;
                scrollbar-width: none;
            }

            .nav-links::-webkit-scrollbar {
                display: none;
            }

            .nav-links li {
                flex: none;
            }

            .modal-content {
                padding: 2.5rem 1rem 1.5rem;
            }

            .wt-part-wrap {
                padding: 1rem;
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
        .type-poison { background: #A040A0; color: white; }
        .type-flying { background: #A890F0; color: white; }
        .type-normal { background: #A8A878; color: white; }

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
                <div class="form-group">
                    <label>Written Guide</label>
                    <textarea id="part-content" required style="min-height: 200px;"></textarea>
                </div>
                <div class="form-group">
                    <label>Key Items & Tips</label>
                    <textarea id="part-tips" placeholder="List important items, strategies, and tips for this section"></textarea>
                </div>
                <div id="add-part-message"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 1rem;">Add Part</button>
            </form>
        </div>
    </div>

    <!-- Add My ROM Hack Modal -->
    <div id="add-myromhack-modal" class="modal">
        <div class="modal-content">
            <button class="close-modal" onclick="closeModal('add-myromhack-modal')">&times;</button>
            <h2 style="color: var(--accent); font-family: 'Press Start 2P', cursive; font-size: 1.3rem; margin-bottom: 2rem;">Add Your ROM Hack</h2>
            
            <form onsubmit="addMyRomHack(event)">
                <div class="form-group">
                    <label>ROM Hack Title</label>
                    <input type="text" id="mrh-title" required>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea id="mrh-description" required></textarea>
                </div>
                <div class="form-group">
                    <label>Features (one per line)</label>
                    <textarea id="mrh-features" placeholder="New region&#10;Custom Pokémon&#10;Enhanced difficulty"></textarea>
                </div>
                <div class="form-group">
                    <label>Version</label>
                    <input type="text" id="mrh-version" placeholder="e.g., v1.0">
                </div>
                <div class="form-group">
                    <label>Patch Download URL</label>
                    <input type="url" id="mrh-patch" required>
                </div>
                <div class="form-group">
                    <label>Dev Log / Updates</label>
                    <textarea id="mrh-devlog"></textarea>
                </div>
                <div class="form-group">
                    <label>Cover Image URL (optional)</label>
                    <input type="url" id="mrh-image">
                </div>
                <div id="add-myromhack-message"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 1rem;">Add ROM Hack</button>
            </form>
        </div>
    </div>

    <!-- View Walkthrough Detail Modal -->
    <div id="walkthrough-detail-modal" class="modal">
        <div class="modal-content" style="max-width: 1200px;">
            <button class="close-modal" onclick="closeModal('walkthrough-detail-modal')">&times;</button>
            <div id="walkthrough-detail-content"></div>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <p>&copy; 2024 Trainer's Odyssey. All rights reserved. Pokémon is a trademark of Nintendo, Game Freak, and The Pokémon Company.</p>
        <div class="social-links" style="margin-top: 1.5rem;">
            <a href="https://youtube.com/@trainersodyssey323" target="_blank">▶</a>
            <a href="https://youtube.com/@handholdhavoc" target="_blank">🎮</a>
            <a href="https://www.instagram.com/pokebattle_reels" target="_blank">📷</a>
        </div>
    </footer>

    <script>
        // Storage using localStorage with persistent data
        const ADMIN_PASSWORD = 'pokemon2024'; // Change this to your preferred password
        let isAdmin = false;

        // Initialize storage
        if (!localStorage.getItem('walkthroughs')) {
            localStorage.setItem('walkthroughs', JSON.stringify([
                {
                    id: 1,
                    title: 'Pokémon FireRed',
                    type: 'official',
                    description: 'Complete walkthrough of Pokémon FireRed with detailed guides, item locations, and strategies.',
                    image: '',
                    parts: []
                },
                {
                    id: 2,
                    title: 'Pokémon Ash Gray',
                    type: 'romhack',
                    description: 'Experience the Pokémon anime through this incredible ROM hack following Ash\'s journey.',
                    image: '',
                    parts: []
                }
            ]));
        }

        if (!localStorage.getItem('myRomHacks')) {
            localStorage.setItem('myRomHacks', JSON.stringify([
                {
                    id: 1,
                    title: 'Giovanni\'s Rise',
                    description: 'Play as Giovanni and build Team Rocket from the ground up in this dark reimagining of the Pokémon world.',
                    features: ['Play as the villain', 'Recruit Team Rocket members', 'Build criminal empire', 'Unique story progression'],
                    version: 'v1.2',
                    patchUrl: '#',
                    devLog: 'Latest update: Added new hideout areas and enhanced battle mechanics.',
                    image: ''
                }
            ]));
        }

        if (!localStorage.getItem('guides')) {
            localStorage.setItem('guides', JSON.stringify([
                {
                    id: 1,
                    title: 'Best Starter Pokémon by Generation',
                    content: 'Comprehensive analysis of all starter Pokémon...',
                    category: 'strategy'
                },
                {
                    id: 2,
                    title: 'How to Install ROM Hacks',
                    content: 'Step-by-step guide to patching and playing ROM hacks...',
                    category: 'tutorial'
                },
                {
                    id: 3,
                    title: 'Top 10 Pokémon ROM Hacks 2024',
                    content: 'The best fan-made Pokémon games you need to play...',
                    category: 'recommendations'
                }
            ]));
        }

        // ===== Built-in walkthrough content =====
        const FR1_IMG = {"1": "data:image/png;base64,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NxmpTraO466ew0BDHJ6gPpZHj+J3TbHaeqxmSsOstuvEt8hK+LBgvBfX7k5hKKqaGKmaJsoOG6lqT/ztn/nKiJ3hZGSgu21G2k1+8e98gRffPsuJC3M89/BRJouD+GKDvKxrOkEc9cwP//vXf0BDhZ/65KMc/9Yx1ganGJr5NIEPJcfqKXFqmobfblE7+z2+/Ffu4fuvHefE7DzPPXzf9TG+9SIra2v8jS98hDMvn8PKTaCnllyb/AZ3GGM7yY4gjqh7GzpXtU4LYet0Xj1L/fvH2TVk0qhUaEw+hGMFWDkHzSlAJFFiZSMIde23lJROE6czU4W+LCnYEoTUtHie6wtg2TSIiT4Kz7UwDFBKKmG7jgwDImnB8jEm4hWe/NjjlJ7exwk3wFZU5C3e71c7VnWvQyjinkPRu5X/+aBifBjuj1jG7C4OEeemODV3ipHmGr/8y1/mxTfPcuLiDcaS51+i2nT5hZ/5NGd/cJJFbYj1gXuYsgY5OjyN9kSfkeppD2bceYxCFk2Dn//0R7ExWPebFO0Moqenm6zjmx0XRVU5enCGei0xUl1ZWWf63p/jvrGpK41UVQUpVPy1MwR6G9My+flPPXPjGM0OrbZPZ10hM3IYVd+Gzf4eYGxd4qqKumnJoKIQqCRGqus+a0tz0GekinmLRqrdTCpOg466ZYnn9H1e45aNVLGzlNZeY3cuoJgr05kssZDRNhXdbyWD2O5Y3axiwIcZ44N8fwA9I9XRTI7i4BFG0GiLVUxTv3GMAzNU6y1aHZ+Vi8ucLT/IdKHPSNWP4+TJIAwOn3+Vhz51P3vGRlBQWFlv8BevHWMkXyKU8aZCXRBFmIbO8TNzdBoBEoXJUoGjzx6h+M43mMiXmS4WeiTNxP4KLj7/2xx5Zoa946MokhvHaIbEQrJvfJQjz8xw8fnfRm4zYPleYFytA9T/ErEkm7VRpcAXcLmSGKnGcXoBhWkAKgJjabARXNtItdvdG0hpOf2vfiPV7i7eJIaIJFJRyWcCGnd9hszuuxguZmlWXDRN5RZrydc9Vtf72Y8Kxgf9/hBSkjUMhJBor/whh54cYf/EGIpUbgpDCMnesREe/sz97D3zIjO5ISw9eTr//11plV76ORu3AAAAVHRFWHRjb21tZW50AEZpbGUgc291cmNlOiBodHRwczovL2FyY2hpdmVzLmJ1bGJhZ2FyZGVuLm5ldC93aWtpL0ZpbGU6UGFsbGV0X1Rvd25fRlJMRy5wbmflxVFUAAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDIzLTA5LTE5VDAxOjA1OjUxKzAwOjAwZFKE4wAAACV0RVh0ZGF0ZTptb2RpZnkAMjAyMy0wOS0xOVQwMTowNTo1MSswMDowMBUPPF8AAAAgdEVYdHNvZnR3YXJlAGh0dHBzOi8vaW1hZ2VtYWdpY2sub3JnvM8dnQAAABh0RVh0VGh1bWI6OkRvY3VtZW50OjpQYWdlcwAxp/+7LwAAABh0RVh0VGh1bWI6OkltYWdlOjpIZWlnaHQAMzIwTiMd3AAAABd0RVh0VGh1bWI6OkltYWdlOjpXaWR0aAAzODQgUGESAAAAGXRFWHRUaHVtYjo6TWltZXR5cGUAaW1hZ2UvcG5nP7JWTgAAABd0RVh0VGh1bWI6Ok1UaW1lADE2OTUwODU1NTFEbfYkAAAAE3RFWHRUaHVtYjo6U2l6ZQAyNDM2NkJC2SZl3gAAAABJRU5ErkJggg==", "2": "data:image/png;base64,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vMRx1/XeDXhvr9Tb19vX29fb1w/0+n8BmfUe3OetB2wAAABRdEVYdGNvbW1lbnQARmlsZSBzb3VyY2U6IGh0dHBzOi8vYXJjaGl2ZXMuYnVsYmFnYXJkZW4ubmV0L3dpa2kvRmlsZTowMDAxQnVsYmFzYXVyLnBuZwqFCfUAAAAldEVYdGRhdGU6Y3JlYXRlADIwMjQtMDEtMTZUMTY6NDE6MjkrMDA6MDDmpLO0AAAAJXRFWHRkYXRlOm1vZGlmeQAyMDI0LTAxLTE2VDE2OjQxOjI5KzAwOjAwl/kLCAAAACB0RVh0c29mdHdhcmUAaHR0cHM6Ly9pbWFnZW1hZ2ljay5vcme8zx2dAAAAGHRFWHRUaHVtYjo6RG9jdW1lbnQ6OlBhZ2VzADGn/7svAAAAGHRFWHRUaHVtYjo6SW1hZ2U6OkhlaWdodAA5Mjfd0A2pAAAAF3RFWHRUaHVtYjo6SW1hZ2U6OldpZHRoADkyN04hXfQAAAAZdEVYdFRodW1iOjpNaW1ldHlwZQBpbWFnZS9wbmc/slZOAAAAF3RFWHRUaHVtYjo6TVRpbWUAMTcwNTQyMzI4OQYpHN0AAAAUdEVYdFRodW1iOjpTaXplADgyMDg3OEJCAQx5WQAAAABJRU5ErkJggg==", "3": "data:image/png;base64,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DgAAAFJ0RVh0Y29tbWVudABGaWxlIHNvdXJjZTogaHR0cHM6Ly9hcmNoaXZlcy5idWxiYWdhcmRlbi5uZXQvd2lraS9GaWxlOjAwMDRDaGFybWFuZGVyLnBuZy7olnQAAAAldEVYdGRhdGU6Y3JlYXRlADIwMjQtMDEtMTZUMTY6NTU6MTQrMDA6MDDBmaotAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDI0LTAxLTE2VDE2OjU1OjE0KzAwOjAwsMQSkQAAACB0RVh0c29mdHdhcmUAaHR0cHM6Ly9pbWFnZW1hZ2ljay5vcme8zx2dAAAAGHRFWHRUaHVtYjo6RG9jdW1lbnQ6OlBhZ2VzADGn/7svAAAAGHRFWHRUaHVtYjo6SW1hZ2U6OkhlaWdodAA5MzK0ochnAAAAF3RFWHRUaHVtYjo6SW1hZ2U6OldpZHRoADkzMidQmDoAAAAZdEVYdFRodW1iOjpNaW1ldHlwZQBpbWFnZS9wbmc/slZOAAAAF3RFWHRUaHVtYjo6TVRpbWUAMTcwNTQyNDExNDbLXckAAAAUdEVYdFRodW1iOjpTaXplADYwNjE0NEJCQ/+tpAAAAABJRU5ErkJggg==", "4": "data:image/png;base64,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lYPPCCAKJMNgg3Dl58Pfd/gJjuL7saKs/MyUadh2z8lHHvrcuScfO7E8Nz0yefr40lt+/ff+OppuXF9YWCI3O8HCpQvLU8cPnJ8/d+qhwvzM37ul4kho91/x6/LBZ9DKf2L+4tnLzWs2DILAV/Uz4MULM5G6E9uqO0T53o/aLaUJWvh+Ko2gP27Y6/uO83+PPPO4AyghJSi1F63brxw/rE4/9vDI5InDD+RmJr5RyS2fArL8lBtewhrE5PL0xBnf8wZXGGhdF+CJF9xpXVevCOsE5ivcDfCqAKJXrfRgvnrl4ANf+r5W/qMLoyP/AIzxKreBPax1+eN7b74o3DJGxA52yD/lIsVKBCKkpLGnLyUNM2XYdq3p9bW4frLJ1gEFMltcWvh6KbP0HP94U+hP7RqbzDB74fSuzftuvS3V3IwfNgTVn95jGEHEpatt13VRYCRikYzHYrnZqWf7d+w+Pn325GsGyCuh7VWhI3vNTs4cff4pvHJxLm4KOtpaSCcTaM9F+z6GIUkm4rQ0N9Lc1IBpmTXloNaaiG3R0tTA0PCw0Tu89T2HH/hS7J+TyXpdXrm5GXzXWZo4c9Kfn5woTo5cuDA3ceVc85oNdAyt29e5/ZqedEMDnudRLFWYHz/LzNnjl1WlfKahuTnmDg5tjUQijZVCfgfQBoy/Vp9FvBEAMSMRhJDtkWTy7kqhcMktFU+GAQX9O/bsHNix+4827bv1ls4Nw9bZgwd5/K/+9PD0icMfB04AdqK5dbP2vZudcqnoVSp/9dOKCP/lAiLxBEBb9+Ztv7vrvg8sdG7cchq4y7Ds1+X7/f8Bi+t9LeYcmFgAAABQdEVYdGNvbW1lbnQARmlsZSBzb3VyY2U6IGh0dHBzOi8vYXJjaGl2ZXMuYnVsYmFnYXJkZW4ubmV0L3dpa2kvRmlsZTowMDA3U3F1aXJ0bGUucG5n9SsjPQAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAyNC0wMS0xNlQxNjozNzoyMyswMDowMGbxiT4AAAAldEVYdGRhdGU6bW9kaWZ5ADIwMjQtMDEtMTZUMTY6Mzc6MjMrMDA6MDAXrDGCAAAAIHRFWHRzb2Z0d2FyZQBodHRwczovL2ltYWdlbWFnaWNrLm9yZ7zPHZ0AAAAYdEVYdFRodW1iOjpEb2N1bWVudDo6UGFnZXMAMaf/uy8AAAAZdEVYdFRodW1iOjpJbWFnZTo6SGVpZ2h0ADEwODbzx1EbAAAAGHRFWHRUaHVtYjo6SW1hZ2U6OldpZHRoADEwODbmjo0CAAAAGXRFWHRUaHVtYjo6TWltZXR5cGUAaW1hZ2UvcG5nP7JWTgAAABd0RVh0VGh1bWI6Ok1UaW1lADE3MDU0MjMwNDNJzW6hAAAAFHRFWHRUaHVtYjo6U2l6ZQA4NjE1MjJCQvzGP7oAAAAASUVORK5CYII=", "5": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///zExMUKUhDlrOTEyMVJSUlKLUmu9pb1SWjY2NlKMUjU1NVJTUyFzY2m7o2qrUWq6ozlsObtSWSJ0ZOdjazMzM0GSgkGTg0KSg2qsUjEzMmq8pGutUkSVhZw5QlFSUVGLUeRiauViajlqOfv7+zEyMlNSUvz9/TQ0NGy7o22+ppo4QVRSUp05QrpRWVFTUru7u7u8vLxRWTMxMb29vWqrUiNyYuZiakOUhDhqOFFRUf78/Dw8PD09PT4+Pj8/P0BAQEFBQUJCQkNDQ0REREVFRUZGRkdHR0hISElJSUpKSktLS0xMTE1NTU5OTk9PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v///7h0a2wAAAABdFJOUwBA5thmAAABC0lEQVR42uyTyXKDMBBE0YjRSIDYDdhgbGObrEaJszjL//9XTqnKASUcckiq3OdX3TU9M45z1v+RYmwad9PlD1O44XSYRKqNbLv8lv2Qr9hwOnS5lL3wXCvlO/7rKpXtUUrZo91RxYHw+Cptj1L2Yu4yO0gBCg9T2eOW86hx7SCBQUR8SqIm4ZzZuUxrXRpEMU+iJonGLVVRE2W6rIkoEHzNo4SNF/0cZiERfeZv1+MFqeGKiKAmAoMVABgcb8iPiSgLAxYTAJhK6xL21mFowXbXAFqXCGDhHFXUtNjk70sArUv2+HI/s+65AAAAUwHsHf+7q1Ds7W7GCnvqV9RRu+XF5a++wll/Qh8DAB/2EkbxKS3KAAAAAElFTkSuQmCC", "6": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///85KQjExMVJSUvdrSqVCOTMxMf///zQxMTU1NfNqSb29vffWnMxKQvemQda1ezY2NvZqSfdrSctJQfPzKVNRUfOjQc5LQvdtSfekQlRSURhjY/f0Kff1KTQyMR8fHyAgICEhISIiIiMjIyQkJCUlJSYmJicnJygoKCkpKSoqKisrKywsLC0tLS4uLi8vLzAwMDExMTIyMjMzMzQ0NDU1NTY2Njc3Nzg4ODk5OTo6Ojs7Ozw8PD09PT4+Pj8/P0BAQEFBQUJCQkNDQ0REREVFRUZGRkdHR0hISElJSUpKSktLS0xMTE1NTU5OTk9PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v///5/s1Z8AAAABdFJOUwBA5thmAAAA20lEQVR42uzUu3bEIAwEUM1ohG2M1+S1eef/P3MLuww2TU6aVX3PIBBgdq8/ranT1TyeEvbB6elhNKv5/XE8WVJIZjV/velAklkazaxevy8HkZSkj63H58vPsZOQzKxeX9MZ3HqbMlLbQeIeaTU3dkNJoc9BgHODv0tKknMAII08jIQkwAEJyWpGo0064O4rXAJeFjQgI9zJUla4HL603BwRNJZSHIDDl1bgTBrDV8cGwdag9/UHAL4fUns6cwQBB8Dj+0jS6ACCHQ+BEV3OOMTcBY3k/SP637oNAIa5BlnB9MIIAAAAAElFTkSuQmCC", "7": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///zExMVJSUlNTU2N7zpSl96XGzjY2NkJanFFSUzIyNFJSUzIzM1NTVDU1NWR8zm1MLJKj9DEyM6PEzEFZmrODSbOzs9Pk9Pz8/GJ5y1RUVJOk9lNTUpWm92J6zaPEzlFRUbKysjMzNGtKKdPk81RUU9bn9/fnlIxjOf///4xkO5Kj80RcnTIxMTExMlJRUaPDy2J6zFJSUTExMGR7zTMyMbODSmV9zrO0tcuyUcyzUs61UmpKKVNSUdTl9mxLK/PkkvTkkjMzM/v7+4tiOPz8/v38+0NbnEhISElJSUpKSktLS0xMTE1NTU5OTk9PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v///zbgmHYAAAABdFJOUwBA5thmAAABLElEQVR42uzUyVLCQBAG4OnJ9EwSyB5CQkLYwgDigrgibijq+7+Rh6BWaRJz40Kfv+7qrvpnCDnU3krUdGY2rDnwBwqocgvrcbhjlbO/ocgkb+YNUAy5AgBEZLKr7xpk4WTRdxAZczOr19y5QimiGBHRaFs9BXLYaec7/IJz/IK8SYiZSckV+ndLM3e6r3lcub4iZiY71CsZyGJ98JE26H1rerLgSrvkljky9fR1dtMIZ3brwSuHUYx49H6sajS0W9Olx4suIUREbqSmjDWog0Zoj85K4eDS7VNK7xIH2Zu9XXrFjhABRDxPJuOwi0Zob5dQGYzVOjm/VWjwNLqoTKSv0c2YbsY0eKlOpK9qsFonjhHAP9kFIKLvIHNrJT1SU7femwA4/DR7r88BAIKOGXfIHUEfAAAAAElFTkSuQmCC", "8": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///0KUhFJSUudrc2OUWjExMUpySkpzSkp0SlFSUVFTUjEyMVJTUlRSUmKSWUKSg2u9pXKzWXO1WqVCSqZCSuRqceVqcjY2Nudsc/6zpP+1pVNRUVNSUTAyMSl5amm7pGq6o2q7o2q8pEOUhESVhXK0Wil7a5JySjEyMjEzMqZDSzIzMeRqclFSUjMxMjU1Nfv7+yp8a1JTU//GAEGTg5RzSqNCSmKTWTMzMzQzMrq6uru7u7u8vCl6alFRUeRrczIxMeVsc1NTU22+pvuyo0GSgvyzo/zEAfz9/f2zo1RTUP78/FRTU0lxSf///09PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v///1/dQkUAAAABdFJOUwBA5thmAAABl0lEQVR42uzUSVvbMBAGYM+MZclObI8cO7LEEickIUASSKALdKFl6wr//+dwMIc2MWkv3Jjzq2+eGT2S573WC5URwjNCiH+wY1FYd15YV843UnPjSooRp0TWnW9wBVG+9e309OfbTqc73wTzTpdixGnetYedL88O4ZnCupKI8i4R0byR3UvZEgURkXVl/sOVRPH6POZeSilliFNbWucOt/DOlXEgWw0yxEDKEBGn9jfubyNi0Gra5nG1mCFq35ch7r/ZxqT9zM5NxUudKa3eSRkiJr7vj46aLshUS535oyxrYyDDxJdSZ/5I6aOmQKWVbqcRIiZtTEZKr0tTMfMStQqxzwwQpRBhoJXOVOtvBwNmXiL2mRkuKU4BIMJAZ6uBMGBmZgAY8NfaAUC0Moz5nNZu0TsQFdSd0ygFmKzscHfWr+FO8Wv4FNYEze7sU4+Z+eDk4RoAonR8BtGHvY/v15Z4cZUOFj3mpzAAGO80PgcjhLite07ELYzP1rquYCGEZy72YJP748TJ8Ptw8p8vVrz+Wy9SjwMANhAj2/LBJxEAAAAASUVORK5CYII=", "9": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///zExMdZjQlJSUveUKbVCOVRSUdNiQvaTKffWc////zQyMNNiQVRTUTMxMfOSKdNjQta1Y0qDcvSSKbJBOFFRUfeUKr29vftZOP9aOf9cOP/nKTY2NjFrWjU1NVNRUTQzMNdkQjUzMVVTUvWTKjIyMveTKbNCOTFqWfeVKTQxMUqEc/5aOP7lKTEyMjQyMv/kKdRjQtZjQTMzMzQ0NDU1NTY2Njc3Nzg4ODk5OTo6Ojs7Ozw8PD09PT4+Pj8/P0BAQEFBQUJCQkNDQ0REREVFRUZGRkdHR0hISElJSUpKSktLS0xMTE1NTU5OTk9PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v////fmHwQAAAABdFJOUwBA5thmAAABTElEQVR42uzTyU7DQBCE4a7qGjtjx3E2SIBxAmHfl/d/OA5YiNiAfOBIX3z59KunJZv9T3cSBrr13d/CtD46GiQ366uHQTKtX46HwpPv5K69CD7PkurHk+MehGBmaRnCBLVKtMnbshc8hFmqq+sQwnYhlTBL9eNpP/gKw9moxLKVKmGp7gd1abYTzDbLELaLKh9J5UHOSTcoB3QBM9sst4vqpplypOo7KErngFk6WKi6aZopOepKSJJ0SBLPkqo8m983zZTM8kk/WJAkKUl6y3x+30yZ7SdBBaGgO0m5pCpnNn/CeD8JiURDegBjjO5q35HGX2G7IekBhhhjjK3EOPN9GCTCQ4Bh9pF0z5nlZHdFAoZVWIE+i+6Si2SWs3MeoP2ApBeSS2L3zfunJ+lefMA28IMEMHNK/Ln2BZMcAs1QcDXs9/91vf/pzPsAv1YSobw/znoAAAAASUVORK5CYII=", "10": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAMAAAC7IEhfAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAIGNIUk0AAHolAACAgwAA+f8AAIDpAAB1MAAA6mAAADqYAAAXb5JfxUYAAAMAUExURf///1JSUjExMVJSU1J7rnut7zY2Nnqr7FJ6q1J7rVNTUmtKKWxLK3mr7FJTVHqs7TpkjYtiOLu7s7u7tL29tc61UmxKKTIyM7ODSVNTUzExMmpKKVFRUVR9rlFSUnl5eTEyMnp6eVF6rFJRUXt7ezIxMYpiOFF5q4xkOv39/bODSjQ0NDU1NcuyUcyzUsy0UzExMPfnlPv7+/z8/Lq6sjhiijMyMbWESlN7q1N8rVRUU32u71RUVDMzM4xjOcy0VDljjM61U/TkkvbmkrKCSVNSUWtKKv38+7SDSf///0pKSktLS0xMTE1NTU5OTk9PT1BQUFFRUVJSUlNTU1RUVFVVVVZWVldXV1hYWFlZWVpaWltbW1xcXF1dXV5eXl9fX2BgYGFhYWJiYmNjY2RkZGVlZWZmZmdnZ2hoaGlpaWpqamtra2xsbG1tbW5ubm9vb3BwcHFxcXJycnNzc3R0dHV1dXZ2dnd3d3h4eHl5eXp6ent7e3x8fH19fX5+fn9/f4CAgIGBgYKCgoODg4SEhIWFhYaGhoeHh4iIiImJiYqKiouLi4yMjI2NjY6Ojo+Pj5CQkJGRkZKSkpOTk5SUlJWVlZaWlpeXl5iYmJmZmZqampubm5ycnJ2dnZ6enp+fn6CgoKGhoaKioqOjo6SkpKWlpaampqenp6ioqKmpqaqqqqurq6ysrK2tra6urq+vr7CwsLGxsbKysrOzs7S0tLW1tba2tre3t7i4uLm5ubq6uru7u7y8vL29vb6+vr+/v8DAwMHBwcLCwsPDw8TExMXFxcbGxsfHx8jIyMnJycrKysvLy8zMzM3Nzc7Ozs/Pz9DQ0NHR0dLS0tPT09TU1NXV1dbW1tfX19jY2NnZ2dra2tvb29zc3N3d3d7e3t/f3+Dg4OHh4eLi4uPj4+Tk5OXl5ebm5ufn5+jo6Onp6erq6uvr6+zs7O3t7e7u7u/v7/Dw8PHx8fLy8vPz8/T09PX19fb29vf39/j4+Pn5+fr6+vv7+/z8/P39/f7+/v///9O2IKEAAAABdFJOUwBA5thmAAABT0lEQVR42uyTx3bCMBRELclPsuUuS3RM72CwCaQnQPr//1AWbG3HycmSWd8zc14ZTbvo/0VxSa4TPpYDr6R8LOO+7IRncokxTr8WhdlTa4Pxa2WwXeA0l1w61bFVu67UKgMxKwCpAzpB8zeEmr1QzvKjqQMA4DJwm71hKOvzfREHAH4k7N7w3artc5Y98QCg6oAfCWlbwWcONzG7ju5V07YHLhLSDqxglDnxhDDwG+OP9vqGIISEHTyNMg0JAwAAfa04QoZJhLStTdb1bgnTPXhWiqOYM90kws7MplijrVgpjmLFDQ90IuR0hLMPTlsIxUpxBrrnGkTUDbObye0aK6XUy932HnRiECHrOYa7Q3RKkiNHYvbA/D4Red9Jd4coVkpxhBiA3+/mPyTGrVOSHDmDYvA8/kopzn7kNE2jGOO0bZbrDy1swl+ae9Hv9D0A5k8fGGdiJDwAAAAASUVORK5CYII=", "11": "data:image/png;base64,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", "12": "data:image/png;base64,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", "13": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyxpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNS1jMDIxIDc5LjE1NDkxMSwgMjAxMy8xMC8yOS0xMTo0NzoxNiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIEVsZW1lbnRzIDEzLjAgKFdpbmRvd3MpIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjYxNTY2MThDODQ1MzExRTdBNTgxOTVENzlCNzA2QkUyIiB4bXBNTTpEb2N1bWVudElEPSJ4bXAuZGlkOjYxNTY2MThEODQ1MzExRTdBNTgxOTVENzlCNzA2QkUyIj4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6NjE1NjYxOEE4NDUzMTFFN0E1ODE5NUQ3OUI3MDZCRTIiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6NjE1NjYxOEI4NDUzMTFFN0E1ODE5NUQ3OUI3MDZCRTIiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz4L9g7IAAABOklEQVR42rRTsY3DMAxkHBdfqvxS5ZceQSNoBI3gETwCR9AIGkHllxpBI6hM+SQtOYTfQYAH/oBLGIdHHUX6Br9hiJa49JjRiIVYe/wSLMKedEXsOQduKnbEyKeu1oA3Bmw/v5I0tQZY23ATiFkX4KqJxWmx4My1vUxSX+oo4rmtqfcZ3onFIv3HOVpzp48v7o1th88PeAdLKQ/6/m4PcT2NS+GeNZDtNgOOiKd7V7nLPEZV+CGRf/CFgfcQQ5CsGCNgTiLc53lUNPOIogzqeVTqYkag2Ke0Fz5hHovhnCN9E9Zar/u3lkwaYSlFpjH1Ddv7RhS7nu3HeAg5ZhfSCqKuWcZIZPtSIpMd27Y1ciXkeIBz1FYavcL1XOQMJa7nlR6rLEXWdW3U4yHMOcszJXb/8jL96XX+EWAAzovFkgdAkw0AAAAASUVORK5CYII=", "14": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAB0SURBVDhP3ZHRCcAgDEQdrSN0JEfIKB0pIzhC80IsIkQK/vngIJynMVrO5TY9Jg1R4/1CTC0Ra0vo4mERaarqou5+ZFK4qm+YGQ4hk8K83nUGj7XIpGwfsD3C94i1Vu+KqLsfmSVb39i5TFyVeRE13nmU8gL1K5iBbIeK4wAAAABJRU5ErkJggg==", "15": "data:image/png;base64,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", "16": "data:image/png;base64,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"};
        const BUILTIN_PARTS = {
            'firered-p1': { title: 'Pokémon Fire Red Walkthrough Part 1', html: "<div class=\"wt-guide\">\n  <p class=\"wt-lead\">This is the walkthrough for Pokémon FireRed and LeafGreen.<\/p>\n\n  <details class=\"wt-collapse wt-toc\" open>\n    <summary>Contents<\/summary>\n    <div class=\"wt-collapse-body\">\n      <ol class=\"wt-toc-list\">\n        <li><a href=\"#fr1-intro\" data-jump>Introduction<\/a><\/li>\n        <li><a href=\"#fr1-pallet\" data-jump>Pallet Town<\/a>\n          <ul>\n            <li><a href=\"#fr1-home\" data-jump>Home<\/a>\n              <ul>\n                <li><a href=\"#fr1-2f\" data-jump>2F<\/a><\/li>\n                <li><a href=\"#fr1-1f\" data-jump>1F<\/a><\/li>\n              <\/ul>\n            <\/li>\n            <li><a href=\"#fr1-oak\" data-jump>Oak Appears!<\/a><\/li>\n          <\/ul>\n        <\/li>\n        <li><a href=\"#fr1-lab\" data-jump>Professor Oak's Lab<\/a>\n          <ul>\n            <li><a href=\"#fr1-rival1\" data-jump>Rival Battle 1<\/a><\/li>\n          <\/ul>\n        <\/li>\n      <\/ol>\n    <\/div>\n  <\/details>\n\n  <h4 class=\"wt-h\" id=\"fr1-intro\">Introduction<\/h4>\n  <p>After a brief cutscene, press the A Button or Start on the title screen. The player is shown a list of controls in order of importance, then with a mission statement from the games' developers. Afterward, the researcher of the Kanto region, Professor Oak, appears on screen and explains a few basics.<\/p>\n  <p>Firstly, Professor Oak asks you to choose your gender and then select a name (7 characters long). Using the Control Pad will allow you to move the cursor and the Select Button to move through three pages of upper-case letters, lower-case letters, and other characters. On this screen, pressing the A Button will select a letter whereas pressing the B Button will delete the previous one. When you are done, press Start or select OK in the bottom-right corner.<\/p>\n  <p>Next, Professor Oak introduces his grandson, who happens to be your rival. The professor is having trouble remembering the boy's name and asks if you might know. Choose his name from a list of preset names or select a new one. With that done, you are transported into the world of Pokémon to begin your adventure!<\/p>\n\n  <div class=\"wt-table-wrap\">\n    <table class=\"wt-table wt-narrow\">\n      <caption>Default Names<\/caption>\n      <thead><tr><th><\/th><th>Pokémon FireRed &amp; LeafGreen<\/th><\/tr><\/thead>\n      <tbody>\n        <tr><th scope=\"row\">Rival<\/th><td>Green, Gary, Kaz, Toru<\/td><\/tr>\n        <tr><th scope=\"row\">Player<\/th><td>Red, Ash, Kene, Geki<\/td><\/tr>\n      <\/tbody>\n    <\/table>\n  <\/div>\n\n  <h4 class=\"wt-h\" id=\"fr1-pallet\">Pallet Town<\/h4>\n  <div class=\"wt-townrow\">\n    <figure class=\"wt-figure\">\n      <img src=\"@@IMG1@@\" alt=\"Pallet Town map\" width=\"300\" height=\"250\" class=\"wt-px\">\n      <figcaption>Pallet Town<\/figcaption>\n    <\/figure>\n    <p>Your journey begins in Pallet Town, in the southwest part of the Kanto region. It is a rather small, quaint town with only three buildings. The western house belongs to you and Mom, while the eastern one is home to your rival and his sister. The large building to the south is Professor Oak's Laboratory. The north part of town leads to the tall grasses of Route 1, and the waters to the south open to Route 21.<\/p>\n  <\/div>\n\n  <details class=\"wt-collapse\" open>\n    <summary>Available Pokémon<\/summary>\n    <div class=\"wt-collapse-body\">\n      <div class=\"wt-starters\"><div class=\"wt-starter\"><img src=\"@@IMG2@@\" alt=\"Bulbasaur\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Bulbasaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Bulbasaur<\/a><\/strong><div><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG5@@\" alt=\"Ivysaur\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Ivysaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Ivysaur<\/a><br><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG8@@\" alt=\"Venusaur\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Venusaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Venusaur<\/a><br><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><\/div><\/div><\/div><div class=\"wt-starter\"><img src=\"@@IMG3@@\" alt=\"Charmander\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmander_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmander<\/a><\/strong><div><span class=\"type-badge type-fire\">Fire<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG6@@\" alt=\"Charmeleon\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmeleon_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmeleon<\/a><br><span class=\"type-badge type-fire\">Fire<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG9@@\" alt=\"Charizard\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charizard_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charizard<\/a><br><span class=\"type-badge type-fire\">Fire<\/span><span class=\"type-badge type-flying\">Flying<\/span><\/div><\/div><\/div><\/div><div class=\"wt-starter\"><img src=\"@@IMG4@@\" alt=\"Squirtle\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Squirtle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Squirtle<\/a><\/strong><div><span class=\"type-badge type-water\">Water<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG7@@\" alt=\"Wartortle\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Wartortle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Wartortle<\/a><br><span class=\"type-badge type-water\">Water<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG10@@\" alt=\"Blastoise\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Blastoise_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Blastoise<\/a><br><span class=\"type-badge type-water\">Water<\/span><\/div><\/div><\/div><\/div><\/div>\n      <div class=\"wt-table-wrap\">\n        <table class=\"wt-table\">\n          <thead><tr><th>Pokémon<\/th><th>Games<\/th><th>Location<\/th><th>Level<\/th><th>Quantity<\/th><\/tr><\/thead>\n          <tbody>\n            <tr><td>Bulbasaur<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><td>First Partner<\/td><td>5<\/td><td>One<\/td><\/tr>\n            <tr><td>Charmander<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><td>First Partner<\/td><td>5<\/td><td>One<\/td><\/tr>\n            <tr><td>Squirtle<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><td>First Partner<\/td><td>5<\/td><td>One<\/td><\/tr>\n          <\/tbody>\n        <\/table>\n      <\/div>\n    <\/div>\n  <\/details>\n\n  <details class=\"wt-collapse\" open>\n    <summary>Items<\/summary>\n    <div class=\"wt-collapse-body\">\n      <div class=\"wt-table-wrap\">\n        <table class=\"wt-table wt-items\">\n          <thead><tr><th>Item<\/th><th>Location<\/th><th>Games<\/th><\/tr><\/thead>\n          <tbody>\n            <tr><td><span class=\"wt-item\"><svg class=\"wt-icon\" viewBox=\"0 0 32 32\" aria-hidden=\"true\"><rect x=\"12\" y=\"2\" width=\"8\" height=\"5\" rx=\"1\" fill=\"#e8e8f0\" stroke=\"#555\" stroke-width=\"1.2\"/><rect x=\"14\" y=\"6\" width=\"4\" height=\"4\" fill=\"#bbb\" stroke=\"#555\" stroke-width=\"1\"/><path d=\"M9 12h14l2 14a3 3 0 0 1-3 4H10a3 3 0 0 1-3-4z\" fill=\"#b25cd6\" stroke=\"#4b1f66\" stroke-width=\"1.5\"/><rect x=\"11\" y=\"16\" width=\"10\" height=\"7\" rx=\"1\" fill=\"#f3e3fb\" opacity=\".85\"/><\/svg><span>Potion<\/span><\/span><\/td><td>Home; retrievable from the player's PC (later visit)<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><\/tr>\n            <tr><td><span class=\"wt-item\"><svg class=\"wt-icon\" viewBox=\"0 0 32 32\" aria-hidden=\"true\"><rect x=\"5\" y=\"3\" width=\"22\" height=\"26\" rx=\"3\" fill=\"#d62828\" stroke=\"#5a0d0d\" stroke-width=\"1.5\"/><rect x=\"9\" y=\"7\" width=\"14\" height=\"10\" rx=\"1\" fill=\"#9be4a2\" stroke=\"#2c5a31\" stroke-width=\"1\"/><circle cx=\"11\" cy=\"22\" r=\"2.2\" fill=\"#fff\" stroke=\"#5a0d0d\"/><rect x=\"16\" y=\"20\" width=\"8\" height=\"2\" fill=\"#5a0d0d\"/><rect x=\"16\" y=\"24\" width=\"8\" height=\"2\" fill=\"#5a0d0d\"/><\/svg><span>Pokédex<\/span><\/span><\/td><td>Oak's Lab; from Professor Oak, after he receives his parcel<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><\/tr>\n            <tr><td><span class=\"wt-item\"><svg class=\"wt-icon\" viewBox=\"0 0 32 32\" aria-hidden=\"true\"><circle cx=\"16\" cy=\"16\" r=\"13\" fill=\"#fff\" stroke=\"#222\" stroke-width=\"2\"/><path d=\"M3 16a13 13 0 0 1 26 0z\" fill=\"#e53935\" stroke=\"#222\" stroke-width=\"2\"/><rect x=\"3\" y=\"14.8\" width=\"26\" height=\"2.4\" fill=\"#222\"/><circle cx=\"16\" cy=\"16\" r=\"4.5\" fill=\"#fff\" stroke=\"#222\" stroke-width=\"2\"/><\/svg><span>Poké Ball ×5<\/span><\/span><\/td><td>Oak's Lab; from Professor Oak, after obtaining the Pokédex<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><\/tr>\n            <tr><td><span class=\"wt-item\"><svg class=\"wt-icon\" viewBox=\"0 0 32 32\" aria-hidden=\"true\"><path d=\"M3 7l8-3 10 3 8-3v21l-8 3-10-3-8 3z\" fill=\"#f3e2b3\" stroke=\"#6b4b1a\" stroke-width=\"1.5\" stroke-linejoin=\"round\"/><path d=\"M11 4v21M21 7v21\" stroke=\"#6b4b1a\" stroke-width=\"1\"/><path d=\"M8 20l4-5 5 3 5-7\" fill=\"none\" stroke=\"#d62828\" stroke-width=\"1.6\" stroke-dasharray=\"2 1.5\"/><circle cx=\"22\" cy=\"11\" r=\"1.8\" fill=\"#d62828\"/><\/svg><span>Town Map<\/span><\/span><\/td><td>Blue's house; from Daisy, after obtaining the Pokédex<\/td><td><span class=\"wt-game\">FR<\/span><span class=\"wt-game\">LG<\/span><\/td><\/tr>\n          <\/tbody>\n        <\/table>\n      <\/div>\n    <\/div>\n  <\/details>\n\n  <h4 class=\"wt-h\" id=\"fr1-home\">Home<\/h4>\n  <h5 class=\"wt-h2\" id=\"fr1-2f\">2F<\/h5>\n  <p>Your journey begins in your bedroom, with you standing in front of your Nintendo Entertainment System. Now that you can control your character, the various buttons and their effects are as follows:<\/p>\n\n  <div class=\"wt-table-wrap\">\n    <table class=\"wt-table wt-narrow\">\n      <thead><tr><th>Input<\/th><th>Effect(s)<\/th><\/tr><\/thead>\n      <tbody>\n        <tr><td>+Control Pad<\/td><td>Moves character; moves cursor in a menu<\/td><\/tr>\n        <tr><td>A Button<\/td><td>Interact with people and the environment; select menu options<\/td><\/tr>\n        <tr><td>B Button<\/td><td>Cancel a selection; exit a menu<\/td><\/tr>\n        <tr><td>Start<\/td><td>Opens the main menu<\/td><\/tr>\n        <tr><td>Select<\/td><td>Sort items; use a registered item<\/td><\/tr>\n        <tr><td>L Button, R Button<\/td><td>Activates the Help System<\/td><\/tr>\n      <\/tbody>\n    <\/table>\n  <\/div>\n\n  <p>The PC in the corner can be used to store items in your item storage and check your Mailbox.<\/p>\n  <p>Your Bag has three pockets: one for Items, one for Key Items, and one for Poké Balls. Each pocket can hold up to 42 different items and up to 999 of each item. If a pocket becomes full, it would be necessary to use or toss some items before obtaining anything new. The PC can hold up to 30 different items from the Items pocket. Deposit Item and Withdraw Item allow for moving items between inventory and storage. A Potion is already in storage, so select Withdraw Item and choose it to add to your Bag. Press the B Button to close the menus and return to your bedroom. To save the game, press Start to open the main menu, select Save, and then Yes. When the menu disappears, your progress is saved and it is safe to exit the game.<\/p>\n  <p>Mail is a type of held item. You may leave a note on each piece of Mail when giving one to one of your Pokémon. This message can be sent to other Trainers by trading Pokémon. When taking a piece of Mail from a Pokémon, you may choose to place it in their Bag or send it to their Mailbox. You can store it in the Mailbox to preserve the original message.<\/p>\n  <p>You can go downstairs by stepping on the stairs in the northeast corner of the room.<\/p>\n\n  <h5 class=\"wt-h2\" id=\"fr1-1f\">1F<\/h5>\n  <p>Your Mom is sitting at the table and tells you that Professor Oak has been looking for you. To leave the house, step on the floor mat along the south wall and press down on the +Control Pad.<\/p>\n\n  <h4 class=\"wt-h\" id=\"fr1-oak\">Oak Appears!<\/h4>\n  <p>Exit the house. Pallet Town has only a few places to explore, and Professor Oak is nowhere to be found. Head for the tall grass on the north side of town. Suddenly, the professor appears! He scolds you for trying to venture off on your own, as it can be dangerous without a Pokémon of your own for defense against wild Pokémon. He will take you to his lab.<\/p>\n\n  <h4 class=\"wt-h\" id=\"fr1-lab\">Professor Oak's Lab<\/h4>\n  <p>Inside his lab Blue is already waiting and gives you the choice of your very first Pokémon. Each has its advantages and disadvantages, so simply choose the one that you like the best.<\/p>\n\n  <div class=\"wt-starters\"><div class=\"wt-starter\"><img src=\"@@IMG2@@\" alt=\"Bulbasaur\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Bulbasaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Bulbasaur<\/a><\/strong><div><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG5@@\" alt=\"Ivysaur\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Ivysaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Ivysaur<\/a><br><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG8@@\" alt=\"Venusaur\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Venusaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Venusaur<\/a><br><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/div><\/div><\/div><\/div><div class=\"wt-starter\"><img src=\"@@IMG3@@\" alt=\"Charmander\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmander_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmander<\/a><\/strong><div><span class=\"type-badge type-fire\">Fire<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG6@@\" alt=\"Charmeleon\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmeleon_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmeleon<\/a><br><span class=\"type-badge type-fire\">Fire<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG9@@\" alt=\"Charizard\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charizard_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charizard<\/a><br><span class=\"type-badge type-fire\">Fire<\/span><span class=\"type-badge type-flying\">Flying<\/span><\/div><\/div><\/div><\/div><div class=\"wt-starter\"><img src=\"@@IMG4@@\" alt=\"Squirtle\" width=\"100\" height=\"100\"><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Squirtle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Squirtle<\/a><\/strong><div><span class=\"type-badge type-water\">Water<\/span><\/div><div class=\"wt-evos\"><div class=\"wt-evo\"><img src=\"@@IMG7@@\" alt=\"Wartortle\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Wartortle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Wartortle<\/a><br><span class=\"type-badge type-water\">Water<\/span><\/div><\/div><div class=\"wt-evo\"><img src=\"@@IMG10@@\" alt=\"Blastoise\" width=\"40\" height=\"40\" class=\"wt-px\"><div><a href=\"https://bulbapedia.bulbagarden.net/wiki/Blastoise_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Blastoise<\/a><br><span class=\"type-badge type-water\">Water<\/span><\/div><\/div><\/div><\/div><\/div>\n\n  <div class=\"wt-table-wrap\">\n    <table class=\"wt-table\">\n      <thead><tr><th><\/th><th>Bulbasaur<\/th><th>Squirtle<\/th><th>Charmander<\/th><\/tr><\/thead>\n      <tbody>\n        <tr><th scope=\"row\">Typing<\/th><td>Grass / Poison<\/td><td>Water<\/td><td>Fire<\/td><\/tr>\n        <tr><th scope=\"row\">Ability<\/th><td>Overgrow<\/td><td>Torrent<\/td><td>Blaze<\/td><\/tr>\n        <tr><th scope=\"row\">Evolves into<\/th><td>Ivysaur → Venusaur<\/td><td>Wartortle → Blastoise<\/td><td>Charmeleon → Charizard <small>(Fire/Flying)<\/small><\/td><\/tr>\n      <\/tbody>\n    <\/table>\n  <\/div>\n\n  <p>Once you are done selecting a Pokémon, you can nickname it if you like. Your rival will pick next and choose the one that has a type advantage over your Pokémon. As you try to leave, he will challenge you to a Pokémon battle!<\/p>\n\n  <h5 class=\"wt-h2\" id=\"fr1-rival1\">Rival Battle 1<\/h5>\n  <p>As you battle your rival, Professor Oak explains the basics. When battling another Trainer, one Pokémon is sent out at a time, and both Pokémon are at Level 5, which is written next to the Pokémon's name. Below is the green health bar, which shows your Pokémon's remaining HP. You win a battle by lowering your opponent's Pokémon's HP to 0. Winning a battle gives you experience points that will level up your Pokémon, and it will eventually evolve.<\/p>\n  <p>Choosing Fight shows you the attacks you can use against your opponent. Each of the Pokémon will have two moves. The first move can damage your opponent and the other one lowers its stats. You can restore your Pokémon to full health when it is low on HP. You can also buy Potions from the Poké Mart to heal your Pokémon on the go.<\/p>\n\n  <div class=\"wt-rivals\">\n    <div class=\"wt-rival\">\n  <div class=\"wt-rival-head\"><img src=\"@@IMG11@@\" alt=\"Bulbasaur\" width=\"40\" height=\"40\" class=\"wt-px\"><span>If the player chose <strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Bulbasaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Bulbasaur<\/a><\/strong>:<\/span><\/div>\n  <div class=\"wt-rival-body\">\n    <div class=\"wt-trainer\"><img src=\"@@IMG12@@\" alt=\"Blue\" width=\"64\" height=\"64\" class=\"wt-px\">\n      <dl><dt>Rival<\/dt><dd><strong>Blue<\/strong><\/dd><dt>Location<\/dt><dd>Professor Oak's Laboratory<\/dd><dt>Games<\/dt><dd>FireRed and LeafGreen<\/dd><dt>Reward<\/dt><dd><strong>$80<\/strong><\/dd><\/dl>\n      <div class=\"wt-balls\"><img src=\"@@IMG13@@\" alt=\"Pokémon\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><\/div><\/div>\n    <div class=\"wt-mon\"><img src=\"@@IMG3@@\" alt=\"Charmander\" width=\"100\" height=\"100\">\n      <div><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmander_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmander<\/a><\/strong> ♂ Lv.5<dl><dt>Type<\/dt><dd><span class=\"type-badge type-fire\">Fire<\/span><\/dd><dt>Ability<\/dt><dd><strong>Blaze<\/strong><\/dd><dt>Held item<\/dt><dd><strong>None<\/strong><\/dd><\/dl><\/div>\n      <ul class=\"wt-moves\"><li><span>Scratch<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><li><span>Growl<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><\/ul><\/div>\n  <\/div><\/div>\n    <div class=\"wt-rival\">\n  <div class=\"wt-rival-head\"><img src=\"@@IMG15@@\" alt=\"Charmander\" width=\"40\" height=\"40\" class=\"wt-px\"><span>If the player chose <strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Charmander_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Charmander<\/a><\/strong>:<\/span><\/div>\n  <div class=\"wt-rival-body\">\n    <div class=\"wt-trainer\"><img src=\"@@IMG12@@\" alt=\"Blue\" width=\"64\" height=\"64\" class=\"wt-px\">\n      <dl><dt>Rival<\/dt><dd><strong>Blue<\/strong><\/dd><dt>Location<\/dt><dd>Professor Oak's Laboratory<\/dd><dt>Games<\/dt><dd>FireRed and LeafGreen<\/dd><dt>Reward<\/dt><dd><strong>$80<\/strong><\/dd><\/dl>\n      <div class=\"wt-balls\"><img src=\"@@IMG13@@\" alt=\"Pokémon\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><\/div><\/div>\n    <div class=\"wt-mon\"><img src=\"@@IMG4@@\" alt=\"Squirtle\" width=\"100\" height=\"100\">\n      <div><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Squirtle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Squirtle<\/a><\/strong> ♂ Lv.5<dl><dt>Type<\/dt><dd><span class=\"type-badge type-water\">Water<\/span><\/dd><dt>Ability<\/dt><dd><strong>Torrent<\/strong><\/dd><dt>Held item<\/dt><dd><strong>None<\/strong><\/dd><\/dl><\/div>\n      <ul class=\"wt-moves\"><li><span>Tackle<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><li><span>Tail Whip<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><\/ul><\/div>\n  <\/div><\/div>\n    <div class=\"wt-rival\">\n  <div class=\"wt-rival-head\"><img src=\"@@IMG16@@\" alt=\"Squirtle\" width=\"40\" height=\"40\" class=\"wt-px\"><span>If the player chose <strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Squirtle_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Squirtle<\/a><\/strong>:<\/span><\/div>\n  <div class=\"wt-rival-body\">\n    <div class=\"wt-trainer\"><img src=\"@@IMG12@@\" alt=\"Blue\" width=\"64\" height=\"64\" class=\"wt-px\">\n      <dl><dt>Rival<\/dt><dd><strong>Blue<\/strong><\/dd><dt>Location<\/dt><dd>Professor Oak's Laboratory<\/dd><dt>Games<\/dt><dd>FireRed and LeafGreen<\/dd><dt>Reward<\/dt><dd><strong>$80<\/strong><\/dd><\/dl>\n      <div class=\"wt-balls\"><img src=\"@@IMG13@@\" alt=\"Pokémon\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><img src=\"@@IMG14@@\" alt=\"Empty slot\" width=\"16\" height=\"16\"><\/div><\/div>\n    <div class=\"wt-mon\"><img src=\"@@IMG2@@\" alt=\"Bulbasaur\" width=\"100\" height=\"100\">\n      <div><strong><a href=\"https://bulbapedia.bulbagarden.net/wiki/Bulbasaur_(Pok%C3%A9mon)\" target=\"_blank\" rel=\"noopener\">Bulbasaur<\/a><\/strong> ♂ Lv.5<dl><dt>Types<\/dt><dd><span class=\"type-badge type-grass\">Grass<\/span><span class=\"type-badge type-poison\">Poison<\/span><\/dd><dt>Ability<\/dt><dd><strong>Overgrow<\/strong><\/dd><dt>Held item<\/dt><dd><strong>None<\/strong><\/dd><\/dl><\/div>\n      <ul class=\"wt-moves\"><li><span>Tackle<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><li><span>Growl<\/span><span class=\"type-badge type-normal\">Normal<\/span><\/li><\/ul><\/div>\n  <\/div><\/div>\n  <\/div>\n\n  <p>You earn $80 in prizes after defeating Blue, after which he leaves. He makes a joke about his sister having two maps and telling her not to lend you one before leaving. Your chosen Pokémon will grow to Level 6. Exit the laboratory and head to Route 1.<\/p>\n<\/div>\n" }
        };

        // Make sure the Pokémon FireRed entry always carries the built-in Part 1
        // (works for brand-new visitors and for browsers that already saved data).
        function ensureBuiltinParts() {
            const list = JSON.parse(localStorage.getItem('walkthroughs')) || [];
            const norm = s => (s || '').toLowerCase().replace(/\s+/g, '');
            const fr = list.find(w => norm(w.title) === 'pokémonfirered') || list.find(w => w.id === 1);
            if (!fr) return;
            fr.parts = fr.parts || [];
            if (!fr.parts.some(p => p.builtin === 'firered-p1')) {
                fr.parts.unshift({ id: 'builtin-firered-p1', builtin: 'firered-p1', title: BUILTIN_PARTS['firered-p1'].title });
                localStorage.setItem('walkthroughs', JSON.stringify(list));
            }
        }
        ensureBuiltinParts();

        function renderBuiltinPart(part) {
            const def = BUILTIN_PARTS[part.builtin];
            if (!def) return '';
            const body = def.html.replace(/@@IMG(\d+)@@/g, (m, n) => FR1_IMG[n] || '');
            return `<div class="wt-part-wrap"><h3>${def.title}</h3>${body}</div>`;
        }

        // Navigation
        function showSection(sectionId) {
            document.querySelectorAll('section').forEach(section => {
                section.style.display = 'none';
            });
            document.getElementById(sectionId).style.display = 'block';
            
            // Load section content
            if (sectionId === 'walkthroughs') loadWalkthroughs();
            if (sectionId === 'myromhacks') loadMyRomHacks();
            if (sectionId === 'guides') loadGuides();
            if (sectionId === 'home') loadHome();
            if (sectionId === 'pokedex') loadPokedex();
            if (sectionId === 'romhacks') loadRomHacksHub();
            if (sectionId === 'videos') loadVideos();
        }

        // Modal functions
        function showAdminLogin() {
            document.getElementById('admin-login-modal').classList.add('active');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
        }

        function adminLogin(event) {
            event.preventDefault();
            const password = document.getElementById('admin-password').value;
            const messageDiv = document.getElementById('login-message');
            
            if (password === ADMIN_PASSWORD) {
                isAdmin = true;
                messageDiv.innerHTML = '<div class="success-msg">Login successful! Admin features enabled.</div>';
                setTimeout(() => {
                    closeModal('admin-login-modal');
                    showAdminPanels();
                }, 1000);
            } else {
                messageDiv.innerHTML = '<div class="error-msg">Incorrect password!</div>';
            }
        }

        function showAdminPanels() {
            document.getElementById('admin-walkthrough-panel').style.display = 'block';
            document.getElementById('admin-myromhacks-panel').style.display = 'block';
        }

        function showAddWalkthroughModal() {
            document.getElementById('add-walkthrough-modal').classList.add('active');
        }

        function showAddMyRomHackModal() {
            document.getElementById('add-myromhack-modal').classList.add('active');
        }

        function addWalkthrough(event) {
            event.preventDefault();
            if (!isAdmin) return;

            const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs'));
            const newWalkthrough = {
                id: Date.now(),
                title: document.getElementById('wt-title').value,
                type: document.getElementById('wt-type').value,
                description: document.getElementById('wt-description').value,
                image: document.getElementById('wt-image').value,
                parts: []
            };

            walkthroughs.push(newWalkthrough);
            localStorage.setItem('walkthroughs', JSON.stringify(walkthroughs));

            document.getElementById('add-walkthrough-message').innerHTML = '<div class="success-msg">Walkthrough added successfully!</div>';
            setTimeout(() => {
                closeModal('add-walkthrough-modal');
                loadWalkthroughs();
                event.target.reset();
            }, 1000);
        }

        function showAddPartModal(gameId) {
            document.getElementById('part-game-id').value = gameId;
            document.getElementById('add-part-modal').classList.add('active');
        }

        function addWalkthroughPart(event) {
            event.preventDefault();
            if (!isAdmin) return;

            const gameId = parseInt(document.getElementById('part-game-id').value);
            const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs'));
            const game = walkthroughs.find(w => w.id === gameId);

            if (game) {
                const newPart = {
                    id: Date.now(),
                    title: document.getElementById('part-title').value,
                    videoUrl: document.getElementById('part-video').value,
                    content: document.getElementById('part-content').value,
                    tips: document.getElementById('part-tips').value
                };

                game.parts.push(newPart);
                localStorage.setItem('walkthroughs', JSON.stringify(walkthroughs));

                document.getElementById('add-part-message').innerHTML = '<div class="success-msg">Part added successfully!</div>';
                setTimeout(() => {
                    closeModal('add-part-modal');
                    event.target.reset();
                }, 1000);
            }
        }

        function addMyRomHack(event) {
            event.preventDefault();
            if (!isAdmin) return;

            const romHacks = JSON.parse(localStorage.getItem('myRomHacks'));
            const newRomHack = {
                id: Date.now(),
                title: document.getElementById('mrh-title').value,
                description: document.getElementById('mrh-description').value,
                features: document.getElementById('mrh-features').value.split('\n').filter(f => f.trim()),
                version: document.getElementById('mrh-version').value,
                patchUrl: document.getElementById('mrh-patch').value,
                devLog: document.getElementById('mrh-devlog').value,
                image: document.getElementById('mrh-image').value
            };

            romHacks.push(newRomHack);
            localStorage.setItem('myRomHacks', JSON.stringify(romHacks));

            document.getElementById('add-myromhack-message').innerHTML = '<div class="success-msg">ROM Hack added successfully!</div>';
            setTimeout(() => {
                closeModal('add-myromhack-modal');
                loadMyRomHacks();
                event.target.reset();
            }, 1000);
        }

        // Load functions
        function loadWalkthroughs() {
            const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs'));
            const grid = document.getElementById('walkthroughs-grid');
            
            grid.innerHTML = walkthroughs.map(wt => `
                <div class="card walkthrough-card" data-type="${wt.type}">
                    ${wt.image ? `<img src="${wt.image}" alt="${wt.title}" style="width: 100%; border-radius: 10px; margin-bottom: 1rem;">` : ''}
                    <h3>${wt.title}</h3>
                    <span class="card-tag">${wt.type === 'official' ? 'Official Game' : 'ROM Hack'}</span>
                    <p>${wt.description}</p>
                    <div style="margin-top: 1.5rem; display: flex; gap: 1rem; flex-wrap: wrap;">
                        <button class="btn" onclick="viewWalkthrough(${wt.id})">View Walkthrough</button>
                        ${isAdmin ? `<button class="btn btn-primary" onclick="showAddPartModal(${wt.id})">+ Add Part</button>` : ''}
                    </div>
                </div>
            `).join('');
        }

        function viewWalkthrough(id) {
            const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs'));
            const wt = walkthroughs.find(w => w.id === id);
            
            if (!wt) return;

            const partsHtml = wt.parts.map(part => {
                if (part.builtin) return renderBuiltinPart(part);
                const videoId = extractYouTubeId(part.videoUrl || '');
                return `
                    <div class="walkthrough-part" style="cursor: default; margin-bottom: 2rem;">
                        <h3 style="color: var(--accent); margin-bottom: 1rem;">${part.title}</h3>
                        ${videoId ? `
                            <div class="video-container">
                                <iframe src="https://www.youtube.com/embed/${videoId}" frameborder="0" allowfullscreen></iframe>
                            </div>
                        ` : ''}
                        <div style="margin-top: 1.5rem; color: rgba(245, 245, 245, 0.9); line-height: 1.8;">
                            ${part.content.replace(/\n/g, '<br>')}
                        </div>
                        ${part.tips ? `
                            <div style="margin-top: 1.5rem; padding: 1rem; background: rgba(255, 222, 0, 0.1); border-left: 3px solid var(--accent); border-radius: 5px;">
                                <strong style="color: var(--accent);">💡 Key Tips & Items:</strong><br>
                                ${part.tips.replace(/\n/g, '<br>')}
                            </div>
                        ` : ''}
                    </div>
                `;
            }).join('');

            const content = `
                <div class="game-header">
                    <h2>${wt.title}</h2>
                    <p style="margin-top: 1rem; font-size: 1.1rem;">${wt.description}</p>
                </div>
                ${wt.parts.length > 0 ? partsHtml : '<p style="text-align: center; color: rgba(245, 245, 245, 0.6);">No walkthrough parts added yet.</p>'}
            `;

            document.getElementById('walkthrough-detail-content').innerHTML = content;
            document.getElementById('walkthrough-detail-modal').classList.add('active');
            document.querySelector('#walkthrough-detail-modal .modal-content').scrollTop = 0;
        }

        function extractYouTubeId(url) {
            const regExp = /^.*((youtu.be\/)|(v\/)|(\/u\/\w\/)|(embed\/)|(watch\?))\??v?=?([^#&?]*).*/;
            const match = url.match(regExp);
            return (match && match[7].length === 11) ? match[7] : null;
        }

        function loadMyRomHacks() {
            const romHacks = JSON.parse(localStorage.getItem('myRomHacks'));
            const grid = document.getElementById('myromhacks-grid');
            
            grid.innerHTML = romHacks.map(rh => `
                <div class="card">
                    ${rh.image ? `<img src="${rh.image}" alt="${rh.title}" style="width: 100%; border-radius: 10px; margin-bottom: 1rem;">` : ''}
                    <h3>${rh.title}</h3>
                    <span class="card-tag">${rh.version}</span>
                    <p>${rh.description}</p>
                    ${rh.features.length > 0 ? `
                        <div style="margin-top: 1rem;">
                            <strong style="color: var(--accent);">Features:</strong>
                            <ul style="margin-top: 0.5rem; padding-left: 1.5rem; color: rgba(245, 245, 245, 0.8);">
                                ${rh.features.map(f => `<li>${f}</li>`).join('')}
                            </ul>
                        </div>
                    ` : ''}
                    ${rh.devLog ? `
                        <div style="margin-top: 1rem; padding: 1rem; background: rgba(59, 76, 202, 0.1); border-radius: 8px;">
                            <strong style="color: var(--secondary);">📝 Dev Log:</strong><br>
                            <span style="color: rgba(245, 245, 245, 0.8);">${rh.devLog}</span>
                        </div>
                    ` : ''}
                    <div style="margin-top: 1.5rem;">
                        <a href="${rh.patchUrl}" class="btn btn-primary" download>⬇ Download Patch</a>
                    </div>
                </div>
            `).join('');
        }

        function loadGuides() {
            const guides = JSON.parse(localStorage.getItem('guides'));
            const grid = document.getElementById('guides-grid');
            
            grid.innerHTML = guides.map(guide => `
                <div class="card">
                    <h3>${guide.title}</h3>
                    <span class="card-tag">${guide.category}</span>
                    <p>${guide.content.substring(0, 150)}...</p>
                    <div style="margin-top: 1.5rem;">
                        <button class="btn">Read More</button>
                    </div>
                </div>
            `).join('');
        }

        function loadHome() {
            const walkthroughs = JSON.parse(localStorage.getItem('walkthroughs'));
            const guides = JSON.parse(localStorage.getItem('guides'));
            const grid = document.getElementById('latest-content');
            
            const latest = [
                ...walkthroughs.slice(-2).map(wt => ({...wt, type: 'walkthrough'})),
                ...guides.slice(-2).map(g => ({...g, type: 'guide'}))
            ];

            grid.innerHTML = latest.map(item => `
                <div class="card">
                    <h3>${item.title}</h3>
                    <span class="card-tag">${item.type === 'walkthrough' ? 'Walkthrough' : 'Guide'}</span>
                    <p>${item.description || item.content?.substring(0, 100) + '...'}</p>
                    <div style="margin-top: 1.5rem;">
                        <button class="btn" onclick="showSection('${item.type === 'walkthrough' ? 'walkthroughs' : 'guides'}')">View ${item.type === 'walkthrough' ? 'Walkthrough' : 'Guide'}</button>
                    </div>
                </div>
            `).join('');
        }

        function loadPokedex() {
            const grid = document.getElementById('pokedex-grid');
            const samplePokemon = [
                { num: 1, name: 'Bulbasaur', type: ['grass'], gen: 'gen1' },
                { num: 4, name: 'Charmander', type: ['fire'], gen: 'gen1' },
                { num: 7, name: 'Squirtle', type: ['water'], gen: 'gen1' },
                { num: 25, name: 'Pikachu', type: ['electric'], gen: 'gen1' },
                { num: 152, name: 'Chikorita', type: ['grass'], gen: 'gen2' },
                { num: 155, name: 'Cyndaquil', type: ['fire'], gen: 'gen2' }
            ];

            grid.innerHTML = samplePokemon.map(p => `
                <div class="card" data-gen="${p.gen}">
                    <h3>#${String(p.num).padStart(3, '0')} ${p.name}</h3>
                    <div style="margin: 1rem 0;">
                        ${p.type.map(t => `<span class="type-badge type-${t}">${t}</span>`).join(' ')}
                    </div>
                    <p>Click to view complete stats, moves, locations, and evolution details.</p>
                    <div style="margin-top: 1.5rem;">
                        <button class="btn">View Details</button>
                    </div>
                </div>
            `).join('');
        }

        function loadRomHacksHub() {
            const grid = document.getElementById('romhacks-grid');
            const sampleRomHacks = [
                { title: 'Pokémon Gaia', region: 'hoenn', difficulty: 'easy', description: 'A quality ROM hack with new region Orbtus' },
                { title: 'Pokémon Unbound', region: 'hoenn', difficulty: 'hard', description: 'Professional-grade hack with modern features' },
                { title: 'Pokémon Radical Red', region: 'kanto', difficulty: 'hard', description: 'Enhanced FireRed with competitive difficulty' }
            ];

            grid.innerHTML = sampleRomHacks.map(rh => `
                <div class="card" data-region="${rh.region}" data-difficulty="${rh.difficulty}">
                    <h3>${rh.title}</h3>
                    <span class="card-tag">${rh.difficulty}</span>
                    <p>${rh.description}</p>
                    <div style="margin-top: 1.5rem;">
                        <button class="btn">View Details</button>
                    </div>
                </div>
            `).join('');
        }

        function loadVideos() {
            const grid = document.getElementById('playlists-grid');
            const playlists = [
                { title: 'Pokémon Ash Gray Complete Series', channel: 'Trainer\'s Odyssey' },
                { title: 'Pokémon FireRed Nuzlocke', channel: 'Trainer\'s Odyssey' },
                { title: 'Naruto Ultimate Ninja Impact', channel: 'Handhold Havoc' },
                { title: 'God of War PSP Collection', channel: 'Handhold Havoc' }
            ];

            grid.innerHTML = playlists.map(pl => `
                <div class="card">
                    <h3>${pl.title}</h3>
                    <span class="card-tag">${pl.channel}</span>
                    <div style="margin-top: 1.5rem;">
                        <button class="btn">Watch Playlist</button>
                    </div>
                </div>
            `).join('');
        }

        // Filter functions
        function filterWalkthroughs(type) {
            const cards = document.querySelectorAll('.walkthrough-card');
            const buttons = document.querySelectorAll('.filters .filter-btn');
            
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            cards.forEach(card => {
                if (type === 'all' || card.dataset.type === type) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        function filterPokedex(gen) {
            const cards = document.querySelectorAll('#pokedex-grid .card');
            const buttons = document.querySelectorAll('#pokedex .filters .filter-btn');
            
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            cards.forEach(card => {
                if (gen === 'all' || card.dataset.gen === gen) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        function filterRomHacks(filter) {
            const cards = document.querySelectorAll('#romhacks-grid .card');
            const buttons = document.querySelectorAll('#romhacks .filters .filter-btn');
            
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            cards.forEach(card => {
                if (filter === 'all' || 
                    card.dataset.region === filter || 
                    card.dataset.difficulty === filter.replace('difficulty-', '')) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // Search functionality
        document.getElementById('walkthrough-search')?.addEventListener('input', (e) => {
            const searchTerm = e.target.value.toLowerCase();
            const cards = document.querySelectorAll('.walkthrough-card');
            
            cards.forEach(card => {
                const title = card.querySelector('h3').textContent.toLowerCase();
                const description = card.querySelector('p').textContent.toLowerCase();
                
                if (title.includes(searchTerm) || description.includes(searchTerm)) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        });

        document.getElementById('pokedex-search')?.addEventListener('input', (e) => {
            const searchTerm = e.target.value.toLowerCase();
            const cards = document.querySelectorAll('#pokedex-grid .card');
            
            cards.forEach(card => {
                const title = card.querySelector('h3').textContent.toLowerCase();
                
                if (title.includes(searchTerm)) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        });

        // Contents links inside the walkthrough modal: scroll the modal, not the page
        document.getElementById('walkthrough-detail-content').addEventListener('click', (e) => {
            const link = e.target.closest('a[data-jump]');
            if (!link) return;
            e.preventDefault();
            const target = document.getElementById(link.getAttribute('href').slice(1));
            if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
        });

        // Header: hide while scrolling down, reveal on scroll up so it never blocks the page
        (function () {
            const header = document.querySelector('header');
            const SHOW_ZONE = 80;   // always visible near the top
            const THRESHOLD = 8;    // ignore tiny scroll jitters
            let lastY = window.scrollY;
            let ticking = false;

            function update() {
                const y = Math.max(window.scrollY, 0);
                const delta = y - lastY;
                if (y < SHOW_ZONE) {
                    header.classList.remove('header-hidden');
                } else if (delta > THRESHOLD) {
                    header.classList.add('header-hidden');
                } else if (delta < -THRESHOLD) {
                    header.classList.remove('header-hidden');
                }
                if (Math.abs(delta) > THRESHOLD) lastY = y;
                ticking = false;
            }

            window.addEventListener('scroll', () => {
                if (!ticking) {
                    window.requestAnimationFrame(update);
                    ticking = true;
                }
            }, { passive: true });
        })();

        // Initialize
        showSection('home');
    </script>
</body>
</html>
