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
            width: 100%;
            color: #1e293b;
        }

        .app-container {
            max-width: 1300px;
            margin: 0 auto;
            background: white;
            border-radius: 32px;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.08), 0 8px 10px -6px rgba(0,0,0,0.02);
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

        /* Tab Menu */
        .tab-menu {
            display: flex;
            gap: 8px;
            margin: 16px 0 20px 0;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 8px;
        }
        .tab-btn {
            background: transparent;
            color: #5b6e8c;
            border: none;
            padding: 10px 24px;
            font-size: 0.9rem;
            font-weight: 600;
            border-radius: 40px;
            width: auto;
            transition: all 0.2s;
            cursor: pointer;
        }
        .tab-btn.active {
            background: #2c7a4d;
            color: white;
            box-shadow: 0 2px 8px rgba(44,122,77,0.3);
        }
        .tab-btn:active {
            transform: scale(0.98);
        }
        .tab-pane {
            display: none;
        }
        .tab-pane.active-pane {
            display: block;
        }

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
            margin-bottom: 0;
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
        .form-group input, .form-group select {
            width: 100%;
            padding: 10px 12px;
            font-size: 0.9rem;
            border: 1px solid #cbd5e1;
            border-radius: 18px;
            background: white;
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
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }
        button:active {
            transform: scale(0.97);
        }
        .btn-outline {
            background: white;
            border: 1px solid #cbd5e1;
            color: #1e293b;
        }
        .btn-danger {
            background: #dc2626;
        }
        .add-new-link {
            margin-top: 8px;
            font-size: 0.7rem;
            color: #2c7a4d;
            cursor: pointer;
            display: inline-block;
        }
        .add-new-link:hover {
            text-decoration: underline;
        }

        /* Tabel Ringkasan Stok Akhir per Barang */
        .stock-summary {
            background: #f0fdf4;
            border-radius: 20px;
            padding: 16px;
            margin: 16px 0;
            border: 1px solid #bbf7d0;
        }
        .stock-summary h3 {
            font-size: 1rem;
            margin-bottom: 12px;
            color: #166534;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .summary-table-wrapper {
            overflow-x: auto;
        }
        .summary-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
        }
        .summary-table th {
            background: #dcfce7;
            padding: 10px;
            text-align: center;
            font-weight: 700;
        }
        .summary-table td {
            padding: 8px;
            text-align: center;
            border-bottom: 1px solid #e2e8f0;
        }
        .stock-tersedia {
            font-weight: 800;
            color: #15803d;
            background: #eef2ff;
            border-radius: 30px;
            display: inline-block;
            padding: 4px 12px;
        }
        .badge-unit-sm {
            background: #e2eaf1;
            padding: 2px 8px;
            border-radius: 20px;
            font-size: 0.7rem;
        }

        /* Tabel Riwayat */
        .table-wrapper {
            overflow-x: auto;
            border-radius: 20px;
            border: 1px solid #eef2f6;
            background: white;
            margin: 12px 0;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.8rem;
            min-width: 600px;
        }
        th {
            background: #eef2f9;
            padding: 12px 8px;
            font-weight: 700;
            text-align: center;
        }
        td {
            padding: 10px 6px;
            text-align: center;
            border-bottom: 1px solid #f0f4f9;
        }
        .row-masuk {
            background-color: #f0fdf4;
            border-left: 4px solid #22c55e;
        }
        .row-keluar {
            background-color: #fef2f2;
            border-left: 4px solid #ef4444;
        }
        .delete-btn {
            background: none;
            border: none;
            font-size: 1.1rem;
            cursor: pointer;
            color: #b45309;
            width: auto;
            padding: 4px 8px;
        }
        .empty-row td {
            text-align: center;
            padding: 40px;
            color: #94a3b8;
        }
        .badge {
            padding: 3px 10px;
            border-radius: 30px;
            font-size: 0.7rem;
            font-weight: 600;
        }
        .badge-masuk {
            background: #22c55e20;
            color: #166534;
        }
        .badge-keluar {
            background: #ef444420;
            color: #b91c1c;
        }

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
        .btn-group {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .footer-note {
            font-size: 0.65rem;
            color: #6b7280;
            text-align: center;
            margin-top: 16px;
        }
        @media print {
            .no-print { display: none; }
            body { background: white; }
        }
    </style>
</head>
<body>
<div class="app-container">
    <div class="header">
        <h1>📦 Smart Stock</h1>

    <!-- Tab Menu -->
    <div class="tab-menu no-print">
        <button class="tab-btn active" data-tab="masuk">📥 Barang Masuk</button>
        <button class="tab-btn" data-tab="keluar">📤 Barang Keluar</button>
    </div>

    <!-- Panel Barang Masuk (Hijau) -->
    <div id="tabMasuk" class="tab-pane active-pane">
        <div class="form-card">
            <div class="form-row">
                <div class="form-group">
                    <label>📅 Tanggal Masuk</label>
                    <input type="date" id="tanggalMasuk">
                </div>
                <div class="form-group">
                    <label>📦 Nama Barang</label>
                    <select id="namaBarangMasuk">
                        <option value="">-- Pilih Barang --</option>
                    </select>
                    <div class="add-new-link" onclick="showAddBarangModal('masuk')">+ Tambah Barang Baru</div>
                </div>
                <div class="form-group">
                    <label>📏 Satuan</label>
                    <select id="satuanMasuk">
                        <option value="">-- Pilih Satuan --</option>
                    </select>
                    <div class="add-new-link" onclick="showAddSatuanModal('masuk')">+ Tambah Satuan Baru</div>
                </div>
                <div class="form-group">
                    <label>🔢 Jumlah Masuk</label>
                    <input type="number" id="jumlahMasuk" value="1" min="1">
                </div>
                <div class="form-group">
                    <label>👤 PIC</label>
                    <input type="text" id="picMasuk" placeholder="Nama">
                </div>
                <button id="btnTambahMasuk">+ Tambah Masuk</button>
            </div>
        </div>
    </div>

    <!-- Panel Barang Keluar (Merah) -->
    <div id="tabKeluar" class="tab-pane">
        <div class="form-card">
            <div class="form-row">
                <div class="form-group">
                    <label>📅 Tanggal Keluar</label>
                    <input type="date" id="tanggalKeluar">
                </div>
                <div class="form-group">
                    <label>📦 Nama Barang</label>
                    <select id="namaBarangKeluar">
                        <option value="">-- Pilih Barang --</option>
                    </select>
                    <div class="add-new-link" onclick="showAddBarangModal('keluar')">+ Tambah Barang Baru</div>
                </div>
                <div class="form-group">
                    <label>📏 Satuan</label>
                    <select id="satuanKeluar">
                        <option value="">-- Pilih Satuan --</option>
                    </select>
                    <div class="add-new-link" onclick="showAddSatuanModal('keluar')">+ Tambah Satuan Baru</div>
                </div>
                <div class="form-group">
                    <label>🔢 Jumlah Keluar</label>
                    <input type="number" id="jumlahKeluar" value="1" min="1">
                </div>
                <div class="form-group">
                    <label>👤 PIC</label>
                    <input type="text" id="picKeluar" placeholder="Nama">
                </div>
                <button id="btnTambahKeluar" style="background:#dc2626;">- Tambah Keluar</button>
            </div>
        </div>
    </div>

    <!-- RINGKASAN TOTAL STOK AKHIR PER NAMA BARANG (MASUK - KELUAR) -->
    <div class="stock-summary no-print">
        <h3>📊 STOCK AKHIR PER NAMA BARANG <span style="font-size:0.75rem;">(Total Masuk - Total Keluar)</span></h3>
        <div class="summary-table-wrapper">
            <table class="summary-table" id="summaryStockTable">
                <thead>
                    <tr>
                        <th>Nama Barang</th>
                        <th>Total Masuk</th>
                        <th>Total Keluar</th>
                        <th>Stok Tersedia di Gudang</th>
                        <th>Satuan</th>
                    </tr>
                </thead>
                <tbody id="summaryStockBody">
                    <tr><td colspan="5" style="text-align:center;">Belum ada data transaksi</td></tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Riwayat Transaksi -->
    <div class="action-bar no-print">
        <div class="search-section">
            <input type="text" id="searchRiwayat" placeholder="🔍 Cari nama barang...">
        </div>
        <div class="btn-group">
            <button id="printBtn" class="btn-outline">🖨️ Print</button>
            <button id="exportExcelBtn" class="btn-outline">📊 Export Excel</button>
            <button id="resetAllBtn" class="btn-danger">🗑️ Reset Semua</button>
        </div>
    </div>

    <div class="table-wrapper">
        <table id="riwayatTable">
            <thead>
                <tr><th>Tanggal</th><th>Tipe</th><th>Nama Barang</th><th>Jumlah</th><th>Satuan</th><th>PIC</th><th class="no-print">Aksi</th></tr>
            </thead>
            <tbody id="riwayatBody">
                <tr class="empty-row"><td colspan="7">📭 Belum ada transaksi</td></tr>
            </tbody>
        </table>
    </div>
    <div class="footer-note no-print">✅ Stok akhir = Total Masuk - Total Keluar (per kombinasi Nama Barang + Satuan) | Data tersimpan otomatis</div>
</div>

<!-- Modal -->
<div id="modalOverlay" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.5); z-index:1000; align-items:center; justify-content:center;">
    <div style="background:white; padding:24px; border-radius:24px; width:300px; max-width:90%;">
        <h3 id="modalTitle" style="margin-bottom:16px;">Tambah Baru</h3>
        <input type="text" id="modalInput" placeholder="Nama..." style="width:100%; padding:10px; border-radius:40px; border:1px solid #ccc; margin-bottom:16px;">
        <div style="display:flex; gap:10px; justify-content:flex-end;">
            <button id="modalCancelBtn" style="background:#e2e8f0; color:#1e293b;">Batal</button>
            <button id="modalSaveBtn" style="background:#2c7a4d;">Simpan</button>
        </div>
    </div>
</div>

<script>
    // ======================== DATA STORAGE ========================
    let transactions = [];      // { id, tanggal, tipe, barang, jumlah, satuan, pic }
    let nextId = 1;
    
    // Master data untuk dropdown
    let masterBarang = [];
    let masterSatuan = [];

    let modalContext = { formType: 'masuk', dataType: 'barang' };

    // DOM Elements
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
    const riwayatBody = document.getElementById('riwayatBody');
    const summaryStockBody = document.getElementById('summaryStockBody')
    const printBtn = document.getElementById('printBtn');
    const exportExcelBtn = document.getElementById('exportExcelBtn');
    const resetAllBtn = document.getElementById('resetAllBtn');

    const modalOverlay = document.getElementById('modalOverlay');
    const modalTitle = document.getElementById('modalTitle');
    const modalInput = document.getElementById('modalInput');
    const modalCancelBtn = document.getElementById('modalCancelBtn');
    const modalSaveBtn = document.getElementById('modalSaveBtn');

    const tabBtns = document.querySelectorAll('.tab-btn');
    const tabMasuk = document.getElementById('tabMasuk');
    const tabKeluar = document.getElementById('tabKeluar');

    // Helper
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
        if (savedBarang) masterBarang = JSON.parse(savedBarang);
        else masterBarang = ["Kabel USB", "Plastik OPP", "Magnet", "Box Kardus", "Tape Lakban"];
        
        const savedSatuan = localStorage.getItem("smartStockMasterSatuan");
        if (savedSatuan) masterSatuan = JSON.parse(savedSatuan);
        else masterSatuan = ["pcs", "lembar", "buah", "box", "roll", "kg", "meter"];
    }

    function saveMasterData() {
        localStorage.setItem("smartStockMasterBarang", JSON.stringify(masterBarang));
        localStorage.setItem("smartStockMasterSatuan", JSON.stringify(masterSatuan));
    }

    function renderDropdowns() {
        let barangHtml = '<option value="">-- Pilih Barang --</option>';
        masterBarang.forEach(b => { barangHtml += `<option value="${escapeHtml(b)}">${escapeHtml(b)}</option>`; });
        namaBarangMasuk.innerHTML = barangHtml;
        namaBarangKeluar.innerHTML = barangHtml;

        let satuanHtml = '<option value="">-- Pilih Satuan --</option>';
        masterSatuan.forEach(s => { satuanHtml += `<option value="${escapeHtml(s)}">${escapeHtml(s)}</option>`; });
        satuanMasuk.innerHTML = satuanHtml;
        satuanKeluar.innerHTML = satuanHtml;
    }

    // Modal
    function showAddBarangModal(formType) {
        modalContext = { formType, dataType: 'barang' };
        modalTitle.innerText = 'Tambah Nama Barang Baru';
        modalInput.value = '';
        modalOverlay.style.display = 'flex';
    }
    function showAddSatuanModal(formType) {
        modalContext = { formType, dataType: 'satuan' };
        modalTitle.innerText = 'Tambah Satuan Baru';
        modalInput.value = '';
        modalOverlay.style.display = 'flex';
    }
    function closeModal() { modalOverlay.style.display = 'none'; }
    function saveModalData() {
        const newValue = modalInput.value.trim();
        if (!newValue) { alert('Nama tidak boleh kosong!'); return; }
        if (modalContext.dataType === 'barang') {
            if (masterBarang.includes(newValue)) { alert('Barang sudah ada!'); closeModal(); return; }
            masterBarang.push(newValue);
            masterBarang.sort((a,b) => a.localeCompare(b, 'id'));
            saveMasterData();
            renderDropdowns();
            if (modalContext.formType === 'masuk') namaBarangMasuk.value = newValue;
            else namaBarangKeluar.value = newValue;
        } else {
            if (masterSatuan.includes(newValue)) { alert('Satuan sudah ada!'); closeModal(); return; }
            masterSatuan.push(newValue);
            masterSatuan.sort();
            saveMasterData();
            renderDropdowns();
            if (modalContext.formType === 'masuk') satuanMasuk.value = newValue;
            else satuanKeluar.value = newValue;
        }
        closeModal();
        showToast(`${modalContext.dataType === 'barang' ? 'Barang' : 'Satuan'} "${newValue}" ditambahkan`, 'success');
    }

    // Fungsi menghitung stok akhir per barang & satuan
    function getStockSummary() {
        const map = new Map(); // key: barang_lower|satuan_lower
        for (const trx of transactions) {
            const key = `${trx.barang.toLowerCase()}|${trx.satuan.toLowerCase()}`;
            if (!map.has(key)) {
                map.set(key, { namaBarang: trx.barang, satuan: trx.satuan, totalMasuk: 0, totalKeluar: 0 });
            }
            const data = map.get(key);
            if (trx.tipe === 'masuk') data.totalMasuk += trx.jumlah;
            else data.totalKeluar += trx.jumlah;
        }
        const summary = Array.from(map.values()).map(item => ({
            ...item,
            stokAkhir: item.totalMasuk - item.totalKeluar
        }));
        summary.sort((a,b) => a.namaBarang.localeCompare(b.namaBarang, 'id'));
        return summary;
    }

    // Hitung total stok keseluruhan
    function getGlobalTotalStock() {
        const summary = getStockSummary();
        return summary.reduce((sum, item) => sum + item.stokAkhir, 0);
    }

    // Render Tabel Ringkasan Stok Akhir per Nama Barang
    function renderStockSummary() {
        const summary = getStockSummary();
        if (summary.length === 0) {
            summaryStockBody.innerHTML = '<tr><td colspan="5" style="text-align:center;">Belum ada data transaksi</td></tr>';
            if(globalStockValue) globalStockValue.innerText = `Total Stok: 0`;
            return;
        }
        let html = '';
        for (const item of summary) {
            html += `<tr>
                        <td style="font-weight:700;">${escapeHtml(item.namaBarang)}</td>
                        <td>${item.totalMasuk}</td>
                        <td>${item.totalKeluar}</td>
                        <td><span class="stock-tersedia">${item.stokAkhir}</span></td>
                        <td><span class="badge-unit-sm">${escapeHtml(item.satuan)}</span></td>
                      </tr>`;
        }
    // Render Riwayat dengan filter
    function renderRiwayat() {
        const keyword = searchRiwayat.value.trim().toLowerCase();
        let filtered = transactions;
        if (keyword !== "") {
            filtered = transactions.filter(t => t.barang.toLowerCase().includes(keyword));
        }
        if (filtered.length === 0) {
            riwayatBody.innerHTML = '<tr class="empty-row"><td colspan="7">🔍 Tidak ada transaksi</td></tr>';
            return;
        }
        let html = '';
        for (const trx of filtered) {
            const rowClass = trx.tipe === 'masuk' ? 'row-masuk' : 'row-keluar';
            const tipeBadge = trx.tipe === 'masuk' ? '<span class="badge badge-masuk">MASUK</span>' : '<span class="badge badge-keluar">KELUAR</span>';
            html += `<tr class="${rowClass}">
                        <td>${escapeHtml(trx.tanggal)}</td>
                        <td>${tipeBadge}</td>
                        <td><strong>${escapeHtml(trx.barang)}</strong></td>
                        <td>${trx.jumlah}</td>
                        <td>${escapeHtml(trx.satuan)}</td>
                        <td>${escapeHtml(trx.pic)}</td>
                        <td class="no-print"><button class="delete-btn" data-id="${trx.id}" title="Hapus">🗑️</button></td>
                      </tr>`;
        }
        riwayatBody.innerHTML = html;
        document.querySelectorAll('.delete-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const id = parseInt(btn.getAttribute('data-id'));
                deleteTransaction(id);
            });
        });
    }

    function deleteTransaction(id) {
        if (confirm("Hapus transaksi ini?")) {
            transactions = transactions.filter(t => t.id !== id);
            if (transactions.length === 0) nextId = 1;
            else {
                const maxId = Math.max(...transactions.map(t=>t.id),0);
                if (nextId <= maxId) nextId = maxId+1;
            }
            saveToLocal();
            renderRiwayat();
            renderStockSummary();
            showToast("Transaksi dihapus", "success");
        }
    }

    // Tambah Masuk
    function addMasuk() {
        const tanggal = tanggalMasuk.value.trim();
        const barang = namaBarangMasuk.value;
        const satuan = satuanMasuk.value;
        let jumlah = parseInt(jumlahMasuk.value);
        const pic = picMasuk.value.trim();

        if (!tanggal) { showToast("Tanggal harus diisi", "info"); return; }
        if (!barang) { showToast("Pilih nama barang", "info"); return; }
        if (!satuan) { showToast("Pilih satuan", "info"); return; }
        if (isNaN(jumlah) || jumlah <= 0) { showToast("Jumlah harus > 0", "info"); return; }
        if (!pic) { showToast("Nama PIC harus diisi", "info"); return; }

        const newTrx = { id: nextId++, tanggal, tipe: 'masuk', barang, jumlah, satuan, pic };
        transactions.push(newTrx);
        resetFormMasuk();
        saveToLocal();
        renderRiwayat();
        renderStockSummary();
        showToast("✅ Barang Masuk ditambahkan", "success");
    }

    // Tambah Keluar dengan validasi stok
    function addKeluar() {
        const tanggal = tanggalKeluar.value.trim();
        const barang = namaBarangKeluar.value;
        const satuan = satuanKeluar.value;
        let jumlah = parseInt(jumlahKeluar.value);
        const pic = picKeluar.value.trim();

        if (!tanggal) { showToast("Tanggal harus diisi", "info"); return; }
        if (!barang) { showToast("Pilih nama barang", "info"); return; }
        if (!satuan) { showToast("Pilih satuan", "info"); return; }
        if (isNaN(jumlah) || jumlah <= 0) { showToast("Jumlah harus > 0", "info"); return; }
        if (!pic) { showToast("Nama PIC harus diisi", "info"); return; }

        // Hitung stok tersedia
        let stokTersedia = 0;
        for (const trx of transactions) {
            if (trx.barang.toLowerCase() === barang.toLowerCase() && trx.satuan.toLowerCase() === satuan.toLowerCase()) {
                if (trx.tipe === 'masuk') stokTersedia += trx.jumlah;
                else if (trx.tipe === 'keluar') stokTersedia -= trx.jumlah;
            }
        }
        if (stokTersedia < jumlah) {
            showToast(`⚠️ Stok ${barang} (${satuan}) tidak mencukupi! Tersedia: ${stokTersedia}`, "info");
            return;
        }

        const newTrx = { id: nextId++, tanggal, tipe: 'keluar', barang, jumlah, satuan, pic };
        transactions.push(newTrx);
        resetFormKeluar();
        saveToLocal();
        renderRiwayat();
        renderStockSummary();
        showToast("Barang Keluar dicatat", "success");
    }

    function resetFormMasuk() {
        const today = new Date().toISOString().slice(0,10);
        tanggalMasuk.value = today;
        namaBarangMasuk.value = '';
        satuanMasuk.value = '';
        jumlahMasuk.value = '1';
        picMasuk.value = '';
        namaBarangMasuk.focus();
    }
    function resetFormKeluar() {
        const today = new Date().toISOString().slice(0,10);
        tanggalKeluar.value = today;
        namaBarangKeluar.value = '';
        satuanKeluar.value = '';
        jumlahKeluar.value = '1';
        picKeluar.value = '';
        namaBarangKeluar.focus();
    }

    function showToast(msg, type) {
        const toast = document.createElement('div');
        toast.innerText = msg;
        toast.style.position = 'fixed';
        toast.style.bottom = '20px';
        toast.style.left = '50%';
        toast.style.transform = 'translateX(-50%)';
        toast.style.backgroundColor = type === 'success' ? '#2c7a4d' : '#334155';
        toast.style.color = 'white';
        toast.style.padding = '10px 20px';
        toast.style.borderRadius = '40px';
        toast.style.fontSize = '0.85rem';
        toast.style.zIndex = '9999';
        document.body.appendChild(toast);
        setTimeout(() => { toast.style.opacity = '0'; setTimeout(() => toast.remove(), 300); }, 2000);
    }

    // Export Excel
    function exportToExcel() {
        const summary = getStockSummary();
        let excelHtml = `<html><head><meta charset="UTF-8"><title>Laporan Stok</title></head><body>
            <h2>📊 Laporan Stok Akhir Per Barang</h2>
            <p>Tanggal Export: ${new Date().toLocaleString('id-ID')}</p>
            <table border="1" cellpadding="5">
                <thead><tr><th>Nama Barang</th><th>Total Masuk</th><th>Total Keluar</th><th>Stok Tersedia</th><th>Satuan</th></tr></thead><tbody>`;
        summary.forEach(s => {
            excelHtml += `<tr><td>${s.namaBarang}</td><td>${s.totalMasuk}</td><td>${s.totalKeluar}</td><td><strong>${s.stokAkhir}</strong></td><td>${s.satuan}</td></tr>`;
        });
        excelHtml += `</tbody></table><h3>Detail Riwayat</h3><table border="1" cellpadding="5"><thead><tr><th>Tanggal</th><th>Tipe</th><th>Barang</th><th>Jumlah</th><th>Satuan</th><th>PIC</th></tr></thead><tbody>`;
        transactions.forEach(t => {
            excelHtml += `<tr><td>${t.tanggal}</td><td>${t.tipe.toUpperCase()}</td><td>${t.barang}</td><td>${t.jumlah}</td><td>${t.satuan}</td><td>${t.pic}</td></tr>`;
        });
        excelHtml += `</tbody></table></body></html>`;
        const blob = new Blob([excelHtml], { type: 'application/vnd.ms-excel' });
        const link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = `Laporan_Stok_${new Date().toISOString().slice(0,19)}.xls`;
        link.click();
        URL.revokeObjectURL(link.href);
        showToast("Export Excel berhasil", "success");
    }

    function printReport() {
        const summary = getStockSummary();
        let summaryRows = '', trxRows = '';
        summary.forEach(s => { summaryRows += `<tr><td>${s.namaBarang}</td><td>${s.totalMasuk}</td><td>${s.totalKeluar}</td><td><strong>${s.stokAkhir}</strong></td><td>${s.satuan}</td></tr>`; });
        transactions.forEach(t => { trxRows += `<tr><td>${t.tanggal}</td><td>${t.tipe.toUpperCase()}</td><td>${t.barang}</td><td>${t.jumlah}</td><td>${t.satuan}</td><td>${t.pic}</td></tr>`; });
        const printWindow = window.open('', '_blank');
        printWindow.document.write(`
            <html><head><title>Cetak Laporan Stok</title><style>body{font-family:sans-serif;}table{border-collapse:collapse;width:100%;}th,td{border:1px solid #888;padding:8px;}th{background:#f0f0f0;}</style></head>
            <body><h2>Laporan Stok Akhir Per Barang</h2><p>Tanggal Cetak: ${new Date().toLocaleString()}</p>
            <table><thead><tr><th>Nama Barang</th><th>Total Masuk</th><th>Total Keluar</th><th>Stok Tersedia</th><th>Satuan</th></tr></thead><tbody>${summaryRows}</tbody></table>
            <h3>Detail Riwayat</h3><table><thead><tr><th>Tanggal</th><th>Tipe</th><th>Barang</th><th>Jumlah</th><th>Satuan</th><th>PIC</th></tr></thead><tbody>${trxRows}</tbody></table>
            </body></html>
        `);
        printWindow.document.close();
        printWindow.print();
    }

    function resetAllData() {
        if (confirm("⚠️ PERINGATAN: Semua data transaksi akan dihapus permanen! Lanjutkan?")) {
            transactions = [];
            nextId = 1;
            saveToLocal();
            renderRiwayat();
            renderStockSummary();
            showToast("Semua data transaksi direset.", "success");
        }
    }

    function saveToLocal() {
        localStorage.setItem("smartStockTransaksi", JSON.stringify({ transactions, nextId }));
    }

    function loadFromLocal() {
        const saved = localStorage.getItem("smartStockTransaksi");
        if (saved) {
            try {
                const parsed = JSON.parse(saved);
                if (parsed.transactions && Array.isArray(parsed.transactions)) {
                    transactions = parsed.transactions;
                    nextId = parsed.nextId || (transactions.length ? Math.max(...transactions.map(t=>t.id),0)+1 : 1);
                } else initSampleData();
            } catch(e) { initSampleData(); }
        } else initSampleData();
        renderRiwayat();
        renderStockSummary();
    }

    function initSampleData() {
        transactions = [];
        const today = new Date().toISOString().slice(0,10);
        const yesterday = new Date(Date.now()-86400000).toISOString().slice(0,10);
        transactions.push({ id:1, tanggal:yesterday, tipe:'masuk', barang:'Kabel USB', jumlah:50, satuan:'pcs', pic:'Ahmad' });
        transactions.push({ id:2, tanggal:today, tipe:'masuk', barang:'Plastik OPP', jumlah:200, satuan:'lembar', pic:'Siti' });
        transactions.push({ id:3, tanggal:today, tipe:'keluar', barang:'Kabel USB', jumlah:10, satuan:'pcs', pic:'Budi' });
        transactions.push({ id:4, tanggal:today, tipe:'masuk', barang:'Magnet', jumlah:30, satuan:'buah', pic:'Ani' });
        transactions.push({ id:5, tanggal:today, tipe:'keluar', barang:'Plastik OPP', jumlah:50, satuan:'lembar', pic:'Cahyo' });
        nextId = 6;
        saveToLocal();
    }

    function switchTab(tabId) {
        tabMasuk.classList.remove('active-pane');
        tabKeluar.classList.remove('active-pane');
        if (tabId === 'masuk') tabMasuk.classList.add('active-pane');
        else tabKeluar.classList.add('active-pane');
        tabBtns.forEach(btn => {
            btn.classList.remove('active');
            if (btn.getAttribute('data-tab') === tabId) btn.classList.add('active');
        });
    }

    function bindEvents() {
        btnTambahMasuk.addEventListener('click', addMasuk);
        btnTambahKeluar.addEventListener('click', addKeluar);
        searchRiwayat.addEventListener('input', renderRiwayat);
        printBtn.addEventListener('click', printReport);
        exportExcelBtn.addEventListener('click', exportToExcel);
        resetAllBtn.addEventListener('click', resetAllData);
        tabBtns.forEach(btn => btn.addEventListener('click', () => switchTab(btn.getAttribute('data-tab'))));
        modalCancelBtn.addEventListener('click', closeModal);
        modalSaveBtn.addEventListener('click', saveModalData);
        modalOverlay.addEventListener('click', (e) => { if (e.target === modalOverlay) closeModal(); });
    }

    function init() {
        setDefaultDates();
        loadMasterData();
        renderDropdowns();
        loadFromLocal();
        bindEvents();
    }
    init();
</script>
</body>
</html>
