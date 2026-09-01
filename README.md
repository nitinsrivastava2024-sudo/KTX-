
<html lang="hi">
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
            --accent-hover: #00cc52;
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

    <div class="api-container">
        <label>Google Gemini API Key:</label>
        <input type="password" id="globalApiKey" placeholder="अपनी फ्री API Key यहाँ दर्ज करें (एक बार डालें, ब्राउज़र में सुरक्षित सेव रहेगी)" oninput="saveApiKey()">
    </div>

    <div class="grid-container">
        
        <div class="vip-card">
            <div>
                <h2>💪 जिम & फिटनेस कोच</h2>
                <div class="input-group">
                    <label>अपनी फिटनेस या डाइट का सवाल पूछें:</label>
                    <textarea id="fitQuery" placeholder="जैसे: बाइसेप्स का साइज बढ़ाने के लिए सबसे बेहतरीन वर्कआउट क्या है?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('fit')">सलाह प्राप्त करें</button>
                <div id="fitResponse" class="output-box"></div>
            </div>
        </div>

        <div class="vip-card">
            <div>
                <h2>💰 फाइनेंस & मनी मैनेजमेंट</h2>
                <div class="input-group">
                    <label>अपने पैसों या बचत से जुड़ा सवाल पूछें:</label>
                    <textarea id="finQuery" placeholder="जैसे: महीने की कमाई से स्मार्ट तरीके से बचत कैसे करें?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('fin')">सलाह प्राप्त करें</button>
                <div id="finResponse" class="output-box"></div>
            </div>
        </div>

        <div class="vip-card">
            <div>
                <h2>💻 वेब डेवलपमेंट गुरु</h2>
                <div class="input-group">
                    <label>कोडिंग या वेबसाइट बनाने का सवाल पूछें:</label>
                    <textarea id="webQuery" placeholder="जैसे: HTML और CSS का इस्तेमाल करके शानदार नेविगेशन बार कैसे बनाएं?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-vip" onclick="askAI('web')">कोडिंग सीखें</button>
                <div id="webResponse" class="output-box"></div>
            </div>
        </div>

    </div>

    <script>
        // पेज खुलते ही लोकल स्टोरेज से API Key लोड करना
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
                alert("कृपया सबसे ऊपर दिए गए बॉक्स में अपनी Google Gemini API Key दर्ज करें!");
                return;
            }

            let query = "";
            let promptPrefix = "";
            let responseDivId = "";

            if (type === 'fit') {
                query = document.getElementById('fitQuery').value.trim();
                promptPrefix = "आप एक विश्वस्तरीय विशेषज्ञ फिटनेस और जिम कोच हैं। उपयोगकर्ता के प्रश्न का उत्तर हिंदी में, बहुत ही सटीक और असरदार तरीके से दें: ";
                responseDivId = "fitResponse";
            } else if (type === 'fin') {
                query = document.getElementById('finQuery').value.trim();
                promptPrefix = "आप एक प्रोफेशनल फाइनेंस और वेल्थ मैनेजमेंट एडवाइजर हैं। उपयोगकर्ता के प्रश्न का उत्तर हिंदी में, आसान और पेशेवर भाषा में दें: ";
                responseDivId = "finResponse";
            } else if (type === 'web') {
                query = document.getElementById('webQuery').value.trim();
                promptPrefix = "आप एक सीनियर फुल-स्टैक वेब डेवलपर और कोडिंग गुरु हैं। उपयोगकर्ता के प्रश्न का उत्तर हिंदी में, उदाहरण और कोड सहित आसान तरीके से दें: ";
                responseDivId = "webResponse";
            }

            if (!query) {
                alert("कृपया पहले इस सेक्शन में अपना सवाल लिखें!");
                return;
            }

            const responseDiv = document.getElementById(responseDivId);
            responseDiv.style.display = 'block';
            responseDiv.innerHTML = 'AI कोच सोच रहे हैं...';

            const url = `https://generativelanguage.googleapis.com/v1/models/gemini-2.5-flash:generateContent?key=${apiKey}`;

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
                    responseDiv.innerHTML = `<strong style="color:#ff4d4d;">एरर:</strong> ${data.error.message}`;
                } else if (data.candidates && data.candidates[0].content.parts[0].text) {
                    responseDiv.innerHTML = data.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                } else {
                    responseDiv.innerHTML = 'क्षमा करें, अभी उत्तर प्राप्त नहीं हो सका।';
                }
            } catch (err) {
                responseDiv.innerHTML = `<strong style="color:#ff4d4d;">कनेक्शन एरर:</strong> ${err.message}`;
            }
        }
    </script>
</body>
</html>            color: var(--accent);
            margin-top: 0;
            font-size: 18px;
        }

        .review-card textarea {
            width: 100%;
            max-width: 600px;
            padding: 12px;
            background-color: #2a2a2a;
            border: 1px solid #444;
            border-radius: 6px;
            color: var(--text-main);
            margin-bottom: 10px;
            box-sizing: border-box;
        }

        .pro-badge {
            display: inline-block;
            background: linear-gradient(45deg, #00e676, #00b0ff);
            color: #000;
            padding: 8px 20px;
            font-weight: bold;
            border-radius: 20px;
            margin-top: 10px;
            font-size: 15px;
        }

        /* मोबाइल रेस्पॉन्सिव (छोटी स्क्रीन पर एक के नीचे एक) */
        @media (max-width: 900px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            .api-global-box {
                flex-direction: column;
                align-items: stretch;
            }
        }
    </style>
</head>
<body>

    <div class="app-header">
        <h1>KTX Hub</h1>
        <p>Fitness, Finance & Web Development AI Platform</p>
    </div>

    <!-- ग्लोबल API की बार (ताकि बार-बार न डालनी पड़े) -->
    <div class="api-global-box">
        <label>Google Gemini API Key:</label>
        <input type="password" id="globalApiKey" placeholder="अपनी फ्री API Key यहाँ एक बार दर्ज करें (लोकल सेव होगी)" oninput="saveGlobalKey()">
    </div>

    <!-- 3-Column Dashboard: लेफ्ट (फिटनेस), बीच (फाइनेंस), राइट (वेब डेवलपमेंट) -->
    <div class="dashboard-grid">
        
        <!-- 1. LEFT SIDE: जिम और फिटनेस -->
        <div class="card">
            <div>
                <h2>💪 जिम & फिटनेस</h2>
                <div class="input-group">
                    <label>फिटनेस सवाल पूछें:</label>
                    <textarea id="fitQuery" rows="3" placeholder="जैसे: चेस्ट मसल्स कैसे चौड़ी करें?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-primary" onclick="askAI('fit')">फिटनेस सलाह लें</button>
                <div id="fitResponse" class="response-box"></div>
            </div>
        </div>

        <!-- 2. MIDDLE: फाइनेंस ट्रैकर -->
        <div class="card">
            <div>
                <h2>💰 फाइनेंस & बजट</h2>
                <div class="input-group">
                    <label>फाइनेंस सवाल पूछें:</label>
                    <textarea id="finQuery" rows="3" placeholder="जैसे: सैलरी से महीने की बचत कैसे करें?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-primary" onclick="askAI('fin')">फाइनेंस सलाह लें</button>
                <div id="finResponse" class="response-box"></div>
            </div>
        </div>

        <!-- 3. RIGHT SIDE: वेबसाइट बनाना सीखें -->
        <div class="card">
            <div>
                <h2>💻 वेब डेवलपमेंट</h2>
                <div class="input-group">
                    <label>कोडिंग सवाल पूछें:</label>
                    <textarea id="webQuery" rows="3" placeholder="जैसे: HTML में इमेज कैसे लगाते हैं?"></textarea>
                </div>
            </div>
            <div>
                <button class="btn-primary" onclick="askAI('web')">कोडिंग सीखें</button>
                <div id="webResponse" class="response-box"></div>
            </div>
        </div>

    </div>

    <!-- नीचे एकदम बीच में: रिव्यू सेक्शन -->
    <div class="bottom-sections">
        <div class="review-card">
            <h2>⭐ अपना कीमती रिव्यू दें</h2>
            <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 15px;">हमें बताएं कि आपको यह ऐप कैसा लगा और इसमें क्या सुधार चाहिए:</p>
            <textarea id="userReview" rows="3" placeholder="यहाँ अपना फीडबैक लिखें..."></textarea>
            <br>
            <button class="btn-primary" style="max-width: 200px; margin: 0 auto;" onclick="submitReview()">रिव्यू भेजें</button>
            <div id="reviewMsg" style="color: var(--accent); margin-top: 10px; font-size: 13px; display: none;">धन्यवाद! आपका रिव्यू दर्ज कर लिया गया है।</div>
        </div>

        <!-- सबसे नीचे: प्रो सब्सक्रिप्शन -->
        <div class="pro-card">
            <h2>🚀 KTX Pro सब्सक्रिप्शन</h2>
            <p style="color: var(--text-muted); font-size: 13px; margin: 5px 0;">अल्िमिटेड एआई फीचर्स, प्रीमियम कोर्सेज और बिना किसी रुकावट के एडवांस टूल्स का आनंद लें।</p>
            <div class="pro-badge">शीघ्र आ रहा है (Coming Soon) - Free Forever for Now!</div>
        </div>
    </div>

    <script>
        // पेज लोड होते ही लोकल स्टोरेज से API Key फेच करना
        window.onload = function() {
            const savedKey = localStorage.getItem('ktx_global_api_key');
            if (savedKey) {
                document.getElementById('globalApiKey').value = savedKey;
            }
        };

        function saveGlobalKey() {
            const key = document.getElementById('globalApiKey').value.trim();
            localStorage.setItem('ktx_global_api_key', key);
        }

        async function askAI(type) {
            const apiKey = document.getElementById('globalApiKey').value.trim();
            if (!apiKey) {
                alert("कृपया सबसे ऊपर दिए गए बॉक्स में अपनी Google Gemini API Key दर्ज करें!");
                return;
            }

            let query = "";
            let promptPrefix = "";
            let responseDivId = "";

            if (type === 'fit') {
                query = document.getElementById('fitQuery').value.trim();
                promptPrefix = "आप एक विशेषज्ञ फिटनेस और जिम कोच हैं। हिंदी में सटीक और असरदार सलाह दें: ";
                responseDivId = "fitResponse";
            } else if (type === 'fin') {
                query = document.getElementById('finQuery').value.trim();
                promptPrefix = "आप एक प्रोफेशनल फाइनेंस और मनी मैनेजमेंट एडवाइजर हैं। हिंदी में आसान भाषा में सलाह दें: ";
                responseDivId = "finResponse";
            } else if (type === 'web') {
                query = document.getElementById('webQuery').value.trim();
                promptPrefix = "आप एक सीनियर वेब डेवलपर और कोडिंग गुरु हैं। हिंदी में उदाहरण सहित आसान तरीके से सिखाएं: ";
                responseDivId = "webResponse";
            }

            if (!query) {
                alert("कृपया इस सेक्शन में अपना सवाल लिखें!");
                return;
            }

            const responseDiv = document.getElementById(responseDivId);
            responseDiv.style.display = 'block';
            responseDiv.innerHTML = 'कोच सोच रहे हैं...';

            // सही और नए v1 मॉडल का यूआरएल (एरर-फ्री)
            const url = `https://generativelanguage.googleapis.com/v1/models/gemini-2.5-flash:generateContent?key=${apiKey}`;

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
                    responseDiv.innerHTML = `एरर: ${data.error.message}`;
                } else if (data.candidates && data.candidates[0].content.parts[0].text) {
                    responseDiv.innerHTML = data.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                } else {
                    responseDiv.innerHTML = 'जवाब नहीं मिल पाया।';
                }
            } catch (err) {
                responseDiv.innerHTML = `कनेक्शन एरर: ${err.message}`;
            }
        }

        function submitReview() {
            const reviewText = document.getElementById('userReview').value.trim();
            if (!reviewText) {
                alert("कृपया पहले अपना रिव्यू लिखें!");
                return;
            }
            const msg = document.getElementById('reviewMsg');
            msg.style.display = 'block';
            document.getElementById('userReview').value = '';
            setTimeout(() => {
                msg.style.display = 'none';
            }, 4000);
        }
    </script>
</body>
</html>        }

        .app-header p {
            color: var(--text-muted);
            margin: 5px 0 0 0;
            font-size: 14px;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            border: 1px solid var(--border-color);
        }

        .card h2 {
            margin: 0 0 15px 0;
            font-size: 18px;
            color: var(--text-main);
            border-left: 4px solid var(--accent);
            padding-left: 10px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 13px;
            color: var(--text-muted);
        }

        .input-group input,
        .input-group textarea {
            width: 100%;
            padding: 12px;
            background-color: #2a2a2a;
            border: 1px solid #444;
            border-radius: 8px;
            color: var(--text-main);
            font-size: 14px;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }

        .input-group input:focus,
        .input-group textarea:focus {
            outline: none;
            border-color: var(--accent);
        }

        .btn-primary {
            width: 100%;
            padding: 14px;
            background-color: var(--accent);
            color: #000000;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn-primary:hover {
            background-color: #00c853;
        }

        .btn-primary:disabled {
            background-color: #555;
            cursor: not-allowed;
        }

        #aiResponse {
            margin-top: 20px;
            padding: 15px;
            background-color: #2a2a2a;
            border-radius: 8px;
            border-left: 3px solid var(--accent);
            font-size: 14px;
            line-height: 1.6;
            display: none;
            white-space: pre-wrap;
        }

        .loader {
            text-align: center;
            display: none;
            margin-top: 15px;
            color: var(--text-muted);
            font-style: italic;
        }

        .workout-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid var(--border-color);
        }

        .workout-item:last-child {
            border-bottom: none;
        }

        .workout-title {
            font-weight: 600;
        }

        .workout-meta {
            color: var(--text-muted);
            font-size: 12px;
        }

        .btn-check {
            padding: 6px 12px;
            background-color: transparent;
            border: 1px solid var(--accent);
            color: var(--accent);
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }
        .btn-check:hover {
             background-color: var(--accent);
             color: #000;
        }
    </style>
</head>
<body>

    <div class="main-container">
        <div class="app-header">
            <h1>KTX Fitness</h1>
            <p>Your Personal AI Coach (Powered by Google Gemini)</p>
        </div>

        <div class="card">
            <h2>💪 आज की चुनौती</h2>
            <div class="workout-item">
                <div>
                    <span class="workout-title">क्वाड्स (Quads) और उठक-बैठक (Squats)</span>
                    <div class="workout-meta">3 सेट | 12-15 रेप्स</div>
                </div>
                <button class="btn-check" onclick="markDone(this)">पूरा हुआ (Done)</button>
            </div>
             <div class="workout-item">
                <div>
                    <span class="workout-title">लेग प्रेस (Leg Press)</span>
                    <div class="workout-meta">3 सेट | 10-12 रेप्स</div>
                </div>
                <button class="btn-check" onclick="markDone(this)">पूरा हुआ (Done)</button>
            </div>
        </div>

        <div class="card">
            <h2>🤖 AI फिटनेस कोच से सलाह लें</h2>
            <div class="input-group">
                <label for="apiKey">Google Gemini API Key दर्ज करें:</label>
                <input type="password" id="apiKey" placeholder="AIzaSy... (यहाँ डालें)" oninput="saveApiKey()">
            </div>

            <div class="input-group">
                <label for="userQuery">आपका फिटनेस या डाइट सवाल:</label>
                <textarea id="userQuery" rows="3" placeholder="जैसे: बाइसेप्स बनाने के लिए बेस्ट एक्सरसाइज क्या है?"></textarea>
            </div>

            <button id="askBtn" class="btn-primary" onclick="fetchGeminiResponse()">सलाह प्राप्त करें</button>
            <div id="loader" class="loader">कोच सोच रहे हैं...</div>
            <div id="aiResponse"></div>
        </div>
    </div>

    <script>
        // पेज खुलते ही चेक करो कि क्या पहले से कोई की सेव है
        window.onload = function() {
            const savedKey = localStorage.getItem('ktx_gemini_api_key');
            if (savedKey) {
                document.getElementById('apiKey').value = savedKey;
            }
        };

        // जैसे ही यूजर की लिखेगा, वो ब्राउज़र में सेव हो जाएगी
        function saveApiKey() {
            const apiKey = document.getElementById('apiKey').value.trim();
            localStorage.setItem('ktx_gemini_api_key', apiKey);
        }

        async function fetchGeminiResponse() {
            const apiKey = document.getElementById('apiKey').value.trim();
            const query = document.getElementById('userQuery').value.trim();
            const responseDiv = document.getElementById('aiResponse');
            const loader = document.getElementById('loader');
            const btn = document.getElementById('askBtn');

            if (!apiKey || !query) {
                alert("कृपया API Key और सवाल दोनों भरें!");
                return;
            }

            // UI Updates
            loader.style.display = 'block';
            responseDiv.style.display = 'none';
            responseDiv.innerHTML = '';
            btn.disabled = true;
            btn.innerText = 'प्रोसेसिंग...';

            const url = `https://generativelanguage.googleapis.com/v1/models/gemini-1.5-flash:generateContent?key=${apiKey}`;

            try {
                const response = await fetch(url, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{ text: `आप एक विशेषज्ञ फिटनेस और डाइट कोच हैं। कृपया उपयोगकर्ता के प्रश्न का उत्तर हिंदी में, सटीक और आसान भाषा में दें। उपयोगकर्ता का सवाल है: ${query}` }]
                        }]
                    }),
                });

                const data = await response.json();

                loader.style.display = 'none';
                btn.disabled = false;
                btn.innerText = 'सलाह प्राप्त करें';

                if (data.error) {
                     responseDiv.innerHTML = `<strong>त्रुटि (Error):</strong> ${data.error.message}`;
                     responseDiv.style.display = 'block';
                } else if (data.candidates && data.candidates[0].content.parts[0].text) {
                    let formattedText = data.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                    responseDiv.innerHTML = formattedText;
                    responseDiv.style.display = 'block';
                } else {
                    responseDiv.innerHTML = 'क्षमा करें, कोच अभी जवाब नहीं दे पा रहे हैं।';
                    responseDiv.style.display = 'block';
                }

            } catch (error) {
                loader.style.display = 'none';
                btn.disabled = false;
                btn.innerText = 'सलाह प्राप्त करें';
                responseDiv.innerHTML = `<strong>Connection Error:</strong> ${error.message}`;
                responseDiv.style.display = 'block';
            }
        }

        function markDone(btn) {
            btn.innerText = 'बहुत बढ़िया!';
            btn.style.backgroundColor = '#00e676';
            btn.style.color = '#000';
            btn.disabled = true;
        }
    </script>
</body>
</html>            padding: 20px 0;
        }
        header h1 {
            color: var(--accent);
            margin: 0;
            font-size: 26px;
        }
        header p {
            color: var(--text-secondary);
            font-size: 14px;
            margin: 5px 0 0 0;
        }
        .card {
            background: var(--card-bg);
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.4);
        }
        .card h3 {
            margin-top: 0;
            color: var(--accent);
            font-size: 18px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-size: 13px;
            color: var(--text-secondary);
        }
        input, textarea {
            width: 100%;
            padding: 12px;
            background: #2a2a2a;
            border: 1px solid #444;
            color: #fff;
            border-radius: 8px;
            margin-bottom: 12px;
            font-size: 14px;
            box-sizing: border-box;
        }
        input:focus, textarea:focus {
            border-color: var(--accent);
            outline: none;
        }
        button {
            background: var(--accent);
            color: #121212;
            border: none;
            padding: 12px 20px;
            font-weight: bold;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-size: 15px;
            transition: background 0.2s;
        }
        button:hover {
            background: #00b386;
        }
        #aiResponse {
            background: #252525;
            padding: 15px;
            border-radius: 8px;
            margin-top: 12px;
            border-left: 4px solid var(--accent);
            font-size: 14px;
            white-space: pre-wrap;
            display: none;
        }
        .loader {
            text-align: center;
            display: none;
            margin-top: 10px;
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>KTX Fitness</h1>
            <p>Powered by Google Gemini AI Coach</p>
        </header>

        <div class="card">
            <h3>💪 आज का वर्कआउट ट्रैकर</h3>
            <p>क्वाड्स (Quads) और उठक-बैठक (Squats) सेशन</p>
            <button onclick="alert('शाबाश नितिन भैया! वर्कआउट पूरा हुआ।')">वर्कआउट कम्प्लीटेड (Mark Done)</button>
        </div>

        <div class="card">
            <h3>🤖 AI फिटनेस कोच (Google Gemini API)</h3>
            <label for="apiKey">Gemini API Key दर्ज करें:</label>
            <input type="password" id="apiKey" placeholder="AIzaSy...">
            
            <label for="userQuery">अपनी फिटनेस या डाइट से जुड़ा सवाल पूछें:</label>
            <textarea id="userQuery" rows="3" placeholder="जैसे: क्वाड्स मसल्स स्ट्रॉन्ग करने के लिए बेस्ट एक्सरसाइज और डाइट क्या है?"></textarea>
            
            <button onclick="askGemini()">AI कोच से सलाह लें</button>
            <div id="loader" class="loader">कोच सोच रहे हैं...</div>
            <div id="aiResponse"></div>
        </div>
    </div>

    <script>
        async function askGemini() {
            const apiKey = document.getElementById('apiKey').value.trim();
            const query = document.getElementById('userQuery').value.trim();
            const responseDiv = document.getElementById('aiResponse');
            const loader = document.getElementById('loader');

            if (!apiKey) {
                alert('कृपया पहले अपनी Gemini API Key दर्ज करें!');
                return;
            }
            if (!query) {
                alert('कृपया कोई सवाल तो लिखें!');
                return;
            }

            loader.style.display = 'block';
            responseDiv.style.display = 'none';
            responseDiv.innerHTML = '';

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/gemini-2.5-flash/models/gemini-2.5-flash:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{ text: "आप एक बेहतरीन फिटनेस और डाइट कोच हैं। हिंदी में आसान और सटीक सलाह दें। सवाल है: " + query }]
                        }]
                    })
                });

                const data = await response.json();
                loader.style.display = 'none';
                responseDiv.style.display = 'block';

                if (data.candidates && data.candidates[0].content.parts[0].text) {
                    responseDiv.innerHTML = data.candidates[0].content.parts[0].text;
                } else if (data.error) {
                    responseDiv.innerHTML = 'Error: ' + data.error.message;
                } else {
                    responseDiv.innerHTML = 'कुछ गड़बड़ हो गई, कृपया दोबारा कोशिश करें।';
                }
            } catch (error) {
                loader.style.display = 'none';
                responseDiv.style.display = 'block';
                responseDiv.innerHTML = 'Connection Error: ' + error.message;
            }
        }
    </script>
</body>
</html>
