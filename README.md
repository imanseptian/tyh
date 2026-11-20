# tangerangyouthhub.web.id

Situs resmi **Tangerang Youth Hub**, ruang tumbuh pemuda Kota Tangerang.

Situs ini satu halaman, tanpa build tool dan tanpa framework. Semua file statis, jadi bisa langsung dilayani GitHub Pages.

## Isi folder

```
index.html          halaman utama
404.html            halaman kalau alamat tidak ditemukan
CNAME               domain kustom untuk GitHub Pages (jangan dihapus)
.nojekyll           mematikan pemrosesan Jekyll
robots.txt          aturan mesin pencari
sitemap.xml         daftar halaman untuk mesin pencari
assets/
  style.css         seluruh tampilan
  script.js         menu ponsel, animasi masuk, tahun footer
  logo.png          lambang (latar transparan)
  logo-640.png      versi 640 px, dipakai di beranda
  logo-320.png      versi 320 px, dipakai di header
  logo-160.png      versi 160 px, dipakai di footer
  favicon.ico       ikon tab peramban
  favicon-32.png    ikon tab ukuran kecil
  favicon-96.png    ikon ukuran sedang
  apple-touch-icon.png  ikon saat disimpan di layar utama iPhone
  og-image.png      gambar pratinjau saat tautan dibagikan
```

## Mengubah isi

Semua teks ada di `index.html` dan ditandai komentar per bagian: HERO, TENTANG, PROGRAM, KEGIATAN, GABUNG, KONTAK.

Yang paling sering diubah:

- **Kegiatan baru.** Cari bagian `<!-- KEGIATAN -->`. Setiap acara adalah satu blok `<article class="event">`. Ganti tanggal, judul, deskripsi, dan daftar `<li>` di dalam `.meta`.
- **Program.** Cari `<!-- PROGRAM -->`. Setiap program satu `<li class="program">`.
- **Tautan sosial.** Cari `#kontak`. Setiap tautan ada di `href` kartu kontak, dan juga di `sameAs` pada data JSON-LD di bagian `<head>`. Ganti keduanya supaya mesin pencari ikut memperbarui.

Setelah mengubah, tidak ada yang perlu dijalankan. Simpan, lalu unggah.

## Melihat di komputer sendiri

```bash
python -m http.server 8088
```

Buka `http://localhost:8088`. Jangan buka `index.html` langsung dengan klik dua kali, karena beberapa hal (favicon, tautan absolut) butuh server.

## Mengunggah

```bash
git add .
git commit -m "Perbarui konten"
git push origin main
```

GitHub Pages akan membangun ulang dalam satu sampai dua menit.

## Pengaturan GitHub Pages

1. Buka **Settings > Pages**.
2. Bagian **Build and deployment**, pilih **Deploy from a branch**.
3. Branch `main`, folder `/ (root)`. Simpan.
4. Di **Custom domain**, isi `tangerangyouthhub.web.id`. Jangan hapus file `CNAME`.
5. Tunggu sampai centang hijau muncul, lalu aktifkan **Enforce HTTPS**.

## DNS di Cloudflare

Catatan A untuk domain utama:

| Tipe | Nama | Isi | Proxy |
|------|------|-----|-------|
| A | `@` | `185.199.108.153` | DNS only |
| A | `@` | `185.199.109.153` | DNS only |
| A | `@` | `185.199.110.153` | DNS only |
| A | `@` | `185.199.111.153` | DNS only |
| CNAME | `www` | `imanseptian.github.io` | DNS only |

Dua hal yang sering bikin gagal:

- **Proxy Cloudflare harus abu-abu (DNS only)** saat pertama kali memasang domain. Kalau oranye, GitHub tidak bisa menerbitkan sertifikat. Setelah sertifikat terbit dan HTTPS aktif, proxy boleh dinyalakan lagi.
- **Mode SSL di Cloudflare** sebaiknya **Full**, bukan Flexible. Mode Flexible membuat situs berputar terus karena GitHub sudah memaksa HTTPS.

## Catatan teknis

- Gambar lambang sudah dibuat transparan. Kalau mengganti lambang, ekspor ulang ke PNG dengan latar transparan, lalu ganti semua ukuran di `assets/`.
- `og-image.png` dipakai saat tautan dibagikan di WhatsApp, Instagram, dan X. Ukurannya 1200 x 630. Kalau teks di dalamnya berubah, buat ulang filenya.
- Semua warna diambil dari lambang dan disimpan sebagai variabel di bagian atas `style.css`. Mengubah `--blue` atau `--orange` akan mengubah seluruh halaman.
