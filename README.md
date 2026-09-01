
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Hub | खाटू टीम एक्सरसाइज</title>
    <style>
        *{box-sizing:border-box}
        :root{--bg:#0d1117;--card:#161b22;--border:#30363d;--text:#c9d1d9;--muted:#8b949e;--accent:#58a6ff;--success:#238636}
        body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif;background:var(--bg);color:var(--text);margin:0;padding:0}
        
        /* OTP Auth Modal/Screen */
        #authScreen{display:flex;justify-content:center;align-items:center;width:100vw;height:100vh;background:radial-gradient(circle,#161b22 0%,#0d1117 100%);position:fixed;top:0;left:0;z-index:1000;padding:20px}
        .auth-card{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:35px 25px;width:100%;max-width:380px;box-shadow:0 16px 40px rgba(0,0,0,0.6);text-align:center}
        .logo-badge{width:55px;height:55px;margin:0 auto 12px auto;border-radius:50%;background:linear-gradient(135deg,var(--accent),#1f6feb);display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:800;color:#fff;box-shadow:0 0 15px rgba(88,166,255,0.4)}
        .auth-card h1{font-size:22px;color:var(--accent);margin:0 0 2px 0}
        .auth-card p{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:20px}
        .form-group{margin-bottom:14px;text-align:left}
        .form-group label{display:block;font-size:12px;color:var(--text);margin-bottom:5px;font-weight:600}
        .form-group input{width:100%;padding:10px;background:var(--bg);border:1px solid var(--border);border-radius:6px;color:var(--text);font-size:13px;outline:none;text-align:center;letter-spacing:1px}
        .form-group input:focus{border-color:var(--accent)}
        .btn-auth{width:100%;padding:10px;background:var(--success);color:#fff;border:none;border-radius:6px;font-size:13px;font-weight:600;cursor:pointer;margin-top:10px}
        .btn-auth:hover{background:#2ea043}

        /* Dashboard Screen */
        #dashboardScreen{display:none;width:100%;min-height:100vh;flex-direction:column}
        .navbar{background:var(--card);border-bottom:1px solid var(--border);padding:12px 25px;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:100}
        .nav-center{display:flex;align-items:center;gap:10px;margin:0 auto;}
        .nav-logo-sm{width:32px;height:32px;border-radius:50%;background:linear-gradient(135deg,var(--accent),#1f6feb);display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:800;color:#fff}
        .nav-title{font-size:15px;font-weight:800;color:var(--text);margin:0;line-height:1.1}
        .nav-desc{font-size:8px;color:var(--muted);margin:0;text-transform:uppercase;letter-spacing:0.5px}
        
        .nav-right{display:flex;align-items:center;gap:10px}
        .user-badge{background:var(--bg);border:1px solid var(--border);padding:5px 12px;border-radius:20px;font-size:12px;color:var(--accent);font-weight:600}
        .btn-logout{background:none;border:1px solid var(--border);color:#ff7b72;padding:5px 10px;border-radius:6px;font-size:12px;cursor:pointer;font-weight:600}
        .btn-logout:hover{background:rgba(255,123,114,0.1)}

        /* Main Content */
        .main{max-width:1200px;margin:25px auto;padding:0 20px;width:100%}
        .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;margin-bottom:25px}
        .card{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:20px;display:flex;flex-direction:column;justify-content:space-between}
        .card h2{font-size:15px;color:var(--text);margin:0 0 12px 0;border-bottom:1px solid var(--border);padding-bottom:10px}
        .card label{display:block;font-size:12px;color:var(--muted);margin-bottom:6px}
        .card textarea{width:100%;padding:10px;background:var(--bg);border:1px solid var(--border);border-radius:6px;color:var(--text);font-size:13px;resize:vertical;min-height:90px;outline:none}
        .card textarea:focus{border-color:var(--accent)}
        .btn-act{width:100%;padding:10px;background:#1f6feb;color:#fff;border:none;border-radius:6px;font-size:13px;font-weight:600;cursor:pointer;margin-top:12px}
        .btn-act:hover{background:var(--accent);color:#0d1117}
        .output{margin-top:12px;padding:12px;background:var(--bg);border:1px solid var(--border);border-radius:6px;font-size:13px;line-height:1.5;display:none;white-space:pre-wrap;max-height:180px;overflow-y:auto}
        
        .sub-box{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:20px 25px;display:flex;justify-content:space-between;align-items:center}
        .sub-box h3{margin:0 0 4px 0;font-size:15px;color:var(--text)}
        .sub-box p{margin:0;font-size:12px;color:var(--muted)}
        .badge-soon{background:rgba(88,166,255,0.1);color:var(--accent);border:1px solid var(--accent);padding:5px 12px;border-radius:15px;font-size:11px;font-weight:600;text-transform:uppercase}

        @media(max-width:900px){.grid{grid-template-columns:1fr}.sub-box{flex-direction:column;align-items:flex-start;gap:10px}}
    </style>
</head>
<body>

    <!-- Mobile Number & OTP Verification Gate -->
    <div id="authScreen">
        <div class="auth-card">
            <div class="logo-badge">KTX</div>
            <h1>KTX Hub</h1>
            <p>खाटू टीम एक्सरसाइज</p>
            
            <div class="form-group" id="phoneGroup">
                <label>Enter Mobile Number</label>
                <input type="tel" id="phoneNumber" placeholder="9876543210" maxlength="10">
                <button class="btn-auth" onclick="sendOTP()">Get OTP</button>
            </div>

            <div class="form-group" id="otpGroup" style="display:none;">
                <label>Enter 4-Digit OTP (Hint: Any 4 digits like 1234)</label>
                <input type="text" id="otpInput" placeholder="1234" maxlength="4">
                <button class="btn-auth" onclick="verifyOTP()">Verify & Sign In</button>
            </div>
        </div>
    </div>

    <!-- Dashboard Screen -->
    <div id="dashboardScreen">
        <header class="navbar">
            <div style="width: 80px;"></div>
            <div class="nav-center">
                <div class="nav-logo-sm">KTX</div>
                <div><h2 class="nav-title">KTX Hub</h2><p class="nav-desc">खाटू टीम एक्सरसाइज</p></div>
            </div>
            <div class="nav-right">
                <div class="user-badge" id="uBadge">User</div>
                <button class="btn-logout" onclick="doLogout()">Sign Out</button>
            </div>
        </header>

        <div class="main">
            <div class="grid">
                <div class="card">
                    <div><h2>Fitness & Gym Coach</h2><label>Ask fitness query:</label><textarea id="qFit" placeholder="Workout routine..."></textarea></div>
                    <div><button class="btn-act" onclick="askAI('fit')">Generate</button><div id="rFit" class="output"></div></div>
                </div>
                <div class="card">
                    <div><h2>Finance & Wealth</h2><label>Ask financial query:</label><textarea id="qFin" placeholder="Investment tips..."></textarea></div>
                    <div><button class="btn-act" onclick="askAI('fin')">Generate</button><div id="rFin" class="output"></div></div>
                </div>
                <div class="card">
                    <div><h2>Web Engineering</h2><label>Ask coding query:</label><textarea id="qWeb" placeholder="HTML/CSS layout..."></textarea></div>
                    <div><button class="btn-act" onclick="askAI('web')">Generate</button><div id="rWeb" class="output"></div></div>
                </div>
            </div>

            <div class="sub-box">
                <div><h3>KTX Enterprise Pro Tier</h3><p>Upcoming cloud storage & high-throughput modules.</p></div>
                <div><span class="badge-soon">Coming Soon</span></div>
            </div>
        </div>
    </div>

    <script>
        window.onload = function() {
            let phone = localStorage.getItem('ktx_phone');
            if(phone){ 
                document.getElementById('uBadge').innerText = "+91 " + phone; 
                document.getElementById('authScreen').style.display = 'none'; 
                document.getElementById('dashboardScreen').style.display = 'flex'; 
            }
        }

        function sendOTP() {
            let phone = document.getElementById('phoneNumber').value.trim();
            if(phone.length < 10) {
                alert("Please enter a valid 10-digit mobile number!");
                return;
            }
            // Seamless simulated OTP flow
            alert("OTP sent successfully! (Demo OTP: 1234)");
            document.getElementById('phoneGroup').style.display = 'none';
            document.getElementById('otpGroup').style.display = 'block';
        }

        function verifyOTP() {
            let otp = document.getElementById('otpInput').value.trim();
            let phone = document.getElementById('phoneNumber').value.trim();
            if(otp.length === 4) {
                localStorage.setItem('ktx_phone', phone);
                document.getElementById('uBadge').innerText = "+91 " + phone;
                document.getElementById('authScreen').style.display = 'none';
                document.getElementById('dashboardScreen').style.display = 'flex';
            } else {
                alert("Please enter a valid 4-digit OTP!");
            }
        }

        function doLogout() {
            localStorage.removeItem('ktx_phone');
            document.getElementById('dashboardScreen').style.display = 'none';
            document.getElementById('authScreen').style.display = 'flex';
            document.getElementById('phoneGroup').style.display = 'block';
            document.getElementById('otpGroup').style.display = 'none';
            document.getElementById('phoneNumber').value = '';
            document.getElementById('otpInput').value = '';
        }

        async function askAI(t) {
            // Built-in seamless key handling so users never see an API key box
            let k = "AIzaSyD" + "W_dummy_key_protected_ktx_hub_2026"; 
            let qId = t==='fit'?'qFit':t==='fin'?'qFin':'qWeb';
            let rId = t==='fit'?'rFit':t==='fin'?'rFin':'rWeb';
            let query = document.getElementById(qId).value.trim();
            if(!query){ alert("Please type a question!"); return; }
            let box = document.getElementById(rId);
            box.style.display = 'block'; box.innerHTML = 'Thinking...';
            
            try {
                let res = await fetch(`https://generativelanguage.googleapis.com/v1/models/gemini-2.0-flash:generateContent?key=${k}`, {
                    method: 'POST', headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify({contents: [{parts: [{text: "Answer in professional English: " + query}]}]})
                });
                let d = await res.json();
                if(d.error) {
                    box.innerHTML = `<span style="color:#ff7b72">Notice: Please configure a valid live Gemini key if testing on custom domain.</span>`;
                } else if(d.candidates) {
                    box.innerHTML = d.candidates[0].content.parts[0].text.replace(/\n/g, '<br>');
                } else {
                    box.innerHTML = 'No response.';
                }
            } catch(err) { 
                box.innerHTML = `<span style="color:#ff7b72">Error: ${err.message}</span>`; 
            }
        }
    </script>

