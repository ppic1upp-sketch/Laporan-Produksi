<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Laporan Produksi - Multi Operator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        /* Login Page */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .login-card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        .login-card h2 {
            text-align: center;
            color: #333;
            margin-bottom: 10px;
        }

        .login-card .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 10px;
            font-size: 14px;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            font-size: 16px;
        }

        .btn-small {
            padding: 8px 16px;
            width: auto;
            font-size: 14px;
        }

        .btn-danger {
            background: #f44336;
        }

        .btn-warning {
            background: #ff9800;
        }

        /* Main App */
        .app-container {
            display: none;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        .header h1 {
            color: #333;
            font-size: 24px;
        }

        .header p {
            color: #666;
            font-size: 14px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-badge {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: bold;
        }

        .logout-btn {
            background: #f44336;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .tab-btn {
            background: white;
            border: none;
            padding: 12px 24px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Card */
        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        .card h2 {
            margin-bottom: 20px;
            border-left: 4px solid #667eea;
            padding-left: 15px;
            color: #333;
        }

        /* Form Grid */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .form-group-full {
            grid-column: 1 / -1;
        }

        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 14px;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        /* Table */
        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background: #f8f9fa;
            font-weight: bold;
            color: #333;
        }

        tr:hover {
            background: #f8f9fa;
        }

        /* Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
        }

        .stat-card h3 {
            font-size: 14px;
            opacity: 0.9;
            margin-bottom: 10px;
        }

        .stat-card .value {
            font-size: 28px;
            font-weight: bold;
        }

        /* Filter */
        .filter-bar {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            align-items: flex-end;
        }

        .filter-bar .form-group {
            margin-bottom: 0;
            flex: 1;
            min-width: 150px;
        }

        /* Alert */
        .alert {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            border-radius: 10px;
            color: white;
            font-weight: bold;
            animation: slideIn 0.3s ease;
            z-index: 1000;
        }

        .alert-success { background: #4caf50; }
        .alert-error { background: #f44336; }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .readonly-input {
            background: #f5f5f5;
            cursor: not-allowed;
        }

        @media (max-width: 768px) {
            .form-grid { grid-template-columns: 1fr; }
            .tab-btn { padding: 8px 16px; font-size: 14px; }
            .header { flex-direction: column; text-align: center; gap: 10px; }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="loginPage" class="login-container">
        <div class="login-card">
            <h2>🏭 SISTEM LAPORAN PRODUKSI</h2>
            <div class="subtitle">PT. NAMA PERUSAHAAN ANDA</div>
            <form id="loginForm">
                <div class="form-group">
                    <label>Username / NIK</label>
                    <input type="text" id="loginUsername" placeholder="Masukkan username" required>
                </div>
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" id="loginPassword" placeholder="Masukkan password" required>
                </div>
                <button type="submit" class="btn">🔐 LOGIN</button>
            </form>
        </div>
    </div>

    <!-- Main App -->
    <div id="appContainer" class="app-container">
        <div class="header">
            <div>
                <h1>🏭 SISTEM LAPORAN PRODUKSI</h1>
                <p>Form Laporan Harian - Lengkap dengan Perhitungan Otomatis</p>
            </div>
            <div class="user-info">
                <div class="user-badge" id="userRoleBadge"></div>
                <span id="userNameDisplay"></span>
                <button class="logout-btn" onclick="logout()">🚪 LOGOUT</button>
            </div>
        </div>

        <div class="tabs" id="tabsContainer"></div>

        <!-- Tab Input Form -->
        <div id="input" class="tab-content">
            <div class="card">
                <h2>📝 FORM LAPORAN PRODUKSI HARIAN</h2>
                <form id="productionForm">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>📅 Tanggal <span style="color:red;">*</span></label>
                            <input type="date" id="tanggal" required>
                        </div>
                        <div class="form-group">
                            <label>🕐 Shift <span style="color:red;">*</span></label>
                            <select id="shift" required>
                                <option value="">Pilih Shift</option>
                                <option value="Shift 1 (Pagi)">Shift 1 (Pagi) - 07:00-15:00</option>
                                <option value="Shift 2 (Siang)">Shift 2 (Siang) - 15:00-23:00</option>
                                <option value="Shift 3 (Malam)">Shift 3 (Malam) - 23:00-07:00</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>👨‍💼 Operator 1 <span style="color:red;">*</span></label>
                            <input type="text" id="operator1" placeholder="Nama Operator 1" required>
                        </div>
                        <div class="form-group">
                            <label>📦 Item / Produk <span style="color:red;">*</span></label>
                            <input type="text" id="item" placeholder="Nama item/produk" required>
                        </div>
                        <div class="form-group">
                            <label>📏 Ukuran</label>
                            <input type="text" id="ukuran" placeholder="Ukuran produk">
                        </div>
                        <div class="form-group">
                            <label>✅ Hasil Qty <span style="color:red;">*</span></label>
                            <input type="number" id="hasilQty" placeholder="Jumlah hasil produksi" required oninput="hitungJumlahBersih()">
                        </div>
                        <div class="form-group">
                            <label>📜 Jumlah Roll</label>
                            <input type="number" id="jumlahRoll" placeholder="Jumlah roll" value="0">
                        </div>
                        <div class="form-group">
                            <label>⚙️ Mesin</label>
                            <input type="text" id="mesin" placeholder="Nomor/nama mesin">
                        </div>
                        <div class="form-group">
                            <label>❌ Reject Sablon</label>
                            <input type="number" id="rejectSablon" placeholder="Jumlah reject sablon" value="0" oninput="hitungJumlahReject()">
                        </div>
                        <div class="form-group">
                            <label>✂️ Reject Cutting</label>
                            <input type="number" id="rejectCutting" placeholder="Jumlah reject cutting" value="0" oninput="hitungJumlahReject()">
                        </div>
                        <div class="form-group">
                            <label>📊 Jumlah Reject (Otomatis)</label>
                            <input type="number" id="jumlahReject" class="readonly-input" readonly>
                        </div>
                        <div class="form-group">
                            <label>✨ Jumlah Bersih (Otomatis)</label>
                            <input type="number" id="jumlahBersih" class="readonly-input" readonly>
                        </div>
                        <div class="form-group">
                            <label>👨‍💼 Operator 2</label>
                            <input type="text" id="operator2" placeholder="Nama Operator 2 (jika ada)">
                        </div>
                        <div class="form-group-full">
                            <label>📝 Keterangan</label>
                            <textarea id="keterangan" rows="2" placeholder="Catatan tambahan..."></textarea>
                        </div>
                    </div>
                    <div style="display: flex; gap: 10px; margin-top: 20px;">
                        <button type="submit" class="btn">💾 SIMPAN LAPORAN</button>
                        <button type="button" class="btn btn-warning" onclick="resetForm()">🔄 RESET FORM</button>
                    </div>
                </form>
            </div>
        </div>

        <!-- Tab Laporan Saya -->
        <div id="laporan" class="tab-content">
            <div class="card">
                <h2>📊 LAPORAN PRODUKSI SAYA</h2>
                <div class="filter-bar">
                    <div class="form-group">
                        <label>Filter Tanggal</label>
                        <input type="date" id="filterTanggal">
                    </div>
                    <div class="form-group">
                        <label>Filter Bulan</label>
                        <input type="month" id="filterBulan">
                    </div>
                    <button class="btn btn-small" onclick="loadLaporan()">🔍 TAMPILKAN</button>
                    <button class="btn btn-small btn-warning" onclick="resetFilter()">🔄 RESET</button>
                    <button class="btn btn-small" onclick="exportToCSV()">📎 EXPORT CSV</button>
                </div>
                <div class="stats-grid" id="statsLaporan"></div>
                <div class="table-container">
                    <table id="laporanTable">
                        <thead>
                            <tr>
                                <th>Tanggal</th><th>Shift</th><th>Operator 1</th><th>Item</th>
                                <th>Ukuran</th><th>Hasil Qty</th><th>Jml Roll</th><th>Mesin</th>
                                <th>Reject Sablon</th><th>Reject Cutting</th><th>Jml Reject</th>
                                <th>Jml Bersih</th><th>Operator 2</th><th>Keterangan</th>
                            </tr>
                        </thead>
                        <tbody id="laporanBody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Tab Rekap Semua Operator (Admin Only) -->
        <div id="rekap" class="tab-content">
            <div class="card">
                <h2>👥 REKAP SEMUA OPERATOR</h2>
                <div class="filter-bar">
                    <div class="form-group">
                        <label>Filter Bulan</label>
                        <input type="month" id="rekapBulan">
                    </div>
                    <div class="form-group">
                        <label>Filter Shift</label>
                        <select id="rekapShift">
                            <option value="">Semua Shift</option>
                            <option value="Shift 1 (Pagi)">Shift 1 (Pagi)</option>
                            <option value="Shift 2 (Siang)">Shift 2 (Siang)</option>
                            <option value="Shift 3 (Malam)">Shift 3 (Malam)</option>
                        </select>
                    </div>
                    <button class="btn btn-small" onclick="loadRekapSemua()">📊 TAMPILKAN</button>
                    <button class="btn btn-small btn-warning" onclick="exportRekapCSV()">📎 EXPORT SEMUA</button>
                </div>
                <div class="table-container">
                    <table id="rekapTable">
                        <thead>
                            <tr>
                                <th>Rank</th><th>Username</th><th>Nama Operator</th><th>Total Hasil Qty</th>
                                <th>Total Reject</th><th>Total Bersih</th><th>Efisiensi</th><th>Jml Laporan</th>
                            </tr>
                        </thead>
                        <tbody id="rekapBody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Tab Manajemen Operator (Admin Only) -->
        <div id="operator" class="tab-content">
            <div class="card">
                <h2>👨‍👩‍👧‍👦 MANAJEMEN OPERATOR</h2>
                <div class="form-grid">
                    <div class="form-group">
                        <label>Username / NIK</label>
                        <input type="text" id="newUsername" placeholder="Username">
                    </div>
                    <div class="form-group">
                        <label>Nama Lengkap</label>
                        <input type="text" id="newNama" placeholder="Nama operator">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" id="newPassword" placeholder="Password">
                    </div>
                    <div class="form-group">
                        <label>Divisi</label>
                        <select id="newDivisi">
                            <option value="Produksi">Produksi</option>
                            <option value="Sablon">Sablon</option>
                            <option value="Cutting">Cutting</option>
                            <option value="Finishing">Finishing</option>
                        </select>
                    </div>
                </div>
                <button class="btn btn-small" onclick="tambahOperator()" style="margin-bottom: 20px;">➕ TAMBAH OPERATOR</button>
                
                <h3>📋 DAFTAR OPERATOR</h3>
                <div class="table-container">
                    <table id="operatorTable">
                        <thead>
                            <tr><th>Username</th><th>Nama</th><th>Divisi</th><th>Total Laporan</th><th>Total Hasil</th><th>Aksi</th></tr>
                        </thead>
                        <tbody id="operatorBody"></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <script>
        // ============ DATA STORAGE ============
        let operators = JSON.parse(localStorage.getItem('operators')) || [];
        let reports = JSON.parse(localStorage.getItem('reports')) || [];
        let currentUser = null;

        // ============ FUNGSI PERHITUNGAN OTOMATIS ============
        function hitungJumlahReject() {
            const rejectSablon = parseInt(document.getElementById('rejectSablon').value) || 0;
            const rejectCutting = parseInt(document.getElementById('rejectCutting').value) || 0;
            const jumlahReject = rejectSablon + rejectCutting;
            document.getElementById('jumlahReject').value = jumlahReject;
            hitungJumlahBersih();
        }

        function hitungJumlahBersih() {
            const hasilQty = parseInt(document.getElementById('hasilQty').value) || 0;
            const jumlahReject = parseInt(document.getElementById('jumlahReject').value) || 0;
            const jumlahBersih = hasilQty - jumlahReject;
            document.getElementById('jumlahBersih').value = jumlahBersih >= 0 ? jumlahBersih : 0;
        }

        // ============ INISIALISASI DATA DEFAULT ============
        function initDefaultData() {
            if (operators.length === 0) {
                operators = [
                    { username: 'admin', nama: 'Administrator', password: 'admin123', role: 'admin', divisi: 'Management', createdAt: new Date().toISOString() },
                    { username: 'OP001', nama: 'Budi Santoso', password: 'op001', role: 'operator', divisi: 'Produksi', createdAt: new Date().toISOString() },
                    { username: 'OP002', nama: 'Siti Nurhaliza', password: 'op002', role: 'operator', divisi: 'Sablon', createdAt: new Date().toISOString() },
                    { username: 'OP003', nama: 'Ahmad Wijaya', password: 'op003', role: 'operator', divisi: 'Cutting', createdAt: new Date().toISOString() },
                    { username: 'OP004', nama: 'Dewi Kartika', password: 'op004', role: 'operator', divisi: 'Finishing', createdAt: new Date().toISOString() },
                    { username: 'OP005', nama: 'Eko Prasetyo', password: 'op005', role: 'operator', divisi: 'Produksi', createdAt: new Date().toISOString() }
                ];
                localStorage.setItem('operators', JSON.stringify(operators));
            }

            // Contoh data jika kosong
            if (reports.length === 0) {
                const today = new Date().toISOString().split('T')[0];
                for (let i = 1; i <= 5; i++) {
                    reports.push({
                        id: Date.now() + i,
                        tanggal: today,
                        shift: 'Shift 1 (Pagi)',
                        operator1: `Operator ${i}`,
                        item: `Produk ${i}`,
                        ukuran: 'M',
                        hasilQty: Math.floor(Math.random() * 500) + 100,
                        jumlahRoll: Math.floor(Math.random() * 20) + 1,
                        mesin: `Mesin ${i}`,
                        rejectSablon: Math.floor(Math.random() * 10),
                        rejectCutting: Math.floor(Math.random() * 10),
                        jumlahReject: 0,
                        jumlahBersih: 0,
                        operator2: '',
                        keterangan: '',
                        createdBy: `OP00${i}`,
                        createdAt: new Date().toISOString()
                    });
                }
                // Hitung ulang reject dan bersih
                reports.forEach(r => {
                    r.jumlahReject = r.rejectSablon + r.rejectCutting;
                    r.jumlahBersih = r.hasilQty - r.jumlahReject;
                });
                localStorage.setItem('reports', JSON.stringify(reports));
            }
        }

        // ============ LOGIN ============
        function login(username, password) {
            const user = operators.find(o => o.username === username && o.password === password);
            if (user) {
                currentUser = user;
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                showApp();
                showAlert(`Selamat datang, ${user.nama}!`, 'success');
                return true;
            }
            showAlert('Username atau password salah!', 'error');
            return false;
        }

        function logout() {
            currentUser = null;
            localStorage.removeItem('currentUser');
            document.getElementById('loginPage').style.display = 'flex';
            document.getElementById('appContainer').style.display = 'none';
        }

        function showApp() {
            document.getElementById('loginPage').style.display = 'none';
            document.getElementById('appContainer').style.display = 'block';
            
            const roleText = currentUser.role === 'admin' ? '👑 ADMIN' : '👤 OPERATOR';
            document.getElementById('userRoleBadge').innerHTML = roleText;
            document.getElementById('userNameDisplay').innerHTML = `${currentUser.nama} (${currentUser.username})`;
            
            setupTabs();
            init();
        }

        // ============ SETUP TABS ============
        function setupTabs() {
            const tabsContainer = document.getElementById('tabsContainer');
            const tabs = [
                { id: 'input', name: '📝 INPUT PRODUKSI', roles: ['admin', 'operator'] },
                { id: 'laporan', name: '📊 LAPORAN SAYA', roles: ['admin', 'operator'] }
            ];
            
            if (currentUser.role === 'admin') {
                tabs.push({ id: 'rekap', name: '👥 REKAP OPERATOR', roles: ['admin'] });
                tabs.push({ id: 'operator', name: '👨‍👩‍👧‍👦 MANAJEMEN', roles: ['admin'] });
            }
            
            tabsContainer.innerHTML = tabs.map(tab => 
                `<button class="tab-btn" onclick="switchTab('${tab.id}')">${tab.name}</button>`
            ).join('');
            
            switchTab('input');
        }

        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            
            const targetTab = document.getElementById(tabName);
            if (targetTab) targetTab.classList.add('active');
            
            if (tabName === 'laporan') loadLaporan();
            if (tabName === 'rekap') loadRekapSemua();
            if (tabName === 'operator') loadDaftarOperator();
        }

        // ============ INIT ============
        function init() {
            document.getElementById('tanggal').valueAsDate = new Date();
            
            // Event listener untuk hitung otomatis
            document.getElementById('hasilQty').addEventListener('input', hitungJumlahBersih);
            document.getElementById('rejectSablon').addEventListener('input', hitungJumlahReject);
            document.getElementById('rejectCutting').addEventListener('input', hitungJumlahReject);
            
            document.getElementById('productionForm').addEventListener('submit', function(e) {
                e.preventDefault();
                simpanLaporan();
            });
        }

        function resetForm() {
            document.getElementById('productionForm').reset();
            document.getElementById('tanggal').valueAsDate = new Date();
            document.getElementById('jumlahReject').value = '';
            document.getElementById('jumlahBersih').value = '';
        }

        // ============ SIMPAN LAPORAN ============
        function simpanLaporan() {
            const rejectSablon = parseInt(document.getElementById('rejectSablon').value) || 0;
            const rejectCutting = parseInt(document.getElementById('rejectCutting').value) || 0;
            const jumlahReject = rejectSablon + rejectCutting;
            const hasilQty = parseInt(document.getElementById('hasilQty').value) || 0;
            const jumlahBersih = hasilQty - jumlahReject;
            
            const data = {
                id: Date.now(),
                tanggal: document.getElementById('tanggal').value,
                shift: document.getElementById('shift').value,
                operator1: document.getElementById('operator1').value,
                item: document.getElementById('item').value,
                ukuran: document.getElementById('ukuran').value,
                hasilQty: hasilQty,
                jumlahRoll: parseInt(document.getElementById('jumlahRoll').value) || 0,
                mesin: document.getElementById('mesin').value,
                rejectSablon: rejectSablon,
                rejectCutting: rejectCutting,
                jumlahReject: jumlahReject,
                jumlahBersih: jumlahBersih >= 0 ? jumlahBersih : 0,
                operator2: document.getElementById('operator2').value,
                keterangan: document.getElementById('keterangan').value,
                createdBy: currentUser.username,
                createdByName: currentUser.nama,
                createdAt: new Date().toISOString()
            };
            
            reports.push(data);
            localStorage.setItem('reports', JSON.stringify(reports));
            
            showAlert('Laporan berhasil disimpan!', 'success');
            resetForm();
            
            if (currentUser.role === 'admin') {
                loadRekapSemua();
            }
        }

        // ============ LOAD LAPORAN PRIBADI ============
        function loadLaporan() {
            let filtered = reports.filter(r => r.createdBy === currentUser.username);
            
            const filterTanggal = document.getElementById('filterTanggal').value;
            const filterBulan = document.getElementById('filterBulan').value;
            
            if (filterTanggal) {
                filtered = filtered.filter(r => r.tanggal === filterTanggal);
            }
            if (filterBulan) {
                filtered = filtered.filter(r => r.tanggal.startsWith(filterBulan));
            }
            
            // Statistik
            const totalHasil = filtered.reduce((s, r) => s + r.hasilQty, 0);
            const totalReject = filtered.reduce((s, r) => s + r.jumlahReject, 0);
            const totalBersih = filtered.reduce((s, r) => s + r.jumlahBersih, 0);
            const efisiensi = totalHasil > 0 ? ((totalBersih / totalHasil) * 100).toFixed(1) : 0;
            
            document.getElementById('statsLaporan').innerHTML = `
                <div class="stat-card"><h3>Total Hasil Qty</h3><div class="value">${totalHasil.toLocaleString()}</div></div>
                <div class="stat-card"><h3>Total Reject</h3><div class="value">${totalReject.toLocaleString()}</div></div>
                <div class="stat-card"><h3>Total Bersih</h3><div class="value">${totalBersih.toLocaleString()}</div></div>
                <div class="stat-card"><h3>Efisiensi</h3><div class="value">${efisiensi}%</div></div>
            `;
            
            const tbody = document.getElementById('laporanBody');
            tbody.innerHTML = '';
            
            filtered.sort((a,b) => b.tanggal.localeCompare(a.tanggal));
            filtered.forEach(r => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${r.tanggal}</td><td>${r.shift}</td><td>${r.operator1}</td><td>${r.item}</td>
                    <td>${r.ukuran || '-'}</td><td>${r.hasilQty.toLocaleString()}</td><td>${r.jumlahRoll}</td>
                    <td>${r.mesin || '-'}</td><td>${r.rejectSablon}</td><td>${r.rejectCutting}</td>
                    <td>${r.jumlahReject}</td><td>${r.jumlahBersih.toLocaleString()}</td>
                    <td>${r.operator2 || '-'}</td><td>${r.keterangan || '-'}</td>
                `;
            });
            
            if (filtered.length === 0) {
                tbody.innerHTML = '<tr><td colspan="14" style="text-align:center">Belum ada data</td></tr>';
            }
        }

        function resetFilter() {
            document.getElementById('filterTanggal').value = '';
            document.getElementById('filterBulan').value = '';
            loadLaporan();
        }

        // ============ REKAP SEMUA OPERATOR (ADMIN) ============
        function loadRekapSemua() {
            const bulan = document.getElementById('rekapBulan').value || new Date().toISOString().slice(0, 7);
            const shift = document.getElementById('rekapShift').value;
            document.getElementById('rekapBulan').value = bulan;
            
            let filtered = reports.filter(r => r.tanggal.startsWith(bulan));
            if (shift) filtered = filtered.filter(r => r.shift === shift);
            
            const operatorStats = {};
            filtered.forEach(r => {
                if (!operatorStats[r.createdBy]) {
                    const op = operators.find(o => o.username === r.createdBy);
                    operatorStats[r.createdBy] = {
                        username: r.createdBy,
                        nama: op ? op.nama : r.createdByName,
                        totalHasil: 0,
                        totalReject: 0,
                        totalBersih: 0,
                        count: 0
                    };
                }
                operatorStats[r.createdBy].totalHasil += r.hasilQty;
                operatorStats[r.createdBy].totalReject += r.jumlahReject;
                operatorStats[r.createdBy].totalBersih += r.jumlahBersih;
                operatorStats[r.createdBy].count++;
            });
            
            const sorted = Object.values(operatorStats).sort((a,b) => 
                (b.totalBersih / b.totalHasil) - (a.totalBersih / a.totalHasil)
            );
            
            const tbody = document.getElementById('rekapBody');
            tbody.innerHTML = '';
            
            sorted.forEach((stat, idx) => {
                const efisiensi = stat.totalHasil > 0 ? ((stat.totalBersih / stat.totalHasil) * 100).toFixed(1) : 0;
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${idx + 1}</td>
                    <td>${stat.username}</td>
                    <td>${stat.nama}</td>
                    <td>${stat.totalHasil.toLocaleString()}</td>
                    <td>${stat.totalReject.toLocaleString()}</td>
                    <td>${stat.totalBersih.toLocaleString()}</td>
                    <td class="${efisiensi >= 80 ? 'performance-good' : 'performance-bad'}" style="font-weight:bold">${efisiensi}%</td>
                    <td>${stat.count}</td>
                `;
            });
        }

        // ============ MANAJEMEN OPERATOR (ADMIN) ============
        function loadDaftarOperator() {
            const tbody = document.getElementById('operatorBody');
            tbody.innerHTML = '';
            
            const opList = operators.filter(o => o.role !== 'admin');
            opList.forEach(op => {
                const opReports = reports.filter(r => r.createdBy === op.username);
                const totalHasil = opReports.reduce((s, r) => s + r.hasilQty, 0);
                
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${op.username}</td>
                    <td>${op.nama}</td>
                    <td>${op.divisi}</td>
                    <td>${opReports.length}</td>
                    <td>${totalHasil.toLocaleString()}</td>
                    <td><button class="btn-small btn-danger" onclick="hapusOperator('${op.username}')">🗑️ Hapus</button></td>
                `;
            });
        }

        function tambahOperator() {
            const username = document.getElementById('newUsername').value.trim();
            const nama = document.getElementById('newNama').value.trim();
            const password = document.getElementById('newPassword').value;
            const divisi = document.getElementById('newDivisi').value;
            
            if (!username || !nama || !password) {
                showAlert('Semua field harus diisi!', 'error');
                return;
            }
            
            if (operators.find(o => o.username === username)) {
                showAlert('Username sudah terdaftar!', 'error');
                return;
            }
            
            operators.push({
                username: username,
                nama: nama,
                password: password,
                role: 'operator',
                divisi: divisi,
                createdAt: new Date().toISOString()
            });
            
            localStorage.setItem('operators', JSON.stringify(operators));
            loadDaftarOperator();
            
            document.getElementById('newUsername').value = '';
            document.getElementById('newNama').value = '';
            document.getElementById('newPassword').value = '';
            
            showAlert('Operator berhasil ditambahkan!', 'success');
        }

        function hapusOperator(username) {
            if (confirm(`Hapus operator ${username}? Semua laporannya juga akan dihapus.`)) {
                operators = operators.filter(o => o.username !== username);
                reports = reports.filter(r => r.createdBy !== username);
                localStorage.setItem('operators', JSON.stringify(operators));
                localStorage.setItem('reports', JSON.stringify(reports));
                loadDaftarOperator();
                showAlert('Operator berhasil dihapus!', 'success');
            }
        }

        // ============ EXPORT CSV ============
        function exportToCSV() {
            let filtered = reports.filter(r => r.createdBy === currentUser.username);
            let csv = "Tanggal,Shift,Operator1,Item,Ukuran,HasilQty,JumlahRoll,Mesin,RejectSablon,RejectCutting,JumlahReject,JumlahBersih,Operator2,Keterangan\n";
            filtered.forEach(r => {
                csv += `"${r.tanggal}","${r.shift}","${r.operator1}","${r.item}","${r.ukuran || ''}",${r.hasilQty},${r.jumlahRoll},"${r.mesin || ''}",${r.rejectSablon},${r.rejectCutting},${r.jumlahReject},${r.jumlahBersih},"${r.operator2 || ''}","${r.keterangan || ''}"\n`;
            });
            downloadCSV(csv, `laporan_${currentUser.username}_${new Date().toISOString().slice(0,10)}.csv`);
        }

        function exportRekapCSV() {
            const bulan = document.getElementById('rekapBulan').value || new Date().toISOString().slice(0, 7);
            let filtered = reports.filter(r => r.tanggal.startsWith(bulan));
            let csv = "Tanggal,Username,Nama,Shift,Item,HasilQty,Reject,JumlahBersih\n";
            filtered.forEach(r => {
                csv += `"${r.tanggal}","${r.createdBy}","${r.createdByName}","${r.shift}","${r.item}",${r.hasilQty},${r.jumlahReject},${r.jumlahBersih}\n`;
            });
            downloadCSV(csv, `rekap_${bulan}.csv`);
        }

        function downloadCSV(csv, filename) {
            const blob = new Blob(["\uFEFF" + csv], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = filename;
            a.click();
            URL.revokeObjectURL(url);
            showAlert('File berhasil diexport!', 'success');
        }

        function showAlert(message, type) {
            const alert = document.createElement('div');
            alert.className = `alert alert-${type}`;
            alert.textContent = message;
            document.body.appendChild(alert);
            setTimeout(() => alert.remove(), 3000);
        }

        // ============ START ============
        initDefaultData();
        
        const savedUser = localStorage.getItem('currentUser');
        if (savedUser) {
            currentUser = JSON.parse(savedUser);
            const userExists = operators.find(o => o.username === currentUser.username);
            if (userExists) {
                showApp();
            } else {
                localStorage.removeItem('currentUser');
            }
        }
        
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            login(username, password);
        });
    </script>
</body>
</html>
