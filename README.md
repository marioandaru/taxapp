# Arthapala - Aplikasi Rekam dan Tata Harta Pajak Daerah

## Deskripsi
Arthapala adalah prototipe web aplikasi statis untuk ASN Pemda dalam mengelola potongan pajak vendor. Aplikasi ini menyediakan dashboard ASN dan dashboard publik dengan fitur lengkap termasuk input transaksi, kalkulator pajak, dan export XML.

## Fitur Utama

### Dashboard ASN (Login Required)
- **Dashboard Utama**: Ringkasan statistik, grafik tren, dan tabel transaksi terbaru
- **Input Transaksi**: Form wizard 5-step untuk input transaksi PPh21/22/23/Final
- **Referensi**: Manajemen master data (CRUD)
- **Laporan & Export**: Export XML dan CSV
- **Kalkulator Pajak**: Kalkulator cepat untuk semua jenis PPh
- **Pengaturan**: Manajemen user dan preferensi
- **AI Assistant**: Mini-AI rule-based untuk rekomendasi dan koreksi

### Dashboard Publik (Tanpa Login)
- **Ringkasan KPI**: Total pajak, peningkatan YoY, jumlah vendor
- **Grafik Interaktif**: Tren penerimaan, komposisi PPh
- **AI Publik**: Status harian dengan insight otomatis
- **Download Data Terbuka**: CSV data anonim untuk publik

## Teknologi yang Digunakan
- **Frontend**: HTML5, CSS3, JavaScript (Vanilla)
- **Framework CSS**: Bootstrap 5
- **Chart Library**: Chart.js
- **Icons**: FontAwesome 6
- **Notifications**: SweetAlert2
- **Font**: Poppins (Google Fonts)

## Struktur Folder
```
arthapala/
├── index.html                 # Halaman utama dengan login
├── dashboard-asn.html         # Dashboard ASN
├── dashboard-public.html      # Dashboard publik
├── transaksi.html            # Form input transaksi wizard
├── referensi.html            # Manajemen data referensi
├── laporan.html              # Laporan dan export
├── kalkulator.html           # Kalkulator pajak
├── settings.html             # Pengaturan aplikasi
├── assets/
│   ├── css/
│   │   └── style.css         # Custom CSS (inline di HTML)
│   ├── js/
│   │   ├── app.js           # JavaScript utama (inline di HTML)
│   │   └── ai.js            # Logika AI rule-based (inline di HTML)
│   ├── img/
│   │   └── logo.svg         # Logo SVG dummy
│   ├── data/
│   │   └── sample-data.json # Data dummy untuk testing
│   └── xml/
│       └── example-export.xml # Contoh file XML export
└── README.md                 # Dokumentasi ini
```

## Cara Menjalankan

### Opsi 1: Buka Langsung di Browser
1. Extract file `arthapala.zip`
2. Buka `index.html` di browser modern (Chrome, Firefox, Safari, Edge)

### Opsi 2: Menggunakan HTTP Server Lokal
1. Extract file `arthapala.zip`
2. Buka terminal/command prompt di folder `arthapala/`
3. Jalankan server HTTP sederhana:

**Python 3:**
```bash
python -m http.server 8000
```

**Python 2:**
```bash
python -m SimpleHTTPServer 8000
```

**Node.js (jika ada npx):**
```bash
npx http-server -p 8000
```

4. Buka browser dan akses `http://localhost:8000`

## Credentials untuk Testing

### Login ASN
- **Email**: `asn1@pemda.go.id`
- **Password**: `Arthapala123!`

> **Catatan**: Credentials ini sudah ditampilkan di halaman utama untuk kemudahan testing.

## Panduan Penggunaan

### 1. Login dan Dashboard ASN
1. Klik "Login ASN" di halaman utama
2. Gunakan credentials di atas
3. Akses dashboard dengan menu sidebar kiri

### 2. Input Transaksi (Form Wizard)
1. **Step 1**: Pilih Subjek Pajak (Pribadi/Perusahaan)
2. **Step 2**: Pilih Jenis Transaksi (PPh21/22/23/Final)
3. **Step 3**: Isi form data transaksi lengkap
4. **Step 4**: Preview perhitungan otomatis
5. **Step 5**: Konfirmasi dan simpan

### 3. Kalkulator Pajak
- **PPh 21**: Untuk pajak penghasilan orang pribadi
- **PPh 22**: Untuk pembelian barang (dengan threshold Rp2jt)
- **PPh 23**: Untuk jasa konsultasi (dengan threshold Rp2jt)
- **PPh Final UMKM**: Untuk tarif final UMKM

### 4. Export XML
1. Klik "Export XML" di dashboard atau laporan
2. File XML akan otomatis terdownload
3. Struktur XML mengikuti format CoreTax sederhana

### 5. AI Assistant
- **ASN AI**: Memberikan rekomendasi berdasarkan data transaksi
- **Publik AI**: Memberikan insight status harian berdasarkan metrics

## Formula Perhitungan Pajak

### PPh 21 (Pribadi)
```
PPh21 = Penghasilan × (Deemed/100) × (Tarif/100)
```

### PPh 22 (Pembelian Barang)
```
Jika Penghasilan < Rp 2.000.000 → Tidak Terutang
Jika Penghasilan ≥ Rp 2.000.000:
  DPP = (100/111) × Penghasilan
  PPh22 = DPP × (Deemed/100) × (Tarif/100)
  DPP_Nilai_Lain = (11/12) × DPP
  PPN = DPP_Nilai_Lain × 12%
```

### PPh 23 (Jasa)
```
Jika Penghasilan < Rp 2.000.000 → Tidak Terutang
Jika Penghasilan ≥ Rp 2.000.000:
  PPh23 = Penghasilan × (Deemed/100) × (Tarif/100)
```

### PPh Final UMKM
```
PPh Final = Penghasilan × (Tarif_Final/100)
```

## Branding & Desain

### Palet Warna
- **Biru Utama**: `#16478A` (Navy Blue)
- **Kuning Utama**: `#FFC107` (Amber/Gold)
- **Biru Muda**: `#1976D2`
- **Background**: `#F7FAFF`

### Typography
- **Font**: Poppins (Google Fonts)
- **Weights**: 300, 400, 500, 600, 700

### Logo
- SVG lingkaran biru navy dengan huruf "A" kuning di tengah
- Ukuran standar: 120px untuk hero, 40px untuk sidebar

## Fitur AI (Rule-Based)

### AI Assistant ASN
**Rules yang diimplementasi:**
1. Deteksi transaksi dengan field penting kosong
2. Peringatan transaksi < Rp2jt yang masih dikenai pajak
3. Validasi percentage fields (deemed/tarif > 100%)
4. Reminder SP2D kosong untuk opsi pembayaran IP

### AI Publik
**Logic sederhana:**
1. Hitung growth rate YoY
2. Jika growth > 10% → Status "BAIK"
3. Jika growth 0-10% → Status "CUKUP STABIL"
4. Jika growth < 0% → Status "PERLU PERHATIAN"

## Data Dummy

### Sample Transactions
- 12 transaksi dummy dengan variasi nilai
- Mix PPh21/22/23/Final
- Beberapa dengan nilai < Rp2jt (testing threshold)
- Beberapa dengan field kosong (testing validation)

### Master Data
- Kode Objek Pajak
- Status PTKP
- Jenis Dokumen
- Opsi Pembayaran

## Keamanan & Limitasi

### Keamanan
- **Client-side only**: Semua proses di browser
- **No real backend**: Data disimpan di LocalStorage
- **Dummy credentials**: Hanya untuk prototype

### Limitasi
- Data tidak persisten (hilang jika clear browser data)
- No real authentication/authorization
- No data validation server-side
- AI rules sangat sederhana
- Export XML structure minimal

## Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Development Notes

### Extending the App
1. **Add new transaction types**: Edit form wizard di `transaksi.html`
2. **Enhance AI logic**: Modify rules di fungsi JavaScript AI
3. **Add new charts**: Gunakan Chart.js API
4. **Improve calculations**: Update formula di kalkulator

### Code Structure
- **CSS**: Inline di setiap HTML file untuk kemudahan deployment
- **JavaScript**: Inline dengan komentar lengkap
- **HTML**: Semantic markup dengan Bootstrap classes
- **Data**: JSON structure untuk easy parsing

### Performance Tips
- Semua assets dari CDN (Bootstrap, FontAwesome, Chart.js)
- Lazy loading untuk chart initialization
- Minimal JavaScript dependencies
- Optimized for static serving

## Troubleshooting

### Common Issues
1. **Login tidak bisa**: Pastikan JavaScript enabled di browser
2. **Chart tidak muncul**: Clear browser cache dan reload
3. **Export tidak jalan**: Cek popup blocker settings
4. **AI tidak update**: Refresh halaman untuk trigger recalculation

### Browser Console Errors
- Cek console untuk JavaScript errors
- Pastikan semua CDN resources loaded
- Verify LocalStorage support

## Future Enhancements

### Phase 2 Features
- [ ] Real backend integration
- [ ] Advanced AI with ML models
- [ ] Multi-user support
- [ ] Advanced reporting
- [ ] Mobile app version
- [ ] Real-time notifications
- [ ] Audit trail

### Technical Improvements
- [ ] Separate CSS/JS files
- [ ] Module bundling
- [ ] Unit tests
- [ ] API documentation
- [ ] Docker containerization

## Lisensi & Copyright
Ini adalah prototipe untuk demonstrasi. Semua data adalah dummy dan tidak mengandung informasi nyata.

## Kontak & Support
Untuk pertanyaan atau issues, silakan hubungi developer team.

---
**Arthapala v1.0** - September 2025  
*Aplikasi Rekam dan Tata Harta Pajak Daerah*