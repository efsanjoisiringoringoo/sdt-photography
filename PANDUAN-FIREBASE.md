# 🔥 Panduan Setup Firebase untuk SDT Photography

Firebase adalah layanan Google yang GRATIS untuk kebutuhan website ini.
Ikuti langkah berikut satu per satu — sekitar 15 menit.

---

## LANGKAH 1 — Buat Project Firebase

1. Buka → https://console.firebase.google.com
2. Login dengan akun Google Anda
3. Klik **"Add project"** / **"Tambahkan project"**
4. Nama project: `sdt-photography` → Next → Next → Create Project
5. Tunggu loading selesai → klik **Continue**

---

## LANGKAH 2 — Tambahkan Web App

1. Di halaman project, klik ikon **`</>`** (Web)
2. App nickname: `SDT Web` → klik **Register app**
3. **COPY** kode `firebaseConfig` yang muncul, contohnya:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "sdt-photography.firebaseapp.com",
  projectId: "sdt-photography",
  storageBucket: "sdt-photography.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456:web:abcdef"
};
```

4. Klik **Continue to console**

---

## LANGKAH 3 — Aktifkan Firestore Database

1. Di sidebar kiri → klik **Firestore Database**
2. Klik **Create database**
3. Pilih **"Start in test mode"** (untuk development)
4. Pilih lokasi server: **asia-southeast1** (Singapore) → Enable
5. Tunggu selesai

---

## LANGKAH 4 — Aktifkan Firebase Storage

1. Di sidebar kiri → klik **Storage**
2. Klik **Get started**
3. Pilih **"Start in test mode"**
4. Pilih lokasi: **asia-southeast1** → Done

---

## LANGKAH 5 — Aktifkan Authentication

1. Di sidebar kiri → klik **Authentication**
2. Klik **Get started**
3. Di tab **Sign-in method**, klik **Email/Password**
4. Toggle ON → Save
5. Pergi ke tab **Users** → klik **Add user**
6. Masukkan email dan password admin Anda
   - Email: `admin@sdtphoto.com` (atau email Anda)
   - Password: buat password yang kuat
7. Klik **Add user**

---

## LANGKAH 6 — Pasang Config di File HTML

Buka `index.html` dan `admin.html` dengan text editor (VS Code, Notepad++, dll).

Cari bagian ini (ada di kedua file):
```js
const firebaseConfig = {
  apiKey: "GANTI_API_KEY_ANDA",
  authDomain: "GANTI_PROJECT_ID.firebaseapp.com",
  ...
};
```

Ganti dengan config yang Anda copy di Langkah 2. Lakukan di **KEDUA** file.

---

## LANGKAH 7 — Upload ke GitHub

Upload SEMUA file ke repository GitHub Anda:
- `index.html` (website utama)
- `admin.html` (panel admin)

### Cara upload:
1. Buka repository GitHub Anda
2. Klik **Add file** → **Upload files**
3. Drag `index.html` DAN `admin.html` sekaligus
4. Klik **Commit changes**

---

## LANGKAH 8 — Aktifkan Security Rules (PENTING!)

Setelah testing selesai, ubah Firestore & Storage rules agar lebih aman.

### Firestore Rules:
Di Firebase Console → Firestore → Rules, paste ini:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Siapapun bisa baca foto (untuk galeri publik)
    match /photos/{doc} {
      allow read: if true;
      allow write: if request.auth != null;
    }
    // Siapapun bisa kirim pesan, hanya admin yang bisa baca
    match /messages/{doc} {
      allow create: if true;
      allow read, update, delete: if request.auth != null;
    }
  }
}
```

### Storage Rules:
Di Firebase Console → Storage → Rules, paste ini:
```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /photos/{file} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

Klik **Publish** di keduanya.

---

## Cara Akses Admin Panel

Setelah deploy, buka:
```
https://[username].github.io/[repo]/admin.html
```

Login dengan email dan password yang dibuat di Langkah 5.

---

## Ringkasan URL Website

| Halaman | URL |
|---------|-----|
| Portfolio utama | `https://username.github.io/sdt-photography/` |
| Admin panel | `https://username.github.io/sdt-photography/admin.html` |

---

## Fitur yang Sudah Aktif ✅

- Upload foto dengan drag & drop
- Foto otomatis muncul di galeri publik
- Filter foto berdasarkan kategori
- Form kontak tersimpan di database
- Admin panel untuk kelola foto & baca pesan
- Login aman dengan email/password
- Progress bar saat upload foto

---

*SDT Photography CMS — dibuat dengan Firebase + GitHub Pages*
