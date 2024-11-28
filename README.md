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
CREATE TABLE IF NOT EXISTS `data_siswa` (
  `id_siswa` int(5) NOT NULL auto_increment,
  `nama_siswa` varchar(20) NOT NULL,
  `nis` varchar(12) NOT NULL,
  `nisn` varchar(10) NOT NULL,
  `kota` varchar(20) NOT NULL,
  `tgl` int(2) NOT NULL,
  `bln` varchar(10) NOT NULL,
  `thn` int(4) NOT NULL,
  `kelamin` enum('laki-laki','perempuan') NOT NULL,
  `agama` varchar(10) NOT NULL,
  `status` varchar(20) NOT NULL,
  `anakke` varchar(10) NOT NULL,
  `alamat_siswa` text NOT NULL,
  `telpon_siswa` varchar(12) NOT NULL,
  `sekolahasal` varchar(20) NOT NULL,
  `kelas` varchar(6) NOT NULL,
  `pd_tgl` int(2) NOT NULL,
  `pd_bln` varchar(10) NOT NULL,
  `pd_thn` int(4) NOT NULL,
  `ayah` varchar(30) NOT NULL,
  `ibu` varchar(30) NOT NULL,
  `alamatortu` varchar(40) NOT NULL,
  `hportu` varchar(13) NOT NULL,
  `pekerjaanayah` varchar(20) NOT NULL,
  `pekerjaanibu` varchar(20) NOT NULL,
  `wali` varchar(30) NOT NULL,
  `alamatwali` varchar(40) NOT NULL,
  `hpwali` varchar(13) NOT NULL,
  `pekerjaanwali` varchar(20) NOT NULL,
  `gambar` varchar(50) NOT NULL,
  `username` varchar(20) NOT NULL,
  `password` varchar(100) NOT NULL,
  PRIMARY KEY  (`id_siswa`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 AUTO_INCREMENT=21 ;
```

Tabel 2: Guru

```
CREATE TABLE IF NOT EXISTS `data_guru` (
  `id_guru` int(3) NOT NULL auto_increment,
  `nama_guru` varchar(20) NOT NULL,
  `nip` varchar(12) NOT NULL,
  `kota` varchar(30) NOT NULL,
  `tgl` int(2) NOT NULL,
  `bln` varchar(15) NOT NULL,
  `thn` int(4) NOT NULL,
  `kelamin` enum('laki-laki','perempuan') NOT NULL,
  `agama` varchar(20) NOT NULL,
  `alamat_guru` text NOT NULL,
  `tm_tanggal` int(2) NOT NULL,
  `tm_bulan` varchar(15) NOT NULL,
  `tm_tahun` int(4) NOT NULL,
  `pendidikan` varchar(30) NOT NULL,
  `golongan` varchar(30) NOT NULL,
  `jabatan` varchar(30) NOT NULL,
  `gambar` varchar(40) NOT NULL,
  `username` varchar(20) NOT NULL,
  `password` varchar(100) NOT NULL,
  PRIMARY KEY  (`id_guru`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 AUTO_INCREMENT=27 ;
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
CREATE TABLE IF NOT EXISTS `setup_pelajaran` (
  `id_pelajaran` int(3) NOT NULL auto_increment,
  `nama_pelajaran` varchar(50) NOT NULL,
  `kkm` char(5) NOT NULL,
  PRIMARY KEY  (`id_pelajaran`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 AUTO_INCREMENT=17 ;

```

Tabel 5: Jadwal

```
CREATE TABLE IF NOT EXISTS `tbl_jadwal` (
  `id_jadwal` int(5) NOT NULL auto_increment,
  `nama_pelajaran` varchar(40) NOT NULL,
  `kkm` int(3) NOT NULL,
  `id_guru` int(3) NOT NULL,
  `kelas` varchar(5) NOT NULL,
  PRIMARY KEY  (`id_jadwal`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 AUTO_INCREMENT=55 ;
```

Tabel 6: Nilai

```
CREATE TABLE IF NOT EXISTS `tbl_nilai` (
  `id_nilai` int(5) NOT NULL auto_increment,
  `id_siswa` int(5) NOT NULL,
  `id_jadwal` int(4) NOT NULL,
  `kelas` varchar(5) NOT NULL,
  `id_guru` int(5) NOT NULL,
  `nilai_uh1` int(3) NOT NULL,
  `nilai_uh2` int(3) NOT NULL,
  `nilai_uh3` int(3) NOT NULL,
  `nilai_uh4` int(3) NOT NULL,
  `nilai_uh5` int(3) NOT NULL,
  `rata_uh` int(3) NOT NULL,
  `nilai_tugas1` int(3) NOT NULL,
  `nilai_tugas2` int(3) NOT NULL,
  `nilai_tugas3` int(3) NOT NULL,
  `nilai_tugas4` int(3) NOT NULL,
  `rata_tugas` int(3) NOT NULL,
  `nilai_harian` int(3) NOT NULL,
  `nilai_uas` int(3) NOT NULL,
  `nilai_rapor` int(3) NOT NULL,
  `kkm` int(3) NOT NULL,
  `ket` varchar(12) NOT NULL,
  PRIMARY KEY  (`id_nilai`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 AUTO_INCREMENT=42 ;
```

### Tahap 4: Perancangan Model Fisik
Implementasi tabel ke dalam MySQL, termasuk pengaturan indeks dan tipe data. Contoh sudah diterapkan di tahap logikal dengan tipe data dan referensi kunci asing.

### Tahap 5: Implementasi
Setelah tabel dibuat di MySQL, data dapat dimasukkan menggunakan INSERT INTO atau melalui form aplikasi.

```
INSERT INTO `data_siswa` (`id_siswa`, `nama_siswa`, `nis`, `nisn`, `kota`, `tgl`, `bln`, `thn`, `kelamin`, `agama`, `status`, `anakke`, `alamat_siswa`, `telpon_siswa`, `sekolahasal`, `kelas`, `pd_tgl`, `pd_bln`, `pd_thn`, `ayah`, `ibu`, `alamatortu`, `hportu`, `pekerjaanayah`, `pekerjaanibu`, `wali`, `alamatwali`, `hpwali`, `pekerjaanwali`, `gambar`, `username`, `password`) VALUES
(2, 'Muhamad Alwi', '50000000', '8787878787', 'Brebes', 1, 'januari', 1991, 'laki-laki', 'islam', 'Anak Angkat', 'II', 'Brebes', '000000000000', 'SD N Brebes', 'VII', 1, 'januari', 1975, 'Sukra', 'Sikra', 'Tegal', '9999999999999', 'Tani', 'IRT', 'Dalban', 'Tegal', '7777777777777', 'Tani', '', 'alwi', '86df28556e29bfe0ab2431a6b07c3b01'),

INSERT INTO `data_guru` (`id_guru`, `nama_guru`, `nip`, `kota`, `tgl`, `bln`, `thn`, `kelamin`, `agama`, `alamat_guru`, `tm_tanggal`, `tm_bulan`, `tm_tahun`, `pendidikan`, `golongan`, `jabatan`, `gambar`, `username`, `password`) VALUES
(1, 'H. Sunartdi, S. Pd, ', '111112', 'Tegal', 1, 'januari', 1975, 'laki-laki', 'islam', 'Bogor', 1, 'januari', 1975, 'S 3', 'IA', 'Guru', '', 'sunar', '699528565f07a4a56dd3efd9f95dfcc2'),

INSERT INTO `setup_kelas` (`id_kelas`, `nama_kelas`, `jurusan`) VALUES
(7, 'IX ', 'SSN'),

INSERT INTO `setup_pelajaran` (`id_pelajaran`, `nama_pelajaran`, `kkm`) VALUES
(1, ' Ilmu Pengetahuan Alam', '90'),
```

### Tahap 6: Pengujian dan Optimasi

Lakukan pengujian dengan memasukkan data melalui antarmuka aplikasi.
Optimasi:
Tambahkan indeks pada kolom yang sering digunakan untuk pencarian (misalnya nis, id_kelas).
Pastikan kunci asing terintegrasi dengan benar untuk menjaga referensial.
