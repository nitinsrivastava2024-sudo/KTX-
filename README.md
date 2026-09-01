
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Student Hub</title>
    <!-- In-browser PDF engine for zero-lag operations -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        
        :root {
            --bg: #0a0a0c;
            --card-bg: #121318;
            --card-hover: #181a22;
            --royal-gold: #d4af37;
            --royal-gold-glow: rgba(212, 175, 55, 0.25);
            --sub-border: #232530;
            --text-main: #f0f3f6;
            --text-muted: #8b949e;
            --btn-blue: #1f6feb;
            --btn-blue-hover: #388bfd;
            --ktx-red: #ff3333;
            --badge-green: #238636;
        }

        body {
            background-color: var(--bg);
            color: var(--text-main);
            min-height: 100vh;
            padding-bottom: 80px;
            scroll-behavior: smooth;
        }

        /* 1. Header */
        .navbar {
            background: var(--card-bg);
            border-bottom: 2px solid var(--royal-gold);
            padding: 16px 20px;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 500;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.8);
        }
        .brand-title {
            font-size: 28px;
            font-weight: 900;
            color: var(--ktx-red);
            letter-spacing: 1.5px;
            text-shadow: 0 0 12px rgba(255, 51, 51, 0.4);
        }
        .brand-sub {
            font-size: 11px;
            color: var(--royal-gold);
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
            margin-top: 2px;
        }

        /* Navigation Quick Jump */
        .quick-nav {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 10px;
            flex-wrap: wrap;
        }
        .nav-btn {
            background: #000;
            border: 1px solid var(--royal-gold);
            color: var(--royal-gold);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 11px;
            text-decoration: none;
            font-weight: bold;
            transition: all 0.2s;
        }
        .nav-btn:hover {
            background: var(--royal-gold);
            color: #000;
        }

        .container {
            max-width: 1200px;
            margin: 25px auto;
            padding: 0 16px;
        }

        /* Section Titles */
        .section-header {
            border-left: 4px solid var(--royal-gold);
            padding-left: 12px;
            margin: 40px 0 20px 0;
        }
        .section-header h2 {
            font-size: 22px;
            color: #fff;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .section-header p {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 3px;
        }

        /* 2. Interactive Tool Workspace (Direct on Page) */
        #toolWorkspace {
            display: none;
            background: var(--card-bg);
            border: 2px solid var(--royal-gold);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 30px;
            box-shadow: 0 0 25px var(--royal-gold-glow);
        }
        .workspace-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--sub-border);
            padding-bottom: 10px;
            margin-bottom: 15px;
        }
        .workspace-top h3 { color: #fff; font-size: 18px; }
        .btn-close-ws {
            background: transparent;
            border: 1px solid var(--ktx-red);
            color: var(--ktx-red);
            padding: 5px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            font-weight: bold;
        }
        .btn-close-ws:hover { background: var(--ktx-red); color: #fff; }
        
        .ws-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
        }
        @media(max-width: 768px) { .ws-grid { grid-template-columns: 1fr; } }

        .ws-panel {
            background: #000;
            border: 1px solid var(--sub-border);
            border-radius: 8px;
            padding: 14px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .ws-panel label {
            color: var(--royal-gold);
            font-size: 12px;
            font-weight: bold;
            text-transform: uppercase;
        }
        .file-upload-zone {
            border: 2px dashed var(--royal-gold);
            border-radius: 6px;
            padding: 25px 10px;
            text-align: center;
            color: var(--text-muted);
            cursor: pointer;
            font-size: 13px;
        }
        .file-upload-zone:hover { background: rgba(212, 175, 55, 0.05); color: #fff; }
        .ws-textarea {
            width: 100%;
            height: 140px;
            background: #0a0a0c;
            border: 1px solid var(--royal-gold);
            border-radius: 6px;
            color: #fff;
            padding: 10px;
            font-size: 13px;
            outline: none;
            resize: vertical;
        }
        .ws-output {
            width: 100%;
            height: 140px;
            background: #0a0a0c;
            border: 1px solid var(--sub-border);
            border-radius: 6px;
            color: #3fb950;
            padding: 10px;
            font-size: 13px;
            overflow-y: auto;
            white-space: pre-wrap;
            font-family: monospace;
        }
        .btn-blue {
            padding: 11px;
            background: var(--btn-blue);
            color: #fff;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            font-size: 13px;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-blue:hover { background: var(--btn-blue-hover); }

        /* 3. Cards Grid */
        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
            gap: 18px;
        }
        .card {
            background: var(--card-bg);
            border: 1.5px solid var(--royal-gold);
            border-radius: 10px;
            padding: 18px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .card:hover {
            transform: translateY(-4px);
            background: var(--card-hover);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.2);
        }
        .card-tag {
            font-size: 10px;
            text-transform: uppercase;
            color: var(--royal-gold);
            background: rgba(212, 175, 55, 0.1);
            border: 1px solid var(--royal-gold);
            padding: 3px 8px;
            border-radius: 4px;
            font-weight: bold;
            width: fit-content;
            margin-bottom: 10px;
        }
        .card h3 { font-size: 16px; color: #fff; margin-bottom: 6px; }
        .card p { font-size: 12px; color: var(--text-muted); line-height: 1.5; margin-bottom: 16px; flex-grow: 1; }
        
        /* Information Detail List inside Fitness/Finance */
        .info-list {
            list-style: none;
            margin-bottom: 12px;
        }
        .info-list li {
            font-size: 12px;
            color: #c9d1d9;
            margin-bottom: 6px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .info-list li::before {
            content: "•";
            color: var(--royal-gold);
            font-weight: bold;
            font-size: 16px;
        }

        #hiddenCanvas { display: none; }
    </style>
</head>
<body>

    <!-- Header -->
    <header class="navbar">
        <div class="brand-title">KTX STUDENT HUB</div>
        <div class="brand-sub">All-in-One Utility, Fitness & Finance Portal</div>
        <div class="quick-nav">
            <a href="#toolsSection" class="nav-btn">🛠 Student Tools</a>
            <a href="#fitnessSection" class="nav-btn">🏋️ Gym & Fitness</a>
            <a href="#financeSection" class="nav-btn">💰 Student Finance</a>
        </div>
    </header>

    <div class="container">

        <!-- Active Tool Interactive Box -->
        <div id="toolWorkspace">
            <div class="workspace-top">
                <div>
                    <h3 id="wsTitle">Tool Name</h3>
                    <p id="wsDesc" style="font-size:12px; color:var(--text-muted);">Description</p>
                </div>
                <button class="btn-close-ws" onclick="closeWorkspace()">✖ Close Tool</button>
            </div>
            <div class="ws-grid">
                <div class="ws-panel">
                    <label>Input</label>
                    <div id="fileArea" class="file-upload-zone" onclick="document.getElementById('actualFileInput').click()">
                        <span id="fileLabel">📁 Click to Select File (Image / PDF)</span>
                        <input type="file" id="actualFileInput" style="display:none" onchange="handleFile(event)">
                    </div>
                    <div id="textArea" style="display:none;">
                        <textarea id="actualTextInput" class="ws-textarea" placeholder="Type or paste text/notes/formula here..."></textarea>
                    </div>
                    <button class="btn-blue" onclick="processTool()">Run Tool (Instant)</button>
                </div>
                <div class="ws-panel">
                    <label>Result / Output</label>
                    <div id="wsOutput" class="ws-output">Result will appear here...</div>
                    <button id="downloadBtn" class="btn-blue" style="display:none; background:var(--badge-green);" onclick="triggerDownload()">⬇ Download Result</button>
                </div>
            </div>
        </div>

        <!-- ================= SECTION 1: STUDENT UTILITY TOOLS ================= -->
        <section id="toolsSection">
            <div class="section-header">
                <h2>🛠️ Student Utility Tools</h2>
                <p>सभी जरूरी टूल्स एक जगह—100% फ्री और बिना किसी रुकावट के</p>
            </div>
            <div class="cards-grid" id="toolsGrid"></div>
        </section>

        <!-- ================= SECTION 2: FITNESS & GYM EXERCISE ================= -->
        <section id="fitnessSection">
            <div class="section-header">
                <h2>🏋️‍♂️ Gym & Fitness Workout Hub</h2>
                <p>छात्रों के लिए सही एक्सरसाइज, स्ट्रेंथ और डेली वर्कआउट गाइड</p>
            </div>
            <div class="cards-grid">
                
                <div class="card">
                    <div>
                        <span class="card-tag">Legs & Quads</span>
                        <h3>Leg Day & Squats Routine</h3>
                        <p>पैरों की ताकत और स्टेमिना बढ़ाने के लिए सबसे असरदार एक्सरसाइज रूटीन।</p>
                        <ul class="info-list">
                            <li>Bodyweight / Barbell Squats (3 x 15)</li>
                            <li>Quad Lunges & Wall Sit (3 Sets)</li>
                            <li>Calf Raises (4 x 20 Reps)</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFitnessDetail('Legs Workout', '• Squats: 4 Sets x 12-15 Reps (पीठ सीधी रखें)\n• Lunges: 3 Sets x 12 Reps प्रत्येक पैर\n• Quad Extensions: 3 Sets x 15 Reps\n• Calf Raises: 4 Sets x 20 Reps\n\nटिप: वर्कआउट से पहले 5 मिनट वॉर्म-अप जरूर करें।')">View Full Guide</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Chest & Triceps</span>
                        <h3>Chest & Upper Body Push</h3>
                        <p>मजबूत सीना और आर्म्स बनाने के लिए पुश वर्कआउट और सही फॉर्म।</p>
                        <ul class="info-list">
                            <li>Standard Pushups (3 x 15-20)</li>
                            <li>Dumbbell / Flat Bench Press (3 x 10)</li>
                            <li>Tricep Dips & Overhead Extension</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFitnessDetail('Chest & Push Day', '• Push-ups: 3 Sets x 15 Reps\n• Bench Press / Dumbbell Press: 3 Sets x 10-12 Reps\n• Incline Dumbbell Press: 3 Sets x 12 Reps\n• Tricep Dips: 3 Sets x 12 Reps\n\nटिप: वजन उठाते समय सांस छोड़ें और धीरे-धीरे नीचे लाएं।')">View Full Guide</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Back & Biceps</span>
                        <h3>Back Pull & Arm Strength</h3>
                        <p>पोस्चर सुधारने और बाइसेप्स साइज बढ़ाने के लिए पुल रूटीन।</p>
                        <ul class="info-list">
                            <li>Pull-ups / Lat Pulldown (3 x 10)</li>
                            <li>Dumbbell / Barbell Rows (3 x 12)</li>
                            <li>Bicep Curls & Hammer Curls</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFitnessDetail('Back & Biceps', '• Pull-ups / Lat Pulldowns: 3 Sets x 8-10 Reps\n• Bent-over Rows: 3 Sets x 12 Reps\n• Bicep Barbell Curls: 3 Sets x 12 Reps\n• Hammer Curls: 3 Sets x 15 Reps\n\nटिप: पढ़ाई के दौरान झुककर बैठने से खराब हुए पोस्चर को बैक वर्कआउट तुरंत ठीक करता है।')">View Full Guide</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Home & Quick</span>
                        <h3>Daily 15-Min Quick Home Routine</h3>
                        <p>बिना किसी जिम उपकरण के कमरे में रहकर फिट और एनर्जेटिक रहने का प्लान।</p>
                        <ul class="info-list">
                            <li>Jumping Jacks & High Knees</li>
                            <li>Pushups & Squats Circuit</li>
                            <li>Plank (1 Minute x 3 Sets)</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFitnessDetail('Home Routine', '• 1 Min Jumping Jacks (Warmup)\n• 20 Pushups\n• 25 Squats\n• 15 Burpees\n• 1 Min Plank\n(इस पूरे सर्किट को 3 बार दोहराएं)\n\nटिप: यह पढ़ाई के बीच सुस्ती भगाने के लिए सबसे बेहतरीन है।')">View Full Guide</button>
                </div>

            </div>
        </section>

        <!-- ================= SECTION 3: STUDENT FINANCE & MONEY ================= -->
        <section id="financeSection">
            <div class="section-header">
                <h2>💰 Student Finance & Smart Money</h2>
                <p>पॉकेट मनी मैनेजमेंट, बजटिंग रूल्स और छात्रों के लिए कमाई के आसान तरीके</p>
            </div>
            <div class="cards-grid">
                
                <div class="card">
                    <div>
                        <span class="card-tag">Budgeting</span>
                        <h3>50-30-20 Pocket Money Rule</h3>
                        <p>अपनी पॉकेट मनी या छोटी कमाई को सही तरीके से बांटने का सबसे आसान गणित।</p>
                        <ul class="info-list">
                            <li>50% जरूरतें (किताबें, रिचार्ज, सफर)</li>
                            <li>30% शौक (कैफे, घूमना, गेम्स)</li>
                            <li>20% सीधी बचत (Emergency Fund)</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFinanceDetail('50-30-20 Rule', 'यदि आपकी पॉकेट मनी ₹2,000 है:\n• ₹1,000 (50%) = ज़रूरी खर्चे (फॉर्म फीस, स्टेशनरी, रिचार्ज)\n• ₹600 (30%) = पर्सनल खर्चे और दोस्तों के साथ आउटिंग\n• ₹400 (20%) = बचत (इसको कभी खर्च न करें)\n\nयह नियम कॉलेज लाइफ से ही आपको फाइनेंशियली स्मार्ट बनाता है।')">Read Details</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Earning</span>
                        <h3>Student Freelance & Side Income</h3>
                        <p>पढ़ाई के साथ-साथ डिजिटल स्किल्स से घर बैठे पैसे कमाने के विकल्प।</p>
                        <ul class="info-list">
                            <li>Thumbnail & Graphic Designing</li>
                            <li>Notes Making & Typing Work</li>
                            <li>Video Editing & AI Prompting</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFinanceDetail('Side Income Ideas', '1. Canva / Thumbnail Design: यूट्यूबर्स को ईमेल करके ₹200-₹500 प्रति थंबनेल कमाएं।\n2. नोट्स टाइपिंग: कोचिंग या ऑनलाइन टीचर्स के लिए नोट्स डिजिटाइज़ करें।\n3. वीडियो एडिटिंग: इंस्टाग्राम रील्स और यूट्यूब शॉट्स एडिट करें।\n\nशुरुआत में सीखने पर ध्यान दें, कमाई अपने आप शुरू हो जाएगी।')">Read Details</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Saving Tips</span>
                        <h3>Smart Student Expense Control</h3>
                        <p>बिना अपनी लाइफस्टाइल कम किए रोज़ाना के छोटे-छोटे खर्चों को कैसे बचाएं।</p>
                        <ul class="info-list">
                            <li>Student Discounts (ID Card का इस्तेमाल)</li>
                            <li>Second Hand & PDF Books का प्रयोग</li>
                            <li>अनचाहे सब्सक्रिप्शन से तुरंत छुटकारा</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFinanceDetail('Expense Control', '• हमेशा कॉलेज/स्कूल आईडी कार्ड से बस, ट्रेन और सॉफ्टवेयर में स्टूडेंट डिस्काउंट लें।\n• नई किताबों की जगह लाइब्रेरी या सीनियर्स से सेकंड हैंड किताबें लें।\n• फास्ट फूड और बाहर खाने का एक वीकली बजट तय करें।')">Read Details</button>
                </div>

                <div class="card">
                    <div>
                        <span class="card-tag">Invest Basic</span>
                        <h3>Emergency Fund & Basic Investing</h3>
                        <p>छात्र जीवन में इमरजेंसी फंड क्यों जरूरी है और 18+ होने पर क्या करें।</p>
                        <ul class="info-list">
                            <li>कम से कम ₹1,000-₹2,000 अलग रखें</li>
                            <li>18+ होने पर बेसिक बैंक खाता व UPI</li>
                            <li>बिना सोचे-समझे ट्रेडिंग से दूरी</li>
                        </ul>
                    </div>
                    <button class="btn-blue" onclick="showFinanceDetail('Emergency Fund', '• इमरजेंसी फंड: कभी फोन खराब हो जाए या अचानक फीस भरनी पड़े, इसके लिए हमेशा एक छोटी रकम सुरक्षित रखें।\n• ट्रेडिंग और गैंबलिंग ऐप्स से पूरी तरह दूर रहें।\n• सबसे पहले अपनी स्किल्स और ज्ञान में इन्वेस्ट करें।')">Read Details</button>
                </div>

            </div>
        </section>

    </div>

    <!-- Hidden Canvas for Graphic Tools -->
    <canvas id="hiddenCanvas"></canvas>

    <script>
        const TOOLS = [
            { id: 1, title: "Photo Background Remover", tag: "Image Tool", type: "image", desc: "फोटो का बैकग्राउंड तुरंत पारदर्शी (Transparent PNG) करें।" },
            { id: 2, title: "Watermark & Stamp Eraser", tag: "Image Fix", type: "image", desc: "Notes या तस्वीरों से अनचाहा वाटरमार्क और टेक्स्ट साफ करें।" },
            { id: 3, title: "Exam Form PDF Compressor", tag: "PDF Tool", type: "pdf", desc: "एडमिशन और फॉर्म्स के लिए PDF को सुरक्षित ऑप्टिमाइज़ करें।" },
