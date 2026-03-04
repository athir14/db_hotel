# db_hotel
Menggunakan Operator Jaringan di SQL 

🏨 Project Database Hotel (db_hotel) 
membuat database hotel menggunakan MySQL/MariaDB dengan Database: db_hotel
Tabel:
tabel_pelanggan
tabel_kamar
tabel_reservasi

Join Data INNER JOIN, LEFT JOIN, dan RIGHT JOIN.

1. Buka Command Prompt
Setting environment for using XAMPP for Windows.
RPL44@DESKTOP-BL56RHE c:\xampp
# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 246
Server version: 10.4.25-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

2. Buat Database 
[PERINTAH DATABASE]
MariaDB [(none)]> CREATE DATABASE db_hotel;
Query OK, 0 rows affected (0.072 sec)

[GUNAKAN DATABASE]
MariaDB [(none)]> use db_hotel;
Query OK, 1 row affected (0.001 sec)

Database changed

3. Buat Table
[🧍 Tabel Pelanggan]
MariaDB [db_hotel]> CREATE TABLE tabel_pelanggan (
    ->     id_pelanggan INT PRIMARY KEY AUTO_INCREMENT,
    ->     nama_pelanggan VARCHAR(100) NOT NULL,
    ->     no_telepon VARCHAR(15),
    ->     alamat TEXT
    -> );
Query OK, 0 rows affected (0.077 sec)

[🛏 Tabel Kamar]
MariaDB [db_hotel]> CREATE TABLE tabel_kamar (
    ->     id_kamar INT PRIMARY KEY AUTO_INCREMENT,
    ->     nomor_kamar VARCHAR(10) NOT NULL,
    ->     tipe_kamar VARCHAR(50),
    ->     harga_per_malam DECIMAL(10,2),
    ->     status_kamar VARCHAR(20)
    -> );
Query OK, 0 rows affected (0.068 sec)

[📅 Tabel Reservasi]
MariaDB [db_hotel]> CREATE TABLE tabel_reservasi (
    ->     id_reservasi INT PRIMARY KEY AUTO_INCREMENT,
    ->     id_pelanggan INT,
    ->     id_kamar INT,
    ->     tanggal_checkin DATE,
    ->     tanggal_checkout DATE,
    ->     FOREIGN KEY (id_pelanggan) REFERENCES tabel_pelanggan(id_pelanggan),
    ->     FOREIGN KEY (id_kamar) REFERENCES tabel_kamar(id_kamar)
    -> );
Query OK, 0 rows affected (0.283 sec)

4. Insert Data
[🔹 Data Pelanggan]
MariaDB [db_hotel]> INSERT INTO tabel_pelanggan (nama_pelanggan, no_telepon, alamat)VALUES
    -> ('athir', '085814157439', 'Padang'),
    -> ('ardo', '085714157439', 'Manado'),
    -> ('thoriq', '085614157439', 'Jambi'),
    -> ('rizky', '085214157439', 'Sukahati');
Query OK, 4 rows affected (0.008 sec)
Records: 4  Duplicates: 0  Warnings: 0

[🔹 Data Kamar]
MariaDB [db_hotel]> INSERT INTO tabel_kamar (nomor_kamar, tipe_kamar, harga_per_malam, status_kamar)VALUES
    -> ('100', 'Misquen', '150000', 'Tersedia'),
    -> ('101', 'Umr', '250000', 'Terisi'),
    -> ('102', 'Tajir', '500000', 'Tersedia'),
    -> ('103', 'Sultan', '1000000', 'Terisi');
Query OK, 4 rows affected (0.007 sec)
Records: 4  Duplicates: 0  Warnings: 0

[🔹 Data Reservasi]
MariaDB [db_hotel]> INSERT INTO tabel_reservasi (id_pelanggan, id_kamar, tanggal_checkin, tanggal_checkout)VALUES
    -> (1, 2, '2025-12-31', '2026-01-01'),
    -> (2, 1, '2026-01-31', '2026-02-01'),
    -> (3, 3, '2026-02-28', '2026-03-01');
Query OK, 3 rows affected (0.011 sec)
Records: 3  Duplicates: 0  Warnings: 0

5. Menampilkan Output Struktur nya
[🔹 Output Pelanggan]
MariaDB [db_hotel]> SELECT * FROM tabel_pelanggan;
+--------------+----------------+--------------+----------+
| id_pelanggan | nama_pelanggan | no_telepon   | alamat   |
+--------------+----------------+--------------+----------+
|            1 | athir          | 085814157439 | Padang   |
|            2 | ardo           | 085714157439 | Manado   |
|            3 | thoriq         | 085614157439 | Jambi    |
|            4 | rizky          | 085214157439 | Sukahati |
+--------------+----------------+--------------+----------+
4 rows in set (0.000 sec)

[🔹 Output Kamar]
MariaDB [db_hotel]> SELECT * FROM tabel_kamar;
+----------+-------------+------------+-----------------+--------------+
| id_kamar | nomor_kamar | tipe_kamar | harga_per_malam | status_kamar |
+----------+-------------+------------+-----------------+--------------+
|        1 | 100         | Misquen    |       150000.00 | Tersedia     |
|        2 | 101         | Umr        |       250000.00 | Terisi       |
|        3 | 102         | Tajir      |       500000.00 | Tersedia     |
|        4 | 103         | Sultan     |      1000000.00 | Terisi       |
+----------+-------------+------------+-----------------+--------------+
4 rows in set (0.001 sec)

[🔹 Output Reservasi]
MariaDB [db_hotel]> SELECT * FROM tabel_reservasi;
+--------------+--------------+----------+-----------------+------------------+
| id_reservasi | id_pelanggan | id_kamar | tanggal_checkin | tanggal_checkout |
+--------------+--------------+----------+-----------------+------------------+
|            1 |            1 |        2 | 2025-12-31      | 2026-01-01       |
|            2 |            2 |        1 | 2026-01-31      | 2026-02-01       |
|            3 |            3 |        3 | 2026-02-28      | 2026-03-01       |
+--------------+--------------+----------+-----------------+------------------+
3 rows in set (0.002 sec)

6. INNER JOIN [Menampilkan data reservasi lengkap dengan nama pelanggan dan nomor kamar].

MariaDB [db_hotel]> SELECT tabel_pelanggan.nama_pelanggan, tabel_kamar.nomor_kamar, tabel_reservasi.tanggal_checkin, tabel_reservasi.tanggal_checkout
    -> FROM tabel_reservasi
    -> INNER JOIN tabel_pelanggan ON tabel_reservasi.id_pelanggan = tabel_reservasi.id_pelanggan
    -> INNER JOIN tabel_kamar ON tabel_kamar.id_kamar = tabel_kamar.id_kamar;


📌 INNER JOIN hanya menampilkan data yang memiliki relasi di semua tabel.

7. LEFT JOIN [Menampilkan semua pelanggan, termasuk yang belum reservasi].
MariaDB [db_hotel]> SELECT tabel_pelanggan.nama_pelanggan, tabel_reservasi.id_reservasi
    -> FROM tabel_pelanggan
    -> LEFT JOIN tabel_reservasi ON tabel_pelanggan.id_pelanggan = tabel_reservasi.id_pelanggan;
+----------------+--------------+
| nama_pelanggan | id_reservasi |
+----------------+--------------+
| athir          |            1 |
| ardo           |            2 |
| thoriq         |            3 |
| rizky          |         NULL |
+----------------+--------------+
4 rows in set (0.001 sec)

📌 rizky muncul walaupun belum reservasi.

8. Right Join [Menampilkan semua kamar, termasuk yang belum pernah dipesan].
MariaDB [db_hotel]> SELECT tabel_kamar.nomor_kamar, tabel_reservasi.id_reservasi
    -> FROM tabel_reservasi
    -> RIGHT JOIN tabel_kamar ON tabel_reservasi.id_kamar = tabel_kamar.id_kamar;
+-------------+--------------+
| nomor_kamar | id_reservasi |
+-------------+--------------+
| 100         |            2 |
| 101         |            1 |
| 102         |            3 |
| 103         |         NULL |
+-------------+--------------+
4 rows in set (0.001 sec)

📌 Kamar 103 muncul walaupun belum ada reservasi.
