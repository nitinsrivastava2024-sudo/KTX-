
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Student Hub - Production Enterprise</title>
    <!-- pdf-lib for in-browser real PDF operations (Zero Backend Lag) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, sans-serif; }
        
        :root {
            --bg: #0a0a0c;
            --card-bg: #121318;
            --card-hover: #191b22;
            --royal-gold: #d4af37;
            --royal-gold-glow: rgba(212, 175, 55, 0.25);
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
            padding-bottom: 70px;
            overflow-x: hidden;
        }

        /* Top Navbar */
        .navbar {
            background: var(--card-bg);
            border-bottom: 2px solid var(--royal-gold);
            padding: 14px 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 500;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.7);
        }
        .brand-box { display: flex; align-items: center; gap: 12px; }
        .brand-title {
            font-size: 24px;
            font-weight: 900;
            color: var(--ktx-red);
            letter-spacing: 1px;
            text-shadow: 0 0 10px rgba(255, 51, 51, 0.4);
        }
        .brand-sub {
            font-size: 10px;
            color: var(--royal-gold);
            text-transform: uppercase;
            letter-spacing: 0.8px;
            font-weight: 600;
        }
        .nav-actions { display: flex; gap: 12px; align-items: center; }
        .wallet-pill {
            background: #000;
            border: 1.5px solid var(--royal-gold);
            padding: 7px 16px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: bold;
            color: var(--royal-gold);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 6px;
            box-shadow: 0 0 10px var(--royal-gold-glow);
            transition: all 0.2s ease;
        }
        .wallet-pill:hover { background: var(--card-bg); border-color: #fff; color: #fff; }
        .btn-profile-toggle {
            background: transparent;
            border: 1.5px solid var(--royal-gold);
            color: var(--royal-gold);
            padding: 7px 15px;
            border-radius: 6px;
            font-size: 13px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s ease;
        }
        .btn-profile-toggle:hover { background: var(--royal-gold); color: #000; }

        /* Main Wrapper */
        .container {
            max-width: 1260px;
            margin: 20px auto;
            padding: 0 20px;
        }

        /* Direct Welcome Banner (Open Door) */
        .welcome-badge-box {
            background: linear-gradient(135deg, rgba(212, 175, 55, 0.12) 0%, rgba(18, 19, 24, 0.95) 100%);
            border: 1.5px solid var(--royal-gold);
            border-radius: 12px;
            padding: 18px 22px;
            margin-bottom: 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }
        .wb-left h2 { font-size: 19px; color: var(--royal-gold); margin-bottom: 4px; font-weight: 800; }
        .wb-left p { font-size: 13px; color: var(--text-main); }
        .wb-pts {
            background: #000;
            border: 1.5px solid var(--royal-gold);
            color: var(--royal-gold);
            padding: 8px 18px;
            border-radius: 8px;
            font-weight: 900;
            font-size: 15px;
            box-shadow: 0 0 10px var(--royal-gold-glow);
        }

        /* Profile & Details Drawer */
        #profileDrawer {
            display: none;
            background: var(--card-bg);
            border: 2px solid var(--royal-gold);
            border-radius: 12px;
            padding: 22px;
            margin-bottom: 25px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.8);
        }
        .profile-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--sub-border);
            padding-bottom: 14px;
            margin-bottom: 15px;
        }
        .profile-header h3 { color: #fff; font-size: 17px; }
        .profile-header p { color: var(--royal-gold); font-size: 12px; }
        .wallet-banner-box {
            background: #000;
            border: 1px solid var(--royal-gold);
            border-radius: 8px;
            padding: 14px;
            margin: 14px 0;
            text-align: left;
        }
        .wallet-banner-box h4 { color: var(--royal-gold); font-size: 14px; margin-bottom: 5px; }
        .wallet-banner-box p { color: var(--text-muted); font-size: 12px; line-height: 1.5; }
        .profile-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 12px;
            margin-top: 15px;
        }
        .stat-box {
            background: #000;
            border: 1px solid var(--sub-border);
            border-radius: 6px;
            padding: 12px;
            text-align: center;
        }
        .stat-box span { font-size: 18px; font-weight: bold; color: var(--text-main); display: block; }
        .stat-box label { font-size: 10px; color: var(--text-muted); text-transform: uppercase; margin-top: 3px; display: block; }

        /* Hero */
        .hero {
            background: radial-gradient(circle at top, #1a1b24 0%, var(--card-bg) 100%);
            border: 1.5px solid var(--royal-gold);
            border-radius: 12px;
            padding: 26px;
            text-align: center;
            margin-bottom: 24px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.6);
        }
        .hero h1 { font-size: 26px; color: #fff; margin-bottom: 6px; font-weight: 900; }
        .hero h1 span { color: var(--ktx-red); }
        .hero p { font-size: 13px; color: var(--text-muted); }

        /* Search & Filters */
        .filter-row {
            display: flex;
            gap: 12px;
            margin-bottom: 22px;
            flex-wrap: wrap;
        }
        .search-tool {
            flex: 1;
            min-width: 230px;
            padding: 12px 16px;
            background: var(--card-bg);
            border: 1.5px solid var(--royal-gold);
            border-radius: 8px;
            color: #fff;
            font-size: 13px;
            outline: none;
        }
        .search-tool:focus { box-shadow: 0 0 10px var(--royal-gold-glow); }
        .category-select {
            padding: 12px 16px;
            background: var(--card-bg);
            border: 1.5px solid var(--royal-gold);
            border-radius: 8px;
            color: #fff;
            font-size: 13px;
            outline: none;
            cursor: pointer;
        }

        /* Real Interactive Studio View (No popups that fail, embedded direct panel) */
        #interactiveStudio {
            display: none;
            background: var(--card-bg);
            border: 2px solid var(--royal-gold);
            border-radius: 14px;
            padding: 24px;
            margin-bottom: 30px;
            box-shadow: 0 0 30px var(--royal-gold-glow);
            animation: fadeIn 0.25s ease-in-out;
        }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(-8px); } to { opacity: 1; transform: translateY(0); } }

        .studio-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--sub-border);
            padding-bottom: 12px;
            margin-bottom: 18px;
        }
        .studio-top h2 { font-size: 20px; color: #fff; }
        .studio-close-btn {
            background: transparent;
            border: 1px solid #ff3333;
            color: #ff3333;
            padding: 6px 14px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            font-size: 12px;
        }
        .studio-close-btn:hover { background: #ff3333; color: #fff; }

        .studio-body { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        @media(max-width: 850px) { .studio-body { grid-template-columns: 1fr; } }

        .studio-panel {
            background: #000;
            border: 1px solid var(--sub-border);
            border-radius: 10px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .studio-panel h4 { color: var(--royal-gold); font-size: 14px; text-transform: uppercase; letter-spacing: 0.5px; }
        
        .custom-file-drop {
            border: 2px dashed var(--royal-gold);
            border-radius: 8px;
            padding: 30px 15px;
            text-align: center;
            color: var(--text-muted);
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .custom-file-drop:hover { background: rgba(212, 175, 55, 0.05); color: #fff; }

        .studio-textarea {
            width: 100%;
            height: 180px;
            background: #0a0a0c;
            border: 1px solid var(--royal-gold);
            border-radius: 8px;
            color: #fff;
            padding: 12px;
            font-size: 13px;
            outline: none;
            resize: vertical;
        }
        .studio-result-box {
            width: 100%;
            height: 180px;
            background: #0a0a0c;
            border: 1px solid var(--sub-border);
            border-radius: 8px;
            color: #3fb950;
            padding: 12px;
            font-size: 13px;
            overflow-y: auto;
            white-space: pre-wrap;
            font-family: monospace;
        }

        .btn-action-trigger {
            padding: 12px;
            background: var(--btn-blue);
            color: #fff;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .btn-action-trigger:hover { background: var(--btn-blue-hover); }
        .btn-action-vip {
            background: linear-gradient(135deg, #d4af37, #aa820a);
            color: #000;
        }
        .btn-action-vip:hover { background: #ffd700; box-shadow: 0 0 14px var(--royal-gold-glow); }

        /* Tools Grid */
        .tools-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(290px, 1fr));
            gap: 20px;
        }
        .tool-card {
            background: var(--card-bg);
            border: 1.5px solid var(--royal-gold);
            border-radius: 12px;
            padding: 22px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.2s ease;
        }
        .tool-card:hover {
            transform: translateY(-4px);
            background: var(--card-hover);
            box-shadow: 0 8px 25px rgba(212, 175, 55, 0.2);
        }
        .tool-badges { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
        .tool-tag {
            font-size: 10px;
            text-transform: uppercase;
            color: var(--royal-gold);
            background: rgba(212, 175, 55, 0.12);
            border: 1px solid var(--royal-gold);
            padding: 3px 8px;
            border-radius: 4px;
            font-weight: 700;
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
        .tool-card h3 { font-size: 17px; color: #fff; margin-bottom: 8px; font-weight: 700; }
        .tool-card p {
            font-size: 12px;
            color: var(--text-muted);
            line-height: 1.55;
            margin-bottom: 20px;
            flex-grow: 1;
        }
        .card-btn {
            width: 100%;
            padding: 11px;
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
        .btn-vip-use:hover { background: #ffd700; box-shadow: 0 0 12px var(--royal-gold-glow); }

        /* Canvas element for client-side image processing */
        #hiddenCanvas { display: none; }
    </style>
</head>
<body>

    <!-- Top Navigation -->
    <header class="navbar">
        <div class="brand-box">
            <div class="brand-title">KTX</div>
            <div class="brand-sub">Student Utility Portal</div>
        </div>
        <div class="nav-actions">
            <div class="wallet-pill" onclick="toggleProfile()">🪙 <span id="walletPts">100</span> Coins</div>
            <button class="btn-profile-toggle" type="button" onclick="toggleProfile()">👤 My Account</button>
        </div>
    </header>

    <div class="container">

        <!-- Open Door Welcome Banner (No popups, 100% Guaranteed zero freeze) -->
        <div class="welcome-badge-box">
            <div class="wb-left">
                <h2>🎉 Instant Access Active (No Barriers)</h2>
                <p>सभी टूल्स सीधे आपके ब्राउज़र में अल्ट्रा-फास्ट काम करते हैं। 100 बोनस कॉइन्स एक्टिव हैं।</p>
            </div>
            <div class="wb-pts">🪙 100 Coins Loaded</div>
        </div>

        <!-- User Profile & Wallet Details -->
        <div id="profileDrawer">
            <div class="profile-header">
                <div>
                    <h3>Verified Student Member</h3>
                    <p>Browser Session Protected (No Login Required)</p>
                </div>
                <span style="font-size:11px; background:rgba(35,134,54,0.2); border:1px solid var(--badge-green); color:#3fb950; padding:5px 12px; border-radius:14px; font-weight:bold;">Active & Ready</span>
            </div>

            <div class="wallet-banner-box">
                <h4>🪙 VIP Wallet Balance: <span id="walletDetailPts" style="color:#fff;">100 Coins</span></h4>
                <p>
                    📌 <strong>नियम:</strong> बेसिक टूल्स हमेशा 100% फ्री रहेंगे। एडवांस्ड VIP टूल्स के लिए कॉइन्स का उपयोग कर सकते हैं।
                </p>
            </div>

            <div class="profile-stats">
                <div class="stat-box"><span id="pWallet">100</span><label>VIP Coins</label></div>
                <div class="stat-box"><span id="toolsCount">10</span><label>Total Tools</label></div>
                <div class="stat-box"><span>Fast WebAssembly</span><label>Engine</label></div>
                <div class="stat-box"><span>0ms</span><label>Server Latency</label></div>
            </div>
        </div>

        <!-- Hero -->
        <div class="hero">
            <h1>All-In-One <span>KTX</span> Student Utility Hub</h1>
            <p>Background Remover, Watermark Eraser, PDF Compressor & AI Assistants (Zero-Lag Engine)</p>
        </div>

        <!-- Direct Embedded Interactive Studio (Replaces Glitchy Popups) -->
        <div id="interactiveStudio">
            <div class="studio-top">
                <div>
                    <h2 id="stTitle">Tool Name</h2>
                    <p id="stDesc" style="font-size:12px; color:var(--text-muted); margin-top:4px;">Tool description</p>
                </div>
                <button class="studio-close-btn" onclick="closeStudio()">✖ Close Tool</button>
            </div>

            <div class="studio-body">
                <!-- Left Input Panel -->
                <div class="studio-panel">
                    <h4>1. Input Source</h4>
                    
                    <div id="stFileArea" class="custom-file-drop" onclick="document.getElementById('actualFileInput').click()">
                        <span id="stFileLabel">📁 Click to Select File (Image / PDF)</span>
                        <input type="file" id="actualFileInput" style="display:none" onchange="onFilePicked(event)">
                    </div>

                    <div id="stTextArea" style="display:none;">
                        <textarea id="actualTextInput" class="studio-textarea" placeholder="Type or paste your text / math equation / notes here..."></textarea>
                    </div>

                    <div id="stVipKeyArea" style="display:none;">
                        <input type="password" id="userGeminiKey" class="search-tool" style="width:100%; font-size:12px;" placeholder="Optional: Enter Gemini API Key (Bypasses Coin Deduction)">
                    </div>

                    <button id="stActionBtn" class="btn-action-trigger" onclick="runToolProcessing()">Execute Tool (Instant)</button>
                </div>

                <!-- Right Output Panel -->
                <div class="studio-panel">
                    <h4>2. Live Output / Download</h4>
                    <div id="stResultBox" class="studio-result-box">Ready for processing...</div>
                    <button id="stDownloadBtn" class="btn-action-trigger" style="display:none; background:var(--badge-green);" onclick="triggerDownload()">⬇ Download Result File</button>
                </div>
            </div>
        </div>

        <!-- Filter Row -->
        <div class="filter-row">
            <input type="text" id="toolSearch" class="search-tool" placeholder="Search any student tool (e.g. background, watermark, pdf, math)..." oninput="filterTools()">
            <select id="catSelect" class="category-select" onchange="filterTools()">
                <option value="ALL">All Categories</option>
                <option value="FREE">Free Tools Only</option>
                <option value="VIP">VIP Tools (Use Coins/Key)</option>
                <option value="Photo Tools">Photo & Image</option>
                <option value="Document / PDF">Document & PDF</option>
                <option value="AI Study">AI Study & Notes</option>
            </select>
        </div>

        <!-- Tools Grid -->
        <div class="tools-grid" id="toolsGrid"></div>

    </div>

    <!-- Hidden canvas for true background & watermark graphic operations -->
    <canvas id="hiddenCanvas"></canvas>

    <script>
        // Master Catalog of High-Performance Tools
        var MASTER_TOOLS = [
            { id: 1, title: "Photo Background Remover", cat: "Photo Tools", isVip: false, cost: 0, tag: "Free AI", inputType: "image", desc: "Passport size फोटो या किसी भी इमेज का बैकग्राउंड पारदर्शी (Transparent PNG) करें।" },
            { id: 2, title: "Watermark & Stamp Eraser", cat: "Photo Tools", isVip: false, cost: 0, tag: "Free Fix", inputType: "image", desc: "Notes, PDFs या तस्वीरों से अनचाहा वाटरमार्क और टेक्स्ट साफ करें।" },
            { id: 3, title: "Ultra HD Image Enhancer & 4K Fix", cat: "Photo Tools", isVip: true, cost: 20,
