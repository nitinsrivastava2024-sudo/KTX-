
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KTX Super Marketplace | खाटू टीम एक्सरसाइज</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        :root { --bg: #0d1117; --card: #161b22; --border: #30363d; --text: #c9d1d9; --accent: #58a6ff; --green: #238636; --gold: #f1e05a; --red: #da3633; }
        body { background: var(--bg); color: var(--text); padding-bottom: 50px; }

        /* Auth Screen */
        #authOverlay { position: fixed; inset: 0; background: rgba(13,17,23,0.95); display: flex; align-items: center; justify-content: center; z-index: 999; padding: 15px; }
        .auth-box { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 25px; width: 100%; max-width: 380px; text-align: center; box-shadow: 0 10px 30px rgba(0,0,0,0.8); }
        .logo { width: 50px; height: 50px; background: linear-gradient(135deg, var(--accent), #1f6feb); border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 10px; font-weight: 800; font-size: 18px; color: #fff; }
        .auth-box h2 { font-size: 20px; color: var(--accent); margin-bottom: 5px; }
        .auth-box p { font-size: 12px; color: #8b949e; margin-bottom: 20px; }
        .input-box { width: 100%; padding: 12px; background: var(--bg); border: 1px solid var(--border); border-radius: 6px; color: var(--text); font-size: 14px; margin-bottom: 12px; outline: none; }
        .input-box:focus { border-color: var(--accent); }
        .btn-main { width: 100%; padding: 12px; background: var(--green); color: #fff; border: none; border-radius: 6px; font-size: 14px; font-weight: bold; cursor: pointer; }
        .btn-main:hover { background: #2ea043; }

        /* Navigation */
        .navbar { background: var(--card); border-bottom: 1px solid var(--border); padding: 12px 20px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 100; }
        .brand { display: flex; align-items: center; gap: 10px; }
        .brand-logo { width: 32px; height: 32px; background: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #0d1117; font-size: 12px; }
        .user-tag { font-size: 12px; background: var(--bg); border: 1px solid var(--border); padding: 6px 12px; border-radius: 20px; color: var(--accent); }

        /* Container & Grid */
        .container { max-width: 1200px; margin: 20px auto; padding: 0 15px; }
        .top-banner { background: linear-gradient(135deg, #1f6feb 0%, #161b22 100%); border: 1px solid var(--border); border-radius: 12px; padding: 25px; margin-bottom: 25px; text-align: center; }
        .top-banner h1 { font-size: 24px; margin-bottom: 8px; color: #fff; }
        .top-banner p { font-size: 13px; color: #c9d1d9; }

        /* Filter & Search Bar */
        .search-row { display: flex; gap: 10px; margin-bottom: 25px; flex-wrap: wrap; }
        .search-row input, .search-row select { padding: 10px 14px; background: var(--card); border: 1px solid var(--border); border-radius: 6px; color: var(--text); font-size: 13px; outline: none; }
        .search-row input { flex: 1; min-width: 200px; }

        /* Marketplace Grid */
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 15px; }
        .card { background: var(--card); border: 1px solid var(--border); border-radius: 8px; padding: 16px; display: flex; flex-direction: column; justify-content: space-between; }
        .cat-badge { font-size: 10px; text-transform: uppercase; background: rgba(88,166,255,0.1); color: var(--accent); border: 1px solid var(--accent); padding: 3px 8px; border-radius: 4px; display: inline-block; margin-bottom: 10px; width: fit-content; }
        .card h3 { font-size: 16px; margin-bottom: 8px; color: #fff; }
        .card p { font-size: 12px; color: #8b949e; line-height: 1.5; margin-bottom: 15px; flex-grow: 1; }
        .card-footer { display: flex; justify-content: space-between; align-items: center; border-top: 1px solid var(--border); padding-top: 12px; }
        .budget { font-size: 14px; font-weight: bold; color: var(--gold); }
        .btn-bid { padding: 6px 14px; background: var(--accent); color: #0d1117; border: none; border-radius: 6px; font-size: 12px; font-weight: bold; cursor: pointer; }

        /* Secret Admin Panel */
        #adminSection { display: none; background: #1c1427; border: 1px solid #8957e5; border-radius: 12px; padding: 20px; margin-bottom: 25px; }
        #adminSection h2 { color: #d2a8ff; font-size: 18px; margin-bottom: 12px; }
        .admin-stats { display: flex; gap: 15px; flex-wrap: wrap; margin-bottom: 15px; }
        .stat-card { background: var(--card); border: 1px solid var(--border); border-radius: 6px; padding: 12px 18px; flex: 1; min-width: 140px; text-align: center; }
        .stat-card span { font-size: 20px; font-weight: bold; color: #fff; display: block; }
        .stat-card label { font-size: 11px; color: #8b949e; }

        @media(max-width: 600px) {
            .navbar { padding: 10px; }
            .search-row { flex-direction: column; }
        }
    </style>
</head>
<body>

    <!-- 1. Mobile & OTP Login Screen -->
    <div id="authOverlay">
        <div class="auth-box">
            <div class="logo">KTX</div>
            <h2>KTX Super Marketplace</h2>
            <p>खाटू टीम एक्सरसाइज</p>
            
            <div id="stepPhone">
                <input type="tel" id="userPhone" class="input-box" placeholder="10 Digit Mobile Number" maxlength="10">
                <select id="userRole" class="input-box">
                    <option value="Client">I Want to Hire (Client)</option>
                    <option value="Programmer">Programmer / Developer</option>
                    <option value="Contractor">Contractor / Builder</option>
                    <option value="Labor">Home Repair / Labor</option>
                    <option value="Doctor">Doctor / Medical</option>
                    <option value="Teacher">Teacher / Tutor</option>
                </select>
                <button class="btn-main" onclick="sendOtp()">Get Instant OTP</button>
            </div>

            <div id="stepOtp" style="display:none;">
                <input type="text" id="otpCode" class="input-box" placeholder="Enter 4-Digit OTP (Hint: 1234)" maxlength="4">
                <button class="btn-main" onclick="verifyOtp()">Sign In to Dashboard</button>
            </div>
        </div>
    </div>

    <!-- 2. Main Platform Header -->
    <header class="navbar">
        <div class="brand">
            <div class="brand-logo">KTX</div>
            <strong>KTX Super Marketplace</strong>
        </div>
        <div style="display: flex; gap: 10px; align-items: center;">
            <div class="user-tag" id="userBadge">+91 XXXXXXXX</div>
            <button onclick="logout()" style="background: none; border: 1px solid var(--border); color: #ff7b72; padding: 5px 10px; border-radius: 6px; cursor: pointer; font-size: 11px;">Exit</button>
        </div>
    </header>

    <div class="container">
        
        <!-- Secret Master Admin Dashboard (Only opens for admin phone) -->
        <div id="adminSection">
            <h2>👑 Secret Admin Master Panel (Live Overview)</h2>
            <div class="admin-stats">
                <div class="stat-card"><span>2,410</span><label>Total Verified Users</label></div>
                <div class="stat-card"><span id="totalServicesCount">20</span><label>Active Services</label></div>
                <div class="stat-card"><span>₹1.48L</span><label>Platform Volume</label></div>
                <div class="stat-card"><span style="color:#3fb950;">0ms</span><label>Zero-Lag Status</label></div>
            </div>
            <button onclick="addNewServicePrompt()" class="btn-main" style="background:#8957e5; max-width:200px;">+ Add New Category/Gig</button>
        </div>

        <!-- Banner -->
        <div class="top-banner">
            <h1>On-Demand Services Marketplace</h1>
            <p>20+ Categories • White Collar & Blue Collar • Real-time Instant Connect</p>
        </div>

        <!-- Search & Category Filters -->
        <div class="search-row">
            <input type="text" id="searchInput" placeholder="Search web dev, plumbing, doctor, contractor..." oninput="filterServices()">
            <select id="catFilter" onchange="filterServices()">
                <option value="ALL">All 20+ Categories</option>
                <option value="Web Development">Web Development</option>
                <option value="Mobile App Development">Mobile App Development</option>
                <option value="Plumbing & Electrical">Plumbing & Electrical</option>
                <option value="Home Repair & Construction">Home Repair & Construction</option>
                <option value="Medical Consultation">Medical Consultation</option>
                <option value="Tutoring & Education">Tutoring & Education</option>
                <option value="Graphic Design">Graphic Design</option>
                <option value="Content Writing">Content Writing</option>
            </select>
        </div>

        <!-- Marketplace Cards -->
        <div class="grid" id="servicesGrid"></div>

    </div>

    <script>
        const MASTER_SERVICES = [
            { id: 1, title: "Full Stack Website Development (FastAPI + React)", cat: "Web Development", desc: "Build high-speed zero-lag web application with custom dashboard.", budget: "₹15,000" },
            { id: 2, title: "Complete House Plumbing & Pipe Fitting", cat: "Plumbing & Electrical", desc: "Bathroom fittings, leakage repair, water tank connection.", budget: "₹1,800" },
            { id: 3, title: "Android & iOS Marketplace App", cat: "Mobile App Development", desc: "Native flutter app with push notifications and OTP flow.", budget: "₹25,000" },
            { id: 4, title: "House Renovation & Construction Contractor", cat: "Home Repair & Construction", desc: "Masonry, tile fitting, wall painting and structural repair.", budget: "₹45,000" },
            { id: 5, title: "Online Medical Consultation & Prescription", cat: "Medical Consultation", desc: "Verified general physician online video consultation.", budget: "₹500" },
            { id: 6, title: "Class 10-12 Physics & Maths Home Tutor", cat: "Tutoring & Education", desc: "Daily 1.5 hours personal coaching for board exams.", budget: "₹4,000/mo" },
            { id: 7, title: "Modern Logo & Brand Identity Pack", cat: "Graphic Design", desc: "3 Logo concepts, business card, letterhead and social kit.", budget: "₹2,500" },
            { id: 8, title: "SEO Optimized Hindi/English Blog Writing", cat: "Content Writing", desc: "100% human-written high ranking 2000-word articles.", budget: "₹1,200" }
        ];

        let activePhone = "";

        window.onload = function() {
            let saved = localStorage.getItem('ktx_market_user');
            if(saved) {
                activePhone = saved;
                initDashboard();
            }
            renderServices(MASTER_SERVICES);
        };

        function sendOtp() {
            let p = document.getElementById('userPhone').value.trim();
            if(p.length < 10) { alert("Please enter valid 10-digit number!"); return; }
            activePhone = p;
            alert("OTP Sent Successfully!\nDemo OTP is: 1234");
            document.getElementById('stepPhone').style.display = 'none';
            document.getElementById('stepOtp').style.display = 'block';
        }

        function verifyOtp() {
            let otp = document.getElementById('otpCode').value.trim();
            if(otp === "1234") {
                localStorage.setItem('ktx_market_user', activePhone);
                initDashboard();
            } else {
                alert("Incorrect OTP. Please enter 1234.");
            }
        }

        function initDashboard() {
            document.getElementById('authOverlay').style.display = 'none';
            document.getElementById('userBadge').innerText = "+91 " + activePhone;
            
            // If phone ends in 0000 or is 9999999999 -> Unlock Master Admin
            if(activePhone === "9999999999" || activePhone.endsWith("0000")) {
                document.getElementById('adminSection').style.display = 'block';
            }
        }

        function logout() {
            localStorage.removeItem('ktx_market_user');
            location.reload();
        }

        function renderServices(list) {
            let grid = document.getElementById('servicesGrid');
            grid.innerHTML = "";
            list.forEach(s => {
                grid.innerHTML += `
                    <div class="card">
                        <div>
                            <span class="cat-badge">${s.cat}</span>
                            <h3>${s.title}</h3>
                            <p>${s.desc}</p>
                        </div>
                        <div class="card-footer">
                            <span class="budget">${s.budget}</span>
                            <button class="btn-bid" onclick="placeBid('${s.title}')">Bid / Contact</button>
                        </div>
                    </div>
                `;
            });
            document.getElementById('totalServicesCount').innerText = list.length;
        }

        function filterServices() {
            let q = document.getElementById('searchInput').value.toLowerCase();
            let c = document.getElementById('catFilter').value;
            let filtered = MASTER_SERVICES.filter(s => {
                let matchCat = (c === "ALL" || s.cat === c);
                let matchQuery = s.title.toLowerCase().includes(q) || s.desc.toLowerCase().includes(q) || s.cat.toLowerCase().includes(q);
                return matchCat && matchQuery;
            });
            renderServices(filtered);
        }

        function placeBid(title) {
            let amount = prompt(`Enter your Bid / Quote amount for: \n"${title}" (in ₹):`);
            if(amount) {
                alert(`✅ Your Proposal of ₹${amount} has been submitted directly to the client!`);
            }
        }

        function addNewServicePrompt() {
            let t = prompt("Enter Service Title:");
            let cat = prompt("Enter Category (e.g., Web Development, Plumbing, Legal):");
            let p = prompt("Enter Price/Budget:");
            if(t && cat && p) {
                MASTER_SERVICES.unshift({ id: Date.now(), title: t, cat: cat, desc: "Directly added from Secret Admin Master Panel.", budget: "₹" + p });
                renderServices(MASTER_SERVICES);
                alert("New Service Listed Live on Marketplace!");
            }
        }
    </script>
</body>
</html>
