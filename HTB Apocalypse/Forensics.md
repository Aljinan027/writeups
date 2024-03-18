
---
# It Has Begun

### Deskripsi
Keributan sudah dekat, dan tantangan pertama telah dirilis! Apakah kalian siap menjadi faksi!? Mengingat ini hanyalah permulaan, jika Anda tidak dapat mengerahkan kerja tim yang dibutuhkan sedini ini, kemungkinan besar kehancuran Anda tidak dapat dihindari.

### Analisis

### Penyelesaian


---


# An Unusual Sighting

### Deskripsi 
Saat persiapan hampir berakhir, dan The Fray semakin dekat setiap harinya, tim kami yang baru dibentuk telah mulai mengerjakan pemfaktoran ulang aplikasi CMS baru untuk kompetisi. Namun, setelah beberapa waktu kami menyadari bahwa banyak pekerjaan kami yang hilang secara misterius! Kami berhasil mengekstrak Log SSH dan Riwayat Bash dari server dev kami yang dimaksud. Faksi yang berhasil mengungkap pelaku akan mendapat bonus besar dalam kompetisi!

### Analisis


### Penyelesaian
```bash
What is the IP Address and Port of the SSH Server (IP:PORT)

> 100.107.36.130:2221

What time is the first successful Login
> 2024-02-13 11:29:50

What is the time of the unusual Login

> 2024-02-19 04:00:14

What is the Fingerprint of the attackers public key

> OPkBSs6okUKraq8pYo4XwwBg55QSo210F09FCe1-yj4

What is the first command the attacker executed after logging in
> whoami

What is the final command the attacker executed before logging out

> ./setup


HTB{B3sT_0f_luck_1n_th3_Fr4y!!}
```


---


# Urgent

### Deskripsi 
Di tengah "Fray" Cybercity, serangan phishing menargetkan faksi-faksinya, sehingga memicu kekacauan. Saat mereka memecahkan kode email tersebut, para detektif dunia maya berlomba untuk melacak sumbernya, dengan tenggat waktu yang ketat. Misi mereka: membuka kedok penyerang dan memulihkan ketertiban kota. Di jalanan yang diterangi lampu neon, pertarungan demi keadilan dunia maya terjadi dan menentukan nasib faksi-faksi tersebut.

### Analisis
Diberikan file dengan tipe .eml yang mana isi file berupa text yang harus di Decrypt untuk mendapatkan Flag.
Decrypt teks paling bawah ke base 64 dan URL Decode.

### Penyelesaian
