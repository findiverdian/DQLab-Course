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
