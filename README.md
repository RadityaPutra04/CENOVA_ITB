# CENOVA_ITB
---
Masalah: 
- tentang permasalahan dimana Poin SKKM di Kampus PNB yang dirasa tidak Konsisten dalam menetapkan poin dan selalu berubah ubah serta tidak adanya transparansi dalam proses pemberian poin.
- ketidaktahuan Poin SKKM yang FIX membuat mahasiswa harus terus bertanya serta menghitung dan mengingat poin mereka secara terus menerus

---
analisis masalah fitur dll:
1. OCR adalah fitur yang unik dan sulit untuk dieksekusi. namun jika dapat dilakukan maka (1) OCR perlu dilatih agar bisa mengenali pola berupa "Tingkat, Peserta, Panitia, Juara 1-3, Juara harapan 1-3". Jika gagal, maka hasil foto scan sertif dapat di cek sendiri oleh manusia (alias man in the loop) yang mana berarti setiap hasil scan "harus tersimpan"

---
ide fitur:
1. nanta - [fitur kalkulasi dimana user memilih opsi kegiatan, tingkat, dan sebagai apa maka hasil poin akan muncul]
problem: di fiturnya bagian "Baris 1: Pilih Kepanitiaan -> BEM -> Anggota = otomatis muncul 2 Poin.
     * Baris 2: Pilih Prestasi Penalaran -> Nasional -> Juara I = otomatis muncul 6 Poin.
     * Sistem langsung menjumlahkan total di bawah tabel menjadi 8 Poin." 
     agak aneh secara alur? bukan aneh, tapi lebih ke tidak efektif karna user harus input banyak kali, user juga bisa sabotase nilai dengan asal memasuki kategori atau sebagai apa
     
- saran: agak aneh karena kita kan bilang make ocr, harusny hasil scan disimpen terus langsung dikalkulasi, poin SKKM keliatan + hasil scan kesimpen. tapi fitur diatas cocok kalau memang ada mode manual dan memang penasaran dengan jumlah poin saat itu juga atau terjadi sistem fall pada scanning atau uploading file. dan juga di akhir akan diminta sebuah file yang berisi bukti bahwa data sebelumnya valid. jika tidak maka user akan diminta untuk input ulang.


---
Flow:
Alur user as Mahasiswa:
1. login dengan nama, nim, jurusan, prodi.
2. menampilkan menu Hero yang berisi 3 opsi: scan, upload file, kalkulator manual (case Nanta)
     if Scan & berhasil:
     1. izin mengakses kamera user untuk mengambil foto
     2. hasil foto akan di cek oleh ocr dengan menyamakan pola pada poin (1) di "analisis masalah fitur dll" yang kemudian akan otomatis tersimpan di data Mahasiswa dan disimpan di arsip > document
     3. hasil poin akan disimpan ke data mahasiswa dan ditampilkan ke dashboard
       if scan & gagal:
        1. hasil scan akan disimpan dan di kirim ke verifikator untuk mengecek apakah ia masuk ke kategori tertentu
           
     if Upload file"
     1. jendela file muncul, user memilih file PDF (biasanya sertifikat sudah dalam bentuk PDF, jika tidak maka user harus konvert ke PDF)
     2. file PDF yang di upload akan di scan oleh OCR dengan pola (1) di "analisis masalah fitur dll" dan hasil poin akan disimpan ke data mahasiswa dan ditampilkan ke dashboard
        
     if Kalkulator manual/input manual:
     1. User diberi kolom atau opsi untuk memasukan data "Kegiatan, Tingkat, Dan sebagai apa" untuk mengecek nilai
     2. dibagian akhir user perlu mengirim file asli sertifikat untuk mengecek apakah input user valid untuk menghindari sabotase poin
     3. jika sesuai maka akan ditampilkan pop up total poin dan user dilempar ke dashboard. data akan disimpan ke data mahasiswa dan disimpan di arsip > document
     4. jika gagal, user disuruh menginput ulang sampai data Valid
  
Alur user as Admin
1. login sebagai admin.
2. menampilkan menu dashboard admin
3. admin mengupload File Peraturan Poin agar sistem OCR dapat mengkalkulasikan poin mahasiswa (problem: apakah OCR cukup pintar untuk menentukan pola?)
   if tidak, maka file HARUS memiliki format yang dapat dimengerti OCR.
     contoh: {{teks1}} = "kondisi1"
             {{teks2}} = "kondisi2"
             {{Pola}}  = "kondisiPola, KondisiPola2, ..."
4. Hasil ouput dari proses masukan File peraturan poin akan diumumkan ke semua orang agar orang tidak bingung jika ternyata peraturan dirubah mendadak.
   (dalam suatu web Server hosting game yang ku beli, mereka seperti melakukan refresh tiap sekian detik namun tidak mempengaruhi input user sampai user menekan tombol "save", mungkin bisa gunakan metode ini juga)






