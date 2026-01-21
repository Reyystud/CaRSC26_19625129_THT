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