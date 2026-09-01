
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX VIP Enterprise | Secure AI Ecosystem</title>
    <style>
        * {
            box-sizing: border-box;
        }

        :root {
            --bg-color: #0d1117;
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
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        /* Container wrappers */
        .page-wrapper {
            width: 100%;
            max-width: 1280px;
            padding: 20px;
        }

        /* --- LOGIN SCREEN STYLES --- */
        #loginScreen {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            min-height: 100vh;
        }

        .login-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 40px;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            text-align: center;
        }

        .login-card h2 {
            color: var(--text-main);
            margin-bottom: 8px;
            font-size: 24px;
        }

        .login-card p {
            color: var(--text-muted);
            font-size: 14px;
            margin-bottom: 24px;
        }

        .form-group {
            margin-bottom: 16px;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-size: 13px;
            color: var(--text-main);
            margin-bottom: 6px;
            font-weight: 600;
        }

        .form-group input {
            width: 100%;
            padding: 10px 12px;
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: var(--text-main);
            font-size: 14px;
            outline: none;
        }

        .form-group input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(88, 166, 255, 0.3);
        }

        .btn-auth {
            width: 100%;
            padding: 10px;
            background-color: var(--success);
            color: #ffffff;
            border: none;
            border-radius: 6px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
            margin-top: 10px;
        }

        .btn-auth:hover {
            background-color: #2ea043;
        }

        /* --- DASHBOARD SCREEN STYLES --- */
        #dashboardScreen {
            display: none;
            width: 100%;
        }

        .dash-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 25px;
        }

        .dash-header h1 {
            font-size: 22px;
            color: var(--text-main);
            margin: 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-badge {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 13px;
            color: var(--accent);
            font-weight: 600;
        }

        /* Global API Key Bar inside Dashboard */
        .api-bar {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            padding: 15px 20px;
            border-radius: 8px;
            margin-bottom: 25px;
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .api-bar label {
            font-size: 13px;
            font-weight: 600;
            color: var(--text-main);
            white-space: nowrap;
        }

        .api-bar input {
            flex: 1;
            padding: 8px 12px;
            background-color: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: var(--text-main);
            font-size: 13px;
            outline: none;
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
            .api-bar, .sub-banner {
                flex-direction: column;
                align-items: stretch;
                gap: 10px;
            }
        }
    </style>
</head>
<body>

    <!-- 1. LOGIN SCREEN (GitHub Style Auth Gate) -->
    <div id="loginScreen">
        <div class="login-card">
            <h2>KTX Enterprise</h2>
            <p>Sign in to your VIP AI Workspace</p>
            <div class="form-group">
                <label>Your Name / Username</label>
                <input type="text" id="loginUser" placeholder="e.g. Nitin Srivastava">
            </div>
            <button class="btn-auth" onclick="handleLogin()">Sign In to Dashboard</button>
        </div>
    </div>

    <!-- 2. MAIN DASHBOARD SCREEN (Loaded After Login) -->
    <div id="dashboardScreen" class="page-wrapper">
        
        <div class="dash-header">
            <h1>KTX Enterprise Hub</h1>
            <div class="user-badge" id="displayUser">VIP User</div>
        </div>

        <!-- Secure API Key Input Bar -->
        <div class="api-bar">
            <label>Google Gemini API Key:</label>
            <input type="password" id="globalApiKey" placeholder="Paste your API key here (Saved securely in browser)..." oninput="saveApiKey()">
        </div>

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

    <script>
        // Check if user is already logged in or has saved key on page load
        window.onload = function() {
            const savedUser = localStorage.getItem('ktx_enterprise_user');
            const savedKey = localStorage.getItem('ktx_enterprise_key');

            if (savedUser) {
                document.getElementById('displayUser').innerText = "VIP: " + savedUser;
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('dashboardScreen').style.display = 'block';
            }
            if (savedKey) {
                document.getElementById('globalApiKey').value = savedKey;
            }
        };

        function handleLogin() {
            const username = document.getElementById('loginUser').value.trim();
            if (!username) {
                alert("Please enter your name to continue!");
                return;
            }
            localStorage.setItem('ktx_enterprise_user', username);
            document.getElementById('displayUser').innerText = "VIP: " + username;
            
            // Smooth transition to dashboard
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('dashboardScreen').style.display = 'block';
        }

        function saveApiKey() {
            const key = document.getElementById('globalApiKey').value.trim();
            localStorage.setItem('ktx_enterprise_key', key);
        }

        async function askAI(type) {
            const apiKey = document.getElementById('globalApiKey').value.trim();
            if (!apiKey) {
                alert("Please enter your Google Gemini API Key in the top configuration bar!");
                return;
            }

            let query = "";
            let promptPrefix = "";
            let responseDivId = "";

            if (type === 'fit') {
                query = document.getElementById('fitQuery').value.trim();
                promptPrefix = "You are an expert elite fitness coach. Provide a precise, professional English response: ";
                responseDivId = "fitResponse";
            } else if (type === 'fin') {
                query = document.getElementById('finQuery').value.trim();
                promptPrefix = "You are a professional wealth manager and corporate finance advisor. Provide a precise, professional English response: ";
                responseDivId = "finResponse";
            } else if (type === 'web') {
                query = document.getElementById('webQuery').value.trim();
                promptPrefix = "You are a senior enterprise software architect and full-stack developer. Provide a clean technical response in English with code blocks if required: ";
                responseDivId = "webResponse";
            }

            if (!query) {
                alert("Please enter a query in the text box first!");
                return;
            }

            const responseDiv = document.getElementById(responseDivId);
            responseDiv.style.display = 'block';
            responseDiv.innerHTML = 'Processing enterprise query...';

            // Fixed and updated to the correct working 2.0 model endpoint to bypass the depreciation error
            const url = `https://generativelanguage.googleapis.com/v1/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

            try {
                const res = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: promptPrefix + query }] }]
                    })
                });

                const data = await res.json();

                if (data.error) {
                    responseDiv.innerHTML = `<strong style="color:#ff7b72;">API Error:</strong> ${data.error.message}`;
                } else if (data.candidates && data.candidates[0].content.parts[0].text) {
                    responseDiv.innerHTML = data.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                } else {
                    responseDiv.innerHTML = 'No response returned from model.';
                }
            } catch (err) {
                responseDiv.innerHTML = `<strong style="color:#ff7b72;">Network Error:</strong> ${err.message}`;
            }
        }
    </script>
