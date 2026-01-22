# **Jawaban Bagian B**

# Dasar Pemrograman 1: OOP

**a. Jelaskan konsep-konsep dasar OOP berikut dan berikan contoh singkat dalam bahasa C++: class, object, abstraction, encapsulation, inheritance, dan polymorphism.**

Pemrograman berorientasi objek (OOP) adalah paradigma pemrograman yang memodelkan sistem sebagai objek yang memiliki data (atribut) dan perilaku (method). Pendekatan ini memudahkan pengembangan sistem kompleks seperti UAV karena kode menjadi lebih terstruktur, modular, dan mudah dikembangkan.

1. Class, adalah blueprint untuk membuat objek. Class mendefinisikan atribut dan method yang dimiliki oleh objek.
Contoh (C++): 
```cpp
class Motor {
public:
    int rpm;

    void setRPM(int value) {
        rpm = value;
    }
};
```

2. Object, adalah instansiasi dari sebuah class. Object merepresentasikan entitas nyata dalam sistem.
Contoh (C++):
```cpp
Motor motor1;
motor1.setRPM(3000);
```
di code ini, motor1 adalah objek dari class Motor.

3. Abstraction, adalah proses menyederhanakan sistem dengan hanya menampilkan fungsi penting dan menyembunyikan detail implementasi yang tidak perlu diketahui oleh user.
Nah didalam konteks UAV, user cukup tau fitur set kecepatan motor tanpa perlu tau soal detail sinyal PWM.
Contoh (C++):
```cpp
class Motor {
public:
    void setSpeed(int speed);
};
```
Implementasi detail dapan disembunyikan di file .cpp.

4. Encapsulation, adalah konsep membungkus data dan method dalam satu unit (class) dan juga membatasi akses langsung ke data tersebut menggunakan access modifier (private, protected, public).
Contoh (C++):
```cpp
class Battery {
private:
    float voltage;

public:
    void setVoltage(float v) {
        voltage = v;
    }

    float getVoltage() {
        return voltage;
    }
};
```
disini terlihat kalo data voltage tidak bisa diakses langsung, sehingga lebih aman.

5. Inheritance, memungkinkan sebuah class mewarisi atribut dan method dari class lain. Konsep ini membantu code reuse dan representasi hubungan hierarkis.
Contoh (C++):
```cpp
class Sensor {
public:
    void readData() {
        // untuk baca sensor dari data
    }
};

class GPSSensor : public Sensor {
public:
    void readPosition() {
        // untuk baca sensor dari GPS
    }
};
```
Dapat dilihat bahwa GPSSensor mewarisi fungsi readData() dari Sensor.

6. Polymorphism, memungkinkan method dengan nama yang sama memiliki perilaku berbeda, tergantung pada objek yang memanggilnya. Biasanya diimplementasikan menggunakan virtual function.
Contoh (C++):
```cpp
class Sensor {
public:
    virtual void read() {
        // untuk baca sensor secara umum
    }
};

class IMUSensor : public Sensor {
public:
    void read() override {
        // untuk baca sensor IMU yang digunakan
    }
};
```
Pemanggilan read() akan bergantung pada tipe objek yang asli, bukan tipe pointernya.

**Referensi**
1. B. Stroustrup, The C++ Programming Language, 4th ed., Addison-Wesley, 2013.
2. R. C. Martin, Clean Code, Prentice Hall, 2008.
3. https://en.cppreference.com/w/, “C++ Classes and Object-Oriented Programming”.
4. P. Deitel and H. Deitel, C++ How to Program, Pearson, 2017.
5. ROS 2 Documentation, https://docs.ros.org/en/humble/

# Dasar Pemrograman 2: Konsep Dasar C++
**2.a. Apa itu #include <file_name> dan #include "file_name" serta perbedaan antara keduanya**

Directive #include diproses oleh preprocessor, sebelum proses kompilasi dimulai. Artinya, isi file header akan disalin secara literal ke file sumber.
- #include <flie_name>
    Digunakan untuk header standar/library sistem/third party. Compiler akan mencari di system include path. Contoh: <iostream>, <vector>
- #include "file_name"
    Digunakan untuk header buatan sendiri. Compiler akan mencari di direktori proyek terlebih dahulu, lalu ke system path. Cocok untuk proyek modular (misalnya UAV subsystem)

Contoh:
```cpp
#include <iostream>      // library standar
#include "motor.hpp"     // header buatan sendiri
```

**2.b. Penggunaan #ifdef, #ifndef, #endif dan #pragma once dalam header file**

Digunakan untuk mencegah multiple inclusion pada header file. Masalah yang dihindari yaitu multiple definition error akibat header di-include lebih dari satu kali.

Cara kerja include guard:
```cpp
#ifndef MOTOR_HPP
#define MOTOR_HPP

class Motor {};

#endif
```
- #ifndef: cek apakah macro belum didefinisikan
- Jika belum → isi file diproses
- Jika sudah → dilewati

```cpp
#pragma once
class Motor {};
```
#pragma once
- Instruksi ke compiler untuk meng-include file hanya sekali
- Lebih ringkas dan minim error
- Banyak dipakai di proyek modern (ROS2, PX4)

**2.c. Penggunaan namespace dan scope resolution operator (::)**

Namespace digunakan untuk mengelompokkan simbol agar tidak bentrok. Tanpa namespace, dua library bisa punya fungsi dengan nama sama, maka akan error atau ambigu.

Contoh:
```cpp
std::cout << "Telemetry aman terkendali icibos!" << std::endl;
```
Pada penerapan in real life bisa digunakan untuk 
- ROS2      : rclcpp::Node
- OpenCV    : cv::Mat

**2.d. Perbedaan #define dan using**

- __#define__

#define adalah macro preprocessor, artinya:
- Dieksekusi sebelum kompilasi
- Hanya melakukan text substitution
- Tidak memiliki tipe data
- Tidak mengikuti scope 
```cpp
#define MAX_SPEED 10
```
Disini terlihat bahwa compiler tidak tahu bahwa MAX_SPEED adalah const atau konstanta numerik, sehingga bisa menyebabkan rawan error tersembunyi.
Contoh masalah:
```cpp
#define SQR(x) x*x
SQR(1+2)  // hasilnya 5, bukan 9
```

- __using__

using diproses oleh compiler, bukan preprocessor:
- Bertipe jelas
- Mengikuti scope
- Aman terhadap debugging dan refactoring
```cpp
using Speed = double;
```
Dalam sistem besar (ROS2, UAV firmware), using:
- Memperjelas maksud tipe data
- Mengurangi bug
- Mempermudah pengembangan jangka panjang
Kesimpulannya adalah, penggunaan using lebih relevan saat ini kecuali untuk conditional compilation.

**2.e. Cara kerja pointer (*) dan address of (&)**

Pointer adalah variabel yang menyimpan alamat memori, bukan nilai langsung.

__Cara kerja di memori:__
```cpp
int altitude = 100;
int* ptr = &altitude;
```
- altitude → disimpan di suatu alamat RAM
- &altitude → alamat memori tersebut
- ptr → menunjuk ke alamat itu
- *ptr → dereference (mengakses isi alamat)

__Kenapa pointer penting?__
1. Efisiensi memori
2. Akses hardware langsung
3. Dynamic memory allocation
4. Interface dengan C / firmware

__Dalam UAV biasanya pointer digunakan untuk:__
- Driver sensor
- Akses register mikrocontroller
- Buffer data real-time

**2.f. Konsep pass by value dan pass by reference dalam definisi variabel dan fungsi**

- __Pass by Value__
```cpp
void process(Data d);
```
- Data disalin ke stack
- Aman, tapi mahal untuk objek besar
- Perubahan tidak memengaruhi data asli

- __Pass by Reference__
```cpp
void process(Data& d);
```
- Tidak membuat salinan
- Lebih cepat dan hemat memori
- Perubahan langsung ke objek asli

Jika dilihat dari design systemnya, biasanya untuk objek kecil menggunakan pass by value dan untuk objek besar atau real time menggunakan pass by reference.

**2.g. Perbedaan std::unique_ptr dan std::shared_ptr**

Smart pointer adalah abstraksi RAII (Resource Acquisition Is Initialization).

- __std::unique_ptr__
- Kepemilikan tunggal
- Tidak bisa di-copy
- Bisa di-move
- Overhead sangat kecil
```cpp
std::unique_ptr<IMUSensor> imu = std::make_unique<IMUSensor>();
```
Digunakan ketika:
- Resource punya pemilik jelas
- Tidak boleh diakses sembarangan
- Cocok untuk driver hardware

- __std::shared_ptr__
- Multiple ownership
- Reference counting
- Overhead lebih besar
- Risiko cyclic reference
```cpp
std::shared_ptr<Map> map = std::make_shared<Map>();
```
Digunakan ketika:
- Banyak modul membutuhkan resource sama
- Lifetime sulit ditentukan

Dalam ROS2, shared_ptr sering dipake buat node dan message tetapi penggunaan yang berlebihan bisa menyebabkan memory leak.

**Referensi**
1. B. Stroustrup, The C++ Programming Language, Addison-Wesley
2. Scott Meyers, Effective Modern C++, O’Reilly
3. ISO C++ Reference – https://en.cppreference.com
4. Herb Sutter – C++ Core Guidelines
5. ROS 2 Documentation – https://docs.ros.org/en/humble/

# Dasar Pemrograman 3: Multithreading
**3.a. Jelaskan konsep dasar multithreading.**

**Multithreading** adalah kemampuan sebuah program untuk menjalankan lebih dari satu alur eksekusi (thread) secara concurrent (bersamaan). Setiap thread memiliki instruction pointer sendiri, tetapi biasanya berbagi memori yang sama dalam satu proses.

Multireading ini penting karena jika memiliki tugas yang berat, aka tidak akan memblokir tugas lainnya. Serta multithreading memanfaatkan multi core CPU dalam cara kerjanya. TErakhir, multithreading menggunakan real time sysstem yaotu beberapa proses harus berjalan secara paralel.

Contoh penggunaan dalam UAV:
- Thread 1: membaca telemetri (GPS, IMU)
- Thread 2: menerima video stream
- Thread 3: kontrol & logging

Tanpa menggunakan multithreading, satu tugas lambat bisa menghambat sistem secara keseluruhan yang akibatnya bisa berbahaya pada sistem real time.

**3.b. Implementasi Program Multithreading**
- Thread 1: simulasi stream video -> print message tiap 2 detik
- Thread 2: simulasi telemetri -> baca filr telemetry.txt, print tiap baris 3 detik
- Keduanya akan berjalan secara bersamaan yang estimasi waktunya adalah +- 10 detik.

Contoh isi telemetry.txt
```txt
ALT: 100 m
SPD: 12 m/s
GPS: -7.95, 112.61
BAT: 11.1 V
```

Kode C++ yang digunakan menggunakan (std::thread)
```cpp
#include <iostream>
#include <thread>
#include <fstream>
#include <chrono>
#include <atomic>

std::atomic<bool> running(true);

void videoStream() {
    while (running) {
        std::cout << "[VIDEO] Receiving video frame..." << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(2));
    }
}

void telemetryStream() {
    std::ifstream file("telemetry.txt");
    std::string line;

    while (running && std::getline(file, line)) {
        std::cout << "[TELEMETRY] " << line << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(3));
    }
}

int main() {
    std::thread videoThread(videoStream);
    std::thread telemetryThread(telemetryStream);

    std::this_thread::sleep_for(std::chrono::seconds(10));
    running = false;

    videoThread.join();
    telemetryThread.join();

    std::cout << "Program finished." << std::endl;
    return 0;
}
```

Masing-masing syntax yang digunakan sangat penting untuk berjalannya program:
- **std::thread**, untuk membuat thread baru.
- **std::this_thread::sleep_for()**, untuk Menyimulasikan delay seperti data real time.
- **std::atomic<bool>**, untuk sinkronisasi aman antar thread serta mencegah race condition.
- **join()**, untuk menunggu thread selesai sebelum program keluar.

Contoh Output ketika sudah di run +- 10 detik:
```txt
[VIDEO] Receiving video frame...
[TELEMETRY] ALT: 100 m
[VIDEO] Receiving video frame...
[TELEMETRY] SPD: 12 m/s
[VIDEO] Receiving video frame...
[VIDEO] Receiving video frame...
[TELEMETRY] GPS: -7.95, 112.61
[VIDEO] Receiving video frame...
Program finished.
```
Disini terlihat bahwa dua thread berjalan secara bersamaan tanpa saling mengganggu.

**Referensi**
1. B. Stroustrup, The C++ Programming Language, Addison-Wesley
2. Anthony Williams, C++ Concurrency in Action, Manning
3. ISO C++ Reference – https://en.cppreference.com/w/cpp/thread
4. Herb Sutter – C++ Concurrency Guidelines
5. ROS 2 Executor & Multithreading Documentation

# Firmware dan Sistem Benam
**1. Apa itu firmware dan bagaimana perbedaannya dengan perangkat lunak (software) pada umumnya? Jelaskan juga peran firmware dalam sistem UAV.**

**Firmware** adalah low level software yang tertanam (embedded) langsung pada hardware dan berfungsi sebagai penghubung antara hardware dan software tingkat atas. Firmware biasanya disimpan pada memori non volatile seperti Flash atau ROM dan jarang diubah dibandingkan software aplikasi.

| Aspek            | Firmware             | Software                  |
| ---------------- | -------------------- | ------------------------- |
| Lokasi           | Tertanam di hardware | Sistem operasi / aplikasi |
| Akses hardware   | Langsung             | Melalui OS / driver       |
| Frekuensi update | Jarang               | Sering                    |
| Real-time        | Iya                   | Tidak selalu              |

Dalam UAV, Firmware berperan penting untuk beberapa aspek. Pertama, firmware mengendalikan motor, sensor, dan aktuator. Selain itu, firmware menjalankan flight control loop. Terakhir, firmware menangani komunikasi (PWM, UART, I2C, SPI). Contoh firmware yang biasanya digunakan di UAV adalah PX4 dan ArduPilot.

_Kesimpulannya, firmware adalah otak utama UAV, tanpa firmware UAV tidak bisa terbang stabil._

**2. Jelaskan konsep Real-Time Operating System (RTOS) dan mengapa RTOS penting dalam pengembangan sistem UAV.**

**RTOS (Real-Time Operating System)** merupakan operation system yang dirancang untuk menjamin respon deterministik terhadap suatu event dalam batas deadline. Namun ini berbeda dengan operating system umum, RTOS tidak hanya mengejar kecepatan, tetapi ketetapan waktu.

**Karakteristik RTOS**
- Deterministic scheduling
- Prioritas task
- Interrupt handling cepat
- Latency rendah

RTOS sangat penting untuk UAV karena UAV merupakan sistem real time sehingga kontrol attitude harus dieksekusi dalam milidetik serta keterlambatan kecil bisa menyebabkan instabilitas atau crash. Sehingga dengan menggunakan RTOS maka control task punya prioritas yang tinggi dan untuk task non kritis seperti logging dan telemetry tidak akan mengganggu kontrol utama.

Contoh RTOS:
- FreeRTOS
- NuttX (digunakan PX4)
- Zephyr

**3. Jelaskan konsep dasar komunikasi serial (UART, SPI, I2C) dan bagaimana protokol-protokol ini digunakan dalam sistem UAV untuk berkomunikasi antara berbagai komponen.**

Dalam sistem UAV, berbagai komponen seperti sensor, aktuator, dan modul komunikasi perlu saling bertukar data secara cepat dan andal. Karena keterbatasan ruang, daya, dan kompleksitas sistem, komunikasi antar komponen tersebut umumnya menggunakan komunikasi serial, yaitu metode pengiriman data satu bit demi satu bit melalui jalur tertentu.

Tiga protokol komunikasi serial yang paling umum digunakan dalam sistem UAV adalah UART, SPI, dan I2C. Ketiganya memiliki karakteristik, kelebihan, dan kegunaan yang berbeda, sehingga pemilihannya sangat bergantung pada kebutuhan sistem dan jenis perangkat yang dihubungkan.

**UART dalam Sistem UAV**

UART (Universal Asynchronous Receiver-Transmitter) adalah protokol komunikasi serial asynchronous, artinya pengirim dan penerima tidak berbagi sinyal clock yang sama. Sebagai gantinya, kedua perangkat harus disepakati terlebih dahulu parameter komunikasi seperti baud rate, jumlah bit data, parity, dan stop bit.

Dalam UAV, UART sangat sering digunakan untuk komunikasi dengan perangkat yang berada relatif jauh dari flight controller atau membutuhkan koneksi sederhana dan stabil. Contohnya adalah modul GPS, radio telemetry, dan link komunikasi dengan ground control station.

Keunggulan utama UART adalah kesederhanaannya. Implementasi UART relatif mudah, baik dari sisi hardware maupun software, dan hampir semua mikrocontroller menyediakan peripheral UART bawaan. Namun, karena bersifat point-to-point dan tidak memiliki mekanisme addressing, UART kurang cocok untuk menghubungkan banyak perangkat dalam satu jalur komunikasi.

**SPI dalam Sistem UAV**

SPI (Serial Peripheral Interface) adalah protokol komunikasi serial synchronous yang menggunakan sinyal clock yang dikirim oleh perangkat master. Dalam sistem UAV, flight controller biasanya bertindak sebagai master, sedangkan sensor bertindak sebagai slave.

SPI dikenal karena kecepatan transfer data yang tinggi dan latensi yang rendah, sehingga sangat cocok untuk perangkat yang memerlukan pembacaan data secara cepat dan kontinu. Oleh karena itu, sensor-sensor kritis seperti IMU (accelerometer dan gyroscope) sering dihubungkan melalui SPI.

Karakteristik utama SPI adalah penggunaan beberapa jalur komunikasi, termasuk jalur clock, data masuk, data keluar, dan chip select. Konsekuensinya, SPI membutuhkan lebih banyak pin dibandingkan protokol lain, sehingga jarak komunikasi biasanya pendek dan topologi sistem menjadi lebih kompleks. Namun, trade-off ini dianggap wajar demi performa yang tinggi, terutama untuk sistem kontrol real-time seperti UAV.

**I2C dalam Sistem UAV**

I2C (Inter-Integrated Circuit) adalah protokol komunikasi serial synchronous yang dirancang untuk menghubungkan banyak perangkat dalam satu bus menggunakan hanya dua jalur, yaitu data (SDA) dan clock (SCL). Setiap perangkat pada bus memiliki alamat unik, sehingga flight controller dapat berkomunikasi dengan banyak sensor menggunakan jalur yang sama.

Dalam UAV, I2C sering digunakan untuk sensor dengan kebutuhan bandwidth yang relatif rendah, seperti barometer, magnetometer, atau sensor suhu. Kelebihan utama I2C adalah efisiensi wiring dan kemudahan integrasi banyak perangkat sekaligus.

Namun, karena menggunakan pull-up resistor dan kecepatan transfer yang lebih rendah dibandingkan SPI, I2C lebih sensitif terhadap noise dan kurang cocok untuk komunikasi berkecepatan tinggi atau jarak jauh. Oleh sebab itu, I2C biasanya digunakan untuk sensor pendukung, bukan sensor utama kontrol stabilitas.

**Pemilihan Protokol dalam Desain UAV**

Dalam praktiknya, sistem UAV jarang hanya menggunakan satu jenis protokol komunikasi. Sebaliknya, desainer sistem akan mengombinasikan UART, SPI, dan I2C sesuai kebutuhan masing-masing komponen. Sensor yang memerlukan data cepat dan presisi tinggi akan dihubungkan melalui SPI, sensor pendukung melalui I2C, dan perangkat komunikasi eksternal melalui UART.

Pendekatan ini memungkinkan UAV memiliki sistem yang efisien, modular, dan andal, serta mampu memenuhi kebutuhan real-time dan keterbatasan hardware yang ada.

**Referensi**
1. Jonathan W. Valvano, Embedded Systems: Real-Time Operating Systems for ARM Cortex-M, Texas Instruments
2. PX4 Autopilot Documentation – https://docs.px4.io
3. NuttX RTOS Documentation – https://nuttx.apache.org
4. FreeRTOS Documentation – https://www.freertos.org
5. ArduPilot Developer Wiki – https://ardupilot.org/dev/