
---
# Iced TEA

### Deskripsi
Terkunci di dalam kabin yang seluruhnya terbuat dari es, Anda diselimuti keheningan yang mengerikan. Mata Anda tertuju pada buku catatan tua, halaman-halamannya dihiasi ribuan simbol matematika yang samar. Ditugaskan untuk menguraikan mesin terbang yang penuh teka-teki ini untuk mengamankan pelarian Anda, Anda mulai bekerja, jari-jari Anda menelusuri setiap lengkungan dan garis yang rumit dengan tekad. Saat Anda mempelajari lebih dalam simbol-simbol misterius tersebut, Anda melihat bahwa pola muncul di beberapa halaman dan secercah harapan mulai muncul. Waktu terus berlalu dan suhu menurun, maukah Anda berhasil sebelum menyatu dengan kabin?

### Analisis
- 

### Penyelesaian 
```python
from Crypto.Util.Padding import unpad
from Crypto.Util.number import bytes_to_long as b2l, long_to_bytes as l2b
from enum import Enum

class Mode(Enum):
    ECB = 0x01
    CBC = 0x02

class Cipher:
    def __init__(self, key, iv=None):
        self.BLOCK_SIZE = 64
        self.KEY = [b2l(key[i:i+self.BLOCK_SIZE//16]) for i in range(0, len(key), self.BLOCK_SIZE//16)]
        self.DELTA = 0x9e3779b9
        self.IV = iv
        if self.IV:
            self.mode = Mode.CBC
        else:
            self.mode = Mode.ECB

    def _xor(self, a, b):
        return b''.join(bytes([_a ^ _b]) for _a, _b in zip(a, b))

    def decrypt(self, ct):
        blocks = [ct[i:i+self.BLOCK_SIZE//8] for i in range(0, len(ct), self.BLOCK_SIZE//8)]

        pt = b''
        if self.mode == Mode.ECB:
            for block in blocks:
                pt += self.decrypt_block(block)
        elif self.mode == Mode.CBC:
            X = self.IV
            for block in blocks:
                decrypted_block = self._xor(X, self.decrypt_block(block))
                pt += decrypted_block
                X = block
        return unpad(pt, self.BLOCK_SIZE//8)

    def decrypt_block(self, block):
        m = b2l(block)
        msk = (1 << (self.BLOCK_SIZE//2)) - 1

        m0 = (m >> (self.BLOCK_SIZE//2)) & msk
        m1 = m & msk

        s = self.DELTA << 5
        for i in range(32):
            m1 -= ((m0 << 4) + self.KEY[2]) ^ (m0 + s) ^ ((m0 >> 5) + self.KEY[3])
            m1 &= msk
            m0 -= ((m1 << 4) + self.KEY[0]) ^ (m1 + s) ^ ((m1 >> 5) + self.KEY[1])
            m0 &= msk
            s -= self.DELTA

        return l2b((m0 << (self.BLOCK_SIZE//2)) + m1)

# Bagian utama program untuk mendekripsi
if __name__ == '__main__':
    with open('output.txt', 'r') as f:
        lines = f.readlines()
        key_hex = lines[0].split(':')[1].strip()
        ct_hex = lines[1].split(':')[1].strip()

    KEY = bytes.fromhex(key_hex)
    CT = bytes.fromhex(ct_hex)

    cipher = Cipher(KEY)
    decrypted_text = cipher.decrypt(CT)

    print("Decrypted Text:", decrypted_text.decode('utf-8'))
```

---


# Dynasty 

### Deskripsi
Anda menemukan diri Anda terjebak di dalam kamar gas yang tertutup rapat, dan tiba-tiba, udara ditembus oleh suara terdistorsi yang diputar melalui kaset yang sudah direkam sebelumnya. Melalui transmisi yang menakutkan ini, Anda mengetahui bahwa dalam 15 menit ke depan, ruangan ini akan dibanjiri dengan hidrogen sianida yang mematikan. Saat pesan rekaman itu berakhir, suara mesin yang tiba-tiba berputar memenuhi ruangan, diikuti oleh detak jam yang tidak menyenangkan. Anda menyadari bahwa setiap ketukan adalah satu langkah lebih dekat dengan kematian. Kegelapan menyelimutimu, tangan kananmu diborgol, dan pintu keluar terkunci. Situasi Anda memburuk ketika Anda menyadari bahwa pintu dan borgol memerlukan kode sandi yang sama untuk membukanya. Kepanikan adalah sebuah kemewahan yang tidak mampu Anda beli; tindakan cepat sangat penting. Saat Anda menjelajahi sekeliling, jari-jari Anda yang gemetar menemukan obor. Seketika, setelah menekan tombolnya, ruangan itu bermandikan cahaya redup, memperlihatkan huruf-huruf samar yang terukir di dinding dan gambar mengganggu seorang kaisar Romawi yang berlumuran darah. Mendekripsi surat-surat itu akan memberi Anda kunci yang diperlukan untuk membuka kunci. Gunakan obor dengan bijak karena baterainya hampir habis!

### Analisis
- 


### Penyelesaian
```python
def from_identity_map(a):
    return chr(a % 26 + 0x41)

def to_identity_map(a):
    return ord(a) - 0x41

def decrypt(c):
    m = ''
    for i in range(len(c)):
        ch = c[i]
        if not ch.isalpha():
            # Jika karakter bukan alfabet, tetapkan ke m
            m += ch
        else:
            # Jika karakter adalah alfabet, konversi ke indeks identitas peta dan dekripsi
            chi = to_identity_map(ch)
            dm = from_identity_map(chi - i)
            m += dm
    return m

encrypted_message = "DJF_CTA_SWYH_NPDKK_MBZ_QPHTIGPMZY_KRZSQE?!_ZL_CN_PGLIMCU_YU_KJODME_RYGZXL"
decrypted_message = decrypt(encrypted_message)
print(decrypted_message)
```

---


# Primary Knowledge 

### Deskripsi
Dikelilingi oleh hutan liar dan perairan sungai Primus yang tenang, satu-satunya tujuan Anda adalah bertahan selama 24 jam. Namun, kelangsungan hidup masih jauh dari jaminan karena kawasan tersebut penuh dengan Ular Derik, Laba-laba, dan Aligator, serta cuaca yang berfluktuasi secara tidak terduga, berubah dari panas terik menjadi hujan deras setiap jamnya. Ancaman tersebut diperparah dengan adanya lingkaran maya yang mengecil setiap menitnya. Apa pun yang tertangkap di luar batasnya, akan habis dimakan api, hanya menyisakan abu di belakangnya. Seiring berlalunya waktu, Anda perlu memprioritaskan tindakan Anda untuk mengamankan alat Anda yang masih hidup. Setiap keputusan menjadi masalah hidup dan mati. Apakah Anda akan fokus untuk mendapatkan tempat berteduh untuk tidur, melindungi diri Anda dari bahaya alam liar, atau mencari cara untuk mengarungi perairan Primus?

### Analisis
- 

### Penyelesaian 
```python
from Crypto.Util.number import long_to_bytes

# Nilai n, e, dan c yang diberikan
n = 144595784022187052238125262458232959109987136704231245881870735843030914418780422519197073054193003090872912033596512666042758783502695953159051463566278382720140120749528617388336646147072604310690631290350467553484062369903150007357049541933018919332888376075574412714397536728967816658337874664379646535347
e = 65537
c = 15114190905253542247495696649766224943647565245575793033722173362381895081574269185793855569028304967185492350704248662115269163914175084627211079781200695659317523835901228170250632843476020488370822347715086086989906717932813405479321939826364601353394090531331666739056025477042690259429336665430591623215

# Fungsi untuk mencari invers modulo (dengan syarat e*d ≡ 1 (mod phi(n)))
def modinv(a, m):
    m0, x0, x1 = m, 0, 1
    while a > 1:
        q = a // m
        m, a = a % m, m
        x0, x1 = x1 - q * x0, x0
    return x1 + m0 if x1 < 0 else x1

# Menghitung nilai phi(n)
phi_n = n - 1

# Menghitung kunci privat d
d = modinv(e, phi_n)

# Melakukan dekripsi pesan c
m_decrypted = pow(c, d, n)

# Konversi nilai m_decrypted menjadi string (dalam bentuk bytes) dan mencetaknya
decrypted_message = long_to_bytes(m_decrypted).decode('utf-8')
print(f'Dekripsi pesan: {decrypted_message}')
```

---


# Makeshift

### Deskripsi
Lemah dan kelaparan, Anda berjuang untuk terus bekerja keras. Makanan adalah komoditas pada tahap ini, namun Anda tidak boleh kehilangan kewaspadaan - jika melakukan hal tersebut berarti kematian. Anda menyadari bahwa untuk bertahan hidup Anda memerlukan senjata, baik untuk membunuh maupun berburu, namun lapangannya kosong dari batu. Saat Anda menjatuhkan tubuh Anda ke lantai, sesuatu yang tajam mencuat dari semak-semak dan masuk ke paha Anda. Saat Anda memegang dan menariknya keluar, Anda menyadari bahwa itu adalah tongkat yang panjang; bukan senjata terbaik, tapi sekali diasah bisa menjadi perbedaan antara mati kelaparan dan mati terhormat dalam pertempuran.

### Analisis
- 

### Penyelesaian
```python
# Mengimpor nilai FLAG yang diubah dari modul secret
encrypted_flag = "!?}De!e3d_5n_nipaOw_3eTR3bt4{_THB"

# Inisialisasi string kosong untuk menyimpan nilai yang akan dikembalikan
recovered_flag = ''

# Menghitung panjang nilai yang diubah
length = len(encrypted_flag)

# Membuat loop untuk mengembalikan urutan karakter yang diubah
for i in range(0, length, 3):
    # Mengembalikan karakter ke-3 dari setiap set tripel
    recovered_flag += encrypted_flag[i+2]
    # Mengembalikan karakter ke-1 dari setiap set tripel
    recovered_flag += encrypted_flag[i]
    # Mengembalikan karakter ke-2 dari setiap set tripel
    recovered_flag += encrypted_flag[i+1]

# Mencetak hasil recovery
print(recovered_flag)
```