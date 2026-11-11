# Text Processing

## 1. `head` — Melihat Baris Awal File

`head` digunakan untuk melihat konten sebuah file di baris awal-awal.

Contoh:

```bash
head linux.txt
```

- Bisa juga diatur mau menampilkan berapa baris pakai `-n`.

```bash
head -n 10 linux.txt
```

Berarti hanya menampilkan 10 baris pertama.

---

## 2. `tail` — Melihat Baris Akhir File

Sama seperti `head`, tapi bedanya ini menampilkan konten dari belakang (baris akhir).

Contoh:

```bash
tail linux.txt
```

- Sama seperti `head`, bisa diatur mau berapa baris yang ditampilkan memakai `-n`.
- Bisa juga pakai `-f` untuk melihat kontennya secara real-time, jadi kalau ada baris baru akan langsung kelihatan.

Contoh:

```bash
tail -f linux.txt
```

`head` dan `tail` bisa juga dipakai dengan pipe, misal:

```bash
history | tail
history | head
```

---

## 3. `grep` — Mencari Kata dalam File

Untuk mencari kata atau pola tertentu di file.

Contoh:

```bash
grep "error" linux.txt
```

Beberapa opsi yang bisa digunakan:

- `-i` — Untuk mengabaikan huruf besar dan kecil.
- `-n` — Untuk memberikan nomor baris.
- `-c` — Untuk menghitung jumlah baris yang cocok dengan kata atau pola yang dicari.
- `-v` — Mencari baris yang tidak mengandung kata atau pola tersebut.
- `-r` — Mencari ke seluruh subdirektori secara rekursif.
- `-E` — Menggunakan Extended Regular Expression (ERE).

Contoh penggunaan `-E`:

```bash
grep -E "500|404" linux.txt
```

Kalau mau mencari kode 500 dan 404 sekaligus.

---

## 4. `wc` — Menghitung Jumlah Baris dan Kata

`wc` digunakan untuk menghitung jumlah baris, kata, dan karakter dalam sebuah file.

Beberapa opsi yang bisa digunakan:

- `-l` — Untuk menunjukkan jumlah baris saja.
- `-w` — Untuk menunjukkan jumlah kata saja.
- `-c` — Untuk menunjukkan jumlah byte.
- `-m` — Untuk menunjukkan jumlah karakter.

Contoh:

```bash
wc linux.txt
wc -l linux.txt
```

---

## 5. `sort` — Mengurutkan Baris

`sort` digunakan untuk mengurutkan baris berdasarkan abjad.

Beberapa opsi yang bisa digunakan:

- `-n` — Buat mengurutkan berdasarkan angka terkecil ke terbesar, karena kalau `sort` biasa itu menganggap angka sebagai teks. Jadi, misalnya 10 bisa muncul sebelum 2 karena karakter depannya adalah 1.
- `-r` — Untuk membalik urutan (reverse).

Contoh:

```bash
sort linux.txt
sort -n angka.txt
sort -r linux.txt
```

---

## 6. `uniq` — Menghilangkan Baris Duplikat

`uniq` digunakan untuk menghilangkan duplikat baris yang bersebelahan, jadi lebih baik pakainya setelah `sort` dulu agar duplikat yang sama terkumpul.

Beberapa opsi yang bisa digunakan:

- `-c` — Untuk menghitung jumlah kemunculan setiap baris duplikat.

Contoh:

```bash
sort linux.txt | uniq
```

Kalau mau menghitung jumlah duplikatnya:

```bash
sort linux.txt | uniq -c
```

---

## 7. Trik Buat Mencari Top 5 IP Address yang Paling Banyak Mengunjungi Web

Misalnya kita punya file log bernama `akses.log` yang berisi IP address pengunjung.

Gunakan command:

```bash
cut -d " " -f 1 akses.log | sort | uniq -c | sort -nr | head -n 5
```

Penjelasan:

1. `cut -d " " -f 1 akses.log` — Mengambil kolom pertama dari setiap baris, yaitu IP address.
2. `sort` — Mengurutkan IP address agar yang sama bersebelahan.
3. `uniq -c` — Menghitung jumlah kemunculan setiap IP address.
4. `sort -nr` — Mengurutkan berdasarkan angka dari yang terbesar.
5. `head -n 5` — Mengambil 5 IP address teratas.

---

## 8. Redirection dan Pipe (`>`, `>>`, `2>`, dan `2>&1`)

- `>` — Menimpa isi file.
- `>>` — Menambahkan output ke bagian akhir file tanpa menghapus konten sebelumnya.
- `2>` — Memasukkan output error (stderr) ke dalam file.
- `2>&1` — Mengarahkan output error (stderr) ke tujuan yang sama dengan output normal (stdout).

Contoh:

```bash
ls /etc/passwd foldergaib > oi.log 2>&1
```

Command di atas akan memasukkan output normal dari `ls /etc/passwd` sekaligus error dari `foldergaib` ke dalam `oi.log`, karena `foldergaib` itu tidak ada.

---

## 9. `sed` — Stream Editor

`sed` itu kayak fitur Find and Replace di Word, tapi ini di terminal dan bisa dipakai ke banyak file sekaligus.

### Mengganti Kata

Format:

```bash
sed 's/katalama/katabaru/g' namafile
```

Ditambah `g` di belakang karena secara default jika kata yang ingin diganti ada lebih dari satu dalam satu baris, `sed` hanya mengganti yang pertama.

`sed` hanya menampilkan hasilnya ke layar dan nggak mengubah file aslinya.

Kalau teks yang mau diganti mengandung `/`, harus pakai karakter lain sebagai pemisah, misalnya `|`.

Contoh:

```bash
sed 's|/var/log|/tmp/log|g' file.txt
```

### Opsi `-i`

`-i` untuk langsung menyimpan perubahan ke file aslinya.

Contoh:

```bash
sed -i 's/katalama/katabaru/g' file.txt
```

### Menghapus Baris dengan `d`

Bisa juga pakai `d` untuk menghapus baris.

Contoh:

```bash
sed '2d' oi.txt
```

Berarti hapus baris kedua.

```bash
sed '1,5d' oi.txt
```

Berarti hapus baris pertama sampai ke-5.

```bash
sed '/anjai/d' oi.txt
```

Berarti hapus baris yang ada kata `anjai`-nya.

```bash
sed '/^$/d' oi.txt
```

Berarti hapus baris kosong.

### Menambahkan Teks

Kalau mau menambah teks bisa kayak gini:

- `i` = Insert (sebelum).
- `a` = Append (sesudah).

Contoh:

```bash
sed '2i baris baru sebelum baris ke 2' oi.txt
```

Berarti menambahkan baris baru sebelum baris kedua.

```bash
sed '2a baris baru sesudah baris ke 2' oi.txt
```

Berarti menambahkan baris baru sesudah baris kedua.

### Opsi `-n`

`-n` untuk menonaktifkan output otomatis dari `sed`, sehingga hanya baris yang diperintahkan untuk ditampilkan yang akan muncul.

Biasanya dikombinasikan dengan `p` (print).

Contoh:

```bash
sed -n '2p' oi.txt
```

Berarti hanya menampilkan baris kedua.

```bash
sed -n '1,5p' oi.txt
```

Berarti hanya menampilkan baris pertama sampai ke-5.

---

## 10. Regex Dasar yang Sering Muncul

| Simbol | Arti |
|---|---|
| `^` | Awal baris |
| `$` | Akhir baris |
| `.` | Satu karakter apa saja |
| `*` | Nol atau lebih dari karakter atau pola sebelumnya |
| `\.` | Titik yang sebenarnya |

Kalau ingin mencari **titik yang sebenarnya**, tulis `\.` karena `.` sendiri dalam regex berarti satu karakter apa saja.