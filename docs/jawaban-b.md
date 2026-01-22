# **Jawaban Bagian B**

---

## **Dasar Pemrograman 1: Object-Oriented Programming (OOP)**

### **a. Konsep dasar OOP dan contoh dalam C++**

Pemrograman berorientasi objek (**OOP**) adalah paradigma pemrograman yang memodelkan sistem sebagai objek yang memiliki data (atribut) dan perilaku (method). Pendekatan ini memudahkan pengembangan sistem kompleks seperti UAV karena kode menjadi lebih terstruktur, modular, dan mudah dikembangkan.

---

### **1. Class**

Class adalah blueprint untuk membuat objek. Class mendefinisikan atribut dan method yang dimiliki oleh objek.

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

---

### **2. Object**

Object adalah instansiasi dari sebuah class. Object merepresentasikan entitas nyata dalam sistem.

Contoh (C++):

```cpp
Motor motor1;
motor1.setRPM(3000);
```

Pada kode di atas, `motor1` adalah objek dari class `Motor`.

---

### **3. Abstraction**

Abstraction adalah proses menyederhanakan sistem dengan hanya menampilkan fungsi penting dan menyembunyikan detail implementasi yang tidak perlu diketahui oleh user.

Dalam konteks UAV, user cukup mengetahui fitur pengaturan kecepatan motor tanpa perlu memahami detail sinyal PWM.

Contoh (C++):

```cpp
class Motor {
public:
    void setSpeed(int speed);
};
```

Detail implementasi dapat disembunyikan di file `.cpp`.

---

### **4. Encapsulation**

Encapsulation adalah konsep membungkus data dan method dalam satu unit (class) serta membatasi akses langsung ke data menggunakan access modifier (`private`, `protected`, `public`).

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

Data `voltage` tidak dapat diakses langsung sehingga lebih aman.

---

### **5. Inheritance**

Inheritance memungkinkan sebuah class mewarisi atribut dan method dari class lain. Konsep ini membantu *code reuse* dan representasi hubungan hierarkis.

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

Class `GPSSensor` mewarisi fungsi `readData()` dari `Sensor`.

---

### **6. Polymorphism**

Polymorphism memungkinkan method dengan nama yang sama memiliki perilaku berbeda tergantung objek yang memanggilnya, biasanya menggunakan *virtual function*.

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

Pemanggilan `read()` bergantung pada tipe objek aslinya.

---

### **Referensi**

1. B. Stroustrup, *The C++ Programming Language*, 4th ed., Addison-Wesley, 2013.
2. R. C. Martin, *Clean Code*, Prentice Hall, 2008.
3. [https://en.cppreference.com/w/](https://en.cppreference.com/w/)
4. P. Deitel and H. Deitel, *C++ How to Program*, Pearson, 2017.
5. ROS 2 Documentation – [https://docs.ros.org/en/humble/](https://docs.ros.org/en/humble/)

---

## **Dasar Pemrograman 2: Konsep Dasar C++**

### **2.a. Perbedaan `#include <file>` dan `#include "file"`**

Directive `#include` diproses oleh preprocessor sebelum kompilasi. Isi file header akan disalin secara literal ke file sumber.

* `#include <file_name>`
  Digunakan untuk header standar atau library sistem/third party. Compiler mencari di *system include path*.

* `#include "file_name"`
  Digunakan untuk header buatan sendiri. Compiler mencari di direktori proyek terlebih dahulu.

Contoh:

```cpp
#include <iostream>
#include "motor.hpp"
```

---

### **2.b. Include guard dan `#pragma once`**

Digunakan untuk mencegah *multiple inclusion*.

```cpp
#ifndef MOTOR_HPP
#define MOTOR_HPP

class Motor {};

#endif
```

Atau menggunakan:

```cpp
#pragma once
class Motor {};
```

`#pragma once` lebih ringkas dan umum digunakan di proyek modern seperti ROS2 dan PX4.

---

### **2.c. Namespace dan scope resolution operator (`::`)**

Namespace digunakan untuk menghindari konflik nama simbol.

Contoh:

```cpp
std::cout << "Telemetry aman terkendali icibos!" << std::endl;
```

Contoh penggunaan nyata:

* `rclcpp::Node`
* `cv::Mat`

---

### **2.d. Perbedaan `#define` dan `using`**

**`#define`**

* Macro preprocessor
* Tidak bertipe
* Tidak mengikuti scope

```cpp
#define MAX_SPEED 10
```

Contoh masalah:

```cpp
#define SQR(x) x*x
SQR(1+2)
```

**`using`**

* Diproses compiler
* Bertipe jelas
* Aman untuk debugging

```cpp
using Speed = double;
```

---

### **2.e. Pointer (`*`) dan address-of (`&`)**

```cpp
int altitude = 100;
int* ptr = &altitude;
```

* `&altitude` → alamat memori
* `ptr` → menyimpan alamat
* `*ptr` → dereference

Pointer penting untuk efisiensi memori, akses hardware, dan real-time system.

---

### **2.f. Pass by value vs pass by reference**

**Pass by Value**

```cpp
void process(Data d);
```

**Pass by Reference**

```cpp
void process(Data& d);
```

Objek besar dan real-time system lebih cocok menggunakan pass by reference.

---

### **2.g. `std::unique_ptr` vs `std::shared_ptr`**

**`std::unique_ptr`**

```cpp
std::unique_ptr<IMUSensor> imu = std::make_unique<IMUSensor>();
```

**`std::shared_ptr`**

```cpp
std::shared_ptr<Map> map = std::make_shared<Map>();
```

`unique_ptr` cocok untuk driver hardware, sedangkan `shared_ptr` sering digunakan di ROS2.

---

## **Dasar Pemrograman 3: Multithreading**

### **3.a. Konsep dasar multithreading**

Multithreading memungkinkan program menjalankan beberapa thread secara bersamaan. Setiap thread memiliki alur eksekusi sendiri tetapi berbagi memori.

Contoh di UAV:

* Thread sensor
* Thread video
* Thread kontrol

---

### **3.b. Implementasi multithreading C++**

Contoh kode:

```cpp
// kode sesuai soal (tidak diubah)
```

Dua thread berjalan bersamaan tanpa saling mengganggu.

---

## **Firmware dan Sistem Benam**

### **1. Firmware dan perannya pada UAV**

Firmware adalah software tingkat rendah yang tertanam pada hardware. Firmware mengontrol motor, sensor, komunikasi, dan flight control loop.

Contoh firmware UAV: PX4 dan ArduPilot.

---

### **2. RTOS pada UAV**

RTOS menjamin respon deterministik terhadap event. RTOS penting untuk kontrol attitude real-time.

Contoh RTOS:

* FreeRTOS
* NuttX
* Zephyr

---

### **3. Komunikasi serial: UART, SPI, dan I2C**

* **UART**: sederhana, point-to-point
* **SPI**: cepat, latensi rendah
* **I2C**: hemat wiring, multi-device

Ketiganya digunakan bersamaan dalam desain UAV.

---

## **Control and Perception (ConCept)**

### **Konsep dasar ROS2**

ROS2 membangun sistem sebagai kumpulan node yang berkomunikasi.

* **Node**: unit proses mandiri
* **Topic**: publish–subscribe
* **Service**: request–response
* **Parameter**: konfigurasi runtime
* **Action**: tugas berdurasi panjang

Pendekatan ini membuat sistem UAV modular, fleksibel, dan mudah dikembangkan.