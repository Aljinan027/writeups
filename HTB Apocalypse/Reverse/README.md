
---
# LootStash

### Deskripsi
Sejumlah besar senjata dan perlengkapan kuat telah dijatuhkan ke arena - tapi ada satu item yang ada dalam pikiran Anda. Bisakah Anda memfilter tumpukan untuk mendapatkan satu hal yang benar-benar Anda butuhkan?

### Penyelesaian

Setelah menjalankan program beberapa kali output yang diberikan selalu berbeda, kami melakukan pencarian strings apa saja yang berada di dalam program dan mendapatkan string dengan format flag HTB. 

```bash
$ strings ./stash | grep HTB

HTB{n33dl3_1n_a_l00t_stack}
```

# BoxCutter

### Deskripsi
Anda telah menerima persediaan makanan dan obat-obatan yang berharga dari sponsor yang murah hati. Hanya ada satu masalah - kotaknya terbuat dari baja padat! Untungnya, ada robot pertahanan otomatis bodoh yang mungkin bisa Anda tipu agar membuka kotak itu untuk Anda - robot ini diprogram untuk hanya menyerang benda dengan label yang benar.

### Penyelesaian

Terdapat error `Box Not Found` saat berusaha menjalankan program tersebut. Langkah pertama untuk mengetahui apa yang terjadi pada program tersebut kami melakukan traccing menggunakan ltrace 



```bash
$ ltrace ./cutter

open("HTB{tr4c1ng_th3_c4ll5}", 0, 00)                                                                 = -1
puts("[X] Error: Box Not Found"[X] Error: Box Not Found
)                                                                      = 25
+++ exited (status 0) +++
```