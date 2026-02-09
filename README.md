# Coffee Shop Sales Tracker - Setup Guide

Aplikasi pencatatan penjualan coffee shop dengan Firestore Database dan deployment ke Vercel.

## ✨ Fitur Baru

- ✅ **Multiple Transaction Input** - Input lebih dari 1 transaksi sekaligus
- ✅ **Firestore Database** - Data tersimpan di cloud secara real-time
- ✅ **UI Colorful & Cerah** - Tampilan lebih menarik dengan warna-warna cerah
- ✅ **Auto-sync** - Data otomatis tersinkronisasi
- ✅ **Responsive Design** - Tampil baik di desktop & mobile

## 📋 Persiapan

Anda memerlukan:
1. Akun Google (untuk Firebase)
2. Akun Vercel (gratis di vercel.com)
3. Git (untuk deployment)

---

## 🔥 STEP 1: Setup Firebase

### 1.1 Buat Project Firebase

1. Buka [Firebase Console](https://console.firebase.google.com/)
2. Klik **"Add project"** atau **"Tambah project"**
3. Isi nama project, misalnya: `coffee-sales-tracker`
4. Disable Google Analytics (opsional, bisa di-skip)
5. Klik **"Create project"**

### 1.2 Buat Web App

1. Di dashboard Firebase, klik ikon **</>** (Web)
2. Isi nama app, misalnya: `Coffee Sales App`
3. **JANGAN** centang Firebase Hosting (kita pakai Vercel)
4. Klik **"Register app"**
5. **COPY** kode konfigurasi yang muncul (akan kita pakai nanti)

Contoh konfigurasi yang perlu di-copy:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyAbc123...",
  authDomain: "coffee-sales-tracker.firebaseapp.com",
  projectId: "coffee-sales-tracker",
  storageBucket: "coffee-sales-tracker.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123..."
};
```

### 1.3 Setup Firestore Database

1. Di sidebar kiri, klik **"Firestore Database"**
2. Klik **"Create database"**
3. Pilih lokasi: **asia-southeast1** (Singapura) atau **asia-southeast2** (Jakarta)
4. Pilih mode: **Start in production mode**
5. Klik **"Enable"**

### 1.4 Atur Firestore Rules

1. Setelah database dibuat, klik tab **"Rules"**
2. Ganti rules dengan kode berikut:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write untuk semua collections
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Klik **"Publish"**

⚠️ **PENTING**: Rules di atas membolehkan akses tanpa autentikasi. Cocok untuk aplikasi pribadi/internal. Jika ingin lebih aman, Anda bisa menambahkan autentikasi Firebase nanti.

### 1.5 Update Kode dengan Config Firebase

1. Buka file `index.html`
2. Cari bagian `// TODO: Replace with your Firebase config` (sekitar baris 476)
3. Replace dengan config yang Anda copy tadi:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyAbc123...",  // Ganti dengan punya Anda
    authDomain: "coffee-sales-tracker.firebaseapp.com",  // Ganti
    projectId: "coffee-sales-tracker",  // Ganti
    storageBucket: "coffee-sales-tracker.appspot.com",  // Ganti
    messagingSenderId: "123456789",  // Ganti
    appId: "1:123456789:web:abc123..."  // Ganti
};
```

4. **Save** file

---

## 🚀 STEP 2: Deploy ke Vercel

### 2.1 Persiapan File

Pastikan Anda punya 2 file di folder yang sama:
- `index.html` (sudah diupdate dengan Firebase config)
- `vercel.json`

### 2.2 Install Vercel CLI (Opsional)

Bisa lewat terminal:
```bash
npm install -g vercel
```

Atau langsung upload lewat dashboard Vercel.

### 2.3 Deploy via Vercel Dashboard (Cara Mudah)

1. Buka [vercel.com](https://vercel.com)
2. Login dengan GitHub/GitLab/Bitbucket
3. Klik **"Add New..."** → **"Project"**

#### Opsi A: Upload Manual
1. Klik **"Deploy from template"** → **"Browse Templates"**
2. Pilih **"Other"**
3. Drag & drop folder yang berisi `index.html` dan `vercel.json`
4. Klik **"Deploy"**

#### Opsi B: Via GitHub (Recommended)
1. Upload file ke GitHub repository baru
2. Di Vercel, klik **"Import Project"**
3. Pilih repository Anda
4. Klik **"Deploy"**

### 2.4 Deploy via Vercel CLI

Jika pakai CLI:

```bash
# Di folder project
cd /path/to/project

# Login ke Vercel
vercel login

# Deploy
vercel

# Untuk production deployment
vercel --prod
```

---

## 🎯 STEP 3: Testing

Setelah deploy:

1. Buka URL yang diberikan Vercel (misalnya: `https://coffee-sales-tracker.vercel.app`)
2. Coba input transaksi
3. Cek di Firebase Console → Firestore Database
4. Data harus muncul di collections: `sales`, `products`, `categories`

---

## 📱 Cara Menggunakan Aplikasi

### Input Multiple Transaksi

1. Klik tab **"📝 Input Transaksi"**
2. Pilih tanggal
3. Isi transaksi pertama (nama produk, kategori, jumlah, harga)
4. Klik **"➕ Tambah Transaksi Lain"** untuk menambah transaksi berikutnya
5. Isi semua transaksi yang ingin diinput
6. Klik **"💾 Simpan Semua Transaksi"**

### Lihat Laporan

1. Klik tab **"📊 Laporan"**
2. Pilih periode keuangan (Harian/Mingguan/Bulanan)
3. Pilih periode detail untuk filter tabel
4. Lihat statistik di card atas (Total Omzet, Item Terjual, Bagi Hasil)

### Kelola Produk & Kategori

1. Klik tab **"🛍️ Produk"**
2. Tambah kategori baru di bagian atas
3. Lihat daftar produk yang pernah dijual

---

## 🔧 Troubleshooting

### Error: "Failed to load data"
- Cek koneksi internet
- Pastikan Firebase config sudah benar
- Cek Firestore rules sudah di-publish

### Data tidak muncul
- Buka Console browser (F12)
- Lihat error di tab Console
- Pastikan tidak ada error merah

### Deploy Vercel gagal
- Pastikan `vercel.json` ada di root folder
- Pastikan `index.html` sudah diupdate dengan Firebase config
- Cek build logs di Vercel dashboard

---

## 📊 Struktur Database Firestore

### Collection: `sales`
```javascript
{
  date: "2024-02-09",
  productName: "Latte",
  productType: "Minuman",
  quantity: 2,
  price: 25000,
  notes: "Extra shot",
  total: 50000,
  timestamp: "2024-02-09T10:30:00.000Z"
}
```

### Collection: `products`
```javascript
{
  name: "Latte",
  type: "Minuman",
  price: 25000,
  totalSold: 10
}
```

### Collection: `categories`
```javascript
{
  list: ["Minuman", "Makanan", "Snack"]
}
```

---

## 🎨 Customization

### Ubah Warna
Edit bagian CSS di `index.html`:
- Header gradient: baris 32-33
- Button gradient: baris 130-131
- Stat cards: baris 267-280

### Ubah Bagi Hasil
Edit di fungsi `displayFinancialReport()` (baris 1193-1194):
```javascript
const myIncome = totalOmzet * 0.75; // Ubah 0.75 sesuai kebutuhan
const shareIncome = totalOmzet * 0.25; // Ubah 0.25 sesuai kebutuhan
```

---

## 📞 Support

Jika ada pertanyaan atau masalah:
1. Cek error di Console browser (F12)
2. Lihat logs di Vercel dashboard
3. Cek Firestore rules dan data

---

## 🔒 Security Tips

Untuk production:
1. Tambahkan Firebase Authentication
2. Update Firestore rules untuk require authentication
3. Tambahkan rate limiting
4. Gunakan environment variables untuk Firebase config

---

## ✅ Checklist Deployment

- [ ] Firebase project sudah dibuat
- [ ] Firestore database sudah di-enable
- [ ] Firestore rules sudah di-publish
- [ ] Firebase config sudah di-copy ke `index.html`
- [ ] File `index.html` dan `vercel.json` sudah siap
- [ ] Deploy ke Vercel berhasil
- [ ] Testing input transaksi berhasil
- [ ] Data muncul di Firestore Console

---

**Selamat! Aplikasi Anda sudah live dan siap digunakan! 🎉**
