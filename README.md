# Mbd_Tugas_SiasSmp

## Tahap 1: Analisis Kebutuhan
Analisis kebutuhan dilakukan untuk menentukan data apa saja yang akan disimpan dalam sistem, fungsi utama yang akan diimplementasikan, serta bagaimana entitas akan saling berhubungan.

Kebutuhan Sistem:

Data Siswa: Menyimpan data lengkap siswa, termasuk identitas, alamat, informasi orang tua, dan kelas.
Data Guru: Menyimpan data identitas guru, mata pelajaran yang diajar, dan jadwal mengajar.
Data Mata Pelajaran: Menyimpan daftar pelajaran yang diajarkan di sekolah.
Data Kelas: Menyimpan informasi mengenai kelas, wali kelas, dan daftar siswa di dalamnya.
Data Jadwal Pelajaran: Mengatur jadwal mata pelajaran untuk setiap kelas.
Data Nilai: Menyimpan nilai siswa berdasarkan mata pelajaran.

### Tahap 2: Perancangan Model Konseptual

Berikut adalah model konseptual menggunakan Entity-Relationship Diagram (ERD):

Entitas:
###### Siswa (ID_Siswa, Nama, NIS, NISN, Alamat, Tanggal_Lahir, Kelas, Orang_Tua, Telepon, Foto)
###### Guru (ID_Guru, Nama, NIP, Mata_Pelajaran, Telepon, Alamat)
###### Kelas (ID_Kelas, Nama_Kelas, Wali_Kelas, Kapasitas)
###### Pelajaran (ID_Pelajaran, Nama_Pelajaran, KKM)
###### Jadwal (ID_Jadwal, Hari, Jam, ID_Kelas, ID_Pelajaran, ID_Guru)
###### Nilai (ID_Nilai, ID_Siswa, ID_Pelajaran, Semester, UTS, UAS, Rata-rata)

### Tahap 3: Perancangan Model Logikal
Di tahap ini, entitas pada tahap konseptual diterjemahkan ke dalam bentuk tabel relasional.

Tabel 1: Siswa
```
CREATE TABLE siswa (
    id_siswa INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(50) NOT NULL,
    nis VARCHAR(12) UNIQUE NOT NULL,
    nisn VARCHAR(10) UNIQUE NOT NULL,
    alamat TEXT NOT NULL,
    tanggal_lahir DATE NOT NULL,
    kelas_id INT NOT NULL,
    orang_tua VARCHAR(100) NOT NULL,
    telepon VARCHAR(15),
    foto VARCHAR(100),
    FOREIGN KEY (kelas_id) REFERENCES kelas(id_kelas)
);
```

Tabel 2: Guru

```
CREATE TABLE guru (
    id_guru INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(50) NOT NULL,
    nip VARCHAR(18) UNIQUE NOT NULL,
    telepon VARCHAR(15),
    alamat TEXT NOT NULL
);
```

Tabel 3: Kelas

```
CREATE TABLE kelas (
    id_kelas INT AUTO_INCREMENT PRIMARY KEY,
    nama_kelas VARCHAR(10) NOT NULL,
    wali_kelas INT NOT NULL,
    kapasitas INT DEFAULT 30,
    FOREIGN KEY (wali_kelas) REFERENCES guru(id_guru)
);
```

Tabel 4: Pelajaran

```
CREATE TABLE pelajaran (
    id_pelajaran INT AUTO_INCREMENT PRIMARY KEY,
    nama_pelajaran VARCHAR(50) NOT NULL,
    kkm INT NOT NULL
);
```

Tabel 5: Jadwal

```
CREATE TABLE jadwal (
    id_jadwal INT AUTO_INCREMENT PRIMARY KEY,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu') NOT NULL,
    jam TIME NOT NULL,
    kelas_id INT NOT NULL,
    pelajaran_id INT NOT NULL,
    guru_id INT NOT NULL,
    FOREIGN KEY (kelas_id) REFERENCES kelas(id_kelas),
    FOREIGN KEY (pelajaran_id) REFERENCES pelajaran(id_pelajaran),
    FOREIGN KEY (guru_id) REFERENCES guru(id_guru)
);
```

Tabel 6: Nilai

```
CREATE TABLE nilai (
    id_nilai INT AUTO_INCREMENT PRIMARY KEY,
    siswa_id INT NOT NULL,
    pelajaran_id INT NOT NULL,
    semester ENUM('1', '2') NOT NULL,
    uts FLOAT NOT NULL,
    uas FLOAT NOT NULL,
    rata_rata FLOAT GENERATED ALWAYS AS ((uts + uas) / 2) STORED,
    FOREIGN KEY (siswa_id) REFERENCES siswa(id_siswa),
    FOREIGN KEY (pelajaran_id) REFERENCES pelajaran(id_pelajaran)
);
```

### Tahap 4: Perancangan Model Fisik
Implementasi tabel ke dalam MySQL, termasuk pengaturan indeks dan tipe data. Contoh sudah diterapkan di tahap logikal dengan tipe data dan referensi kunci asing.

### Tahap 5: Implementasi
Setelah tabel dibuat di MySQL, data dapat dimasukkan menggunakan INSERT INTO atau melalui form aplikasi.

```
INSERT INTO siswa (nama, nis, nisn, alamat, tanggal_lahir, kelas_id, orang_tua, telepon, foto) 
VALUES ('Ali Ahmad', '12345', '9876543210', 'Jl. Merdeka No. 1', '2010-05-20', 1, 'Bapak Ahmad', '081234567890', 'ali.jpg');

INSERT INTO guru (nama, nip, telepon, alamat) 
VALUES ('Bu Rina', '198765432112345', '081298765432', 'Jl. Kebangsaan No. 2');

INSERT INTO kelas (nama_kelas, wali_kelas, kapasitas) 
VALUES ('VII-A', 1, 30);

INSERT INTO pelajaran (nama_pelajaran, kkm) 
VALUES ('Matematika', 75);
```

### Tahap 6: Pengujian dan Optimasi

Lakukan pengujian dengan memasukkan data melalui antarmuka aplikasi.
Optimasi:
Tambahkan indeks pada kolom yang sering digunakan untuk pencarian (misalnya nis, id_kelas).
Pastikan kunci asing terintegrasi dengan benar untuk menjaga referensial.
