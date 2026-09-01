
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX VIP Hub | Fitness, Finance & Tech</title>
    <style>
        * {
            box-sizing: border-box;
        }

        :root {
            --bg-color: #0b0f19;
            --card-bg: #131b2e;
            --accent: #00ff66;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: #1e293b;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 25px;
        }

        .header {
            text-align: center;
            margin-bottom: 35px;
        }

        .header h1 {
            color: var(--accent);
            margin: 0;
            font-size: 36px;
            font-weight: 800;
            letter-spacing: 2px;
            text-transform: uppercase;
            text-shadow: 0 0 20px rgba(0, 255, 102, 0.2);
        }

        .header p {
            color: var(--text-muted);
            margin: 8px 0 0 0;
            font-size: 15px;
        }

        /* VIP Global API Box */
        .api-container {
            max-width: 1280px;
            margin: 0 auto 25px auto;
            background: var(--card-bg);
            padding: 18px 25px;
            border-radius: 16px;
            border: 1px solid var(--border);
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
        }

        .api-container label {
            font-size: 14px;
            color: var(--accent);
            font-weight: 700;
            white-space: nowrap;
        }

        .api-container input {
            flex: 1;
            padding: 12px 15px;
            background-color: #0b0f19;
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-main);
            font-size: 14px;
            outline: none;
            transition: border-color 0.3s;
        }

        .api-container input:focus {
            border-color: var(--accent);
        }

        /* 3-Column VIP Dashboard Grid */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
            max-width: 1280px;
            margin: 0 auto;
        }

        .vip-card {
            background-color: var(--card-bg);
            border-radius: 20px;
            padding: 25px;
            border: 1px solid var(--border);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.3s, border-color 0.3s;
        }

        .vip-card:hover {
            border-color: rgba(0, 255, 102, 0.4);
            transform: translateY(-3px);
        }

        .vip-card h2 {
            margin: 0 0 20px 0;
            font-size: 20px;
            color: var(--accent);
            border-bottom: 2px solid var(--border);
            padding-bottom: 12px;
            font-weight: 700;
        }

        .input-group {
            margin-bottom: 18px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 13px;
            color: var(--text-muted);
            font-weight: 600;
        }

        .input-group textarea {
            width: 100%;
            padding: 14px;
            background-color: #0b0f19;
            border: 1px solid var(--border);
            border-radius: 10px;
            color: var(--text-main);
            font-size: 14px;
            box-sizing: border-box;
            resize: vertical;
            outline: none;
            min-height: 100px;
            transition: border-color 0.3s;
        }

        .input-group textarea:focus {
            border-color: var(--accent);
        }

        .btn-vip {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, var(--accent), #00b347);
            color: #0b0f19;
            border: none;
            border-radius: 10px;
            font-size: 15px;
            font-weight: 700;
            cursor: pointer;
            transition: opacity 0.3s, transform 0.2s;
        }

        .btn-vip:hover {
            opacity: 0.9;
            transform: scale(1.01);
        }

        .output-box {
            margin-top: 18px;
            padding: 15px;
            background-color: #0b0f19;
            border-radius: 10px;
            font-size: 14px;
            line-height: 1.6;
            display: none;
            border-left: 4px solid var(--accent);
            white-space: pre-wrap;
            color: #e2e8f0;
        }

        /* Mobile Responsive */
        @media (max-width: 1024px) {
            .grid-container {
                grid-template-columns: 1fr;
            }
            .api-container {
                flex-direction: column;
                align-items: stretch;
            }
        }
    </style>
</head>
<body>

    <div class="header">
        <h1>KTX VIP Hub</h1>
        <p>Next-Gen AI Powered Fitness, Finance & Development Ecosystem</p>
    </div>

    <!-- Global Secure API Key Box -->
    <div class="api-container">
        <label>Google Gemini API Key:</label>
        <input type="password" id="globalApiKey" placeholder="Enter your free Gemini API Key here (Saved locally)" oninput="saveApiKey()">
    </div>

    <!-- 3-Column VIP Dashboard Grid -->
    <div class="grid-container">
        
        <!-- 1. LEFT: Fitness -->
        <div class="vip-card">
            <div>
                <h2>💪 Fitness & Gym Coach</h2>
                <div class="input-group">
                    <label>Ask your fitness or diet question:</label>
                    <textarea id="fitQuery" placeholder="e.g., Best workout routine to build bigger biceps?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('fit')">Get Expert Advice</button>
                <div id="fitResponse" class="output-box"></div>
            </div>
        </div>

        <!-- 2. MIDDLE: Finance -->
        <div class="vip-card">
            <div>
                <h2>💰 Finance & Budgeting</h2>
                <div class="input-group">
                    <label>Ask your money or savings question:</label>
                    <textarea id="finQuery" placeholder="e.g., How to start budgeting and saving money effectively?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('fin')">Get Financial Advice</button>
                <div id="finResponse" class="output-box"></div>
            </div>
        </div>

        <!-- 3. RIGHT: Web Development -->
        <div class="vip-card">
            <div>
                <h2>💻 Web Development</h2>
                <div class="input-group">
                    <label>Ask your coding or web dev question:</label>
                    <textarea id="webQuery" placeholder="e.g., How to create a responsive navigation bar using HTML and CSS?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('web')">Learn Coding</button>
                <div id="webResponse" class="output-box"></div>
            </div>
        </div>

    </div>

    <script>
        window.onload = function() {
            const savedKey = localStorage.getItem('ktx_vip_api_key');
            if (savedKey) {
                document.getElementById('globalApiKey').value = savedKey;
            }
        };

        function saveApiKey() {
            const key = document.getElementById('globalApiKey').value.trim();
            localStorage.setItem('ktx_vip_api_key', key);
        }

        async function askAI(type) {
            const apiKey = document.getElementById('globalApiKey').value.trim();
            if (!apiKey) {
                alert("Please enter your Google Gemini API Key in the top box first!");
                return;
            }

            let query = "";
            let promptPrefix = "";
            let responseDivId = "";

            if (type === 'fit') {
                query = document.getElementById('fitQuery').value.trim();
                promptPrefix = "You are an expert fitness and gym coach. Answer the user's question in clear and professional English: ";
                responseDivId = "fitResponse";
            } else if (type === 'fin') {
                query = document.getElementById('finQuery').value.trim();
                promptPrefix = "You are a professional finance and wealth management advisor. Answer the user's question in clear and professional English: ";
                responseDivId = "finResponse";
            } else if (type === 'web') {
                query = document.getElementById('webQuery').value.trim();
                promptPrefix = "You are a senior full-stack web developer and coding mentor. Answer the user's question in clear English with code examples if needed: ";
                responseDivId = "webResponse";
            }

            if (!query) {
                alert("Please type your question in this section first!");
                return;
            }

            const responseDiv = document.getElementById(responseDivId);
            responseDiv.style.display = 'block';
            responseDiv.innerHTML = 'AI Coach is thinking...';

            const url = `https://generativelanguage.googleapis.com/v1/models/gemini-2.5-flash:generateContent?key=${apiKey}`;

            try {
                const res = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: promptPrefix + query }] }]
                    })
                });

                const data = x = await res.json();

                if (data.error) {
                    responseDiv.innerHTML = `<strong style="color:#ff4d4d;">Error:</strong> ${data.error.message}`;
                } else if (data.candidates && data.candidates[0].content.parts[0].text) {
                    responseDiv.innerHTML = data.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                } else {
                    responseDiv.innerHTML = 'Sorry, could not retrieve a response at this moment.';
                }
            } catch (err) {
                responseDiv.innerHTML = `<strong style="color:#ff4d4d;">Connection Error:</strong> ${err.message}`;
            }
        }
    </script>
</body>
</html>
