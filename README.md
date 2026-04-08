# IBM_Cognos_Analytics_Dashboard
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>SwiftRoute AI | Logistics Intelligence</title>
    <!-- Google Fonts & Font Awesome -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: radial-gradient(circle at 10% 20%, #0B1120, #07101F);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* ========= LOGIN PAGE STYLES ========= */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: radial-gradient(ellipse at 30% 40%, #0a0f2a, #030617);
            backdrop-filter: blur(2px);
        }

        .glass-card {
            background: rgba(15, 25, 45, 0.55);
            backdrop-filter: blur(12px);
            border-radius: 2rem;
            padding: 2.5rem 2rem;
            width: 420px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.4), 0 0 0 1px rgba(72, 187, 255, 0.2);
            transition: all 0.3s ease;
            border: 1px solid rgba(0, 255, 255, 0.2);
        }

        .glass-card h2 {
            font-size: 2rem;
            font-weight: 700;
            background: linear-gradient(135deg, #A0E9FF, #6C63FF, #FF8C42);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 0.5rem;
        }

        .input-group {
            margin-bottom: 1.5rem;
        }

        .input-group label {
            display: block;
            color: #b9e6ff;
            font-weight: 500;
            margin-bottom: 0.5rem;
            font-size: 0.85rem;
        }

        .input-group input {
            width: 100%;
            background: rgba(10, 20, 35, 0.7);
            border: 1px solid #2c4f6e;
            padding: 0.9rem 1rem;
            border-radius: 1rem;
            color: white;
            font-size: 1rem;
            outline: none;
            transition: 0.2s;
        }

        .input-group input:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 12px rgba(59,130,246,0.3);
        }

        .login-btn {
            background: linear-gradient(95deg, #2A6FDB, #6C63FF);
            border: none;
            width: 100%;
            padding: 0.9rem;
            border-radius: 2rem;
            font-weight: bold;
            font-size: 1rem;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .login-btn:hover {
            transform: scale(1.02);
            background: linear-gradient(95deg, #3a7feb, #7c73ff);
            box-shadow: 0 8px 25px rgba(108,99,255,0.4);
        }

        .error-msg {
            color: #ff7b72;
            font-size: 0.8rem;
            margin-top: 0.8rem;
            text-align: center;
        }

        /* ========= DASHBOARD (main app) ========= */
        .dashboard-wrapper {
            display: none;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        /* sidebar */
        .app-layout {
            display: flex;
            min-height: 100vh;
        }

        .sidebar {
            width: 260px;
            background: rgba(8, 18, 30, 0.7);
            backdrop-filter: blur(16px);
            border-right: 1px solid rgba(0, 255, 255, 0.15);
            padding: 1.8rem 1rem;
            transition: all 0.3s;
            position: sticky;
            top: 0;
            height: 100vh;
        }

        .logo-area {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 2.5rem;
            padding-left: 0.5rem;
        }

        .logo-icon {
            font-size: 2rem;
            background: linear-gradient(145deg, #FFB347, #FF6B6B);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .logo-text {
            font-weight: 800;
            font-size: 1.5rem;
            background: linear-gradient(120deg, #C0F2FF, #AA7EFF);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 0.8rem 1rem;
            margin: 0.5rem 0;
            border-radius: 1rem;
            color: #b0d4ff;
            font-weight: 500;
            transition: 0.2s;
            cursor: pointer;
        }

        .nav-item i {
            width: 24px;
            font-size: 1.2rem;
        }

        .nav-item.active, .nav-item:hover {
            background: rgba(45, 125, 255, 0.2);
            color: white;
            backdrop-filter: blur(4px);
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        /* main content */
        .main-content {
            flex: 1;
            padding: 1.5rem 2rem;
            overflow-x: auto;
        }

        /* navbar */
        .top-navbar {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 12px;
            background: rgba(255,255,255,0.08);
            padding: 0.5rem 1rem;
            border-radius: 2rem;
            backdrop-filter: blur(4px);
        }

        .logout-btn {
            background: rgba(255,80,80,0.2);
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 2rem;
            color: #FFB3B3;
            cursor: pointer;
            font-weight: 500;
            transition: 0.2s;
        }

        .logout-btn:hover {
            background: #ff4d4d;
            color: white;
        }

        /* KPI Grid */
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .kpi-card {
            background: rgba(20, 32, 55, 0.6);
            backdrop-filter: blur(12px);
            border-radius: 1.5rem;
            padding: 1.2rem 1rem;
            transition: all 0.25s ease;
            border: 1px solid rgba(72,187,255,0.2);
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
        }

        .kpi-card:hover {
            transform: translateY(-5px);
            background: rgba(30, 48, 80, 0.7);
            border-color: rgba(0, 255, 255, 0.5);
        }

        .kpi-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .kpi-icon {
            font-size: 2rem;
            background: linear-gradient(145deg, #FFD966, #FF9966);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .kpi-value {
            font-size: 2rem;
            font-weight: 800;
            color: white;
            margin: 0.5rem 0 0.2rem;
        }

        .trend {
            font-size: 0.8rem;
            font-weight: 500;
        }

        .trend.up { color: #4ade80; }
        .trend.down { color: #f87171; }

        /* charts row */
        .charts-row {
            display: flex;
            flex-wrap: wrap;
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .chart-card {
            flex: 1;
            min-width: 280px;
            background: rgba(12, 22, 40, 0.65);
            backdrop-filter: blur(10px);
            border-radius: 1.5rem;
            padding: 1rem;
            border: 1px solid rgba(0, 200, 255, 0.2);
            transition: all 0.2s;
        }

        .chart-card canvas {
            max-height: 260px;
            width: 100%;
        }

        /* table */
        .table-container {
            background: rgba(8, 18, 32, 0.7);
            backdrop-filter: blur(8px);
            border-radius: 1.5rem;
            padding: 1rem;
            overflow-x: auto;
            margin-top: 1rem;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 1rem 0.8rem;
            text-align: left;
            color: #e2f0ff;
        }

        th {
            font-weight: 600;
            background: rgba(0, 100, 150, 0.2);
            border-radius: 1rem;
        }

        tr {
            border-bottom: 1px solid rgba(72, 187, 255, 0.1);
            transition: 0.1s;
        }

        tr:hover {
            background: rgba(72, 187, 255, 0.1);
        }

        .status-badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 2rem;
            font-size: 0.75rem;
            font-weight: 600;
        }

        .status-on-time { background: #10b98120; color: #34d399; border: 1px solid #10b98160; }
        .status-delayed { background: #f59e0b20; color: #fbbf24; border: 1px solid #f59e0b60; }
        .status-failed { background: #ef444420; color: #f87171; border: 1px solid #ef444460; }

        @media (max-width: 800px) {
            .sidebar { width: 80px; padding: 1rem 0.5rem; }
            .sidebar .nav-item span:not(.logo-text) { display: none; }
            .logo-text { display: none; }
            .main-content { padding: 1rem; }
        }
    </style>
</head>
<body>
    <!-- LOGIN PAGE -->
    <div id="loginPage" class="login-container">
        <div class="glass-card">
            <div style="text-align: center; margin-bottom: 1rem;">
                <i class="fas fa-route" style="font-size: 3rem; background: linear-gradient(145deg, #00E0FF, #A855F7); -webkit-background-clip: text; background-clip: text; color: transparent;"></i>
            </div>
            <h2 style="text-align: center;">SwiftRoute AI</h2>
            <p style="text-align: center; color: #9bb8da; margin-bottom: 2rem;">Logistics Intelligence</p>
            <div class="input-group">
                <label><i class="fas fa-user"></i> Email</label>
                <input type="text" id="loginEmail" placeholder="admin@swiftroute.com" value="demo@swiftroute.com">
            </div>
            <div class="input-group">
                <label><i class="fas fa-lock"></i> Password</label>
                <input type="password" id="loginPassword" placeholder="••••••" value="swift123">
            </div>
            <button class="login-btn" id="doLoginBtn"><i class="fas fa-sign-in-alt"></i> Access Dashboard</button>
            <div class="error-msg" id="loginError"></div>
            <div style="text-align: center; margin-top: 1.5rem; font-size: 0.7rem; color: #4f7ea0;">Demo: any email / any password</div>
        </div>
    </div>

    <!-- DASHBOARD APP -->
    <div id="dashboardApp" class="dashboard-wrapper">
        <div class="app-layout">
            <aside class="sidebar">
                <div class="logo-area">
                    <i class="fas fa-route logo-icon"></i>
                    <span class="logo-text">SwiftRoute</span>
                </div>
                <div class="nav-item active"><i class="fas fa-tachometer-alt"></i><span> Dashboard</span></div>
                <div class="nav-item"><i class="fas fa-ship"></i><span> Shipments</span></div>
                <div class="nav-item"><i class="fas fa-chart-line"></i><span> Analytics</span></div>
                <div class="nav-item"><i class="fas fa-truck"></i><span> Fleet</span></div>
            </aside>
            <main class="main-content">
                <div class="top-navbar">
                    <div class="user-profile">
                        <i class="fas fa-user-circle" style="font-size: 1.5rem;"></i>
                        <span>Logistics Manager</span>
                    </div>
                    <button id="logoutBtnDashboard" class="logout-btn"><i class="fas fa-sign-out-alt"></i> Logout</button>
                </div>

                <!-- KPI SECTION -->
                <div class="kpi-grid" id="kpiContainer"></div>

                <!-- CHARTS SECTION -->
                <div class="charts-row">
                    <div class="chart-card">
                        <h4 style="margin-bottom: 12px; color:#caf0ff;"><i class="fas fa-chart-line"></i> Weekly Performance</h4>
                        <canvas id="lineChart" width="400" height="200"></canvas>
                    </div>
                    <div class="chart-card">
                        <h4 style="margin-bottom: 12px; color:#caf0ff;"><i class="fas fa-chart-bar"></i> Shipments by Vehicle</h4>
                        <canvas id="barChart" width="400" height="200"></canvas>
                    </div>
                    <div class="chart-card">
                        <h4 style="margin-bottom: 12px; color:#caf0ff;"><i class="fas fa-chart-pie"></i> Delivery Status</h4>
                        <canvas id="donutChart" width="400" height="200"></canvas>
                    </div>
                </div>

                <!-- RECENT SHIPMENTS TABLE -->
                <div class="table-container">
                    <h4 style="margin-bottom: 12px; color:#fff;"><i class="fas fa-list-ul"></i> Recent Shipments</h4>
                    <table id="shipmentsTable">
                        <thead>
                            <tr><th>Shipment ID</th><th>Client</th><th>Origin</th><th>Destination</th><th>Status</th><th>Rating</th></tr>
                        </thead>
                        <tbody id="tableBody"></tbody>
                    </table>
                </div>
            </main>
        </div>
    </div>

    <script>
        // ---------- MOCK DATASET (derived from xlsx summary) ----------
        const fullShipments = [
            { id:"SHP00001", client:"HUL", origin:"Mumbai", dest:"Lucknow", status:"On-Time", rating:3.3, fuel:101.7, distance:1040 },
            { id:"SHP00002", client:"Cipla", origin:"Hyderabad", dest:"Jaipur", status:"On-Time", rating:1.3, fuel:79, distance:600 },
            { id:"SHP00003", client:"D-Mart", origin:"Chennai", dest:"Kochi", status:"Delayed", rating:2.4, fuel:103.6, distance:965 },
            { id:"SHP00004", client:"Flipkart", origin:"Mumbai", dest:"Chandigarh", status:"Failed", rating:1.6, fuel:11.3, distance:122 },
            { id:"SHP00005", client:"Reliance Retail", origin:"Chennai", dest:"Nagpur", status:"Failed", rating:2.9, fuel:252.1, distance:1732 },
            { id:"SHP00006", client:"HUL", origin:"Chennai", dest:"Surat", status:"Delayed", rating:4.2, fuel:88.3, distance:759 },
            { id:"SHP00007", client:"D-Mart", origin:"Ahmedabad", dest:"Kochi", status:"Failed", rating:1.0, fuel:129.2, distance:1386 },
            { id:"SHP00008", client:"Cipla", origin:"Ahmedabad", dest:"Lucknow", status:"Failed", rating:1.2, fuel:52.2, distance:429 },
            { id:"SHP00009", client:"Reliance Retail", origin:"Mumbai", dest:"Coimbatore", status:"Delayed", rating:3.4, fuel:91.5, distance:724 },
            { id:"SHP00010", client:"HUL", origin:"Hyderabad", dest:"Surat", status:"Failed", rating:3.7, fuel:130.1, distance:1292 },
            { id:"SHP00011", client:"BigBasket", origin:"Kolkata", dest:"Jaipur", status:"Delayed", rating:4.8, fuel:26.7, distance:311 },
            { id:"SHP00012", client:"D-Mart", origin:"Delhi", dest:"Bhopal", status:"Delayed", rating:4.4, fuel:15.2, distance:140 },
            { id:"SHP00013", client:"Reliance Retail", origin:"Bengaluru", dest:"Nagpur", status:"Delayed", rating:4.9, fuel:139.1, distance:1192 },
            { id:"SHP00014", client:"Amazon India", origin:"Pune", dest:"Bhopal", status:"Failed", rating:3.5, fuel:113.2, distance:1200 },
            { id:"SHP00015", client:"Reliance Retail", origin:"Bengaluru", dest:"Kochi", status:"On-Time", rating:1.8, fuel:50.7, distance:478 }
        ];

        // generate aggregated KPIs
        function computeKPIs(data) {
            const totalShipments = data.length;
            const onTimeCount = data.filter(s => s.status === "On-Time").length;
            const failedCount = data.filter(s => s.status === "Failed").length;
            const avgRating = (data.reduce((sum, s) => sum + s.rating, 0) / totalShipments).toFixed(1);
            const totalFuel = data.reduce((sum, s) => sum + s.fuel, 0);
            return { totalShipments, onTimeCount, failedCount, avgRating, totalFuel };
        }

        // render KPIs
        function renderKPIs() {
            const kpis = computeKPIs(fullShipments);
            const container = document.getElementById('kpiContainer');
            container.innerHTML = `
                <div class="kpi-card"><div class="kpi-header"><span>Total Shipments</span><i class="fas fa-truck kpi-icon"></i></div><div class="kpi-value">${kpis.totalShipments}</div><div class="trend up"><i class="fas fa-arrow-up"></i> +12% vs last month</div></div>
                <div class="kpi-card"><div class="kpi-header"><span>On-Time Delivery</span><i class="fas fa-clock kpi-icon"></i></div><div class="kpi-value">${kpis.onTimeCount}</div><div class="trend up"><i class="fas fa-arrow-up"></i> +8%</div></div>
                <div class="kpi-card"><div class="kpi-header"><span>Failed Shipments</span><i class="fas fa-exclamation-triangle kpi-icon"></i></div><div class="kpi-value">${kpis.failedCount}</div><div class="trend down"><i class="fas fa-arrow-down"></i> -5% risk</div></div>
                <div class="kpi-card"><div class="kpi-header"><span>Avg Rating</span><i class="fas fa-star kpi-icon"></i></div><div class="kpi-value">${kpis.avgRating} ★</div><div class="trend up"><i class="fas fa-arrow-up"></i> +0.3</div></div>
                <div class="kpi-card"><div class="kpi-header"><span>Fuel Used (L)</span><i class="fas fa-gas-pump kpi-icon"></i></div><div class="kpi-value">${Math.round(kpis.totalFuel)}</div><div class="trend down"><i class="fas fa-arrow-down"></i> efficient</div></div>
            `;
        }

        // render table
        function renderTable() {
            const tbody = document.getElementById('tableBody');
            const recent = fullShipments.slice(0, 10);
            tbody.innerHTML = recent.map(s => {
                let statusClass = '';
                if(s.status === 'On-Time') statusClass = 'status-on-time';
                else if(s.status === 'Delayed') statusClass = 'status-delayed';
                else statusClass = 'status-failed';
                return `<tr>
                    <td>${s.id}</td><td>${s.client}</td><td>${s.origin}</td><td>${s.dest}</td>
                    <td><span class="status-badge ${statusClass}">${s.status}</span></td>
                    <td>${s.rating} <i class="fas fa-star" style="color:#ffb347; font-size:0.7rem;"></i></td>
                </tr>`;
            }).join('');
        }

        // ----- CHARTS INIT (with gradient animations)
        let lineChart, barChart, donutChart;

        function initCharts() {
            // line chart: weekly trend mock data
            const ctxLine = document.getElementById('lineChart').getContext('2d');
            const grad = ctxLine.createLinearGradient(0, 0, 0, 300);
            grad.addColorStop(0, 'rgba(0, 230, 200, 0.6)');
            grad.addColorStop(1, 'rgba(0, 100, 200, 0.1)');
            lineChart = new Chart(ctxLine, {
                type: 'line',
                data: { labels: ['Week 1', 'Week 2', 'Week 3', 'Week 4'], datasets: [{ label: 'On-Time %', data: [72, 68, 81, 78], borderColor: '#2dd4bf', backgroundColor: grad, fill: true, tension: 0.3, pointBackgroundColor: '#facc15' }] },
                options: { responsive: true, maintainAspectRatio: true, plugins: { legend: { labels: { color: '#cbd5e1' } } } }
            });
            const ctxBar = document.getElementById('barChart').getContext('2d');
            barChart = new Chart(ctxBar, {
                type: 'bar',
                data: { labels: ['Truck', 'Van', 'Bike'], datasets: [{ label: 'Shipments count', data: [42, 58, 45], backgroundColor: ['#3b82f6', '#a855f7', '#f97316'], borderRadius: 10 }] },
                options: { responsive: true, plugins: { legend: { labels: { color: '#cbd5e1' } } } }
            });
            const ctxDonut = document.getElementById('donutChart').getContext('2d');
            const statusCount = { 'On-Time': fullShipments.filter(s=>s.status==='On-Time').length, 'Delayed': fullShipments.filter(s=>s.status==='Delayed').length, 'Failed': fullShipments.filter(s=>s.status==='Failed').length };
            donutChart = new Chart(ctxDonut, {
                type: 'doughnut',
                data: { labels: ['On-Time', 'Delayed', 'Failed'], datasets: [{ data: [statusCount['On-Time'], statusCount['Delayed'], statusCount['Failed']], backgroundColor: ['#10b981', '#f59e0b', '#ef4444'], borderWidth: 0, hoverOffset: 8 }] },
                options: { cutout: '60%', plugins: { legend: { position: 'bottom', labels: { color: '#e2e8f0' } }, tooltip: { callbacks: { label: (ctx) => `${ctx.label}: ${ctx.raw} shipments` } } } }
            });
        }

        function updateChartsDynamic() {
            if (lineChart) lineChart.data.datasets[0].data = [74, 70, 83, 79]; lineChart.update();
            if (barChart) barChart.update();
            const statusCountUp = { 'On-Time': fullShipments.filter(s=>s.status==='On-Time').length, 'Delayed': fullShipments.filter(s=>s.status==='Delayed').length, 'Failed': fullShipments.filter(s=>s.status==='Failed').length };
            if(donutChart) donutChart.data.datasets[0].data = [statusCountUp['On-Time'], statusCountUp['Delayed'], statusCountUp['Failed']]; donutChart.update();
        }

        // ---------- AUTH LOGIC (demo with validation & local storage) ----------
        let isLoggedIn = false;

        function showDashboard() {
            document.getElementById('loginPage').style.display = 'none';
            const dashboard = document.getElementById('dashboardApp');
            dashboard.style.display = 'block';
            setTimeout(() => { dashboard.style.opacity = '1'; }, 20);
            renderKPIs();
            renderTable();
            if(!lineChart) initCharts(); else updateChartsDynamic();
        }

        function showLogin() {
            document.getElementById('dashboardApp').style.opacity = '0';
            setTimeout(() => {
                document.getElementById('dashboardApp').style.display = 'none';
                document.getElementById('loginPage').style.display = 'flex';
            }, 200);
        }

        // login handler
        document.getElementById('doLoginBtn').addEventListener('click', () => {
            const email = document.getElementById('loginEmail').value.trim();
            const pwd = document.getElementById('loginPassword').value.trim();
            // simple any demo credentials
            if(email.length > 0 && pwd.length > 0) {
                localStorage.setItem('swift_auth', 'true');
                isLoggedIn = true;
                showDashboard();
                document.getElementById('loginError').innerText = '';
            } else {
                document.getElementById('loginError').innerText = 'Please enter email/password (demo mode)';
            }
        });

        document.getElementById('logoutBtnDashboard')?.addEventListener('click', () => {
            localStorage.removeItem('swift_auth');
            isLoggedIn = false;
            showLogin();
        });

        // check saved session
        function checkAuth() {
            const saved = localStorage.getItem('swift_auth');
            if(saved === 'true') {
                isLoggedIn = true;
                showDashboard();
            } else {
                showLogin();
            }
        }

        // small animation updates every 8 sec (simulate micro-interaction)
        setInterval(() => {
            if (document.getElementById('dashboardApp').style.display === 'block') {
                const kpis = computeKPIs(fullShipments);
                const ratingSpan = document.querySelector('.kpi-card:nth-child(4) .kpi-value');
                if(ratingSpan) ratingSpan.innerHTML = `${kpis.avgRating} ★`;
                const fuelSpan = document.querySelector('.kpi-card:nth-child(5) .kpi-value');
                if(fuelSpan) fuelSpan.innerHTML = `${Math.round(kpis.totalFuel)}`;
            }
        }, 5000);

        // final start
        checkAuth();
        window.addEventListener('resize', () => { if(lineChart) lineChart.resize(); if(barChart) barChart.resize(); if(donutChart) donutChart.resize(); });
    </script>
</body>
</html>
