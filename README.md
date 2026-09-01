
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Fitness | Your Personal AI Coach</title>
    <style>
        :root {
            --primary-bg: #121212;
            --card-bg: #1e1e1e;
            --accent: #00e676;
            --text-main: #ffffff;
            --text-muted: #b0b0b0;
            --border-color: #333333;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--primary-bg);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .main-container {
            width: 100%;
            max-width: 500px;
            padding: 20px;
            box-sizing: border-box;
        }

        .app-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .app-header h1 {
            color: var(--accent);
            margin: 0;
            font-size: 32px;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

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
