
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Student Hub | खाटू टीम एक्सरसाइज</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        
        :root {
            --bg: #0a0a0c;
            --card-bg: #121318;
            --royal-border: #d4af37;
            --sub-border: #232530;
            --text-main: #f0f3f6;
            --text-muted: #8b949e;
            --btn-blue: #1f6feb;
            --btn-blue-hover: #388bfd;
            --ktx-red: #ff3333;
            --badge-green: #238636;
            --vip-gold: #ffd700;
        }

        body {
            background-color: var(--bg);
            color: var(--text-main);
            min-height: 100vh;
            padding-bottom: 60px;
        }

        /* 1. Terms & Conditions Modal (First Visit) */
        #termsModal {
            position: fixed;
            inset: 0;
            background: rgba(10, 10, 12, 0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 15px;
        }
        .terms-card {
            background: var(--card-bg);
            border: 2px solid var(--royal-border);
            border-radius: 12px;
            padding: 30px 25px;
            width: 100%;
            max-width: 440px;
            text-align: center;
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.25);
        }
        .ktx-logo-big {
            font-size: 32px;
            font-weight: 900;
            color: var(--ktx-red);
            letter-spacing: 2px;
            margin-bottom: 5px;
            text-shadow: 0 0 10px rgba(255, 51, 51, 0.4);
        }
        .terms-sub {
            font-size: 11px;
            color: var(--royal-border);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 15px;
        }
        .terms-box {
            background: #000;
            border: 1px solid var(--sub-border);
            border-radius: 8px;
            padding: 12px;
            text-align: left;
            font-size: 12px;
            color: var(--text-muted);
            line-height: 1.6;
            margin-bottom: 20px;
            max-height: 150px;
            overflow-y: auto;
        }
        .terms-box strong { color: var(--text-main); }
        .btn-blue-action {
            width: 100%;
            padding: 12px;
            background: var(--btn-blue);
            color: #ffffff;
            border: none;
            border-radius: 6px;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s ease;
        }
        .btn-blue-action:hover {
            background: var(--btn-blue-hover);
            box-shadow: 0 0 12px rgba(31, 111, 235, 0.6);
        }

        /* 2. Top Navigation Bar */
        .navbar {
            background: var(--card-bg);
            border-bottom: 2px solid var(--royal-border);
            padding: 12px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .brand-title {
            font-size: 20px;
            font-weight: 900;
            color: var(--ktx-red);
            text-shadow: 0 0 8px rgba(255, 51, 51, 0.3);
        }
        .brand-sub {
            font-size: 9px;
            color: var(--royal-border);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        .nav-actions {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .wallet-pill {
            background: #000;
            border: 1.5px solid var(--royal-border);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: bold;
            color: var(--royal-border);
            cursor: pointer;
            box-shadow: 0 0 8px rgba(212, 175, 55, 0.2);
        }
        .btn-profile-toggle {
            background: transparent;
            border: 1px solid var(--royal-border);
            color: var(--royal-border);
            padding: 6px 14px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: bold;
            cursor: pointer;
        }
        .btn-profile-toggle:hover {
            background: var(--royal-border);
            color: #000;
        }

        /* 3. Main Container */
        .container {
            max-width: 1200px;
            margin: 25px auto;
            padding: 0 20px;
        }

        /* 4. Student Profile & Wallet Drawer */
        #profileDrawer {
            display: none;
            background: var(--card-bg);
            border: 2px solid var(--royal-border);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
            box-shadow: 0 0 20px rgba(0,0,0,0.8);
        }
        .profile-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--sub-border);
            padding-bottom: 12px;
            margin-bottom: 15px;
        }
        .profile-info h3 { color: #fff; font-size: 16px; }
        .profile-info p { color: var(--royal-border); font-size: 12px; }
        
        .wallet-banner-box {
            background: #000;
            border: 1.5px solid var(--royal-border);
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
            text-align: left;
        }
        .wallet-banner-box h4 {
            color: var(--royal-border);
            font-size: 14px;
            margin-bottom: 6px;
        }
        .wallet-banner-box p {
            color: var(--text-muted);
            font-size: 12px;
            line-height: 1.5;
        }
        .profile-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 12px;
            margin-top: 15px;
        }
        .stat-box {
            background: #000;
            border: 1px solid var(--sub-border);
            border-radius: 6px;
            padding: 10px;
            text-align: center;
        }
        .stat-box span {
            font-size: 16px;
            font-weight: bold;
            color: var(--text-main);
            display: block;
        }
        .stat-box label {
            font-size: 10px;
            color: var(--text-muted);
            text-transform: uppercase;
        }

        /* 5. Hero Banner */
        .hero {
            background: radial-gradient(circle at top, #1c1a24 0%, var(--card-bg) 100%);
            border: 1px solid var(--royal-border);
            border-radius: 12px;
            padding: 25px;
            text-align: center;
            margin-bottom: 25px;
        }
        .hero h1 { font-size: 24px; color: #fff; margin-bottom: 6px; }
        .hero h1 span { color: var(--ktx-red); }
        .hero p { font-size: 13px; color: var(--text-muted); }

        /* 6. Tool Category Tabs & Search */
        .filter-row {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .search-tool {
            flex: 1;
            min-width: 220px;
            padding: 10px 15px;
            background: var(--card-bg);
            border: 1px solid var(--royal-border);
            border-radius: 6px;
            color: #fff;
            font-size: 13px;
            outline: none;
        }
        .category-select {
            padding: 10px 15px;
            background: var(--card-bg);
            border: 1px solid var(--royal-border);
            border-radius: 6px;
            color: #fff;
            font-size: 13px;
            outline: none;
        }

        /* 7. Student Tools Grid */
        .tools-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }
        .tool-card {
            background: var(--card-bg);
            border: 1.5px solid var(--royal-border);
            border-radius: 10px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        .tool-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.15);
        }
        .tool-badges {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }
        .tool-tag {
            font-size: 10px;
            text-transform: uppercase;
            color: var(--royal-border);
            background: rgba(212, 175, 55, 0.1);
            border: 1px solid var(--royal-border);
            padding: 3px 8px;
            border-radius: 4px;
            font-weight: bold;
        }
        .vip-badge {
            font-size: 10px;
            color: #000;
            background: var(--vip-gold);
            padding: 3px 8px;
            border-radius: 4px;
            font-weight: 900;
            text-transform: uppercase;
        }
        .tool-card h3 { font-size: 16px; color: #ffffff; margin-bottom: 8px; }
        .tool-card p {
            font-size: 12px;
            color: var(--text-muted);
            line-height: 1.5;
            margin-bottom: 20px;
            flex-grow: 1;
        }
        .card-btn {
            width: 100%;
            padding: 10px;
            background: var(--btn-blue);
            color: #ffffff;
            border: none;
            border-radius: 6px;
            font-size: 13px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s ease;
        }
        .card-btn:hover { background: var(--btn-blue-hover); }
        .btn-vip-use {
            background: linear-gradient(135deg, #d4af37, #aa820a);
            color: #000;
        }
        .btn-vip-use:hover {
            background: #ffd700;
            box-shadow: 0 0 12px rgba(212, 175, 55, 0.6);
        }

        /* 8. Interactive Modals */
        #toolModal, #congratsModal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.88);
            align-items: center;
            justify-content: center;
            z-index: 2000;
            padding: 20px;
        }
        .modal-box {
            background: var(--card-bg);
            border: 2px solid var(--royal-border);
            border-radius: 12px;
            padding: 25px;
            width: 100%;
            max-width: 480px;
            box-shadow: 0 0 30px rgba(0,0,0,0.9);
            text-align: center;
        }
        .modal-box h2 { font-size: 18px; color: #fff; margin-bottom: 8px; }
        .modal-box p { font-size: 12px; color: var(--text-muted); margin-bottom: 15px; }
        
        .interactive-area {
            width: 100%;
            padding: 12px;
            background: #000;
            border: 1px solid var(--royal-border);
            border-radius: 6px;
            color: #fff;
            font-size: 13px;
            min-height: 90px;
            margin-bottom: 12px;
            outline: none;
            resize: vertical;
            text-align: left;
        }
        .api-input-field {
            width: 100%;
            padding: 10px;
            background: #000;
            border: 1px solid var(--royal-border);
            border-radius: 6px;
            color: #fff;
            font-size: 12px;
            margin-bottom: 12px;
            outline: none;
            text-align: center;
        }
        .drop-zone {
            border: 2px dashed var(--royal-border);
            border-radius: 8px;
            padding: 25px 15px;
            text-align: center;
            color: var(--text-muted);
            font-size: 13px;
            margin-bottom: 15px;
            background: #000;
            cursor: pointer;
        }
        .drop-zone:hover { color: #fff; border-color: #fff; }
        .modal-close {
            background: transparent;
            border: 1px solid var(--sub-border);
            color: var(--text-muted);
            padding: 8px 14px;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
            margin-top: 8px;
            width: 100%;
        }
        .modal-close:hover { color: #fff; border-color: #fff; }

        /* Congratulations Bounce */
        .congrats-icon { font-size: 48px; margin-bottom: 10px; animation: bounce 1s infinite alternate; }
        .points-badge {
            display: inline-block;
            background: rgba(212, 175, 55, 0.15);
            border: 1px solid var(--royal-border);
            color: var(--royal-border);
            font-size: 18px;
            font-weight: 900;
            padding: 8px 18px;
            border-radius: 30px;
            margin: 15px 0;
            box-shadow: 0 0 15px rgba(212, 175, 55, 0.3);
        }

        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(-8px); }
        }

        @media(max-width: 600px) {
            .navbar { padding: 10px 15px; }
            .tools-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- 1. Terms and Conditions Acceptance Modal (Shows Once, No Login Needed) -->
    <div id="termsModal">
        <div class="terms-card">
            <div class="ktx-logo-big">KTX</div>
            <div class="terms-sub">Student Utility & Tools Portal</div>
            
            <div class="terms-box">
                <strong>📜 Terms & Conditions:</strong><br>
                1. <strong>100% Free Access:</strong> All core student tools (Background Remover, Watermark Eraser, PDF Tools, Summarizer) require NO login & NO payment.<br>
                2. <strong>Privacy Assured:</strong> All uploaded files and notes are processed instantly in your browser.<br>
                3. <strong>VIP Members:</strong> High-bandwidth VIP tools consume Welcome Bonus Coins or optional Gemini API Keys.<br>
                4. <strong>Fair Use:</strong> Please use the platform for educational & productivity purposes only.
            </div>

            <button class="btn-blue-action" onclick="acceptTermsAndEnter()">I Agree & Enter Platform (YES) 👍</button>
        </div>
    </div>

    <!-- 2. Congratulations Modal (Unlocks right after Terms Agree) -->
    <div id="congratsModal">
        <div class="modal-box">
            <div class="congrats-icon">🎉</div>
            <h2 style="color:var(--royal-border); font-size:22px;">Welcome to KTX!</h2>
            <p style="color:#fff; font-size:14px; margin-top:5px;">Instant Access Unlocked</p>
            <div class="points-badge">+100 Welcome Coins Added! 🪙</div>
            <p style="font-size:12px; color:var(--text-muted); margin-bottom: 20px;">
                आपके वॉलेट में <strong>100 कॉइन्स</strong> एक्टिव कर दिए गए हैं। इनका इस्तेमाल आप भविष्य में <strong>VIP Member Tools</strong> अनलॉक करने के लिए कर सकते हैं।
            </p>
            <button class="btn-blue-action" onclick="closeCongrats()">Explore All Tools 🚀</button>
        </div>
    </div>

    <!-- 3. Top Navigation Bar -->
    <header class="navbar">
        <div>
            <div class="brand-title">KTX</div>
            <div class="brand-sub">Student Utility Portal</div>
        </div>
        <div class="nav-actions">
            <div class="wallet-pill" onclick="toggleProfile()">🪙 <span id="walletPts">100</span> Coins</div>
            <button class="btn-profile-toggle" onclick="toggleProfile()">👤 Guest Student</button>
        </div>
    </header>

    <div class="container">

        <!-- User Profile & Wallet Details -->
        <div id="profileDrawer">
            <div class="profile-header">
                <div class="profile-info">
                    <h3>Guest Student</h3>
                    <p>Open Access Mode (No Login Required)</p>
                </div>
                <span style="font-size:11px; background:rgba(35,134,54,0.2); border:1px solid var(--badge-green); color:#3fb950; padding:4px 10px; border-radius:12px; font-weight:bold;">Active Session</span>
            </div>

            <!-- Wallet Notice -->
            <div class="wallet-banner-box">
                <h4>🪙 VIP Wallet: <span id="walletDetailPts" style="color:#fff;">100 Coins</span></h4>
                <p>
                    📌 <strong>उपयोग निर्देश:</strong> सभी <strong>Free Tools</strong> हमेशा 100% फ्री रहेंगे। यह 100 कॉइन्स केवल <strong>VIP Member Tools</strong> (जैसे 4K Image Enhancer, Deep Research Assistant) को प्रोसेस करने के लिए उपयोग किए जा सकते हैं।
                </p>
            </div>

            <div class="profile-stats">
                <div class="stat-box"><span id="pWallet">100</span><label>VIP Coins</label></div>
                <div class="stat-box"><span>10</span><label>Total Tools</label></div>
                <div class="stat-box"><span>Gold Tier</span><label>Student Level</label></div>
                <div class="stat-box"><span>Open Access</span><label>No Login Barrier</label></div>
            </div>
        </div>

        <!-- Hero Banner -->
        <div class="hero">
            <h1>All-In-One <span>KTX</span> Student Toolbox</h1>
            <p>Background Remover, Watermark Eraser, PDF Compressor & VIP AI Tools (Zero Barrier)</p>
        </div>

        <!-- Search & Filter Bar -->
        <div class="filter-row">
            <input type="text" id="toolSearch" class="search-tool" placeholder="Search any student tool (e.g. background, watermark, pdf, vip)..." oninput="filterTools()">
            <select id="catSelect" class="category-select" onchange="filterTools()">
                <option value="ALL">All Categories</option>
                <option value="FREE">Free Tools Only</option>
                <option value="VIP">VIP Tools (Use Coins/API Key)</option>
                <option value="Photo Tools">Photo & Image</option>
                <option value="Document / PDF">Document & PDF</option>
                <option value="AI Study">AI Study & Notes</option>
            </select>
        </div>

        <!-- Student Tools Grid -->
        <div class="tools-grid" id="toolsGrid"></div>

    </div>

    <!-- 4. Tool Interactive Modal Window -->
    <div id="toolModal">
        <div class="modal-box">
            <h2 id="mTitle">Tool Name</h2>
            <p id="mDesc">Tool description goes here.</p>
            
            <div id="apiKeySection" style="display:none;">
                <input type="password" id="userApiKey" class="api-input-field" placeholder="Paste Gemini API Key (Optional for VIP) / Uses Coins">
            </div>

            <div id="toolInputContainer">
                <div class="drop-zone" onclick="document.getElementById('fileInput').click()">
                    📁 Click to Upload Document / Photo or Drag & Drop Here
                    <input type="file" id="fileInput" style="display:none" onchange="handleFileSelected()">
                </div>
            </div>

            <textarea id="toolTextArea" class="interactive-area" style="display:none;" placeholder="Type or paste your notes/question here..."></textarea>
            
            <div id="actionProgress" style="display:none; color:var(--royal-border); font-size:13px; text-align:center; margin-bottom:12px;">
                ⚙️ Processing with Zero-Lag Engine...
            </div>

            <button id="modalActionBtn" class="btn-blue-action" onclick="executeToolAction()">Start Processing</button>
        
