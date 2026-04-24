<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>Smart Stock - Manajemen Stok Gudang</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Roboto, 'Helvetica Neue', system-ui, -apple-system, sans-serif;
            background: #f0f4f8;
            padding: 16px;
            min-width: 360px;
            color: #1e293b;
        }

        .app-container {
            max-width: 1300px;
            margin: 0 auto;
            background: white;
            border-radius: 32px;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.08);
            overflow: hidden;
            padding: 20px 18px 28px 18px;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 16px;
            padding-bottom: 12px;
            border-bottom: 2px solid #eef2f6;
        }
        h1 {
            font-size: 1.5rem;
            font-weight: 700;
            color: #0f3b2c;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .global-stock {
            background: #e9f4e8;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: 600;
            color: #2b6e3c;
        }

        /* Tab Utama */
        .tab-menu {
            display: flex;
            gap: 8px;
            margin: 16px 0 20px 0;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 8px;
            flex-wrap: wrap;
        }
        .tab-btn {
            background: transparent;
            color: #5b6e8c;
            border: none;
            padding: 10px 24px;
            font-size: 0.9rem;
            font-weight: 600;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.2s;
        }
        .tab-btn.active {
            background: #2c7a4d;
            color: white;
        }
        .tab-pane {
            display: none;
        }
        .tab-pane.active-pane {
            display: block;
        }

        /* Form Card */
        .form-card {
            background: #f8fafc;
            border-radius: 24px;
            padding: 18px;
            margin: 16px 0 20px 0;
            border: 1px solid #e2e8f0;
        }
        .form-row {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: flex-end;
        }
        .form-group {
            flex: 1;
            min-width: 140px;
        }
        .form-group label {
            display: block;
            font-size: 0.7rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: #5b6e8c;
            margin-bottom: 5px;
        }
        .input-with-icon {
            position: relative;
            display: flex;
            align-items: center;
        }
        .input-with-icon input, .input-with-icon select {
            width: 100%;
            padding: 10px 12px 10px 36px;
            font-size: 0.9rem;
            border: 1px solid #cbd5e1;
            border-radius: 18px;
            background: white;
        }
        .input-with-icon select {
            padding: 10px 12px 10px 36px;
        }
        .input-icon {
            position: absolute;
            left: 12px;
            font-size: 1rem;
            pointer-events: none;
        }
        button {
            background: #2c7a4d;
            border: none;
            color: white;
            font-weight: 600;
            padding: 10px 18px;
            border-radius: 40px;
            font-size: 0.85rem;
            cursor: pointer;
            transition: all 0.2s;
        }
        button:active {
            transform: scale(0.97);
        }
        .btn-outline {
            background: white;
            border: 1px solid #cbd5e1;
            color: #1e293b;
        }
        .btn-outline:hover {
            background: #f1f5f9;
        }
        .btn-danger {
            background: #dc2626;
        }
        .btn-danger:hover {
            background: #b91c1c;
        }
        .add-new-link {
            margin-top: 8px;
            font-size: 0.7rem;
            color: #2c7a4d;
            cursor: pointer;
            display: inline-block;
        }

        /* Ringkasan Stok */
        .stock-summary {
            background: #f0fdf4;
            border-radius: 20px;
            padding: 16px;
            margin: 16px 0;
            border: 1px solid #bbf7d0;
        }
        .summary-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.8rem;
        }
        .summary-table th, .summary-table td {
            padding: 8px;
            text-align: center;
            border-bottom: 1px solid #e2e8f0;
        }
        .summary-table th {
            background: #dcfce7;
        }
        .stock-tersedia {
            font-weight: 800;
            color: #15803d;
            background: #eef2ff;
            border-radius: 30px;
            padding: 4px 12px;
            display: inline-block;
        }

        /* Halaman Rekap (Tab Baru) - Tabel kecil tanpa scroll */
        .rekap-container {
            background: white;
            border-radius: 20px;
            padding: 8px;
            overflow-x: auto;
        }
        .rekap-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.7rem;
            min-width: 300px;
        }
        .rekap-table th, .rekap-table td {
            padding: 6px 4px;
            text-align: center;
            border: 1px solid #e2e8f0;
            font-size: 0.7rem;
        }
        .rekap-table th {
            background: #eef2f9;
            font-weight: 700;
        }
        .rekap-section-title {
            font-size: 0.85rem;
            font-weight: 700;
            margin: 16px 0 8px 0;
            color: #1e293b;
            background: #f1f5f9;
            padding: 6px 12px;
            border-radius: 20px;
        }

        /* Riwayat per Bulan */
        .month-section {
            margin-bottom: 28px;
            border: 1px solid #e2e8f0;
            border-radius: 20px;
            overflow: hidden;
        }
        .month-header {
            background: #1e293b;
            color: white;
            padding: 12px 16px;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
        }
        .month-table-wrapper {
            overflow-x: auto;
        }
        .month-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.75rem;
        }
        .month-table th, .month-table td {
            padding: 8px 6px;
            text-align: center;
            border-bottom: 1px solid #f0f4f9;
        }
        .month-table th {
            background: #eef2f9;
        }
        .row-masuk { background-color: #f0fdf4; border-left: 4px solid #22c55e; }
        .row-keluar { background-color: #fef2f2; border-left: 4px solid #ef4444; }
        .badge-masuk { background: #22c55e20; color: #166534; padding: 2px 8px; border-radius: 20px; font-size: 0.65rem; }
        .badge-keluar { background: #ef444420; color: #b91c1c; padding: 2px 8px; border-radius: 20px; font-size: 0.65rem; }
        .action-btn {
            background: none;
            border: none;
            font-size: 0.7rem;
            font-weight: 600;
            cursor: pointer;
            padding: 4px 10px;
            border-radius: 30px;
            margin: 0 2px;
        }
        .edit-btn { background: #e0e7ff; color: #1e40af; }
        .delete-btn { background: #fee2e2; color: #b91c1c; }

        .action-bar {
            background: white;
            border-radius: 28px;
            padding: 12px 16px;
            margin: 16px 0;
            border: 1px solid #e9edf2;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: space-between;
            align-items: center;
        }
        .search-section input {
            padding: 8px 16px;
            border-radius: 40px;
            border: 1px solid #cbd5e1;
            width: 220px;
        }
        .btn-group { display: flex; gap: 8px; flex-wrap: wrap; }
        .footer-note { font-size: 0.65rem; color: #6b7280; text-align: center; margin-top: 16px; }
        
        @media print { .no-print { display: none; } body { background: white; } }

        /* Modal */
        .edit-modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5); z-index: 1000;
            display: flex; align-items: center; justify-content: center;
        }
        .edit-modal-content {
            background: white; border-radius: 28px; padding: 24px;
            width: 500px; max-width: 90%;
        }
        .edit-form-group { margin-bottom: 16px; }
        .edit-form-group label { display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 5px; }
        .edit-form-group input, .edit-form-group select {
            width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 18px;
        }
        .edit-modal-buttons { display: flex; gap: 12px; margin-top: 20px; justify-content: flex-end; }
        .btn-cancel { background: #e2e8f0; color: #1e293b; }
    </style>
</head>
<body>
<div class="app-container">
    <div class="header">
        <h1>📦 Smart Stock</h1>
        <span class="global-stock" id="globalStockValue">Total Stok: 0</span>
    </div>

    <!-- Tab Menu Utama -->
    <div class="tab-menu no-print">
        <button class="tab-btn active" data-tab="masuk">Barang Masuk</button>
        <button class="tab-btn" data-tab="keluar">Barang Keluar</button>
        <button class="tab-btn" data-tab="rekap">📊 Rekap Bulanan</button>
    </div>

    <!-- Panel Barang Masuk -->
    <div id="tabMasuk" class="tab-pane active-pane">
        <div class="form-card">
            <div class="form-row">
                <div class="form-group">
                    <label>Tanggal Masuk</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📅</span>
                        <input type="date" id="tanggalMasuk">
                    </div>
                </div>
                <div class="form-group">
                    <label>Nama Barang</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📦</span>
                        <select id="namaBarangMasuk"><option value="">-- Pilih --</option></select>
                    </div>
                    <div class="add-new-link" onclick="showAddBarangModal('masuk')">+ Tambah Barang Baru</div>
                </div>
                <div class="form-group">
                    <label>Satuan</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📏</span>
                        <select id="satuanMasuk"><option value="">-- Pilih --</option></select>
                    </div>
                    <div class="add-new-link" onclick="showAddSatuanModal('masuk')">+ Tambah Satuan Baru</div>
                </div>
                <div class="form-group">
                    <label>Jumlah Masuk</label>
                    <div class="input-with-icon">
                        <span class="input-icon">🔢</span>
                        <input type="number" id="jumlahMasuk" value="1" min="1">
                    </div>
                </div>
                <div class="form-group">
                    <label>PIC</label>
                    <div class="input-with-icon">
                        <span class="input-icon">👤</span>
                        <input type="text" id="picMasuk" placeholder="Nama">
                    </div>
                </div>
                <button id="btnTambahMasuk">Tambah Masuk</button>
            </div>
        </div>
    </div>

    <!-- Panel Barang Keluar -->
    <div id="tabKeluar" class="tab-pane">
        <div class="form-card">
            <div class="form-row">
                <div class="form-group">
                    <label>Tanggal Keluar</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📅</span>
                        <input type="date" id="tanggalKeluar">
                    </div>
                </div>
                <div class="form-group">
                    <label>Nama Barang</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📦</span>
                        <select id="namaBarangKeluar"><option value="">-- Pilih --</option></select>
                    </div>
                    <div class="add-new-link" onclick="showAddBarangModal('keluar')">+ Tambah Barang Baru</div>
                </div>
                <div class="form-group">
                    <label>Satuan</label>
                    <div class="input-with-icon">
                        <span class="input-icon">📏</span>
                        <select id="satuanKeluar"><option value="">-- Pilih --</option></select>
                    </div>
                    <div class="add-new-link" onclick="showAddSatuanModal('keluar')">+ Tambah Satuan Baru</div>
                </div>
                <div class="form-group">
                    <label>Jumlah Keluar</label>
                    <div class="input-with-icon">
                        <span class="input-icon">🔢</span>
                        <input type="number" id="jumlahKeluar" value="1" min="1">
                    </div>
                </div>
                <div class="form-group">
                    <label>PIC</label>
                    <div class="input-with-icon">
                        <span class="input-icon">👤</span>
                        <input type="text" id="picKeluar" placeholder="Nama">
                    </div>
                </div>
                <button id="btnTambahKeluar" style="background:#dc2626;">Tambah Keluar</button>
            </div>
        </div>
    </div>

    <!-- Panel Rekap Bulanan (Halaman Baru) -->
    <div id="tabRekap" class="tab-pane">
        <div class="stock-summary" style="background:#f8fafc; border-color:#cbd5e1;">
            <h3 style="color:#1e293b; margin-bottom:12px;">📊 REKAP BULANAN - TOTAL MASUK & KELUAR</h3>
            <div id="rekapContainer" class="rekap-container">
                <div style="text-align:center; padding:20px;">Memuat data...</div>
            </div>
            <div style="margin-top:16px; padding:8px; background:#eef2ff; border-radius:16px;">
                <div style="font-size:0.7rem; color:#1e40af; text-align:center;">✅ Rekap per bulan: Total quantity barang masuk dan keluar, serta jumlah item / transaksi</div>
            </div>
        </div>
    </div>

    <!-- RINGKASAN STOK AKHIR (hanya tampil di tab masuk/keluar) -->
    <div class="stock-summary no-print" id="stockSummaryPanel">
        <h3>STOCK AKHIR PER NAMA BARANG (Masuk - Keluar)</h3>
        <div class="summary-table-wrapper">
            <table class="summary-table">
                <thead><tr><th>Nama Barang</th><th>Total Masuk</th><th>Total Keluar</th><th>Stok Tersedia</th><th>Satuan</th></tr></thead>
                <tbody id="summaryStockBody"><tr><td colspan="5">Belum ada data</td></tr></tbody>
            </table>
        </div>
    </div>

    <!-- Riwayat Transaksi & Aksi -->
    <div class="action-bar no-print">
        <div class="search-section">
            <div class="input-with-icon">
                <span class="input-icon">🔍</span>
                <input type="text" id="searchRiwayat" placeholder="Cari nama barang...">
            </div>
        </div>
        <div class="btn-group">
            <button id="printBtn" class="btn-outline">Print</button>
            <button id="exportExcelBtn" class="btn-outline">Export Excel</button>
            <button id="resetAllBtn" class="btn-danger">Reset Semua</button>
        </div>
    </div>

    <div id="riwayatContainer" class="riwayat-container"></div>
    <div class="footer-note no-print">Stok akhir = Total Masuk - Total Keluar | Klik bulan untuk expand/collapse | Data tersimpan otomatis</div>
</div>

<!-- Modal Tambah Barang/Satuan -->
<div id="modalOverlay" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.5); z-index:1000; align-items:center; justify-content:center;">
    <div style="background:white; padding:24px; border-radius:24px; width:300px;">
        <h3 id="modalTitle" style="margin-bottom:16px;">Tambah Baru</h3>
        <input type="text" id="modalInput" placeholder="Nama..." style="width:100%; padding:10px; border-radius:40px; border:1px solid #ccc; margin-bottom:16px;">
        <div style="display:flex; gap:10px; justify-content:flex-end;">
            <button id="modalCancelBtn" style="background:#e2e8f0;">Batal</button>
            <button id="modalSaveBtn" style="background:#2c7a4d;">Simpan</button>
        </div>
    </div>
</div>

<script>
    // ======================== DATA ========================
    let transactions = [];
    let nextId = 1;
    let masterBarang = [];
    let masterSatuan = [];
    let modalContext = { formType: 'masuk', dataType: 'barang' };

    // DOM
    const tanggalMasuk = document.getElementById('tanggalMasuk');
    const namaBarangMasuk = document.getElementById('namaBarangMasuk');
    const satuanMasuk = document.getElementById('satuanMasuk');
    const jumlahMasuk = document.getElementById('jumlahMasuk');
    const picMasuk = document.getElementById('picMasuk');
    const btnTambahMasuk = document.getElementById('btnTambahMasuk');

    const tanggalKeluar = document.getElementById('tanggalKeluar');
    const namaBarangKeluar = document.getElementById('namaBarangKeluar');
    const satuanKeluar = document.getElementById('satuanKeluar');
    const jumlahKeluar = document.getElementById('jumlahKeluar');
    const picKeluar = document.getElementById('picKeluar');
    const btnTambahKeluar = document.getElementById('btnTambahKeluar');

    const searchRiwayat = document.getElementById('searchRiwayat');
    const riwayatContainer = document.getElementById('riwayatContainer');
    const summaryStockBody = document.getElementById('summaryStockBody');
    const globalStockValue = document.getElementById('globalStockValue');
    const rekapContainer = document.getElementById('rekapContainer');
    const printBtn = document.getElementById('printBtn');
    const exportExcelBtn = document.getElementById('exportExcelBtn');
    const resetAllBtn = document.getElementById('resetAllBtn');

    const modalOverlay = document.getElementById('modalOverlay');
    const modalInput = document.getElementById('modalInput');
    const modalCancelBtn = document.getElementById('modalCancelBtn');
    const modalSaveBtn = document.getElementById('modalSaveBtn');

    const tabBtns = document.querySelectorAll('.tab-btn');
    const tabMasukDiv = document.getElementById('tabMasuk');
    const tabKeluarDiv = document.getElementById('tabKeluar');
    const tabRekapDiv = document.getElementById('tabRekap');
    const stockSummaryPanel = document.getElementById('stockSummaryPanel');

    // Helper
    function formatTanggal(dateString) {
        if (!dateString) return '-';
        const parts = dateString.split('-');
        if (parts.length === 3) return `${parts[2]}/${parts[1]}/${parts[0]}`;
        return dateString;
    }

    function setDefaultDates() {
        const today = new Date().toISOString().slice(0,10);
        if (!tanggalMasuk.value) tanggalMasuk.value = today;
        if (!tanggalKeluar.value) tanggalKeluar.value = today;
    }

    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, m => m === '&' ? '&amp;' : (m === '<' ? '&lt;' : '&gt;'));
    }

    // Master Data
    function loadMasterData() {
        const savedBarang = localStorage.getItem("smartStockMasterBarang");
        masterBarang = savedBarang ? JSON.parse(savedBarang) : ["Kabel USB", "Plastik OPP", "Magnet", "Box Kardus", "Tape Lakban"];
        const savedSatuan = localStorage.getItem("smartStockMasterSatuan");
        masterSatuan = savedSatuan ? JSON.parse(savedSatuan) : ["pcs", "lembar", "buah", "box", "roll", "kg", "meter"];
    }
    function saveMasterData() {
        localStorage.setItem("smartStockMasterBarang", JSON.stringify(masterBarang));
        localStorage.setItem("smartStockMasterSatuan", JSON.stringify(masterSatuan));
    }
    function renderDropdowns() {
        let barangHtml = '<option value="">-- Pilih Barang --</option>';
        masterBarang.forEach(b => barangHtml += `<option value="${escapeHtml(b)}">${escapeHtml(b)}</option>`);
        namaBarangMasuk.innerHTML = barangHtml;
        namaBarangKeluar.innerHTML = barangHtml;
        let satuanHtml = '<option value="">-- Pilih Satuan --</option>';
        masterSatuan.forEach(s => satuanHtml += `<option value="${escapeHtml(s)}">${escapeHtml(s)}</option>`);
        satuanMasuk.innerHTML = satuanHtml;
        satuanKeluar.innerHTML = satuanHtml;
    }

    // Modal
    function showAddBarangModal(formType) { modalContext = { formType, dataType: 'barang' }; modalOverlay.style.display = 'flex'; }
    function showAddSatuanModal(formType) { modalContext = { formType, dataType: 'satuan' }; modalOverlay.style.display = 'flex'; }
    function closeModal() { modalOverlay.style.display = 'none'; }
    function saveModalData() {
        const newValue = modalInput.value.trim();
        if (!newValue) { alert('Nama tidak boleh kosong!'); return; }
        if (modalContext.dataType === 'barang') {
            if (masterBarang.includes(newValue)) { alert('Barang sudah ada!'); closeModal(); return; }
            masterBarang.push(newValue);
            masterBarang.sort((a,b) => a.localeCompare(b, 'id'));
            saveMasterData(); renderDropdowns();
            if (modalContext.formType === 'masuk') namaBarangMasuk.value = newValue;
            else namaBarangKeluar.value = newValue;
        } else {
            if (masterSatuan.includes(newValue)) { alert('Satuan sudah ada!'); closeModal(); return; }
            masterSatuan.push(newValue);
            masterSatuan.sort();
            saveMasterData(); renderDropdowns();
            if (modalContext.formType === 'masuk') satuanMasuk.value = newValue;
            else satuanKeluar.value = newValue;
        }
        closeModal();
        showToast(`${modalContext.dataType === 'barang' ? 'Barang' : 'Satuan'} "${newValue}" ditambahkan`, 'success');
    }

    // Stok Summary
    function getStockSummary() {
        const map = new Map();
        for (const trx of transactions) {
            const key = `${trx.barang.toLowerCase()}|${trx.satuan.toLowerCase()}`;
            if (!map.has(key)) map.set(key, { namaBarang: trx.barang, satuan: trx.satuan, totalMasuk: 0, totalKeluar: 0 });
            const data = map.get(key);
            if (trx.tipe === 'masuk') data.totalMasuk += trx.jumlah;
            else data.totalKeluar += trx.jumlah;
        }
        const summary = Array.from(map.values()).map(item => ({ ...item, stokAkhir: item.totalMasuk - item.totalKeluar }));
        summary.sort((a,b) => a.namaBarang.localeCompare(b.namaBarang, 'id'));
        return summary;
    }
    function renderStockSummary() {
        const summary = getStockSummary();
        if (summary.length === 0) { summaryStockBody.innerHTML = '<tr><td colspan="5">Belum ada data</td></tr>'; globalStockValue.innerText = 'Total Stok: 0'; return; }
        let html = '';
        summary.forEach(item => {
            html += `<tr><td style="font-weight:700;">${escapeHtml(item.namaBarang)}</td><td>${item.totalMasuk}</td><td>${item.totalKeluar}</td><td><span class="stock-tersedia">${item.stokAkhir}</span></td><td>${escapeHtml(item.satuan)}</td></tr>`;
        });
        summaryStockBody.innerHTML = html;
        globalStockValue.innerText = `Total Stok: ${summary.reduce((s,item) => s + item.stokAkhir, 0)}`;
    }

    // REKAP BULANAN: total quantity masuk/keluar, jumlah transaksi, jumlah nama barang unik
    function renderRekapBulanan() {
        const grouped = new Map(); // key: bulan-tahun
        for (const trx of transactions) {
            const date = new Date(trx.tanggal);
            const monthYear = `${date.getFullYear()}-${String(date.getMonth()+1).padStart(2,'0')}`;
            const monthName = date.toLocaleDateString('id-ID', { year: 'numeric', month: 'long' });
            if (!grouped.has(monthYear)) {
                grouped.set(monthYear, { name: monthName, totalMasukQty: 0, totalKeluarQty: 0, totalMasukTrans: 0, totalKeluarTrans: 0, barangSet: new Set() });
            }
            const data = grouped.get(monthYear);
            if (trx.tipe === 'masuk') {
                data.totalMasukQty += trx.jumlah;
                data.totalMasukTrans++;
            } else {
                data.totalKeluarQty += trx.jumlah;
                data.totalKeluarTrans++;
            }
            data.barangSet.add(trx.barang.toLowerCase());
        }
        if (grouped.size === 0) {
            rekapContainer.innerHTML = '<div style="text-align:center; padding:20px;">Belum ada data transaksi</div>';
            return;
        }
        const sorted = Array.from(grouped.entries()).sort((a,b) => b[0].localeCompare(a[0]));
        let html = '<table class="rekap-table"><thead><tr><th>Bulan</th><th>Total Masuk (Qty)</th><th>Total Keluar (Qty)</th><th>Selisih</th><th>Jumlah Transaksi Masuk</th><th>Jumlah Transaksi Keluar</th><th>Jenis Barang Unik</th></tr></thead><tbody>';
        for (const [key, val] of sorted) {
            const selisih = val.totalMasukQty - val.totalKeluarQty;
            html += `<tr>
                        <td><strong>${val.name}</strong></td>
                        <td style="color:#15803d;">${val.totalMasukQty}</td>
                        <td style="color:#b91c1c;">${val.totalKeluarQty}</td>
                        <td style="font-weight:bold;">${selisih}</td>
                        <td>${val.totalMasukTrans}</td>
                        <td>${val.totalKeluarTrans}</td>
                        <td>${val.barangSet.size}</td>
                     </tr>`;
        }
        html += `</tbody></table><div style="margin-top:12px; font-size:0.65rem; text-align:center; color:#475569;">📌 Keterangan: Selisih = Total Masuk - Total Keluar | Jenis Barang Unik = jumlah nama barang berbeda dalam bulan tersebut</div>`;
        rekapContainer.innerHTML = html;
    }

    // Riwayat per Bulan
    function renderRiwayatPerBulan() {
        const keyword = searchRiwayat.value.trim().toLowerCase();
        let filtered = keyword ? transactions.filter(t => t.barang.toLowerCase().includes(keyword)) : transactions;
        if (filtered.length === 0) { riwayatContainer.innerHTML = '<div class="empty-data">Tidak ada transaksi</div>'; return; }
        const grouped = {};
        filtered.forEach(trx => {
            const date = new Date(trx.tanggal);
            const monthYear = `${date.getFullYear()}-${String(date.getMonth()+1).padStart(2,'0')}`;
            const monthName = date.toLocaleDateString('id-ID', { year: 'numeric', month: 'long' });
            if (!grouped[monthYear]) grouped[monthYear] = { name: monthName, data: [] };
            grouped[monthYear].data.push(trx);
        });
        const sortedMonths = Object.keys(grouped).sort((a,b) => b.localeCompare(a));
        let html = '';
        for (const monthKey of sortedMonths) {
            const month = grouped[monthKey];
            month.data.sort((a,b) => a.tanggal.localeCompare(b.tanggal));
            let rows = '';
            for (const trx of month.data) {
                const rowClass = trx.tipe === 'masuk' ? 'row-masuk' : 'row-keluar';
                const tipeBadge = trx.tipe === 'masuk' ? '<span class="badge-masuk">MASUK</span>' : '<span class="badge-keluar">KELUAR</span>';
                rows += `<tr class="${rowClass}">
                            <td>${formatTanggal(trx.tanggal)}</td>
                            <td>${tipeBadge}</td>
                            <td><strong>${escapeHtml(trx.barang)}</strong></td>
                            <td>${trx.jumlah}</td>
                            <td>${escapeHtml(trx.satuan)}</td>
                            <td>${escapeHtml(trx.pic)}</td>
                            <td class="no-print">
                                <button class="action-btn edit-btn" data-id="${trx.id}">Edit</button>
                                <button class="action-btn delete-btn" data-id="${trx.id}">Hapus</button>
                            </td>
                          </tr>`;
            }
            html += `<div class="month-section">
                        <div class="month-header" onclick="toggleMonth(this)"><span>📅 ${month.name}</span><span>▼</span></div>
                        <div class="month-table-wrapper"><table class="month-table"><thead><tr><th>Tanggal</th><th>Tipe</th><th>Barang</th><th>Jumlah</th><th>Satuan</th><th>PIC</th><th>Aksi</th></tr></thead><tbody>${rows}</tbody></table></div>
                     </div>`;
        }
        riwayatContainer.innerHTML = html;
        document.querySelectorAll('.edit-btn').forEach(btn => btn.addEventListener('click', (e) => openEditModal(parseInt(btn.dataset.id))));
        document.querySelectorAll('.delete-btn').forEach(btn => btn.addEventListener('click', (e) => deleteTransaction(parseInt(btn.dataset.id))));
    }

    window.toggleMonth = function(header) {
        const wrapper = header.nextElementSibling;
        if (wrapper.style.display === 'none') { wrapper.style.display = 'block'; header.querySelector('span:last-child').innerHTML = '▼'; }
        else { wrapper.style.display = 'none'; header.querySelector('span:last-child').innerHTML = '▶'; }
    };

    function openEditModal(id) {
        const trx = transactions.find(t => t.id === id);
        if (!trx) return;
        const modalDiv = document.createElement('div'); modalDiv.className = 'edit-modal';
        modalDiv.innerHTML = `<div class="edit-modal-content"><h3>Edit Transaksi</h3>
            <div class="edit-form-group"><label>Tanggal</label><input type="date" id="editTanggal" value="${trx.tanggal}"></div>
            <div class="edit-form-group"><label>Nama Barang</label><select id="editBarang">${masterBarang.map(b => `<option value="${escapeHtml(b)}" ${b===trx.barang?'selected':''}>${escapeHtml(b)}</option>`).join('')}</select></div>
            <div class="edit-form-group"><label>Satuan</label><select id="editSatuan">${masterSatuan.map(s => `<option value="${escapeHtml(s)}" ${s===trx.satuan?'selected':''}>${escapeHtml(s)}</option>`).join('')}</select></div>
            <div class="edit-form-group"><label>Jumlah</label><input type="number" id="editJumlah" value="${trx.jumlah}" min="1"></div>
            <div class="edit-form-group"><label>PIC</label><input type="text" id="editPic" value="${escapeHtml(trx.pic)}"></div>
            <div class="edit-modal-buttons"><button id="editCancelBtn" class="btn-cancel">Batal</button><button id="editSaveBtn" style="background:#2c7a4d;">Simpan</button></div></div>`;
        document.body.appendChild(modalDiv);
        document.getElementById('editCancelBtn').addEventListener('click', () => modalDiv.remove());
        document.getElementById('editSaveBtn').addEventListener('click', () => {
            const newTanggal = document.getElementById('editTanggal').value;
            const newBarang = document.getElementById('editBarang').value;
            const newSatuan = document.getElementById('editSatuan').value;
            const newJumlah = parseInt(document.getElementById('editJumlah').value);
            const newPic = document.getElementById('editPic').value.trim();
            if (!newTanggal || !newBarang || !newSatuan || isNaN(newJumlah) || newJumlah<=0 || !newPic) { showToast("Data tidak lengkap","info"); return; }
            if (trx.tipe === 'keluar') {
                let stok = 0;
                for (const t of transactions) if (t.id !== id && t.barang.toLowerCase()===newBarang.toLowerCase() && t.satuan.toLowerCase()===newSatuan.toLowerCase()) stok += t.tipe==='masuk' ? t.jumlah : -t.jumlah;
                if (stok < newJumlah) { showToast(`Stok ${newBarang} tidak mencukupi! Tersedia: ${stok}`,"info"); return; }
            }
            const idx = transactions.findIndex(t=>t.id===id);
            if(idx!==-1) transactions[idx] = {...transactions[idx], tanggal:newTanggal, barang:newBarang, satuan:newSatuan, jumlah:newJumlah, pic:newPic};
            saveToLocal(); renderRiwayatPerBulan(); renderStockSummary(); renderRekapBulanan(); showToast("Data diperbarui","success");
            modalDiv.remove();
        });
    }

    function deleteTransaction(id) {
        if (confirm("Hapus transaksi ini?")) {
            transactions = transactions.filter(t => t.id !== id);
            if (transactions.length===0) nextId=1; else nextId = Math.max(...transactions.map(t=>t.id),0)+1;
            saveToLocal(); renderRiwayatPerBulan(); renderStockSummary(); renderRekapBulanan(); showToast("Transaksi dihapus","success");
        }
    }

    function addMasuk() {
        const tanggal = tanggalMasuk.value, barang = namaBarangMasuk.value, satuan = satuanMasuk.value, jumlah = parseInt(jumlahMasuk.value), pic = picMasuk.value.trim();
        if (!tanggal || !barang || !satuan || isNaN(jumlah) || jumlah<=0 || !pic) { showToast("Lengkapi semua field","info"); return; }
        transactions.push({ id: nextId++, tanggal, tipe: 'masuk', barang, jumlah, satuan, pic });
        resetFormMasuk(); saveAllAndRender(); showToast("Barang Masuk ditambahkan","success");
    }

    function addKeluar() {
        const tanggal = tanggalKeluar.value, barang = namaBarangKeluar.value, satuan = satuanKeluar.value, jumlah = parseInt(jumlahKeluar.value), pic = picKeluar.value.trim();
        if (!tanggal || !barang || !satuan || isNaN(jumlah) || jumlah<=0 || !pic) { showToast("Lengkapi semua field","info"); return; }
        let stok = 0;
        for (const trx of transactions) if (trx.barang.toLowerCase()===barang.toLowerCase() && trx.satuan.toLowerCase()===satuan.toLowerCase()) stok += trx.tipe==='masuk' ? trx.jumlah : -trx.jumlah;
        if (stok < jumlah) { showToast(`Stok ${barang} (${satuan}) tidak mencukupi! Tersedia: ${stok}`,"info"); return; }
        transactions.push({ id: nextId++, tanggal, tipe: 'keluar', barang, jumlah, satuan, pic });
        resetFormKeluar(); saveAllAndRender(); showToast("Barang Keluar dicatat","success");
    }

    function resetFormMasuk() { const today = new Date().toISOString().slice(0,10); tanggalMasuk.value = today; namaBarangMasuk.value = ''; satuanMasuk.value = ''; jumlahMasuk.value = '1'; picMasuk.value = ''; }
    function resetFormKeluar() { const today = new Date().toISOString().slice(0,10); tanggalKeluar.value = today; namaBarangKeluar.value = ''; satuanKeluar.value = ''; jumlahKeluar.value = '1'; picKeluar.value = ''; }

    function saveAllAndRender() { saveToLocal(); renderRiwayatPerBulan(); renderStockSummary(); renderRekapBulanan(); }
    function showToast(msg, type) { const toast = document.createElement('div'); toast.innerText = msg; toast.style.cssText = 'position:fixed; bottom:20px; left:50%; transform:translateX(-50%); background:'+(type==='success'?'#2c7a4d':'#334155')+'; color:white; padding:10px 20px; border-radius:40px; font-size:0.85rem; z-index:9999;'; document.body.appendChild(toast); setTimeout(()=>{toast.style.opacity='0'; setTimeout(()=>toast.remove(),300);},2000); }

    function exportToExcel() {
        const summary = getStockSummary();
        let excel = `<html><head><meta charset="UTF-8"><title>Laporan Stok</title></head><body><h2>Laporan Stok Akhir</h2><table border="1"><thead><tr><th>Barang</th><th>Total Masuk</th><th>Total Keluar</th><th>Stok</th><th>Satuan</th></tr></thead><tbody>${summary.map(s=>`<tr><td>${s.namaBarang}</td><td>${s.totalMasuk}</td><td>${s.totalKeluar}</td><td><strong>${s.stokAkhir}</strong></td><td>${s.satuan}</td></tr>`).join('')}</tbody></table><h3>Riwayat</h3><table border="1"><thead><tr><th>Tanggal</th><th>Tipe</th><th>Barang</th><th>Jumlah</th><th>Satuan</th><th>PIC</th></tr></thead><tbody>${transactions.map(t=>`<tr><td>${formatTanggal(t.tanggal)}</td><td>${t.tipe.toUpperCase()}</td><td>${t.barang}</td><td>${t.jumlah}</td><td>${t.satuan}</td><td>${t.pic}</td></tr>`).join('')}</tbody></table></body></html>`;
        const blob = new Blob([excel], {type:'application/vnd.ms-excel'}); const link = document.createElement('a'); link.href = URL.createObjectURL(blob); link.download = `Laporan_Stok_${new Date().toISOString().slice(0,19)}.xls`; link.click(); URL.revokeObjectURL(link.href); showToast("Export Excel berhasil","success");
    }
    function printReport() { window.print(); }
    function resetAllData() { if(confirm("Hapus semua transaksi?")){ transactions=[]; nextId=1; saveToLocal(); renderRiwayatPerBulan(); renderStockSummary(); renderRekapBulanan(); showToast("Semua data direset","success"); } }

    function saveToLocal() { localStorage.setItem("smartStockTransaksi", JSON.stringify({ transactions, nextId })); }
    function loadFromLocal() {
        const saved = localStorage.getItem("smartStockTransaksi");
        if(saved) { try { const p = JSON.parse(saved); if(p.transactions) { transactions = p.transactions; nextId = p.nextId || (transactions.length?Math.max(...transactions.map(t=>t.id),0)+1:1); } else initSampleData(); } catch(e){ initSampleData(); } } else initSampleData();
        renderRiwayatPerBulan(); renderStockSummary(); renderRekapBulanan();
    }
    function initSampleData() {
        transactions = [];
        const today = new Date().toISOString().slice(0,10);
        const yesterday = new Date(Date.now()-86400000).toISOString().slice(0,10);
        const lastMonth = new Date(Date.now()-30*86400000).toISOString().slice(0,10);
        transactions.push({ id:1, tanggal:lastMonth, tipe:'masuk', barang:'Kabel USB', jumlah:50, satuan:'pcs', pic:'Ahmad' });
        transactions.push({ id:2, tanggal:yesterday, tipe:'masuk', barang:'Plastik OPP', jumlah:200, satuan:'lembar', pic:'Siti' });
        transactions.push({ id:3, tanggal:today, tipe:'keluar', barang:'Kabel USB', jumlah:10, satuan:'pcs', pic:'Budi' });
        transactions.push({ id:4, tanggal:today, tipe:'masuk', barang:'Magnet', jumlah:30, satuan:'buah', pic:'Ani' });
        transactions.push({ id:5, tanggal:today, tipe:'keluar', barang:'Plastik OPP', jumlah:50, satuan:'lembar', pic:'Cahyo' });
        nextId = 6; saveToLocal();
    }

    function switchTab(tabId) {
        tabMasukDiv.classList.remove('active-pane'); tabKeluarDiv.classList.remove('active-pane'); tabRekapDiv.classList.remove('active-pane');
        if (tabId === 'masuk') tabMasukDiv.classList.add('active-pane');
        else if (tabId === 'keluar') tabKeluarDiv.classList.add('active-pane');
        else tabRekapDiv.classList.add('active-pane');
        tabBtns.forEach(btn => { btn.classList.remove('active'); if(btn.getAttribute('data-tab')===tabId) btn.classList.add('active'); });
        // sembunyikan stock summary di tab rekap
        if (tabId === 'rekap') stockSummaryPanel.style.display = 'none';
        else stockSummaryPanel.style.display = 'block';
        if (tabId === 'rekap') renderRekapBulanan();
    }

    function bindEvents() {
        btnTambahMasuk.addEventListener('click', addMasuk);
        btnTambahKeluar.addEventListener('click', addKeluar);
        searchRiwayat.addEventListener('input', () => { renderRiwayatPerBulan(); if(document.getElementById('tabRekap').classList.contains('active-pane')) renderRekapBulanan(); });
        printBtn.addEventListener('click', printReport);
        exportExcelBtn.addEventListener('click', exportToExcel);
        resetAllBtn.addEventListener('click', resetAllData);
        tabBtns.forEach(btn => btn.addEventListener('click', () => switchTab(btn.getAttribute('data-tab'))));
        modalCancelBtn.addEventListener('click', closeModal);
        modalSaveBtn.addEventListener('click', saveModalData);
    }

    function init() { setDefaultDates(); loadMasterData(); renderDropdowns(); loadFromLocal(); bindEvents(); switchTab('masuk'); }
    init();
</script>
</body>
</html>
