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

**e. Branching dan Pull Request**

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

**b. Jelaskan apa itu gerak roll, yaw, dan pitch; air speed dan ground speed (beserta hubungan antara keduanya); serta HDOP dalam GPS dan RSSI dalam telekomunikasi UAV.**

**Roll, Pitch, dan Yaw**
- *Roll adalah rotasi terhadap sumbu longitudinal (miring kiri-kanan)*
- *Pitch adalah rotasi terhadap sumbu lateral (naik-turun hidung)*
- *Yaw adalah rotasi terhadap sumbu vertikal (berbelok kiri-kanan)*
Ketiga gerak ini membentuk attitude UAV.

**Airspeed dan Ground Speed**
- *Airspeed merupakan kecepatan UAV relatif terhadap udara*
- *Ground speed merupakan kecepatan UAV relatif terhadap permukaan bumi*
**Ground Speed = Airspeed + Wind Speed (vektor)**, artinya angin dapat membuat ground speed lebih kecil atau lebih besar dari airspeed.

**HDOP dan RSSI**
**HDOP (Horizontal Dilution of Precision)**
- *Mengukur kualitas geometri satelit GPS.*
- *Semakin kecil HDOP → semakin akurat posisi horizontal.*

**RSSI (Received Signal Strength Indicator)**
- *Mengukur kekuatan sinyal komunikasi radio antara UAV dan GCS.*
- *RSSI rendah → risiko kehilangan link.*

**c. Komponen dalam UAV untuk pemetaan dan diagramnya**
1. Frame – struktur utama
2. Motor & Propeller – menghasilkan gaya angkat
3. ESC – mengatur kecepatan motor
4. Flight Controller (Autopilot) – pusat kendali
5. Sensor
6. IMU (gyro, accelerometer)
7. GPS
8. Barometer
9. Power System
10. Baterai Li-Po
11. Power Distribution Board
12. Payload
13. Kamera pemetaan
14. Communication System
15. Telemetry radio
16. RC receiver
17. Ground Control Station (GCS)

Berikut adalah diagram integrasi antar komponen pada UAV untuk pemetaan menurut aku:
![uav](../src/a/5c/THTRSC26.jpg)

**d. Share insight tentang artikel yang dibaca**

**Multirotor UAV—A Multidisciplinary Platform for Teaching Mechatronics Engineering**

Penelitian ini membahas pengembangan platform pembelajaran berbasis Unmanned Aerial Vehicle (UAV) atau drone multirotor yang digunakan sebagai media pembelajaran untuk mahasiswa teknik mekatronika. Tujuan utama dari penelitian ini adalah membantu mahasiswa memahami hubungan antara teori matematika yang cukup rumit dengan penerapannya secara langsung di dunia nyata.

Dalam penelitian ini digunakan ekosistem PX4 yang dipadukan dengan MATLAB/Simulink sebagai lingkungan pemrograman dan simulasi. Dengan pendekatan ini, mahasiswa dapat melakukan proses pembelajaran secara bertahap, mulai dari membuat model matematika, menjalankan simulasi, hingga mengimplementasikannya langsung ke perangkat keras drone.

Artikel ini juga menjelaskan capaian pembelajaran yang diharapkan, seperti kemampuan mahasiswa dalam memodelkan sistem drone secara matematis, mengenali dan memahami komponen perangkat keras (sensor dan aktuator), serta melakukan pengujian sistem kontrol pada drone multirotor.

Selain itu, penelitian ini memanfaatkan teknologi additive manufacturing (cetak 3D) untuk pembuatan rangka drone. Hal ini memberikan keuntungan karena desain airframe dapat dimodifikasi dengan mudah sesuai kebutuhan eksperimen, serta dapat dibuat dengan biaya yang relatif rendah.

Mahasiswa dilibatkan secara langsung melalui serangkaian workshop yang mencakup proses perakitan drone hingga pengujian perangkat lunak untuk mengatur stabilitas dan kontrol penerbangan.

Dari pembahasan tersebut, terdapat beberapa poin penting yang dapat dipahami. Pertama, UAV bukan hanya sekadar alat terbang, tetapi merupakan sistem mekatronika yang menggabungkan berbagai bidang seperti mekanik, elektronika, dan pemrograman. Hal ini menjadikan drone sebagai media pembelajaran yang sangat baik untuk memahami cara kerja sistem terintegrasi.

Kedua, simulasi memiliki peran yang sangat penting sebelum dilakukan pengujian langsung. Dengan menggunakan MATLAB/Simulink, mahasiswa dapat mencoba berbagai skenario tanpa risiko merusak perangkat keras, sehingga proses belajar menjadi lebih aman dan efektif.

Ketiga, penggunaan komponen yang mudah didapat serta teknologi cetak 3D menunjukkan bahwa pengembangan sistem UAV untuk pembelajaran dapat dilakukan dengan biaya yang terjangkau. Hal ini membuka peluang bagi institusi pendidikan untuk mengadopsi teknologi drone tanpa memerlukan anggaran yang besar.

Terakhir, penggunaan sistem otonom berbasis open-source seperti PX4 memberikan pengalaman yang relevan dengan kebutuhan industri saat ini. Mahasiswa menjadi lebih siap menghadapi perkembangan teknologi drone yang banyak digunakan di berbagai bidang seperti pertanian, logistik, dan pemantauan infrastruktur.

*Untuk Artikel penuhnya ada disini https://www.mdpi.com/1424-8220/25/4/1007*

# **Jawaban untuk nomer A6**

**a. Algoritma A* (A Star) dan D* (D star)**

*Algoritma A-Star* merupakan pengembangan dari *algoritma BFS (Breadth First Search)* sehingga dasar pencarian dan algoritma hampir sama. Perbedaannya yaitu algoritma A-Star akan memilih jalur dengan nominal nilai atau biaya terkecil. Algoritma ini pertama kali dideskripsikan pada tahun 1968 oleh Peter Hart, Nils Nilsson, dan Bertram Raphael, dengan rumus :

                                   f(v) = g(s → v) + h(v→ r)

Persamaan digunakan untuk mengisi nilai masing-masing titik (node) tetangga selama proses pencarian jalur terjadi, dimana :

- g(s ~> v) : Estimasi biaya/jarak dari titik start (s) ke titik v.
- h(v ~>r) : Estimasi biaya/jarak tertentu (unik) dari titik v ke titik goal (r).
- f(v) : Total biaya / jarak yang berasal dari titik awal ke titik goal yang melewati titik v.

*Algoritma A-Star* membutuhkan variabel khusus yaitu variabel open agar tidak adanya
pemeriksaan dua kali. Lalu algoritma A-Star akan mendaftarkan node tetangga dari setiap node yang saat ini sedang dikunjungi. Tetapi pada perulangan selanjutnya algoritma A-Star akan memilih nilai terendah dari kumpulan node pada variabel open yang terdaftar. Sehingga properti nilai pada masing-masing node adalah mutlak ada. Berikut adalah graf pohon dari algoritma A-star:

![graf](../src/a/6a/grafalgoritmaa.jpeg)

Dimana node A mencari node N, urutan pemeriksaan graf pohon diatas adalah A, B, C, F, dan terakhir N, yaitu node goal ditemukan. Pada graf tersebut nilai masing-masing node dihitung dengan Persamaan 1. Garis putus-putus pada graf tersebut menandakan area yang belum dikunjungi, garis tegas yang tidak tebal adalah node yang akan dikunjungi selanjutnya (masuk ke dalam variabel open), sedangkan garis tebal adalah node yang telah dikunjungi dan diberi tanda closed agar tidak dikunjungi kembali.

*D-Star* adalah pengembangan dari A* yang dirancang untuk lingkungan dinamis. D* tidak menghitung ulang jalur dari awal ketika ada perubahan, tetapi memperbarui jalur secara inkremental.

**Prinsip utama D* adalah:**
- Perencanaan jalur dilakukan dari tujuan ke posisi robot
- Ketika ada obstacle baru, algoritma memperbarui jalur lokal tanpa full replan 

**Kapan & di mana digunakan:**
- UAV atau robot di lingkungan tidak diketahui
- Eksplorasi area
- Robot search and rescue
- Autonomous ground vehicle militer / planetary rover

**Perbedaan utama A* vs D*:**
- A*: peta statis
- D*: peta dinamis dan beruba

**b. Proportional-Integral-Derivative (PID)**

PID adalah algoritma kontrol umpan balik (feedback control) yang digunakan untuk menjaga sistem berada pada nilai yang diinginkan (setpoint).

PID terdiri dari tiga komponen:
1. Proportional (P)
Menghasilkan output sebanding dengan error saat ini.
Terlalu besar → sistem berosilasi.
2. Integral (I)
Mengakumulasi error dari waktu ke waktu untuk menghilangkan steady-state error.
3. Derivative (D)
Memprediksi tren error di masa depan dengan melihat laju perubahan error, sehingga meredam osilasi.

Rumus umum PID:
![rumuspid](../src/a/6b/rumuspid.jpeg)

ini adalah contoh diagram algoritma control pid:
![pid](../src/a/6b/diagrampid.jpeg)

**Kapan & di mana digunakan:**
1. Kontrol attitude UAV (roll, pitch, yaw)
2. Kontrol kecepatan motor
3. Kontrol ketinggian (altitude hold)
4. Sistem autopilot (PX4, ArduPilot)

**Alasan PID populer:**
1. Sederhana
2. Efektif
3. Mudah dituning
4. Cocok untuk sistem real-time

**c. Kalman Filter dan Extended Kalman Filter (EKF)**

**Kalman Filter** adalah algoritma estimasi yang digunakan untuk memperkirakan keadaan sistem (state) dari data sensor yang bising (noisy).

KF bekerja dalam dua tahap utama:
1. **Prediction**, memprediksi state berdasarkan model sistem
2. **Update**, mengoreksi prediksi menggunakan data sensor
KF optimal untuk sistem linear dengan noise Gaussian.

**Digunakan untuk:**
- Estimasi posisi dan kecepatan
- Sensor fusion (menggabungkan beberapa sensor)
- Tracking objek

Karena sistem UAV bersifat non-linear, digunakan **Extended Kalman Filter (EKF)**. EKF melakukan:
- Linearisasi sistem non-linear menggunakan Jacobian
- Estimasi state pada sistem kompleks seperti UAV

Kapan & di mana digunakan:
1. Estimasi attitude UAV
2. Sensor fusion IMU + GPS + barometer
3. Autopilot PX4 & ArduPilot
4. Navigasi drone otonom

Kenapa EKF penting di UAV:
- Sensor murah → noise tinggi
- Data saling melengkapi
- Posisi dan orientasi harus akurat

# Referensi
__A* & D*__
1. Hart, P. E., Nilsson, N. J., & Raphael, B. (1968). A Formal Basis for the Heuristic Determination of Minimum Cost Paths. IEEE Transactions on Systems Science and Cybernetics.
2. Koenig, S., & Likhachev, M. (2002). D Lite*. AAAI Conference on Artificial Intelligence.
3. https://www.jsi.stikom-bali.ac.id/index.php/jsi/article/download/335/209*


__PID__
1. Åström, K. J., & Hägglund, T. (2006). Advanced PID Control. ISA.
2. ArduPilot Documentation – Control Theory
https://ardupilot.org/copter/docs/attitude-control.html
3. https://www.ni.com/en/shop/labview/pid-theory-explained.html?srsltid=AfmBOoroTMZYO1wPY19L_B5mRm-nNP4iZakr_Y3_TzAcccdc2uGdDvPy#section--2054068860
4. ChatGPT

__Kalman Filter & EKF__
1. Kalman, R. E. (1960). A New Approach to Linear Filtering and Prediction Problems. ASME Journal of Basic Engineering.
2. Mahony, R., Kumar, V., & Corke, P. (2012). Multirotor Aerial Vehicles: Modeling, Estimation, and Control. IEEE Robotics & Automation Magazine.
3. PX4 Autopilot – State Estimation
https://docs.px4.io/main/en/advanced_config/ekf2.html