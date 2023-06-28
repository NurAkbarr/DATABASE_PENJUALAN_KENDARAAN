## Kelompok 3

```
1. FADHLUROHMAN FATIKH NAVINTINO
2. MUHAMMAD FARHAN FAHREZA
3. ASSANDRA JULYANT FIRDHAUSY
4. NURUL AKBAR
5. EGA CHATRINA BUDDY
```

## DAFTAR ISI

Menu

- ERD
- DDL
- SQL CRUD
- SQL JOIN

# DATABASE PENJUALAN KENDARAAN

• Mengelola data Kendaraan
• Mengelola data Customer
• Mengelola data Sales
• Mengelola data Transaksi penjualan
• Laporan Transaksi

## _ER-D_

ERD Penjualan Kendaraan
[img](gambar/ERD.png)
Dalam ERD tersebut terdapat 5 entitas utama yaitu sebagai berikut :

1. customer
2. sales
3. kendaraan
4. transaksi
5. laporan_transaksi

Adapun relasi dan kardinalitasnya adalah sebagai berikut :

1. customer berelasi dengan sales, dengan relasi many to one (n:1)
2. sales berelasi dengan kendaraan, dengan relasi one to many (1:m)
3. sales berelasi dengan transaksi, dengan relasi one to one (1:1)
4. customer berelasi dengan transaksi, dengan relasi one to one (1:1)
5. kendaran berelasi dengan transaksi, dengan relasi one to one (1:1)
6. transaksi berelasi dengan laporan, dengan relasi one to one (1:1)

Berikut adalah penjelasan untuk setiap relasi dalam ERD Penjualan Kendaraan:

1. Relasi antara entitas "customer" dan "sales" (many to one):

- Setiap "customer" dapat memiliki hubungan dengan satu atau lebih "sales".
- Namun, setiap "sales" hanya terkait dengan satu "customer".
- Ini menunjukkan bahwa banyak pelanggan dapat dilayani oleh satu penjualan (misalnya, satu salesperson dapat melayani beberapa pelanggan).

2. Relasi antara entitas "sales" dan "kendaraan" (one to many):

- Setiap "sales" dapat memiliki hubungan dengan satu atau lebih "kendaraan".
- Namun, setiap "kendaraan" hanya terkait dengan satu "sales".
- Ini menunjukkan bahwa satu penjualan dapat melibatkan beberapa kendaraan (misalnya, satu salesperson dapat menjual beberapa kendaraan kepada pelanggan).

3. Relasi antara entitas "sales" dan "transaksi" (one to one):

- Setiap "sales" terkait dengan satu "transaksi".
- Dan setiap "transaksi" hanya terkait dengan satu "sales".
- Ini menunjukkan bahwa satu penjualan dapat menghasilkan satu transaksi.

4. Relasi antara entitas "customer" dan "transaksi" (one to one):

- Setiap "customer" terkait dengan satu "transaksi".
- Dan setiap "transaksi" hanya terkait dengan satu "customer".
- Ini menunjukkan bahwa satu pelanggan dapat memiliki satu transaksi (misalnya, pembelian kendaraan oleh pelanggan).

5. Relasi antara entitas "kendaraan" dan "transaksi" (one to one):

- Setiap "kendaraan" terkait dengan satu "transaksi".
- Dan setiap "transaksi" hanya terkait dengan satu "kendaraan".
- Ini menunjukkan bahwa satu kendaraan terjual dalam satu transaksi.

6. Relasi antara entitas "transaksi" dan "laporan_transaksi" (one to one):

- Setiap "transaksi" terkait dengan satu "laporan_transaksi".
- Dan setiap "laporan_transaksi" hanya terkait dengan satu "transaksi".
- Ini menunjukkan bahwa setiap transaksi memiliki satu laporan transaksi terkait yang berisi informasi dan detail penting tentang transaksi tersebut.

## _DDL Script_

```sql
SHOW DATABASES;
```

```sql
CREATE DATABASE penjualan_kendaraan;
```

```sql
USE penjualan_kendaraan;
```

```sql
SHOW TABLES;
```

```sql
DESC customer;
```

```sql
DESC sales;
```

```sql
DESC kendaraan;
```

```sql
DESC transaksi;
```

```sql
DESC laporan_transaksi;
```

```sql
CREATE TABLE customer (
id_customer INT PRIMARY KEY,
nama VARCHAR(50),
alamat VARCHAR(50),
email VARCHAR(50),
no_telepon NUMERIC(12),
nik INT(16),
id_sales INT
);
```

```sql
CREATE TABLE sales (
id_sales INT PRIMARY KEY,
nama VARCHAR(50),
alamat VARCHAR(50),
email VARHCAR(50)
no_telpon NUMERIC(12)
);
```

```sql
CREATE TABLE kendaraan (
id_kendaraan INT PRIMARY KEY,
merk VARCHAR(20),
nama VARCHAR(50),
stok INT,
harga VARCHAR(12),
id_sales INT
);
```

```sql
CREATE TABLE transaksi (
id_transaksi INT PRIMARY KEY,
jumlah_pembelian INT,
id_sales INT,
id_customer INT,
id_kendaraan INT
);
```

```sql
CREATE TABLE laporan_transaksi (
id_laporan INT PRIMARY KEY,
tanggal DATE,
id_transaksi
);
```

```sql
ALTER TABLE `customer`
ADD PRIMARY KEY (`id_customer`),
ADD KEY `id_sales` (`id_sales`);
```

```sql
ALTER TABLE `kendaraan`
ADD PRIMARY KEY (`id_kendaraan`),
ADD KEY `id_sales` (`id_sales`);
```

```sql
ALTER TABLE `laporan_transaksi`
ADD PRIMARY KEY (`id_laporan`),
ADD KEY `id_transaksi` (`id_transaksi`);
```

```sql
ALTER TABLE `sales`
ADD PRIMARY KEY (`id_sales`);
```

```sql
ALTER TABLE `transaksi`
ADD PRIMARY KEY (`id_transaksi`),
ADD KEY `id_customer` (`id_customer`),
ADD KEY `id_sales` (`id_sales`),
ADD KEY `id_kendaraan` (`id_kendaraan`);
```

```sql
ALTER TABLE `customer`
ADD CONSTRAINT `customer_ibfk_1` FOREIGN KEY (`id_sales`) REFERENCES `sales` (`id_sales`);
```

```sql
ALTER TABLE `kendaraan`
ADD CONSTRAINT `kendaraan_ibfk_1` FOREIGN KEY (`id_sales`) REFERENCES `sales` (`id_sales`);
```

```sql
ALTER TABLE `laporan_transaksi`
ADD CONSTRAINT `laporan_transaksi_ibfk_1` FOREIGN KEY (`id_transaksi`) REFERENCES `transaksi` (`id_transaksi`);
```

```sql
ALTER TABLE `transaksi`
ADD CONSTRAINT `transaksi_ibfk_1` FOREIGN KEY (`id_customer`) REFERENCES `customer` (`id_customer`),
ADD CONSTRAINT `transaksi_ibfk_2` FOREIGN KEY (`id_sales`) REFERENCES `sales` (`id_sales`),
ADD CONSTRAINT `transaksi_ibfk_3` FOREIGN KEY (`id_kendaraan`) REFERENCES `kendaraan` (`id_kendaraan`);
COMMIT;
```

## _SQL CRUD Script_

```sql
INSERT INTO customer (id_customer,nama,alamat,email,no_telpon,nik,id_sales) VALUES
('1','John Doe','Jl. Contoh 123','johndoe@example.com','123456789','214783647','1'),
('2','Jane Smith','Jl. Contoh 456','janesmith@example.com','9876543210','214783647','2'),
('3','David Johnson','Jl. Contoh 789','davidjohnson@example.com','2468135790','214783647','3');
```

```sql
INSERT INTO sales (id_sales,nama,alamat,email,no_telpon) VALUES
('1','Mark Anderson','Jl. Sales 123','markanderson@example.com','1111111111'),
('2','Lisa Thompson','Jl. Sales 456','lisathompson@example.com','2222222222'),
('3','Steven Davis','Jl. Sales 789','stevendavis@example.com','3333333333');
```

```sql
INSERT INTO kendaraan (id_kendaraan,merk,nama,stok,harga,id_sales) VALUES
('1','Honda','Civic','5','200000000','1'),
('2','Toyota','Corolla','3','220000000','2'),
('3','Nissan','X-Trail','2','250000000','1');
```

```sql
INSERT INTO jtransaksi (id_transaksi,jumlah_pembelian,id_sales,id_customer,id_kendaraa) VALUES
('1','2','1','1','1'),
('2','1','2','2','2'),
('3','3','3','3','3');
```

```sql
INSERT INTO laporan_transaksi (id_laporan,tanggal,id_transaksi) VALUES
('1','2023-06-01','1'),
('2','2023-06-05','2'),
('3','2023-06-09','3');
```

```sql
SELECT \* FROM customer;
```

```sql
SELECT \* FROM sales;
```

```sql
SELECT \* FROM kendaraan;
```

```sql
SELECT \* FROM transaksi;
```

```sql
SELECT \* FROM laporan_transaksi;
```

```sql
UPDATE customer
SET alamat = 'jl. Baru No. 123'
WHERE id_customer = 1;
```

```sql
UPDATE transaksi
SET jumlah_pembelian = 5
WHERE id_transaksi = 1;
```

```sql
DELETE FROM transaksi
WHERE id_customer = 2;
```

```sql
DELETE FROM customer
WHERE id_customer = 2;
```

## _SQL JOIN Script_

```sql
SELECT _
FROM customer
LEFT JOIN sales ON customer.id_sales = sales.id_sales
UNION
SELECT _
FROM customer
RIGHT JOIN sales ON customer.id_sales = sales.id_sales;
```

```sql
SELECT \*
FROM customer
INNER JOIN sales ON customer.id_sales = sales.id_sales;
```

```sql
SELECT \*
FROM customer
LEFT JOIN sales ON customer.id_sales = sales.id_sales;
```

```sql
SELECT \*
FROM customer
RIGHT JOIN sales ON customer.id_sales = sales.id_sales;
```

## *Selesai*
