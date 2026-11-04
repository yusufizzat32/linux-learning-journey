# Linux besik komen

## 1. `cd` — Pindah Direktori

`cd` digunakan untuk berpindah antar folder (direktori).

- `cd .` — Menunjuk ke folder saat ini.
- `cd ..` — Menuju folder induk (parent directory).
- `cd -` — Kembali ke folder yang terakhir dikunjungi.

---

## 2. `ls` — Melihat Isi Direktori

`ls` digunakan untuk melihat konten yang ada di dalam folder.

- `ls -a` — Melihat semua konten, termasuk file dan folder tersembunyi.
- `ls -l` — Menampilkan konten beserta informasinya seperti permission, pemilik, ukuran, dan waktu modifikasi.
- `ls -lh` — Sama seperti `-l`, tetapi ukuran file ditampilkan dalam format yang lebih mudah dibaca.
- `ls -r` — Membalik urutan hasil pengurutan.
- `ls -t` — Mengurutkan berdasarkan waktu modifikasi, dari yang terbaru.
- `ls *` — Melihat semua file dan folder yang cocok dengan wildcard `*`, serta menampilkan isi setiap folder yang cocok.
- `ls -R` — Menampilkan isi direktori beserta seluruh subdirektori di dalamnya secara rekursif.

Bisa juga dikombinasikan sesuai keperluan.

---

## 3. `touch` — Membuat File Kosong

`touch` digunakan untuk membuat file kosong.

Contoh:

```bash
touch catatan.txt
```

Kalau menggunakan `touch` pada file yang sudah ada, waktu akses dan modifikasinya akan diperbarui.

Beberapa opsi yang bisa digunakan:

- `-a` — Mengubah waktu akses saja.
- `-m` — Mengubah waktu modifikasi saja.
- `-d` — Mengatur waktu akses dan modifikasi ke waktu tertentu.
- `-r` — Mengubah waktu akses dan modifikasi sesuai referensi file lain.

  Contoh penggunaan:

  ```bash
  touch -r referensi.txt target.txt
  ```

- `-c` — Jika file tidak ada, `touch` tidak akan membuat file baru.

---

## 4. `cat` — Menampilkan Isi File

`cat` digunakan untuk menampilkan konten file.

Contoh:

```bash
cat teks.txt
```

Beberapa opsi yang bisa digunakan:

- `-n` — Memberikan nomor pada semua baris, dimulai dari 1.
- `-b` — Memberikan nomor hanya pada baris yang tidak kosong.
- `-s` — Menggabungkan beberapa baris kosong berturut-turut menjadi satu baris kosong.
- `-A` — Menampilkan karakter non-printable, tab, dan penanda akhir baris.

### Menggabungkan Isi Beberapa File

Bisa juga menggabungkan isi dua file atau lebih, lalu memasukkannya ke dalam satu file yang sudah ada atau membuat file baru.

Contoh:

```bash
cat kucing anjing > hewan
```

**Note:** Tanda `>` akan menghapus konten sebelumnya di file `hewan`, lalu mengisinya ulang dengan konten dari file `kucing` dan `anjing`.

Kalau tidak mau menghapus konten sebelumnya, bisa menggunakan `>>`.

### Menulis Catatan Menggunakan Cat

`cat` juga bisa digunakan untuk menulis catatan ke dalam file yang sudah ada atau membuat file baru.

```bash
cat > teks.txt
```

```bash
cat >> teks.txt
```

- `>` — Membuat file baru atau menimpa isi file yang sudah ada.
- `>>` — Menambahkan konten ke bagian akhir file tanpa menghapus konten sebelumnya.

Tekan `Ctrl + D` untuk mengakhiri input.

---

## 5. `less` — Menampilkan Isi File Secara Interaktif

Selain `cat`, ada juga `less` yang lebih interaktif untuk menampilkan konten file.

Beberapa opsi yang bisa digunakan:

- `-N` — Menambahkan nomor pada setiap baris.
- `+G` — Langsung lompat ke bagian akhir file.
- `+F` — Menampilkan konten file secara real-time. Jadi, kalau ada baris baru masuk, konten akan langsung ditampilkan tanpa perlu refresh. Sama seperti `tail -f`.

---

## 6. `history` — Melihat Riwayat Command

`history` digunakan untuk melihat riwayat command yang pernah dijalankan di terminal.

Beberapa opsi yang bisa digunakan:

- `-d` — Menghapus riwayat command berdasarkan nomor tertentu.
- `-c` — Menghapus seluruh riwayat command dari memori shell.
- `-w` — Menulis riwayat command dari memori shell ke file history.

Tips untuk menghapus seluruh riwayat command dari memori dan file history:

```bash
history -c && history -w
```

### Mengeksekusi Command Sebelumnya

Bisa juga menggunakan beberapa shortcut untuk mengeksekusi command sebelumnya.

- `!100` — Mengeksekusi command nomor 100.
- `!!` — Mengeksekusi command terakhir.
- `!ls` — Mengeksekusi command terakhir yang diawali dengan `ls`.
- `!$` — Mengambil argumen terakhir dari command sebelumnya.
- `!^` — Mengambil argumen pertama dari command sebelumnya.

Kalau mau mencari command secara interaktif, bisa menekan `Ctrl + R`.

---

## 7. `cp` — Menyalin File dan Folder

`cp` digunakan untuk menyalin file atau folder.

Contoh:

```bash
cp namafile tujuan
```

Bisa juga langsung menentukan nama file barunya di dalam command.

Contoh:

```bash
cp namafile tujuan/namafilebaru
```

Bisa juga menyalin banyak file sekaligus.

Contoh:

```bash
cp file1 file2 file3 Documents/kocak
```

### Wildcard untuk Memilih Banyak File

Kalau mau memilih banyak file secara spesifik, bisa menggunakan wildcard untuk memudahkan.

**1. `*` — Mewakili karakter apa saja dengan jumlah berapa pun.**

Contoh:

- `cp anjai*` — Memilih semua file yang namanya diawali dengan `anjai`, bisa `anjai_ganteng.txt`, `anjai3.png`, `anjai.pdf`.
- `cp *.pdf` — Memilih semua file yang berakhiran `.pdf`.
- `cp anjai.*` — Memilih semua file yang namanya persis `anjai`, lalu diikuti format apa saja.

**2. `?` — Mewakili tepat satu karakter.**

Contoh:

`file?.txt` berarti memilih:

- `file1.txt`
- `filea.txt`
- `file2.txt`

Tetapi tidak memilih `file12.txt` karena `12` terdiri dari dua karakter, dan juga tidak memilih `file.txt`.

**3. `[]` — Mencocokkan karakter yang ada di dalam kurung.**

Contoh:

- `file[1-3].txt` — Memilih `file1.txt`, `file2.txt`, dan `file3.txt`.
- `file[123].txt`
- `file[abc].txt`

### Menyalin Folder

Kalau mau menyalin folder beserta semua isinya, gunakan `-r` atau `-R`, keduanya sama saja.

Beberapa opsi lain yang bisa digunakan:

- `-a` — Menyalin secara rekursif sekaligus mempertahankan atribut file seperti permission, kepemilikan, dan timestamp.
- `-i` — Memberikan konfirmasi sebelum menimpa file yang sudah ada.
- `-n` — Tidak menimpa file tujuan yang sudah ada.
- `-f` — Memaksa proses penyalinan dengan menghapus file tujuan yang tidak bisa dibuka untuk ditimpa, lalu mencoba menyalin kembali.
- `-u` — Menyalin file jika file tujuan belum ada atau file sumber lebih baru daripada file tujuan.
- `-b` — Membuat backup file tujuan yang akan ditimpa agar tidak langsung hilang.

Kombinasi mantap buat backup:

```bash
cp -au
```

(Gabungan `-a` dan `-u`).

Bisa juga menggunakan:

```bash
cp -an
```

Namun, file tujuan yang sudah ada tidak akan ditimpa.

---

## 8. `mv` — Memindahkan dan Mengganti Nama File

`mv` digunakan untuk memindahkan file atau folder, bisa juga untuk mengganti nama.

Contoh memindahkan file:

```bash
mv namafile destinasi
```

Atau bisa juga untuk mengganti nama:

```bash
mv namafile namafilebaru
```

Beberapa opsi yang bisa digunakan:

- `-i` — Memberikan konfirmasi sebelum menimpa file yang sudah ada.
- `-n` — Tidak menimpa file tujuan yang sudah ada.
- `-b` — Membuat backup file tujuan yang sudah ada agar tidak hilang saat ditimpa.
- `-v` — Menampilkan proses pemindahan file.

Bisa dikombinasikan sesuai keperluan.

---

## 9. `mkdir` — Membuat Direktori

`mkdir` digunakan untuk membuat folder.

Beberapa opsi yang bisa digunakan:

- `-p` — Membuat folder bertingkat (parent directory) sekaligus.
- `-m` — Menentukan hak akses (permission) folder saat dibuat.

### Memahami Permission dengan Angka

Contoh: `755`

1. **Angka Pertama (7):** Hak akses untuk Pemilik (Owner/User).
2. **Angka Kedua (5):** Hak akses untuk Kelompok (Group).
3. **Angka Ketiga (5):** Hak akses untuk Orang Lain (Others/Public).

**Dari mana angka 7 dan 5 itu berasal?**

Setiap tindakan (baca, tulis, eksekusi) punya nilai:

- `r` (Read / Baca) = **4**
- `w` (Write / Tulis/Ubah) = **2**
- `x` (Execute / Eksekusi/Jalankan) = **1**

Contoh perhitungan:

- `7` = 4 + 2 + 1 = `rwx`
- `5` = 4 + 1 = `r-x`

Jadi, permission `755` berarti:

- Owner: `rwx`
- Group: `r-x`
- Others: `r-x`

---

## 10. `rm` — Menghapus File dan Folder

`rm` digunakan untuk menghapus file.

Contoh:

```bash
rm namafile
```

Kalau mau menghapus folder beserta seluruh isinya, gunakan `-r`.

```bash
rm -r namafolder
```

`rmdir` digunakan untuk menghapus folder kosong.

Kalau nama file atau folder diawali dengan tanda `-`, gunakan `--` agar nama tersebut tidak dianggap sebagai opsi atau perintah.

---

## 11. `find` — Mencari File dan Folder

`find` digunakan untuk mencari file atau folder berdasarkan kriteria tertentu.

Format:

```bash
find [lokasi] [kriteria] [nilai]
```

Contoh:

```bash
find file1/file2 -name anjai.txt
```

### Menggunakan Wildcard pada Find

Di `find`, wildcard bisa digunakan, tetapi harus dibarengi dengan tanda kutip agar tidak diproses terlebih dahulu oleh shell.

Contoh:

```bash
find prikitiw -name "anjai?.txt"
```

```bash
find prikitiw -name "anjai.*"
```

### Kriteria Pencarian Find

Ada beberapa kriteria pencarian yang bisa digunakan:

**1. `-name`**

Untuk mencari berdasarkan nama file atau folder.

**2. `-iname`**

Sama seperti `-name`, tetapi mengabaikan huruf kapital dan huruf kecil.

**3. `-type`**

Untuk menentukan tipe file yang dicari.

Di `-type` ada dua kategori yang sering digunakan:

- `-type d` — Untuk mencari folder (directory).
- `-type f` — Untuk mencari file biasa (regular file).

**4. `-size`**

Untuk menentukan ukuran file yang dicari.

Contoh:

- `-size -100M` — File dengan ukuran kurang dari 100 MB.
- `-size +100k` — File dengan ukuran lebih dari 100 KB.

**5. `-mtime`**

Untuk mencari file berdasarkan waktu modifikasi.

Contoh:

- `-mtime +30` — File yang terakhir dimodifikasi lebih dari 30 hari yang lalu.
- `-mtime -7` — File yang terakhir dimodifikasi kurang dari 7 hari yang lalu.

**6. `-exec` (Execute)**

buat jalanin command yg argumennya pakai file/folder yg udah ditemuin pake find

Contoh:

```bash
find prikitiw -type f -name "ucup*.txt" -exec cp -t folder1 {} \;
```

**7. `-delete`**

Menghapus file yang ditemukan berdasarkan kriteria pencarian.

Contoh:

```bash
find prikitiw -type f -name "*.txt" -delete
```
