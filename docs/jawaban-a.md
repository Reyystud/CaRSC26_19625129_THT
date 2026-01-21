# **Jawaban untuk nomer A1**
_gundampegasus@gmail.com_

# **Jawaban untuk nomer A2**

**a. Sebutkan setidaknya 4 commands dalam Git dan jelaskan kegunaan serta contoh penggunaannya.**
1. **git init**, ini biasanya digunakan untuk menginialisasi repository Git baru (contoh: git init)
2. **git status**, untuk menampilkan status file dalam repo (contoh: git status)
3. **git add**, untuk menambahkan file ke staging area (contoh: git add .)
4. **git commit**, untuk menyimpan perubahan ke repo dengan pesan (contoh: git commit -m "add initial files")

**b. Lakukan setup untuk menghubungkan Git dan VSCode dengan GitHub.**

Untuk setup dari github ke VSCode udah pernah aku lakuin sebelum" ini dan perubahan file dapat terdeteksi secara otomatis pada tab Source Control, serta branch aktif dapat terlihat dan dikelola langsung dari VSCode.

Screenshot bukti VSCode udah terintegrasi sama GitHub:
![Integrated](../src/a/2b/intgrtd.jpeg)

Screenshot tab Source Control pada VSCode:
![Source Control](../src/a/2b/sourcectl.jpeg)

**c. Tamatkan 4 topik Main pertama (hingga 4: Rebase Introduction) dan 6 topik Remote pertama (hingga 6: Git Pushin') di https://learngitbranching.js.org**

Aku udah selesaiin 4 topik pertama pada bagian Main hingga Rebase Introduction serta 6 topik pertama pada bagian Remote hingga Git Pushin' di situs Learn Git Branching.

Screenshot sebagai bukti penyelesaian:
![Main](../src/a/2c/gitmain.jpeg)
![Remote](../src/a/2c/gitremote.jpeg)

**d. Pelajari bagaimana Git dan GitHub berkomunikasi dengan SSH (Secure Shell)**

Aku udah belajar tentang mekanisme komunikasi Git dan GitHub menggunakan SSH (Secure Shell), di mana autentikasi dilakukan menggunakan pasangan public key dan private key tanpa perlu memasukkan username dan password setiap kali melakukan operasi Git. Dan juga, udah ngerjain exercise "Git SSH Security" pada W3Schools sebagai bukti pemahaman terkait penggunaan SSH dalam Git.

Screenshot bukti penyelesaian exercise:
![Exercise](../src/a/2d/exercisessh.jpeg)

**e Branching dan Pull Request**

Disini aku pake branching pada Git dengan membuat branch __jawaban-a__ untuk mengerjakan Bagian A dan branch __jawaban-b__ untuk mengerjakan Bagian B. Setelah pengerjaan selesai, kedua branch tersebut digabungkan ke branch __main__ pake pull request di GitHub.

Screenshot history branch dan proses merge menggunakan Pull Request:
![Merge](../src/a/2e/gitmerge.jpeg)

# **Jawaban untuk nomer A3**

**a. Install QGroundControl di Linux**
Saya menggunakan QGroundControl sebagai ground control station untuk UAV.

Ini screenshot dari main page QGC:
![MainQGC](../src/a/3a/mainpageqgc.jpeg)

**b. Fitur-fitur utama QGroundControl**
1. **Flight Planning**  
   Digunakan untuk merancang misi penerbangan UAV dengan menentukan waypoint, ketinggian, dan pola penerbangan sebelum misi dijalankan.
2. **Real-Time Telemetry Monitoring**  
   Menampilkan data penerbangan secara langsung seperti posisi GPS, ketinggian, kecepatan, orientasi UAV, serta status baterai.
3. **Vehicle Setup & Parameter Configuration**  
   Memungkinkan pengguna untuk mengonfigurasi parameter UAV, termasuk sensor, kontroler, dan kalibrasi sebelum penerbangan.
4. **Map & Mission Visualization**  
   Menampilkan peta lokasi UAV dan jalur misi secara visual sehingga operator dapat memantau pergerakan UAV dengan mudah.

**c. Misi pemetaan sederhana 100 x 80** 
Aku bikin pemetaan sederhana berbentuk area persegi panjang dengan panjang sekitar 100 meter dan lebar sekitar 80 meter pake fitur survey pada QGroundControl. Misi ini dirancang untuk mensimulasikan pemetaan area menggunakan UAV dengan jalur waypoint otomatis.

Berikut adalah file misi/screenshot hasil perancangan misi pemetaan:
![simulasiqgc](../src/a/3c/plan100x80.jpeg)

atau file export ada di ../lampiran/mapping_100x80.plan

# **Jawaban untuk nomer A4**
**a. Install Ubuntu**

Karena saat ini aku udah pake Arch linux jadi aku pake distrobox di sistem host Arch linux buat pake Ubuntu 22.04 LTS nya. Di dalam environment Ubuntu tersebut, aku install paket-paket pendukung pengembangan menggunakan apt serta menginstal ROS2 Humble.

![Arch](../src/a/4/arch.jpeg)
![Ubuntu](../src/a/4/ubuntu.jpeg)

Untuk screenshot install python dll tadi lupa di screenshot, jadi aku pake bagian install rosnya aja

![Rosinstall](../src/a/4/instalros.jpeg)

**b. Menjalankan sistem talker-listener sederhana**

Setelah instalasi berhasil, aku coba run sistem talker–listener bawaan ROS2 Humble menggunakan dua terminal terpisah, dimana node talker mengirimkan pesan dan node listener menerima pesan tersebut secara real-time.

![talkListen](../src/a/4/talk-listen.jpeg)

# **Jawaban untuk nomer A5**
**a. Klasifikasi UAV berdasarkan cara terbangnya**
**1. VTOL (Vertical Take-Off and Landing / Rotary Wing)**

Drone VTOL (Vertical Take-Off and Landing) adalah sebuah drone yang mampu melakukan penerbangan dan mendarat dengan posisi vertikal, seperti helikopter. Mereka memiliki kemampuan unik untuk terbang dan mendarat di tempat yang terbatas atau tidak rata, yang seringkali sulit dilakukan oleh drone biasa. Drone VTOL juga dapat terbang dengan kecepatan yang lebih tinggi dan lebih stabil dibandingkan drone biasa, karena memiliki lebih banyak motor yang bisa membantu menjaga agar tetap stabil di udara. Selain itu, VTOL drone juga lebih mudah dioperasikan karena tidak memerlukan pemantauan yang ketat selama penerbangan. VTOL drone biasanya digunakan untuk berbagai keperluan, seperti pemetaan, inspeksi industri, pemantauan lingkungan, dan bahkan sebagai alat transportasi.

**Contoh: Quadcopter, Helicopter, Tilt-rotor UAV (mirip mini osprey)**

**Mekanisme terbang:**
- Gaya angkat dihasilkan langsung dari putaran baling-baling (propeller).
- Gerak dikontrol dengan perbedaan kecepatan rotasi antar motor.

**Kelebihan:**
- Tidak butuh runway
- Sangat stabil untuk hovering
- Cocok untuk pemetaan area sempit dan inspeksi

**Kekurangan:**
- Efisiensi energi rendah
- Waktu terbang relatif singkat

*sumber: https://www.drone.instiperjogja.ac.id/blog-details-46.html#:~:text=Drone%20VTOL%20(Vertical%20Take%2DOff,sulit%20dilakukan%20oleh%20drone%20biasa.*

**2. HTOL (Horizontal Take-Off and Landing / Fixed Wing)**

HTOL (Horizontal Take-Off and Landing) adalah jenis drone yang harus menggunakan landasan horizontal untuk takeoff dan landing. HTOL, memiliki keunggulan dalam kemampuan terbang yang lebih tinggi dan daya tahan terbang yang lebih lama dibandingkan dengan VTOL. HTOL juga dapat mengangkut muatan yang lebih berat dan besar, sehingga lebih cocok untuk aplikasi pengangkutan barang. Namun, HTOL harus memiliki landasan horizontal yang memadai untuk takeoff dan landing, sehingga tidak fleksibel digunakan di lokasi yang terbatas atau tidak memiliki landasan yang memadai.

**Contoh: Fixed Wing UAV dan UAV dengan launcher catapult**

**Mekanisme terbang:**
- Gaya angkat dihasilkan dari airfoil (sayap) saat UAV bergerak maju.
- Membutuhkan kecepatan minimum (airspeed) untuk menghasilkan lift.

**Kelebihan:**
- Sangat efisien secara energi
- Jangkauan dan endurance panjang
- Cocok untuk pemetaan area luas

**Kekurangan:**
- Membutuhkan runway atau pelontar
- Tidak bisa hovering

*sumber: https://training.terra-drone.co.id/drone-vtol-vs-drone-htol/#:~:text=VTOL%20(Vertical%20Take%2DOff%20and,horizontal%20untuk%20takeoff%20dan%20landing.*

**3. Hybrid UAV**

Hybrid UAV menggabungkan mekanisme VTOL dan HTOL.

**Mekanisme terbang:**
- Take-off & landing secara vertikal
- Cruise secara horizontal menggunakan sayap

**Kelebihan:**
- Fleksibel
- Efisiensi lebih baik daripada rotary-wing murni

**Kekurangan:**
- Sistem lebih kompleks
- Bobot dan kontrol lebih sulit