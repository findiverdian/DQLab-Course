# Day One Project DQLab 
“Jadi, apakah kamu bisa menyiapkan data transaksi penjualan dengan total revenue >= IDR 100.000? 

Format datanya yang akan kamu tampilkan adalah: kode_pelanggan, nama_produk, qty, harga, dan total, serta diurutkan mulai dari total revenue terbesar,” pinta Senja padaku.
Kalau kasusnya seperti ini, berarti aku perlu meng-query data tersebut dari tabel tr_penjualan yang terdapat di database perusahaan.
Aku dapat melakukan
1. Perkalian antara kolom qty dan harga untuk memperoleh total revenue setiap kode pelanggan yang dinyatakan ke dalam kolom total,
2. Menggunakan “ORDER BY total DESC” pada akhir query untuk mengurutkan data.
Aku pun menerima tantangan proyek ini! Senja pun segera mengirim detailnya melalui email yang berisi contoh tabel sebagai berikut untuk segera kukerjakan.
![image](https://user-images.githubusercontent.com/110141670/188921409-37fd3e8f-28da-4ed8-8fe6-f7ba63f3caa0.png)


## The Syntax
(SELECT kode_pelanggan, nama_produk,qty,harga,qty * harga AS total FROM tr_penjualan WHERE qty * harga >= 100000 
ORDER BY total DESC;)


## The Final Table 
![image](https://user-images.githubusercontent.com/110141670/188921527-90152ca4-6cc0-428c-935d-77ae270a0844.png)

# DAY TWO

## Gunakan fungsi UPPER() untuk mengubah kolom FirstName menjadi seluruhnya kapital dan gunakan LOWER() untuk mengubah kolom LastName menjadi seluruhnya non-kapital. Gunakan kedua fungsi tersebut dalam satu SELECT-Statement.

SELECT StudentID, UPPER(FirstName) as FirstName, LOWER(LastName) as LastName

FROM students;

## Gunakan fungsi MIN() dan MAX() untuk menghitung nilai dari kolom Semester1 dan Semester2. Aku menggunakan fungsi tersebut dalam satu SELECT-Statement.

SELECT MIN(Semester1) as Min1,MAX(Semester1) as Max1,MIN(Semester2) as Min2, MAX(Semester2) as Max2

FROM students;

## Group by Single Column

Fungsi Group by Single Column memastikan data dapat dikelompokkan menggunakan kriteria dari satu kolom saja, misalnya mengelompokkan data berdasarkan provinsi saja

SELECT province,

COUNT(DISTINCT order_id) as total_order,

SUM(item_price) as total_price

FROM sales_retail_2019

GROUP BY province;

## Group by Multiple Column

Dengan fungsi Group by Multiple Column, data dapat dikelompokkan menggunakan kriteria dari dua kolom atau lebih, misalnya mengelompokkan data berdasarkan province dan brand.

SELECT province, brand,

COUNT(DISTINCT order_id) as total_order,

SUM(item_price) as total_price FROM sales_retail_2019

GROUP BY province, brand;

## Fungsi Aggregate dengan Grouping

Sekarang coba kamu gunakan fungsi agregasi dan GROUP BY untuk menghitung total penjualan dari setiap provinsi di tahun 2019, dan kita bandingkan dengan hasil fungsi agregasi tanpa menggunakan group by

SELECT province, COUNT(DISTINCT order_id) as total_unique_order, SUM(item_price) as revenue FROM sales_retail_2019

GROUP BY province;

# Tugas:
Dengan menggunakan data sales_retail_2019,  buatlah syntax query yang menggunakan fungsi skalar MONTH() untuk mengubah order_date dari tanggal ke bulan, fungsi aggregate SUM() untuk menjumlahkan kolom item_price.

Tambahkan kolom remark menggunakan CASE… WHEN… statement. Jika sum(item_price) >= 30.000.000.000, maka remark-nya 'Target Achieved'; Jika sum(item_price) <= 25.000.000.000 maka remark-nya 'Less performed'; Selain itu, beri remark 'Follow Up'.
SELECT MONTH(order_date) AS order_month, SUM(item_price) AS total_price, 

CASE  
    WHEN sum(item_price) >= 30000000000 THEN 'Target Achieved'
    WHEN sum(item_price) <= 25000000000 THEN 'Less Performed'
    ELSE 'Follow Up'

END as remark

FROM sales_retail_2019

GROUP BY MONTH(order_date);

Proyek Pekerjaan - Analisis Penjualan Part 1

Aku pun membuka email proyek dari Senja sambil menyeruput boba milk tea favoritku.

 

# Saya mau minta tolong agar kamu melakukan analisis penjualan di suatu store. Adapun laporan yang diminta sebagai berikut:

Total jumlah seluruh penjualan (total/revenue).
Total quantity seluruh produk yang terjual.
Total quantity dan total revenue untuk setiap kode produk.
Rata - Rata total belanja per kode pelanggan.
Selain itu,  jangan lupa untuk menambahkan kolom baru dengan nama ‘kategori’ yang mengkategorikan total/revenue ke dalam 3 kategori: High: > 300K; Medium: 100K - 300K; Low: <100K.
Tabel: tr_penjualan
## 1. Total jumlah seluruh penjualan (total/revenue).
SELECT SUM(total) as total 

FROM tr_penjualan;

## 2. Total quantity seluruh produk yang terjual.
SELECT SUM(qty) as qty 

FROM tr_penjualan;
## 3. Total quantity dan total revenue untuk setiap kode produk.
SELECT kode_produk, SUM(qty) as qty, SUM(total) as total 

FROM tr_penjualan

GROUP BY kode_produk;

## 4. Rata - Rata total belanja per kode pelanggan.
SELECT kode_pelanggan, AVG(total) as avg_total 

FROM tr_penjualan

GROUP BY kode_pelanggan;
## 5. Selain itu,  jangan lupa untuk menambahkan kolom baru dengan nama ‘kategori’ yang mengkategorikan total/revenue ke dalam 3 kategori: High: > 300K; Medium: 100K - 300K; Low: <100K.
SELECT kode_transaksi,kode_pelanggan,no_urut,kode_produk, nama_produk, qty, total,

CASE  
    WHEN total > 300000 THEN 'High'
    WHEN total < 100000 THEN 'Low'   
    ELSE 'Medium'  

END as kategori 

FROM tr_penjualan;

# DAY THREE
## Dalam database, terdapat tabel ms_pelanggan yang berisi data - data pelanggan yang membeli produk dan tabel tr_penjualan yang berisi data transaksi pembelian di suatu store.
Suatu hari, departemen marketing & promotion meminta bantuan untuk meng-query data-data pelanggan yang membeli produk Kotak Pensil DQLab, Flashdisk DQLab 32 GB, dan Sticky Notes DQLab 500 sheets.

Buatlah query menggunakan tabel ms_pelanggan dan tr_penjualan untuk mendapatkan data - data yang diminta oleh marketing yaitu kode_pelanggan, nama_customer, alamat.
NB: Gunakan SELECT DISTINCT untuk menghilangkan duplikasi, jika diperlukan.

SELECT DISTINCT ms_pelanggan.kode_pelanggan, ms_pelanggan.nama_customer, ms_pelanggan.alamat

FROM ms_pelanggan

INNER JOIN tr_penjualan

ON ms_pelanggan.kode_pelanggan = tr_penjualan.kode_pelanggan

WHERE tr_penjualan.nama_produk = 'Kotak Pensil DQLab'OR tr_penjualan.nama_produk = 'Flashdisk DQLab 32 GB'OR tr_penjualan.nama_produk = 'Sticky Notes DQLab 500 sheets';

## Persiapkanlah data katalog mengenai mengenai nama - nama produk yang akan dijual di suatu store. Data tersebut akan digunakan dalam meeting untuk mereview produk mana saja yang akan dilanjutkan penjualannya dan mana yang tidak akan dilanjutkan.
Siapkan hanya data produk dengan harga di bawah 100K untuk kode produk prod-1 sampai prod-5; dan dibawah 50K untuk kode produk prod-6 sampai prod-10, tanpa mencantumkan kolom no_urut.

Saat mengecek data produk di database, terdapat 2 tabel yang sama - sama berisi data katalog, yaitu:

SELECT nama_produk, kode_produk, harga FROM ms_produk_1 WHERE harga <100000

UNION 

SELECT  nama_produk,kode_produk, harga FROM ms_produk_2 WHERE harga <50000;

## Contoh penggunaan HAVING
Untuk penggunaan HAVING pada data yang ada pada bab sebelumnya, kita akan mencari customer_id yang melakukan perpindahan
subscription pada table subscription. 
Teman-teman silahkan mengikuti query dibawah ini

SELECT customer_id FROM Subscription GROUP BY customer_id HAVING COUNT(customer_id) > 1;
Menampilkan Konsumen yang berubah berlangganan

Selanjutnya kita akan menampilkan perubahan yang dilakukan konsumen tersebut.
Sekarang teman-teman melengkapi query yang ada di code editor dengan menampilkan:

1.	customer_id

2.	product_id

3.	subscription_date

SELECT 

customer_id,

product_id,

subscription_date

FROM Subscription 

WHERE customer_id IN 

(SELECT 

customer_id 

FROM Subscription 

GROUP BY customer_id 

HAVING COUNT(customer_id) > 1

) 

ORDER BY customer_id ASC;

## Menampilkan detail konsumen
Sekarang kita coba menggabungkan ilmu yang sudah ada sebelumnya.
Kita menggunakan JOIN untuk mendapatkan data dari table customer.
Tugas Praktek
Isikan bagian yang kosong dengan melakukan JOIN table subscription dan customer dengan menggabungkan
customer_id dari table subscription dan id dari table customer

SELECT 

b.name,

b.address,

b.phone, 

a.product_id, 

a.subscription_date 

FROM subscription a 

JOIN customer b 

ON a.customer_id=b.id

WHERE b.id IN 

(

SELECT 

customer_id 

FROM Subscription 

GROUP BY customer_id 

HAVING COUNT(customer_id) > 1

) 

ORDER BY b.id ASC;
