<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Fitness & AI Coach</title>
    <style>
        :root {
            --bg-color: #121212;
            --card-bg: #1e1e1e;
            --accent: #00ffcc;
            --text-color: #ffffff;
            --text-secondary: #b0b0b0;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 15px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
        }
        header {
            text-align: center;
            padding: 20px 0;
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
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`, {
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
