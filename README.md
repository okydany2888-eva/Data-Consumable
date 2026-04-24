<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximal-scale=1:0, viewport-fit=cover, user-scalable=yes">
    <title>Data Konsumable</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', 'Helvetica Neue', Roboto, system-ui, -apple-system, sans-serif;
            background: #f0f4f8;
            padding: 16px;
            color: #1e293b;
        }

        /* Container utama */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 28px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.05);
            overflow: hidden;
            padding: 20px 16px 28px 16px;
        }

        /* Judul */
        h1 {
            font-size: 1.7rem;
            font-weight: 600;
            margin-bottom: 6px;
            color: #0f3b2c;
            display: flex;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: space-between;
        }
        .badge-total {
            background: #e9f4e8;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 0.9rem;
            font-weight: normal;
            color: #2b6e3c;
        }

        /* Form tambah data */
        .form-card {
            background: #ffffff;
            border-radius: 24px;
            padding: 16px;
            margin: 20px 0 24px 0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.03);
            border: 1px solid #e2e8f0;
        }
        .form-row {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 12px;
        }
        .form-field {
            flex: 1 1 160px;
            min-width: 130px;
        }
        .form-field label {
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: #5b6e8c;
            display: block;
            margin-bottom: 4px;
        }
        input, select {
            width: 100%;
            padding: 10px 12px;
            border-radius: 16px;
            border: 1px solid #cbd5e1;
            background: #fff;
            font-size: 0.9rem;
            outline: none;
            transition: 0.2s;
        }
        input:focus, select:focus {
            border-color: #2c7a4d;
            box-shadow: 0 0 0 2px rgba(44,122,77,0.2);
        }
        button {
            background: #2c7a4d;
            border: none;
            color: white;
            font-weight: 600;
            padding: 10px 18px;
            border-radius: 36px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
        }
        button:hover {
            background: #1f5e3a;
            transform: scale(0.98);
        }
        .btn-secondary {
            background: #475569;
        }
        .btn-secondary:hover {
            background: #334155;
        }
        .btn-outline {
            background: transparent;
            border: 1px solid #cbd5e1;
            color: #1e293b;
            box-shadow: none;
        }
        .btn-outline:hover {
            background: #f1f5f9;
            transform: none;
        }
        .btn-danger {
            background: #b91c1c;
        }

        /* Pencarian + aksi */
        .action-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            gap: 12px;
            margin-bottom: 20px;
            background: #f8fafc;
            padding: 12px 16px;
            border-radius: 48px;
        }
        .search-box {
            flex: 2;
            min-width: 180px;
            position: relative;
        }
        .search-box input {
            padding-right: 36px;
            border-radius: 40px;
            background: white;
        }
        .total-qty {
            background: #eef2ff;
            padding: 6px 18px;
            border-radius: 32px;
            font-weight: 700;
            font-size: 1rem;
        }
        .btn-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        /* Tabel data - scroll horizontal jika perlu */
        .table-wrapper {
            overflow-x: auto;
            border-radius: 20px;
            border: 1px solid #eef2f6;
            background: white;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
            min-width: 600px;
        }
        th {
            background: #eef2f9;
            padding: 14px 8px;
            text-align: center;
            font-weight: 600;
            color: #1f3a3f;
            border-bottom: 1px solid #dce3ec;
        }
        td {
            padding: 12px 8px;
            text-align: center;
            border-bottom: 1px solid #e9edf2;
            vertical-align: middle;
        }
        tr:hover td {
            background-color: #fafcff;
        }
        .btn-icon {
            background: none;
            border: none;
            font-size: 1.2rem;
            cursor: pointer;
            padding: 6px 8px;
            color: #5f6c84;
            box-shadow: none;
        }
        .btn-icon:hover {
            background: #e2e8f0;
            border-radius: 40px;
            transform: none;
        }
        .empty-row td {
            text-align: center;
            padding: 40px;
            color: #94a3b8;
        }

        /* footer & responsive android */
        @media (max-width: 320x) {
            body {
                padding: 10px;
            }
            .container {
                padding: 14px;
            }
            .form-field {
                min-width: 100%;
            }
            .form-row {
                flex-direction: column;
                gap: 8px;
            }
            .action-bar {
                flex-direction: column;
                align-items: stretch;
                border-radius: 24px;
            }
            .btn-group {
                justify-content: center;
            }
            th, td {
                font-size: 0.75rem;
                padding: 10px 4px;
            }
        }

        /* Landscape mode: lebih rapat*/
        @media (min-width: 320px) and (orientation: landscape) {
            .form-row {
                flex-wrap: nowrap;
            }
            .form-field {
                min-width: 140px;
            }
            .container {
                padding: 20px 24px;
            }
            table {
                font-size: 0.9rem;
            }
        }
        .print-hide {
            print-color-adjust: exact;
        }
        @media print {
            .no-print, .form-card, .action-bar, .btn-group, .btn-icon, .btn-danger {
                display: none !important;
            }
            body {
                background: white;
                padding: 0;
                margin: 0;
            }
            .container {
                box-shadow: none;
                padding: 0;
                margin: 0;
                border-radius: 0;
            }
            table {
                border: 1px solid #ccc;
            }
            th {
                background: #f1f1f1;
            }
        }
        .warning-delete {
            font-size: 0.7rem;
            color: #b45353;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>
        📦 Data Konsumable
        <span class="badge-total" id="globalTotalBadge">Total: 0</span>
    </h1>

    <!-- Form Input Data -->
    <div class="form-card no-print">
        <div class="form-row">
            <div class="form-field">
                <label>📅 Tanggal</label>
                <input type="date" id="tanggalInput" value="">
            </div>
            <div class="form-field">
                <label>👤 Nama (PIC)</label>
                <input type="text" id="namaInput" placeholder="Misal: Andi / Gudang" maxlength="50">
            </div>
            <div class="form-field">
                <label>📦 Nama Barang</label>
                <input type="text" id="barangInput" placeholder="Contoh: Kertas A4" maxlength="60">
            </div>
            <div class="form-field">
                <label>🔢 Quantity</label>
                <input type="number" id="qtyInput" placeholder="0" value="0" min="0" step="0">
            </div>
            <div class="form-field">
                <label>📏 Unit / Satuan</label>
                <input type="text" id="unitInput" placeholder="pcs, box, kg" maxlength="20">
            </div>
            <div class="form-field">
                <label>✏️ Keterangan</label>
                <input type="text" id="keteranganInput" placeholder="Opsional" maxlength="80">
            </div>
            <div class="form-field" style="display: flex; align-items: flex-end;">
                <button id="btnTambah">Tambah</button>
            </div>
        </div>
    </div>

    <!-- Pencarian dan Total Jumlah & Tombol Aksi -->
    <div class="action-bar no-print">
        <div class="search-box">
            <input type="text" id="searchBarang" placeholder="🔍 Cari nama barang... (ketik untuk filter)" autocomplete="off">
        </div>
        <div class="total-qty" id="totalQuantityDisplay">Total Jumlah: 0</div>
        <div class="btn-group">
            <button id="printBtn" class="btn-outline">🖨️ Print Data</button>
            <button id="downloadBtn" class="btn-outline">📁 Download CSV</button>
            <button id="resetDataBtn" class="btn-secondary" style="background:#475569;">🗑️ Reset Semua</button>
        </div>
    </div>

    <!-- Tabel Data Konsumable -->
    <div class="table-wrapper">
        <table id="dataTable">
            <thead>
                <tr>
                    <th>Tanggal</th><th>Nama</th><th>Nama Barang</th><th>Quantity</th><th>Satuan</th><th>Keterangan</th>
                    <th class="no-print">Aksi</th>
                </tr>
            </thead>
            <tbody id="tableBody">
                <tr class="empty-row"><td colspan="7">Belum ada data. Tambahkan barang konsumable.</td></tr>
            </tbody>
        </table>
    </div>
    <div style="font-size:12px; margin-top: 12px; text-align:center; color:#6b7280;" class="no-print">
        ⚡ Pencarian berdasarkan <strong>Nama Barang</strong> — Total quantity & total global otomatis update
    </div>
</div>

<script>
    // ----- Data Storage -----
    let consumableData = [];     // setiap item: { id, tanggal, nama, barang, quantity, unit, keterangan }
    let nextId = 1;

    // ----- DOM Elements -----
    const tanggalInput = document.getElementById('tanggalInput');
    const namaInput = document.getElementById('namaInput');
    const barangInput = document.getElementById('barangInput');
    const qtyInput = document.getElementById('qtyInput');
    const unitInput = document.getElementById('unitInput');
    const keteranganInput = document.getElementById('keteranganInput');
    const btnTambah = document.getElementById('btnTambah');
    const searchBarang = document.getElementById('searchBarang');
    const tableBody = document.getElementById('tableBody');
    const totalQuantityDisplay = document.getElementById('totalQuantityDisplay');
    const globalTotalBadge = document.getElementById('globalTotalBadge');
    const printBtn = document.getElementById('printBtn');
    const downloadBtn = document.getElementById('downloadBtn');
    const resetDataBtn = document.getElementById('resetDataBtn');

    // Helper: set default tanggal hari ini (format YYYY-MM-DD)
    function setDefaultDate() {
        if (!tanggalInput.value) {
            const today = new Date();
            const yyyy = today.getFullYear();
            const mm = String(today.getMonth() + 1).padStart(2, '0');
            const dd = String(today.getDate()).padStart(2, '0');
            tanggalInput.value = `${yyyy}-${mm}-${dd}`;
        }
    }

    // Fungsi untuk render tabel berdasarkan filter (pencarian nama barang)
    function renderTable() {
        const keyword = searchBarang.value.trim().toLowerCase();
        let filteredData = consumableData;
        if (keyword !== "") {
            filteredData = consumableData.filter(item => item.barang.toLowerCase().includes(keyword));
        }

        // Hitung total quantity dari hasil filter
        let totalFilteredQty = 0;
        filteredData.forEach(item => { totalFilteredQty += item.quantity; });
        totalQuantityDisplay.innerText = `Total Jumlah: ${totalFilteredQty}`;

        // Hitung total global (semua data tanpa filter)
        let globalTotal = 0;
        consumableData.forEach(item => { globalTotal += item.quantity; });
        globalTotalBadge.innerText = `Total: ${globalTotal}`;

        // Jika tidak ada data setelah filter
        if (filteredData.length === 0) {
            tableBody.innerHTML = `<tr class="empty-row"><td colspan="7">⚠️ Data tidak ditemukan atau belum ada data.</td></tr>`;
            return;
        }

        // Generate baris tabel
        let html = '';
        filteredData.forEach(item => {
            html += `
                <tr>
                    <td>${escapeHtml(item.tanggal)}</td>
                    <td>${escapeHtml(item.nama)}</td>
                    <td>${escapeHtml(item.barang)}</td>
                    <td style="font-weight:500;">${item.quantity}</td>
                    <td>${escapeHtml(item.unit)}</td>
                    <td>${escapeHtml(item.keterangan || '-')}</td>
                    <td class="no-print" style="text-align:center;">
                        <button class="btn-icon delete-item" data-id="${item.id}" title="Hapus">🗑️</button>
                    </td>
                </tr>
            `;
        });
        tableBody.innerHTML = html;

        // Tambahkan event listener untuk tombol hapus di setiap baris
        document.querySelectorAll('.delete-item').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const id = parseInt(btn.getAttribute('data-id'));
                deleteItemById(id);
            });
        });
    }

    // fungsi hapus item
    function deleteItemById(id) {
        if (confirm("Yakin ingin menghapus data ini?")) {
            consumableData = consumableData.filter(item => item.id !== id);
            renderTable();      // re-render sesuai filter & update total
            saveToLocal();      // simpan ke localStorage
        }
    }

    // Tambah data baru
    function addNewItem() {
        // validasi field wajib
        const tanggal = tanggalInput.value.trim();
        const nama = namaInput.value.trim();
        const barang = barangInput.value.trim();
        let quantity = parseInt(qtyInput.value);
        const unit = unitInput.value.trim();
        const keterangan = keteranganInput.value.trim();

        if (!tanggal) {
            alert("Tanggal harus diisi!");
            return;
        }
        if (!nama) {
            alert("Nama (PIC) harus diisi!");
            return;
        }
        if (!barang) {
            alert("Nama barang harus diisi!");
            return;
        }
        if (isNaN(quantity) || quantity <= 0) {
            alert("Quantity harus angka > 0");
            return;
        }
        if (!unit) {
            alert("Satuan / Unit harus diisi!");
            return;
        }

        // tambah item baru
        const newItem = {
            id: nextId++,
            tanggal: tanggal,
            nama: nama,
            barang: barang,
            quantity: quantity,
            unit: unit,
            keterangan: keterangan || ""
        };
        consumableData.push(newItem);
        // reset form & set default tanggal biar tetap fresh (beberapa field dikosongkan opsional)
        resetFormFields();
        // Re-render tabel berdasarkan filter yang sedang aktif
        renderTable();
        saveToLocal();
        // sedikit feedback
        alert(`✅ ${barang} berhasil ditambahkan!`);
    }

    function resetFormFields() {
        // tanggal diisi default hari ini
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
        // fokus ke input nama
        namaInput.focus();
    }

    // reset semua data (clear all)
    function resetAllData() {
        if (confirm("⚠️ PERINGATAN: Semua data konsumable akan dihapus permanen. Lanjutkan?")) {
            consumableData = [];
            nextId = 1;
            resetFormFields();
            renderTable();
            saveToLocal();
            alert("Semua data telah direset.");
        }
    }

    // Simpan data ke localStorage agar data tetap tersedia
    function saveToLocal() {
        const toStore = {
            data: consumableData,
            nextId: nextId
        };
        localStorage.setItem("konsumableDataApp", JSON.stringify(toStore));
    }

    // Load data dari localStorage
    function loadFromLocal() {
        const stored = localStorage.getItem("konsumableDataApp");
        if (stored) {
            try {
                const parsed = JSON.parse(stored);
                if (parsed.data && Array.isArray(parsed.data)) {
                    consumableData = parsed.data;
                    nextId = parsed.nextId || (consumableData.length > 0 ? Math.max(...consumableData.map(i=>i.id),0)+1 : 1);
                } else {
                    initDefaultSample();
                }
            } catch(e) {
                initDefaultSample();
            }
        } else {
            // data awal contoh supaya menarik
            initDefaultSample();
        }
        // setelah load data, render
        renderTable();
    }

    // Contoh data awal jika kosong
    function initDefaultSample() {
        if (consumableData.length === 0) {
            const todayStr = new Date().toISOString().slice(0,10);
            consumableData = [
                { id: 1, tanggal: todayStr, nama: "Rudi", barang: "Kertas HVS A4", quantity: 10, unit: "rim", keterangan: "Gudang utama" },
                { id: 2, tanggal: todayStr, nama: "Siti", barang: "Tinta Printer Hitam", quantity: 5, unit: "botol", keterangan: "Epson L3110" },
                { id: 3, tanggal: todayStr, nama: "Budi", barang: "Spidol Whiteboard", quantity: 12, unit: "pcs", keterangan: "Rapat meeting" },
                { id: 4, tanggal: todayStr, nama: "Ani", barang: "Amplop Coklat", quantity: 30, unit: "lembar", keterangan: "Keperluan surat" }
            ];
            nextId = 5;
        } else {
            // jika ada data namun nextId mungkin perlu sync
            if(nextId <= Math.max(...consumableData.map(i=>i.id),0)) {
                nextId = Math.max(...consumableData.map(i=>i.id),0) + 1;
            }
        }
    }

    // Utility untuk menghindari XSS
    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        }).replace(/[\uD800-\uDBFF][\uDC00-\uDFFF]/g, function(c) {
            return c;
        });
    }

    // ----- PRINT data sesuai yang tampil (termasuk hasil filter) -----
    function printFilteredData() {
        // ambil data berdasarkan teks pencarian saat ini
        const keyword = searchBarang.value.trim().toLowerCase();
        let dataToPrint = consumableData;
        if (keyword !== "") {
            dataToPrint = consumableData.filter(item => item.barang.toLowerCase().includes(keyword));
        }
        if (dataToPrint.length === 0) {
            alert("Tidak ada data yang sesuai untuk dicetak.");
            return;
        }

        // Hitung total jumlah dari data tercetak
        let totalQtyPrint = dataToPrint.reduce((sum,item)=> sum+item.quantity,0);
        
        let printWindow = window.open('', '_blank');
        let currentDate = new Date().toLocaleString('id-ID');
        let htmlContent = `
            <!DOCTYPE html>
            <html>
            <head>
                <title>Laporan Data Konsumable</title>
                <meta charset="UTF-8">
                <style>
                    body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 20px; }
                    h2 { text-align: center; color: #2c5e3a; }
                    .info-print { text-align: center; margin-bottom: 20px; color: #4b5563; }
                    table { width: 100%; border-collapse: collapse; margin-top: 12px; }
                    th, td { border: 1px solid #aaa; padding: 8px 6px; text-align: center; }
                    th { background: #ecfdf5; }
                    .footer { margin-top: 25px; font-size: 12px; text-align: right; }
                    .total-print { font-weight: bold; margin: 16px 0; text-align: right; padding: 8px; background: #f9f9f9; }
                </style>
            </head>
            <body>
                <h2>📋 Laporan Data Konsumable</h2>
                <div class="info-print">Tanggal Cetak: ${currentDate} | Filter: ${keyword ? "Nama barang mengandung '"+escapeHtml(keyword)+"'" : "Semua data"}</div>
                <table>
                    <thead><tr><th>Tanggal</th><th>Nama</th><th>Nama Barang</th><th>Quantity</th><th>Satuan</th><th>Keterangan</th></tr></thead>
                    <tbody>
        `;
        dataToPrint.forEach(item => {
            htmlContent += `<tr>
                <td>${escapeHtml(item.tanggal)}</td>
                <td>${escapeHtml(item.nama)}</td>
                <td>${escapeHtml(item.barang)}</td>
                <td>${item.quantity}</td>
                <td>${escapeHtml(item.unit)}</td>
                <td>${escapeHtml(item.keterangan || '-')}</td>
            </tr>`;
        });
        htmlContent += `
                    </tbody>
                </table>
                <div class="total-print">📊 TOTAL Quantity (data yang dicetak): ${totalQtyPrint} unit/satuan</div>
                <div class="footer">Dicetak dari Aplikasi Konsumable</div>
            </body>
            </html>
        `;
        printWindow.document.write(htmlContent);
        printWindow.document.close();
        printWindow.print();
    }

    // Download file CSV sesuai data yang tampil (filter pencarian)
    function downloadCSV() {
        const keyword = searchBarang.value.trim().toLowerCase();
        let dataToExport = consumableData;
        if (keyword !== "") {
            dataToExport = consumableData.filter(item => item.barang.toLowerCase().includes(keyword));
        }
        if (dataToExport.length === 0) {
            alert("Tidak ada data untuk diekspor.");
            return;
        }
        // Header CSV
        let csvRows = [["Tanggal","Nama","Nama Barang","Quantity","Unit/Satuan","Keterangan"]];
        for (let item of dataToExport) {
            csvRows.push([
                item.tanggal,
                item.nama,
                item.barang,
                item.quantity,
                item.unit,
                item.keterangan || ""
            ]);
        }
        const csvContent = csvRows.map(row => row.map(cell => `"${String(cell).replace(/"/g, '""')}"`).join(",")).join("\n");
        const blob = new Blob(["\uFEFF" + csvContent], { type: "text/csv;charset=utf-8;" });
        const link = document.createElement("a");
        const url = URL.createObjectURL(blob);
        link.href = url;
        link.setAttribute("download", "data_konsumable.csv");
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        URL.revokeObjectURL(url);
    }

    // Event listeners
    btnTambah.addEventListener('click', addNewItem);
    searchBarang.addEventListener('input', () => renderTable());
    printBtn.addEventListener('click', printFilteredData);
    downloadBtn.addEventListener('click', downloadCSV);
    resetDataBtn.addEventListener('click', resetAllData);

    // Inisialisasi tanggal default dan load data
    setDefaultDate();
    loadFromLocal();

    // support tombol enter pada form (optional)
    const formInputs = ['tanggalInput','namaInput','barangInput','qtyInput','unitInput','keteranganInput'];
    formInputs.forEach(id => {
        const el = document.getElementById(id);
        if(el) el.addEventListener('keypress', (e) => {
            if(e.key === 'Enter') {
                e.preventDefault();
                btnTambah.click();
            }
        });
    });
</script>
</body>
</html>
