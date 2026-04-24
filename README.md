<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>Smart Stock - Total Per Barang</title>
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
            max-width: 600px;
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
        .global-total {
            background: #e9f4e8;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: 600;
            color: #2b6e3c;
        }

        .form-card {
            background: #f8fafc;
            border-radius: 24px;
            padding: 18px;
            margin: 16px 0 20px 0;
            border: 1px solid #e2e8f0;
        }
        .form-group {
            margin-bottom: 14px;
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
        .form-group input,
        .form-group select {
            width: 100%;
            padding: 12px 14px;
            font-size: 0.95rem;
            border: 1px solid #cbd5e1;
            border-radius: 18px;
            background: white;
            transition: all 0.2s;
        }
        .form-group input:focus,
        .form-group select:focus {
            border-color: #2c7a4d;
            outline: none;
            box-shadow: 0 0 0 3px rgba(44,122,77,0.15);
        }
        .double-row {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }
        .double-row .form-group {
            flex: 1;
            min-width: 120px;
        }
        button {
            background: #2c7a4d;
            border: none;
            color: white;
            font-weight: 600;
            padding: 12px 20px;
            border-radius: 40px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.2s;
            width: 100%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        button:active {
            transform: scale(0.97);
        }

        .action-bar {
            background: white;
            border-radius: 28px;
            padding: 12px 16px;
            margin: 16px 0;
            border: 1px solid #e9edf2;
        }
        .search-section {
            margin-bottom: 12px;
        }
        .search-section input {
            width: 100%;
            padding: 12px 16px;
            border-radius: 40px;
            border: 1px solid #cbd5e1;
            font-size: 0.9rem;
            background: #f8fafc;
        }
        .stats-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 12px 0;
            padding: 8px 0;
            border-top: 1px solid #eef2f6;
            border-bottom: 1px solid #eef2f6;
        }
        .total-filter {
            font-weight: 700;
            background: #eef2ff;
            padding: 6px 14px;
            border-radius: 30px;
            font-size: 0.85rem;
        }
        .btn-group {
            display: flex;
            gap: 10px;
            margin-top: 8px;
        }
        .btn-group button {
            flex: 1;
            padding: 10px 12px;
            font-size: 0.8rem;
        }
        .btn-outline {
            background: white;
            border: 1px solid #cbd5e1;
            color: #1e293b;
        }
        .btn-outline:active {
            background: #f1f5f9;
        }
        .btn-danger {
            background: #dc2626;
        }

        /* Ringkasan Total per Barang */
        .summary-card {
            background: #fefce8;
            border-radius: 20px;
            padding: 14px 16px;
            margin: 12px 0 8px 0;
            border: 1px solid #fde047;
        }
        .summary-title {
            font-weight: 800;
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #854d0e;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .summary-items {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-height: 220px;
            overflow-y: auto;
        }
        .summary-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: white;
            padding: 8px 12px;
            border-radius: 40px;
            border-left: 4px solid #eab308;
            font-size: 0.85rem;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
        }
        .item-name {
            font-weight: 700;
            color: #1e293b;
            display: flex;
            align-items: center;
            gap: 6px;
            flex-wrap: wrap;
        }
        .item-total {
            font-weight: 800;
            background: #f1f5f9;
            padding: 4px 10px;
            border-radius: 30px;
            color: #2c7a4d;
            font-size: 0.85rem;
        }
        .badge-unit-sum {
            background: #e2eaf1;
            border-radius: 20px;
            padding: 2px 8px;
            font-size: 0.65rem;
            font-weight: normal;
        }
        .empty-summary {
            text-align: center;
            color: #94a3b8;
            padding: 20px;
            font-style: italic;
        }

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
            min-width: 560px;
        }
        th {
            background: #eef2f9;
            padding: 12px 8px;
            font-weight: 700;
            color: #1f3a3f;
            text-align: center;
            border-bottom: 1px solid #dce3ec;
        }
        td {
            padding: 10px 6px;
            text-align: center;
            border-bottom: 1px solid #f0f4f9;
        }
        .delete-btn {
            background: none;
            border: none;
            font-size: 1.2rem;
            padding: 5px 10px;
            cursor: pointer;
            color: #b45309;
            width: auto;
        }
        .delete-btn:active {
            background: #fee2e2;
            border-radius: 30px;
        }
        .empty-row td {
            text-align: center;
            padding: 40px;
            color: #94a3b8;
        }
        .badge-unit {
            background: #e2eaf1;
            padding: 3px 8px;
            border-radius: 30px;
            font-size: 0.7rem;
        }

        .footer-note {
            font-size: 0.65rem;
            color: #6b7280;
            text-align: center;
            margin-top: 16px;
            padding-top: 12px;
            border-top: 1px solid #eef2f6;
        }

        @media print {
            .no-print, .form-card, .action-bar, .btn-group, .delete-btn, .summary-card {
                display: none !important;
            }
            body {
                background: white;
                padding: 0;
                margin: 0;
            }
            .app-container {
                max-width: 100%;
                padding: 0;
                box-shadow: none;
            }
            table {
                border: 1px solid #ccc;
            }
        }
    </style>
</head>
<body>
<div class="app-container">
    <div class="header">
        <h1>📦 Smart Stock</h1>
        <span class="global-total" id="globalTotal">Total: 0</span>
    </div>

    <!-- Form Input -->
    <div class="form-card no-print">
        <div class="form-group">
            <label>📅 Tanggal</label>
            <input type="date" id="tanggalInput">
        </div>
        <div class="form-group">
            <label>👤 Nama PIC</label>
            <input type="text" id="namaInput" placeholder="Masukkan nama..." maxlength="50">
        </div>
        <div class="form-group">
            <label>📦 Nama Barang</label>
            <input type="text" id="barangInput" placeholder="Contoh: Plastik, Magnet, dll" maxlength="60">
        </div>
        <div class="double-row">
            <div class="form-group">
                <label>🔢 Quantity</label>
                <input type="number" id="qtyInput" value="1" min="1" step="1">
            </div>
            <div class="form-group">
                <label>📏 Satuan</label>
                <input type="text" id="unitInput" placeholder="pcs, box, kg" maxlength="20">
            </div>
        </div>
        <div class="form-group">
            <label>✏️ Keterangan</label>
            <input type="text" id="keteranganInput" placeholder="Opsional" maxlength="80">
        </div>
        <button id="btnTambah">➕ Tambah Data</button>
    </div>

    <!-- Ringkasan Total Per Nama Barang (Nilai Akumulasi) -->
    <div class="summary-card no-print" id="summaryCard">
        <div class="summary-title">
            🧾 TOTAL STOK PER NAMA BARANG
        </div>
        <div id="summaryContainer" class="summary-items">
            <!-- dynamic summary berdasarkan data -->
            <div class="empty-summary">Belum ada data</div>
        </div>
    </div>

    <!-- Action & Search -->
    <div class="action-bar no-print">
        <div class="search-section">
            <input type="text" id="searchInput" placeholder="🔍 Cari nama barang...">
        </div>
        <div class="stats-row">
            <span>📊 Hasil filter:</span>
            <span class="total-filter" id="filterTotalDisplay">Total: 0</span>
        </div>
        <div class="btn-group">
            <button id="printBtn" class="btn-outline">🖨️ Print</button>
            <button id="downloadBtn" class="btn-outline">📁 CSV</button>
            <button id="resetBtn" class="btn-danger">🗑️ Reset Semua</button>
        </div>
    </div>

    <!-- Tabel Data -->
    <div class="table-wrapper">
        <table id="dataTable">
            <thead>
                <tr>
                    <th>Tanggal</th>
                    <th>PIC</th>
                    <th>Nama Barang</th>
                    <th>Qty</th>
                    <th>Satuan</th>
                    <th>Keterangan</th>
                    <th class="no-print">Aksi</th>
                </tr>
            </thead>
            <tbody id="tableBody">
                <tr class="empty-row"><td colspan="7">📭 Belum ada data. Silakan tambah barang.</td></tr>
            </tbody>
        </table>
    </div>

    <div class="footer-note no-print">
        ⚡ Fitur: Total otomatis per Nama Barang (akumulasi quantity) • Data tersimpan lokal
    </div>
</div>

<script>
    // ======================== DATA STORAGE ========================
    let stockData = [];
    let nextId = 1;

    // DOM Elements
    const tanggalInput = document.getElementById('tanggalInput');
    const namaInput = document.getElementById('namaInput');
    const barangInput = document.getElementById('barangInput');
    const qtyInput = document.getElementById('qtyInput');
    const unitInput = document.getElementById('unitInput');
    const keteranganInput = document.getElementById('keteranganInput');
    const btnTambah = document.getElementById('btnTambah');
    const searchInput = document.getElementById('searchInput');
    const tableBody = document.getElementById('tableBody');
    const filterTotalDisplay = document.getElementById('filterTotalDisplay');
    const globalTotalSpan = document.getElementById('globalTotal');
    const printBtn = document.getElementById('printBtn');
    const downloadBtn = document.getElementById('downloadBtn');
    const resetBtn = document.getElementById('resetBtn');
    const summaryContainer = document.getElementById('summaryContainer');

    // Helper: Escape HTML
    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        });
    }

    // Set default tanggal hari ini
    function setDefaultDate() {
        if (!tanggalInput.value) {
            const today = new Date();
            const yyyy = today.getFullYear();
            const mm = String(today.getMonth() + 1).padStart(2, '0');
            const dd = String(today.getDate()).padStart(2, '0');
            tanggalInput.value = `${yyyy}-${mm}-${dd}`;
        }
    }

    // ========== FUNGSI UTAMA: Hitung total per nama barang ==========
    function getSummaryPerItem() {
        const summaryMap = new Map(); // key: nama_barang|satuan -> { totalQty, unit }
        for (const item of stockData) {
            const key = `${item.barang.toLowerCase()}|${item.unit}`;
            if (summaryMap.has(key)) {
                const existing = summaryMap.get(key);
                existing.totalQty += item.quantity;
            } else {
                summaryMap.set(key, {
                    namaBarang: item.barang,
                    unit: item.unit,
                    totalQty: item.quantity
                });
            }
        }
        // Konversi ke array dan urutkan berdasarkan nama barang
        const summaryArray = Array.from(summaryMap.values());
        summaryArray.sort((a,b) => a.namaBarang.localeCompare(b.namaBarang, 'id'));
        return summaryArray;
    }

    // Render card ringkasan total per barang (akumulasi dari semua data, tanpa filter)
    function renderSummary() {
        const summary = getSummaryPerItem();
        if (summary.length === 0) {
            summaryContainer.innerHTML = '<div class="empty-summary">📭 Belum ada data</div>';
            return;
        }
        let html = '';
        for (const item of summary) {
            html += `
                <div class="summary-item">
                    <div class="item-name">
                        📦 ${escapeHtml(item.namaBarang)}
                        <span class="badge-unit-sum">${escapeHtml(item.unit)}</span>
                    </div>
                    <div class="item-total">
                        ${item.totalQty} <span style="font-weight:normal;">${escapeHtml(item.unit)}</span>
                    </div>
                </div>
            `;
        }
        summaryContainer.innerHTML = html;
    }

    // Render tabel dengan filter (search berdasarkan nama barang)
    function renderTable() {
        const keyword = searchInput.value.trim().toLowerCase();
        let filteredData = stockData;
        if (keyword !== "") {
            filteredData = stockData.filter(item => item.barang.toLowerCase().includes(keyword));
        }

        // Hitung total quantity filter
        let filterTotalQty = 0;
        filteredData.forEach(item => { filterTotalQty += item.quantity; });
        filterTotalDisplay.innerText = `Total: ${filterTotalQty}`;

        // Hitung global total (semua data)
        let globalTotalQty = 0;
        stockData.forEach(item => { globalTotalQty += item.quantity; });
        globalTotalSpan.innerText = `Total: ${globalTotalQty}`;

        if (filteredData.length === 0) {
            tableBody.innerHTML = `<tr class="empty-row"><td colspan="7">🔍 Tidak ada data / kosong</td></tr>`;
            return;
        }

        let html = '';
        filteredData.forEach(item => {
            html += `
                <tr>
                    <td>${escapeHtml(item.tanggal)}</td>
                    <td>${escapeHtml(item.nama)}</td>
                    <td style="font-weight:500;">${escapeHtml(item.barang)}</td>
                    <td><strong>${item.quantity}</strong></td>
                    <td><span class="badge-unit">${escapeHtml(item.unit)}</span></td>
                    <td>${escapeHtml(item.keterangan) || '-'}</td>
                    <td class="no-print">
                        <button class="delete-btn" data-id="${item.id}" title="Hapus">🗑️</button>
                    </td>
                </tr>
            `;
        });
        tableBody.innerHTML = html;

        // Re-attach event delete
        document.querySelectorAll('.delete-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const id = parseInt(btn.getAttribute('data-id'));
                deleteById(id);
            });
        });
    }

    // Hapus data berdasarkan ID
    function deleteById(id) {
        if (confirm("⚠️ Yakin ingin menghapus data ini?")) {
            stockData = stockData.filter(item => item.id !== id);
            if (stockData.length === 0) {
                nextId = 1;
            } else {
                const maxId = stockData.reduce((max, item) => Math.max(max, item.id), 0);
                if (nextId <= maxId) nextId = maxId + 1;
            }
            renderTable();
            renderSummary();     // Update ringkasan total per barang
            saveToLocal();
            showToast("Data berhasil dihapus", "success");
        }
    }

    // Notifikasi singkat
    function showToast(message, type = "info") {
        const toast = document.createElement('div');
        toast.innerText = message;
        toast.style.position = 'fixed';
        toast.style.bottom = '20px';
        toast.style.left = '50%';
        toast.style.transform = 'translateX(-50%)';
        toast.style.backgroundColor = type === 'success' ? '#2c7a4d' : '#334155';
        toast.style.color = 'white';
        toast.style.padding = '10px 20px';
        toast.style.borderRadius = '40px';
        toast.style.fontSize = '0.85rem';
        toast.style.fontWeight = '500';
        toast.style.zIndex = '9999';
        toast.style.boxShadow = '0 4px 12px rgba(0,0,0,0.15)';
        toast.style.whiteSpace = 'nowrap';
        document.body.appendChild(toast);
        setTimeout(() => {
            toast.style.opacity = '0';
            setTimeout(() => toast.remove(), 300);
        }, 2000);
    }

    // Tambah transaksi baru
    function addTransaction() {
        const tanggal = tanggalInput.value.trim();
        const nama = namaInput.value.trim();
        const barang = barangInput.value.trim();
        let quantity = parseInt(qtyInput.value);
        const unit = unitInput.value.trim();
        const keterangan = keteranganInput.value.trim();

        if (!tanggal) { showToast("Tanggal wajib diisi!", "info"); return; }
        if (!nama) { showToast("Nama PIC harus diisi!", "info"); return; }
        if (!barang) { showToast("Nama barang harus diisi!", "info"); return; }
        if (isNaN(quantity) || quantity <= 0) { showToast("Quantity harus angka > 0", "info"); return; }
        if (!unit) { showToast("Satuan harus diisi!", "info"); return; }

        const newItem = {
            id: nextId++,
            tanggal: tanggal,
            nama: nama,
            barang: barang,
            quantity: quantity,
            unit: unit,
            keterangan: keterangan || ""
        };
        stockData.push(newItem);
        
        resetForm();
        renderTable();
        renderSummary();   // Update ringkasan total per barang
        saveToLocal();
        showToast(`✅ "${barang}" berhasil ditambahkan!`, "success");
    }

    // Reset form input
    function resetForm() {
        const today = new Date();
        const yyyy = today.getFullYear();
        const mm = String(today.getMonth() + 1).padStart(2, '0');
        const dd = String(today.getDate()).padStart(2, '0');
        tanggalInput.value = `${yyyy}-${mm}-${dd}`;
        namaInput.value = '';
        barangInput.value = '';
        qtyInput.value = '1';
        unitInput.value = 'pcs';
        keteranganInput.value = '';
        namaInput.focus();
    }

    // Reset semua data
    function resetAllData() {
        if (confirm("⚠️ PERINGATAN: Semua data akan dihapus permanen! Lanjutkan?")) {
            stockData = [];
            nextId = 1;
            resetForm();
            renderTable();
            renderSummary();
            saveToLocal();
            showToast("Semua data telah direset.", "success");
        }
    }

    // Print laporan (filter aktif + ringkasan tidak tercetak karena print CSS)
    function printData() {
        const keyword = searchInput.value.trim().toLowerCase();
        let dataToPrint = stockData;
        if (keyword !== "") {
            dataToPrint = stockData.filter(item => item.barang.toLowerCase().includes(keyword));
        }
        
        const printWindow = window.open('', '_blank');
        let rowsHtml = '';
        let totalQtyPrint = 0;
        
        dataToPrint.forEach(item => {
            totalQtyPrint += item.quantity;
            rowsHtml += `
                <tr>
                    <td style="border:1px solid #aaa; padding:8px;">${escapeHtml(item.tanggal)}</td>
                    <td style="border:1px solid #aaa; padding:8px;">${escapeHtml(item.nama)}</td>
                    <td style="border:1px solid #aaa; padding:8px;">${escapeHtml(item.barang)}</td>
                    <td style="border:1px solid #aaa; padding:8px; text-align:center">${item.quantity}</td>
                    <td style="border:1px solid #aaa; padding:8px;">${escapeHtml(item.unit)}</td>
                    <td style="border:1px solid #aaa; padding:8px;">${escapeHtml(item.keterangan || '-')}</td>
                </tr>
            `;
        });

        // Buat juga ringkasan total per barang untuk cetak (opsional, biar informatif)
        const summaryAll = getSummaryPerItem();
        let summaryPrintHtml = '';
        if (summaryAll.length > 0) {
            summaryPrintHtml = `<div style="margin-top:20px;"><h3>📊 Ringkasan Total Stok per Nama Barang (Keseluruhan)</h3>
            <table style="border-collapse:collapse; width:auto; margin-top:10px;">
                <thead><tr><th style="border:1px solid #888; padding:6px;">Nama Barang</th><th style="border:1px solid #888; padding:6px;">Total Qty</th><th style="border:1px solid #888; padding:6px;">Satuan</th></tr></thead>
                <tbody>`;
            summaryAll.forEach(s => {
                summaryPrintHtml += `<tr><td style="border:1px solid #aaa; padding:6px;">${escapeHtml(s.namaBarang)}</td>
                <td style="border:1px solid #aaa; padding:6px; text-align:center">${s.totalQty}</td>
                <td style="border:1px solid #aaa; padding:6px;">${escapeHtml(s.unit)}</td></tr>`;
            });
            summaryPrintHtml += `</tbody></table></div>`;
        }
        
        printWindow.document.write(`
            <html>
            <head>
                <title>Laporan Stok - Smart Stock</title>
                <style>
                    body { font-family: system-ui, 'Segoe UI', sans-serif; margin: 25px; }
                    h2 { color: #2c7a4d; }
                    table { border-collapse: collapse; width: 100%; margin-top: 16px; }
                    th, td { border: 1px solid #888; padding: 8px; text-align: left; }
                    th { background: #eef2f5; }
                    .header-info { margin-bottom: 20px; }
                </style>
            </head>
            <body>
                <div class="header-info">
                    <h2>📋 Laporan Stok Barang</h2>
                    <p><strong>Tanggal cetak:</strong> ${new Date().toLocaleString('id-ID')}</p>
                    <p><strong>Filter pencarian:</strong> ${keyword || 'Semua data'}</p>
                    <p><strong>Jumlah transaksi:</strong> ${dataToPrint.length} | <strong>Total quantity (filter):</strong> ${totalQtyPrint}</p>
                </div>
                <h3>📄 Detail Transaksi</h3>
                <table>
                    <thead>
                        <tr><th>Tanggal</th><th>PIC</th><th>Nama Barang</th><th>Qty</th><th>Satuan</th><th>Keterangan</th></tr>
                    </thead>
                    <tbody>${rowsHtml}</tbody>
                </table>
                ${summaryPrintHtml}
                <p style="margin-top:20px;">* Ringkasan total per barang dihitung dari keseluruhan data (tanpa filter).</p>
            </body>
            </html>
        `);
        printWindow.document.close();
        printWindow.print();
    }

    // Download CSV (data terfilter)
    function downloadCSV() {
        const keyword = searchInput.value.trim().toLowerCase();
        let dataToExport = stockData;
        if (keyword !== "") {
            dataToExport = stockData.filter(item => item.barang.toLowerCase().includes(keyword));
        }
        
        if (dataToExport.length === 0) {
            showToast("Tidak ada data untuk diekspor", "info");
            return;
        }

        const headers = ["Tanggal", "Nama PIC", "Nama Barang", "Quantity", "Satuan", "Keterangan"];
        const rows = dataToExport.map(item => [
            item.tanggal, item.nama, item.barang, item.quantity, item.unit, item.keterangan || ''
        ]);
        
        let csvContent = headers.join(",") + "\n";
        rows.forEach(row => {
            const escapedRow = row.map(cell => {
                let cellStr = String(cell);
                if (cellStr.includes(',') || cellStr.includes('"') || cellStr.includes('\n')) {
                    cellStr = `"${cellStr.replace(/"/g, '""')}"`;
                }
                return cellStr;
            }).join(",");
            csvContent += escapedRow + "\n";
        });
        
        const blob = new Blob(["\uFEFF" + csvContent], {type: "text/csv;charset=utf-8;"});
        const link = document.createElement('a');
        const url = URL.createObjectURL(blob);
        link.href = url;
        link.setAttribute("download", `smartstock_${new Date().toISOString().slice(0,19)}.csv`);
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        URL.revokeObjectURL(url);
        showToast("CSV berhasil diunduh ✓", "success");
    }

    // Simpan ke localStorage
    function saveToLocal() {
        localStorage.setItem("smartStockApp", JSON.stringify({ data: stockData, nextId: nextId }));
    }

    // Muat dari localStorage atau sample data
    function loadFromLocal() {
        const saved = localStorage.getItem("smartStockApp");
        if (saved) {
            try {
                const parsed = JSON.parse(saved);
                if (parsed.data && Array.isArray(parsed.data)) {
                    stockData = parsed.data;
                    nextId = parsed.nextId || (stockData.length > 0 ? Math.max(...stockData.map(i => i.id), 0) + 1 : 1);
                    stockData = stockData.filter(item => item.id && item.tanggal && item.nama && item.barang && typeof item.quantity === 'number' && item.unit);
                    if (stockData.length > 0 && nextId <= Math.max(...stockData.map(i=>i.id),0)) {
                        nextId = Math.max(...stockData.map(i=>i.id),0) + 1;
                    }
                } else {
                    initSampleData();
                }
            } catch(e) {
                initSampleData();
            }
        } else {
            initSampleData();
        }
        renderTable();
        renderSummary();
    }

    // Data contoh awal
    function initSampleData() {
        stockData = [];
        const today = new Date().toISOString().slice(0,10);
        const yesterday = new Date(Date.now() - 86400000).toISOString().slice(0,10);
        stockData.push({ id: 1, tanggal: yesterday, nama: "Ahmad", barang: "Kabel USB", quantity: 15, unit: "pcs", keterangan: "Untuk packing" });
        stockData.push({ id: 2, tanggal: today, nama: "Siti", barang: "Plastik OPP", quantity: 200, unit: "lembar", keterangan: "Ukuran 10x15" });
        stockData.push({ id: 3, tanggal: today, nama: "Budi", barang: "Magnet Ferrite", quantity: 50, unit: "buah", keterangan: "Diameter 5mm" });
        stockData.push({ id: 4, tanggal: today, nama: "Ani", barang: "Kabel USB", quantity: 10, unit: "pcs", keterangan: "Tambahan stok" });
        nextId = 5;
        saveToLocal();
    }

    // Event listeners
    function initEventListeners() {
        btnTambah.addEventListener('click', addTransaction);
        searchInput.addEventListener('input', () => renderTable());
        printBtn.addEventListener('click', printData);
        downloadBtn.addEventListener('click', downloadCSV);
        resetBtn.addEventListener('click', resetAllData);
        const formInputs = [namaInput, barangInput, qtyInput, unitInput, keteranganInput];
        formInputs.forEach(input => {
            input.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    addTransaction();
                }
            });
        });
    }

    function init() {
        setDefaultDate();
        loadFromLocal();
        initEventListeners();
    }
    
    init();
</script>
</body>
</html>
