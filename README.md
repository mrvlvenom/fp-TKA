# 🔥 FINAL PROJECT (FP) TEKNOLOGI KOMPUTASI AWAN 🔥

# Final Project 
### Teknologi Komputasi Awan

**Kelas A**

**Kelompok 1**
|Nama|NRP  |
|--|--|
|Bhisma Elki Pratama|5027221005|
|M. Januar Eko Wicaksono|5027221006|
|Jeany Aurellia Putri Dewati|5027221008|
|Siti Nur Ellyzah|5027221014|

## Permasalahan
Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Kemampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.(menurut kurikulum IT ITS 2023 😙)

Pada suatu saat teman anda ingin mengajak anda memulai bisnis di bidang digital marketing, anda diberikan sebuah aplikasi berbasis API File: app.py dengan spesifikasi sebagai berikut.

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah 1 juta rupiah per bulan (65 US$) konfigurasi cloud terbaik seperti apa yang bisa dibuat?

## Rancangan Arsitektur dan Tabel Harga Spesifikasi VM
- Berikut adalah rancangan arsitektur yang telah kami buat untuk final project kami
![arsitektur](./img/archi.png)
- Kami memilih untuk menggunakan Digital Ocean sebagai lingkungan cloud yang akan kami gunakan. Berikut adalah tabel harga spesifikasi VM yang kami buat <br>
![tabel harga](./img/table.png)

## Langkah Implementasi dan Konfigurasi Teknologi
1. Buat database dan copy connection string
![e9bf51bc-fff5-416d-9208-c6f6ab0734e7](./img/createdb.jpg)

2. Create new connection dengan string database yang sudah di-copy sebelumnya
![0b04f257-0ef6-48e9-988b-1737c8475b16](./img/newconnect.jpg)

3. Buat database sesuai dengan variabel yang sudah dibuat di dalam app.py
![Screenshot 2023-12-13 133954](./img/code.jpg)

4. Create database baru dengan collection order, add data (import json file)lalu pilih file orders.json yang berisi data-data yang akan dimasukan ke database<br>
![268eff90-912c-475b-b165-7919dc1d8d74](./img/inputdata.jpg)

5. Run app.py hingga muncul url-nya
![73269c30-c764-4838-867b-f74991970945](./img/runpy.jpg)

6. Untuk mengecek database-nya bisa menggunakan postman, request ke url/orders. Jika statusnya sudah 200 ok, maka database sudah bisa berjalan dengan normal
![73269c30-c764-4838-867b-f74991970945](./img/postman.jpg)

7. Deploy VM untuk worker dengan installasi requirement yang diperlukan di worker
![8d40b7fd-b13c-4b93-828f-97572effd529](./img/deploy.png)

8. Install Nginx pada VM load Balancer, kemudian konfigurasikan dengan IP Address yang dimiliki oleh kedua worker, didalam konfigurasi nginx. Seperti dibawah ini:
![Konfigurasi Nginx](./img/konfigurasi_nginx.jpg)

9. Kemudian jalankan nginx, dengan cara dibawah ini:
![Run Nginx](./img/run_nginx.jpg)

10. Setelah itu, IP Address dari loud balancer yang ada di digital ocean diuji coba, jika muncul database seperti dibawah ini maka sudah berhasil:
![Database](./img/database.jpg)

11. Jika tidak ada error, maka worker sudah berjalan

## Hasil Pengujian Setiap Endpoint
1. Get All Orders
![get all orders](./img/postman.jpg)

2. Get a Specific Orders by ID
![get order by id](./img/getid.jpg)

3. Create a New Order
![create](./img/create.jpg)

4. Update an Order by ID
![update order](./img/updateid.jpg)

5. Delete an Order by ID
![delete](./img/deleteid.jpg)

## Hasil Pengujian dan Analisis Loadtesting Locust
1. Endpoint Get Order pada Load Balancing yang menajalankan 1 worker nginx sebagai load balancing pada 1 device
- RPS Maksimum (load testing 60 detik)
- Peak Concurrency Maksimum (spawn rate 25, load testing 60 detik)

- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)

- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)
![Result-charts](./img/result.jpg)
![Results](./img/result_1.jpg)


## Kesimpulan dan Saran
- Setelah melakukan pengecekan harga antara Azure dan Digital Ocean, ternyata harga untuk digital ocean lebih murah dibandingkan azure.
- Setelah melakukan percobaan, testing pada locust. Ketika spawn rate lebih rendah, persentase failures nya itu lebih kecil dibandingkan dengan spawn rate yang lebih tinggi  hingga 0% untuk persentasi failurse nya. Seperti pada grafik diatas.
- Setelah percobaan yang kami lakukan berulang kali, jumlah load balancer sebaiknya sama dengan jumlah worker karena ketika kami mencoba menggunakan 1 load balancer dan 3 worker terjadi down pada ketiga worker tersebut.
![a78daaeb-889e-458f-aa5b-e7457f011a95](./img/simpul.png)
