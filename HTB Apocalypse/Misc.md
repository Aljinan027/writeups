
---
# CHARACTER

### Deskripsi 
Keamanan melalui Kebosanan yang Diinduksi adalah pendekatan favorit pribadi saya. Tidak semenarik sesuatu seperti The Fray, tapi saya suka membuatnya sebodoh mungkin untuk melihat rahasia saya, jadi Anda hanya bisa mendapatkan satu karakter dalam satu waktu!

### Analisis
Diminta untuk memasukkan setiap index sesuai urutan flag. Jadi kami menggunakan automation bash script untuk mengirim setiap indeks dari pertanyaan tersebut.

### Penyelesaian
```bash
#!/bin/bash

# Set the IP address and port
IP_ADDRESS="94.237.60.112"
PORT="50146"

# Loop from index 1 to 1000
for ((i=1; i<=1000; i++)); do
    # Connect to the server and retrieve the character at the specified index
    character=$(echo "$i" | nc -w 1 "$IP_ADDRESS" "$PORT")

    # Check if the character is empty (no response from the server)
    if [ -z "$character" ]; then
        echo "Error: No response from the server at index $i. Exiting."
        exit 1
    fi

    # Print the result
    echo "Character at Index $i: $character"
done
```

### Flag
```
Flag=HTB{tH15_1s_4_r3aLly_l0nG_fL4g_i_h0p3_f0r_y0Ur_s4k3_tH4t_y0U_sCr1pTEd_tH1s_oR_els3_iT_t0oK_qU1t3_l0ng!!}
```