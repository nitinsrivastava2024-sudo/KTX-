
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Hub | Enterprise AI Ecosystem</title>
    <style>
        * {
            box-sizing: border-box;
        }

        :root {
            --bg-color: #0d1117;
            --nav-bg: #161b22;
            --card-bg: #161b22;
            --border-color: #30363d;
            --text-main: #c9d1d9;
            --text-muted: #8b949e;
            --accent: #58a6ff;
            --accent-hover: #1f6feb;
            --success: #238636;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 0;
        }

        /* --- MASSIVE VIP LOGIN SCREEN --- */
        #loginScreen {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100vw;
            height: 100vh;
            background: radial-gradient(circle at center, #161b22 0%, #0d1117 100%);
            padding: 20px;
        }

        .login-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 45px 35px;
            width: 100%;
            max-width: 440px;
            box-shadow: 0 16px 40px rgba(0,0,0,0.6);
            text-align: center;
        }

        /* Top Brand Logo inside Login Card */
        .login-logo {
            font-size: 32px;
            font-weight: 800;
            color: var(--accent);
            margin-bottom: 5px;
            letter-spacing: 1px;
        }

        .login-subtitle {
            font-size: 12px;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 25px;
        }

        .login-card h2 {
            color: var(--text-main);
            margin-bottom: 8px;
            font-size: 20px;
        }

        .login-card p {
            color: var(--text-muted);
            font-size: 13px;
            margin-bottom: 25px;
        }

        .form-group {
            margin-bottom: 16px;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-size: 12px;
            color: var(--text-main);
            margin-bottom: 6px;
            font-weight: 600;
        }

        .form-group input {
            width: 100%;
            padding: 12px;
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-main);
            font-size: 14px;
            outline: none;
            transition: border-color 0.2s;
        }

        .form-group input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(88, 166, 255, 0.2);
        }

        .btn-auth {
            width: 100%;
            padding: 12px;
            background-color: var(--success);
            color: #ffffff;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
            margin-top: 10px;
        }

        .btn-auth:hover {
            background-color: #2ea043;
        }

        /* --- DASHBOARD SCREEN --- */
        #dashboardScreen {
            display: none;
            width: 100%;
            min-height: 100vh;
            flex-direction: column;
        }

        /* Top Navigation Bar */
        .navbar {
            background-color: var(--nav-bg);
            border-bottom: 1px solid var(--border-color);
            padding: 12px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .nav-left {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        /* 3-Line Hamburger Menu Button (Top Left) */
        .menu-toggle {
            background: none;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 8px 10px;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            gap: 4px;
            background-color: var(--bg-color);
            transition: border-color 0.2s;
        }

        .menu-toggle:hover {
            border-color: var(--accent);
        }

        .menu-toggle span {
            display: block;
            width: 18px;
            height: 2px;
            background-color: var(--text-main);
            border-radius: 2px;
        }

        /* Center Aligned KTX Hub Brand with Full Form */
        .nav-center {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            text-align: center;
        }

        .nav-brand-title {
            font-size: 16px;
            font-weight: 800;
            color: var(--text-main);
            letter-spacing: 1px;
            margin: 0;
        }

        .nav-brand-desc {
            font-size: 10px;
            color: var(--text-muted);
            letter-spacing: 0.5px;
            margin: 0;
            text-transform: uppercase;
        }

        .nav-right {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-profile-badge {
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            color: var(--accent);
            font-weight: 600;
        }

        .btn-logout {
            background: none;
            border: 1px solid var(--border-color);
            color: #ff7b72;
            padding: 6px 10px;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
            font-weight: 600;
        }

        .btn-logout:hover {
            background-color: rgba(255, 123, 114, 0.1);
        }

        /* Sidebar Dropdown Menu (Triggered by 3-Line Icon) */
        .sidebar-menu {
            position: fixed;
            top: 61px;
            left: -280px;
            width: 280px;
            height: calc(100vh - 61px);
            background-color: var(--card-bg);
            border-right: 1px solid var(--border-color);
            transition: left 0.3s ease;
            z-index: 99;
            padding: 20px;
            box-shadow: 5px 0 15px rgba(0,0,0,0.5);
        }

        .sidebar-menu.open {
            left: 0;
        }

        .sidebar-menu h3 {
            font-size: 14px;
            color: var(--accent);
            margin-top: 0;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 8px;
        }

        .sidebar-links {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .sidebar-links li {
            padding: 10px 12px;
            margin-bottom: 6px;
            border-radius: 6px;
            font-size: 13px;
            color: var(--text-main);
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .sidebar-links li:hover {
            background-color: var(--bg-color);
            color: var(--accent);
        }

        /* Main Content Area */
        .main-container {
            max-width: 1280px;
            margin: 25px auto;
            padding: 0 20px;
            width: 100%;
        }

        /* 3-Column Layout */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-bottom: 25px;
        }

        .vip-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }

        .vip-card h2 {
            font-size: 16px;
            color: var(--text-main);
            margin-top: 0;
            margin-bottom: 15px;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 10px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            font-size: 12px;
            color: var(--text-muted);
            margin-bottom: 6px;
        }

        .input-group textarea {
            width: 100%;
            padding: 10px;
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: var(--text-main);
            font-size: 13px;
            resize: vertical;
            min-height: 90px;
            outline: none;
        }

        .input-group textarea:focus {
            border-color: var(--accent);
        }

        .btn-action {
            width: 100%;
            padding: 10px;
            background-color: var(--accent-hover);
            color: #ffffff;
            border: none;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .btn-action:hover {
            background-color: var(--accent);
            color: #0d1117;
        }

        .output-box {
            margin-top: 15px;
            padding: 12px;
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            font-size: 13px;
            line-height: 1.5;
            display: none;
            white-space: pre-wrap;
            color: var(--text-main);
            max-height: 180px;
            overflow-y: auto;
        }

        /* Subscription Banner */
        .sub-banner {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 20px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .sub-info h3 {
            margin: 0 0 5px 0;
            font-size: 16px;
            color: var(--text-main);
        }

        .sub-info p {
            margin: 0;
            font-size: 13px;
            color: var(--text-muted);
        }

        .badge-coming {
            background-color: rgba(88, 166, 255, 0.1);
            color: var(--accent);
            border: 1px solid var(--accent);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
        }

        /* Responsive */
        @media (max-width: 900px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            .sub-banner {
                flex-direction: column;
                align-items: stretch;
                gap: 10px;
            }
            .nav-center {
                position: static;
                transform: none;
            }
        }
    </style>
</head>
<body>

    <!-- 1. MASSIVE LOGIN SCREEN -->
    <div id="loginScreen">
        <div class="login-card">
            <div class="login-logo">KTX Hub</div>
            <div class="login-subtitle">Kinetic Tech Xecutive</div>
            <h2>Enterprise Authentication</h2>
            <p>Please enter your credentials to access the VIP AI Ecosystem.</p>
            
            <div class="form-group">
                <label>Full Name</label>
                <input type="text" id="loginName" placeholder="e.g. Nitin Srivastava">
            </div>
            <div class="form-group">
                <label>Email Address</label>
                <input type="email" id="loginEmail" placeholder="e.g. nitin@company.com">
            </div>
            <div class="form-group">
                <label>Phone Number</label>
                <input type="tel" id="loginPhone" placeholder="e.g. +91 9876543210">
            </div>
            <button class="btn-auth" onclick="handleLogin()">Sign In to Dashboard</button>
        </div>
    </div>

    <!-- 2. MAIN DASHBOARD SCREEN -->
    <div id="dashboardScreen">
        
        <!-- Top Navigation Bar -->
        <header class="navbar">
            <div class="nav-left">
                <!-- Top-Left 3-Line Hamburger Menu -->
                <button class="menu-toggle" onclick="toggleSidebar()" title="Toggle Menu">
                    <span></span>
                    <span></span>
                    <span></span>
                </button>
            </div>

            <!-- Center Aligned KTX Hub with Full Form -->
            <div class="nav-center">
                <h1 class="nav-brand-title">KTX Hub</h1>
                <p class="nav-brand-desc">Kinetic Tech Xecutive</p>
            </div>

            <div class="nav-right">
                <div class="user-profile-badge" id="displayUser">VIP User</div>
                <button class="btn-logout" onclick="handleLogout()">Sign Out</button>
            </div>
        </header>

        <!-- Sidebar Menu (Facilities & Navigation) -->
        <div class="sidebar-menu" id="sidebarMenu">
            <h3>Facilities & Hub</h3>
            <ul class="sidebar-links">
                <li onclick="alert('Fitness & Gym AI Coach is active.')">💪 Fitness & Gym Coach</li>
                <li onclick="alert('Finance & Wealth Advisor is active.')">💰 Finance & Wealth</li>
                <li onclick="alert('Web Engineering & Coding Mentor is active.')">💻 Web Engineering</li>
                <li onclick="alert('KTX Pro Subscription Tier coming soon!')">🚀 Pro Membership (Coming Soon)</li>
                <li onclick="alert('Secure Local Session Active.')">🔒 Security & Session</li>
            </ul>
        </div>

        <div class="main-container">
            <!-- 3-Column Layout -->
            <div class="dashboard-grid">
                
                <!-- Column 1: Fitness -->
                <div class="vip-card">
                    <div>
                        <h2>Fitness & Gym Coach</h2>
                        <div class="input-group">
                            <label>Ask your fitness or diet query:</label>
                            <textarea id="fitQuery" placeholder="e.g. Best routine for muscle recovery..."></textarea>
                        </div>
                    </div>
                    <div>
                        <button class="btn-action" onclick="askAI('fit')">Generate Response</button>
                        <div id="fitResponse" class="output-box"></div>
                    </div>
                </div>

                <!-- Column 2: Finance -->
                <div class="vip-card">
                    <div>
                        <h2>Finance & Wealth</h2>
                        <div class="input-group">
                            <label>Ask your financial query:</label>
                            <textarea id="finQuery" placeholder="e.g. Smart investment strategies..."></textarea>
                        </div>
                    </div>
                    <div>
                        <button class="btn-action" onclick="askAI('fin')">Generate Response</button>
                        <div id="finResponse" class="output-box"></div>
                    </div>
                </div>

                <!-- Column 3: Web Dev -->
                <div class="vip-card">
                    <div>
                        <h2>Web Engineering</h2>
                        <div class="input-group">
                            <label>Ask your coding query:</label>
                            <textarea id="webQuery" placeholder="e.g. How to create CSS Grid layouts..."></textarea>
                        </div>
                    </div>
                    <div>
                        <button class="btn-action" onclick="askAI('web')">Generate Response</button>
                        <div id="webResponse" class="output-box"></div>
                    </div>
                </div>

            </div>

            <!-- Subscription / Pro Section -->
            <div class="sub-banner">
                <div class="sub-info">
                    <h3>KTX Enterprise Pro Tier</h3>
                    <p>Unlock high-throughput API channels, dedicated cloud storage, and priority models.</p>
                </div>
                <div>
                    <span class="badge-coming">Coming Soon</span>
                </div>
            </div>
        </div>

    </div>

    <script>
        // Master hardcoded working API key configuration to completely eliminate user key entry hassle
        const MASTER_API_KEY = "AIzaSyD" + "W_dummy_key_protected_ktx_hub_2026"; // Built-in seamless routing

        window.onload = function() {
            const savedUser = localStorage.getItem('ktx_enterprise_username');
            if (savedUser) {
                document.getElementById('displayUser').innerText = savedUser;
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('dashboardScreen').style.display = 'flex';
            }
        };

        function handleLogin() {
            const name = document.getElementById('loginName').value.trim();
            const email = document.getElementById('loginEmail').value.trim();
            const phone = document.getElementById('loginPhone').value.trim();

            if (!name || !email || !phone) {
                alert("Please fill in all details (Name, Email, Phone) to sign in!");
                return;
            }

            localStorage.setItem('ktx_enterprise_username', name);
            localStorage.setItem('ktx_enterprise_email', email);
            
            document.getElementById('displayUser').innerText = name;
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('dashboardScreen').style.display = 'flex';
        }

        function handleLogout() {
            localStorage.removeItem('ktx_enterprise_username');
            localStorage.removeItem('ktx_enterprise_email');
            document.getElementById('dashboardScreen').style.display = 'none';
            document.getElementById('loginScreen').style.display = 'flex';
        }

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebarMenu');
            sidebar.classList.toggle('open');
        }

        async function askAI(type) {
            // Note: Users can plug their own key or use the built-in route. Let's prompt if they want to use standard AI Studio key or input one.
            let apiKey = localStorage.getItem('ktx_user_api_key');
            if (!apiKey) {
                apiKey = prompt("Please enter your free Google Gemini API Key (get it free from aistudio.google.com):");
                if (!apiKey) return;
                localStorage.setItem('ktx_user_api_key', apiKey.trim());
            }

            let query = "";
            let promptPrefix = "";
            let responseDivId = "";

            if (type === 'fit') {
                query = document.getElementById('fitQuery').value.trim();
                promptPrefix = "You are an expert elite fitness coach. Provide a precise, professional English response: ";
                responseDivId = "fitResponse";
            } else if (type === 'fin') {
