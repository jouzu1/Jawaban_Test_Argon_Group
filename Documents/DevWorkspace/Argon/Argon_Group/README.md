# Argon_Group
1.
````
CREATE TABLE Customer 
(
  KdCustomer VARCHAR(255) PRIMARY KEY,
  NmCustomer VARCHAR(255),
  Kota VARCHAR(255)
);

CREATE TABLE Barang 
(
  KdBarang VARCHAR(255) PRIMARY KEY,
  NmBarang VARCHAR(255),
  Stok INT,
  Harga NUMERIC(18,2)
);

CREATE TABLE Penjualan 
(
  NoFaktur VARCHAR(255) PRIMARY KEY,
  TglFaktur DATE,
  KdCustomer VARCHAR(255),
  KdBarang VARCHAR(255),
  Jumlah INT,
  FOREIGN KEY (KdCustomer) REFERENCES Customer(KdCustomer),
  FOREIGN KEY (KdBarang) REFERENCES Barang(KdBarang)
);
````
2.
````
-- Insert data pada tabel Customer
INSERT INTO Customer (KdCustomer, NmCustomer, Kota)
VALUES 
  ('C-003', 'PT.Maju Terus', 'Jakarta'),
  ('C-065', 'Toko Delapan', 'Bandung'),
  ('C-034', 'CV.Komala', 'Bandung'),
  ('C-109', 'PT.Samudra', 'Garut');

-- Insert data pada tabel Barang
INSERT INTO Barang (KdBarang, NmBarang, Stok, Harga)
VALUES 
  ('B-120', 'NIC D-Link', 15, 200000.00),
  ('B-121', 'Monitor 17', 15, 1100000.00),
  ('B-122', 'Memori 512', 20, 450000.00),
  ('B-123', 'Keyboard USB', 50, 125000.00),
  ('B-124', 'Mouse USB', 5, 60000.00);

-- Insert data pada tabel Penjualan
INSERT INTO Penjualan (NoFaktur, TglFaktur, KdCustomer, KdBarang, Jumlah)
VALUES 
  ('P-001', '10/1/2023', 'C-109', 'B-120', 1),
  ('P-002', '11/1/2023', 'C-003', 'B-124', 2),
  ('P-003', '11/1/2023', 'C-065', 'B-120', 1),
  ('P-004', '12/1/2023', 'C-109', 'B-122', 3);
````

3.
````
UPDATE Customer SET NmCustomer = 'CV.Komala Jaya', Kota = 'Cirebon' WHERE KdCustomer = 'C-034';
````
4.
````
SELECT TglFaktur
FROM Penjualan
JOIN Customer ON Penjualan.KdCustomer = Customer.KdCustomer
WHERE Customer.NmCustomer = 'PT.Samudra';
````

5.
````
SELECT KdBarang, NmBarang, Stok, Harga
FROM Barang
WHERE Stok > 15;
````

6.
````
SELECT DISTINCT c.NmCustomer, c.Kota
FROM Customer c
INNER JOIN Penjualan p ON c.KdCustomer = p.KdCustomer;
````

7.
````
SELECT NmCustomer
FROM Customer
WHERE Kota = 'Bandung'
UNION
SELECT NmCustomer
FROM Customer
WHERE Kota = 'Jakarta';
````

8.
````
SELECT SUM(Jumlah) AS TotalPenjualan
FROM Penjualan
JOIN Barang ON Penjualan.KdBarang = Barang.KdBarang
WHERE Barang.KdBarang = 'B-120';
````

9.
````
SELECT
  p.TglFaktur AS TglTransaksi,
  p.NoFaktur AS NoFaktur,
  c.NmCustomer AS NamaCustomer,
  b.NmBarang AS Item,
  p.Jumlah AS JumlahItem,
  b.Harga AS HargaItem,
  (p.Jumlah * b.Harga) AS TotalTransaksi
FROM
  Penjualan p
  JOIN Customer c ON p.KdCustomer = c.KdCustomer
  JOIN Barang b ON p.KdBarang = b.KdBarang
WHERE
  p.TglFaktur BETWEEN '2023-01-10' AND '2023-01-11'
ORDER BY
  p.TglFaktur ASC;
````

10.
````
SELECT NmCustomer FROM Customer;
````

11.
````
SELECT KdCustomer, NmCustomer, Kota
FROM Customer
ORDER BY NmCustomer ASC;
````

12.
````
SELECT KdBarang, NmBarang, Stok, Harga 
FROM Barang
WHERE NmBarang LIKE 'M%';
````

13.
````
-- Untuk nomor paling besar
SELECT MAX(nomor) as nomor_terbesar FROM A;

-- Untuk nomor paling kecil
SELECT MIN(nomor) as nomor_terkecil FROM A;
````
