
---
# Flag Command

### Deskripsi 
Mulailah "Quest Pelarian Dimensi" di mana Anda terbangun di labirin hutan misterius yang bukan berasal dari dunia ini. Jelajahi tupai bernyanyi, bidadari nakal, dan penyihir pemarah di labirin aneh yang mungkin membawa kejutan dari dunia lain. Akankah Anda menaklukkan labirin ajaib atau menemukan diri Anda tersesat dalam dimensi tantangan magis yang berbeda? Perjalanan terungkap dalam pelarian mistis ini!

### Analisis
Web teka teki 

### Penyelesaian 
Script 

```JS
// HTTP REQUESTS
// ---------------------------------------
async function CheckMessage() {
    fetchingResponse = true;
    currentCommand = commandHistory[commandHistory.length - 1];

    if (availableOptions[currentStep].includes(currentCommand) || availableOptions['secret'].includes(currentCommand)) {
        await fetch('/api/monitor', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ 'command': currentCommand })
        })
            .then((res) => res.json())
            .then(async (data) => {
                console.log(data)
                await displayLineInTerminal({ text: data.message });

                if(data.message.includes('Game over')) {
                    playerLost();
                    fetchingResponse = false;
                    return;
                }

                if(data.message.includes('HTB{')) {
                    playerWon();
                    fetchingResponse = false;

                    return;
                }

                if (currentCommand == 'HEAD NORTH') {
                    currentStep = '2';
                }
                else if (currentCommand == 'FOLLOW A MYSTERIOUS PATH') {
                    currentStep = '3'
                }
                else if (currentCommand == 'SET UP CAMP') {
                    currentStep = '4'
                }

                let lineBreak = document.createElement("br");


                beforeDiv.parentNode.insertBefore(lineBreak, beforeDiv);
                displayLineInTerminal({ text: '<span class="command">You have 4 options!</span>' })
                displayLinesInTerminal({ lines: availableOptions[currentStep] })
                fetchingResponse = false;
            });


    }
    else {
        displayLineInTerminal({ text: "You do realise its not a park where you can just play around and move around pick from options how are hard it is for you????" });
        fetchingResponse = false;
    }
```

Jawaban dari teka teki di dalam Web yang benar ialah :
- HEAD NORTH
- FOLLOW A MYSTERIOUS PATH
- SET UP CAMP
```
- Blip-Blop, in a pickle with a hiccup! Shmiggity-shmack
```

---


# KORP Terminal 

### Deskripsi 
Faksi Anda harus menyusup ke terminal KORP™ dan mendapatkan akses ke informasi istimewa Legiun serta mencari tahu lebih banyak tentang penyelenggara Fray. Layar login terminal dilindungi oleh enkripsi dan protokol keamanan canggih.

### Analisis
Web yang berisi login form memiliki kerentanan SQL Injection di parameter username.

### Penyelesaian 
- Melakukan SQL Injection dengan sqlmap
- Terdapat username admin tapi password ter-encrypt
- Brute force password admin dengan turbo intruder dan mendapat di password123

```
flag HTB {t3rm1n4l_cr4ck1ng_sh3n4nig4n5}
```


---


# TimeKORP

### Deskripsi 
Apakah Anda siap mengungkap misteri dan mengungkap kebenaran yang tersembunyi dalam domain digital KROP? Bergabunglah dengan tantangan ini dan buktikan kehebatan Anda di dunia keamanan siber. Ingat, waktu adalah uang, namun dalam kasus ini, imbalannya mungkin jauh lebih besar dari yang Anda bayangkan.

### Analisis
Dari source code yang diberikan, pada file config flag berada di directory yang mana ada clue untuk ***attack vector command injection***

### Penyelesaian