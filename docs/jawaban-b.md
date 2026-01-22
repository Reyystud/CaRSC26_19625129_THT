# **Jawaban Bagian B**

---

## **Dasar Pemrograman 1: OOP**

### **a. Jelaskan konsep-konsep dasar OOP berikut dan berikan contoh singkat dalam bahasa C++**

Pemrograman berorientasi objek (OOP) adalah paradigma pemrograman yang memodelkan sistem sebagai objek yang memiliki data (atribut) dan perilaku (method). Pendekatan ini memudahkan pengembangan sistem kompleks seperti UAV karena kode menjadi lebih terstruktur, modular, dan mudah dikembangkan.

---

### **1. Class**

Class adalah blueprint untuk membuat objek. Class mendefinisikan atribut dan method yang dimiliki oleh objek.

**Contoh (C++):**

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

Object adalah instansiasi dari sebuah class dan merepresentasikan entitas nyata dalam sistem.

**Contoh (C++):**

```cpp
Motor motor1;
motor1.setRPM(3000);
```

di code ini, `motor1` adalah objek dari class `Motor`.

---

### **3. Abstraction**

Abstraction adalah proses menyederhanakan sistem dengan hanya menampilkan fungsi penting dan menyembunyikan detail implementasi yang tidak perlu diketahui oleh user.

Dalam konteks UAV, user cukup mengetahui fungsi pengaturan kecepatan motor tanpa perlu memahami detail sinyal PWM.

**Contoh (C++):**

```cpp
class Motor {
public:
    void setSpeed(int speed);
};
```

Implementasi detail dapat disembunyikan di file `.cpp`.

---

### **4. Encapsulation**

Encapsulation adalah konsep membungkus data dan method dalam satu unit (class) serta membatasi akses langsung ke data menggunakan access modifier (`private`, `protected`, `public`).

**Contoh (C++):**

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

di sini terlihat bahwa data `voltage` tidak bisa diakses langsung sehingga lebih aman.

---

### **5. Inheritance**

Inheritance memungkinkan sebuah class mewarisi atribut dan method dari class lain. Konsep ini membantu *code reuse* dan representasi hubungan hierarkis.

**Contoh (C++):**

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

Dapat dilihat bahwa `GPSSensor` mewarisi fungsi `readData()` dari class `Sensor`.

---

### **6. Polymorphism**

Polymorphism memungkinkan method dengan nama yang sama memiliki perilaku berbeda tergantung pada objek yang memanggilnya. Biasanya diimplementasikan menggunakan *virtual function*.

**Contoh (C++):**

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

Pemanggilan `read()` akan bergantung pada tipe objek yang sebenarnya, bukan tipe pointernya.

---

### **Referensi**

1. B. Stroustrup, *The C++ Programming Language*, 4th ed., Addison-Wesley, 2013.
2. R. C. Martin, *Clean Code*, Prentice Hall, 2008.
3. [https://en.cppreference.com/w/](https://en.cppreference.com/w/)
4. P. Deitel and H. Deitel, *C++ How to Program*, Pearson, 2017.
5. ROS 2 Documentation, [https://docs.ros.org/en/humble/](https://docs.ros.org/en/humble/)

---

## **Dasar Pemrograman 2: Konsep Dasar C++**

### **2.a. Perbedaan `#include <file_name>` dan `#include "file_name"`**

Directive `#include` diproses oleh *preprocessor* sebelum kompilasi dimulai, di mana isi file header disalin secara literal ke file sumber.

* **`#include <file_name>`**
  Digunakan untuk header standar atau library sistem. Compiler akan mencari di *system include path*.
  Contoh: `<iostream>`, `<vector>`

* **`#include "file_name"`**
  Digunakan untuk header buatan sendiri. Compiler akan mencari di direktori proyek terlebih dahulu, lalu ke system path.

**Contoh:**

```cpp
#include <iostream>
#include "motor.hpp"
```

---

### **2.b. Penggunaan `#ifdef`, `#ifndef`, `#endif`, dan `#pragma once`**

Digunakan untuk mencegah *multiple inclusion* pada header file yang dapat menyebabkan *multiple definition error*.

**Include guard:**

```cpp
#ifndef MOTOR_HPP
#define MOTOR_HPP

class Motor {};

#endif
```

**`#pragma once`:**

```cpp
#pragma once
class Motor {};
```

Digunakan di banyak proyek modern seperti ROS2 dan PX4.

---

### **2.c. Namespace dan scope resolution operator (`::`)**

Namespace digunakan untuk mengelompokkan simbol agar tidak terjadi konflik nama.

**Contoh:**

```cpp
std::cout << "Telemetry aman terkendali icibos!" << std::endl;
```

Contoh penerapan:

* ROS2: `rclcpp::Node`
* OpenCV: `cv::Mat`

---

### **2.d. Perbedaan `#define` dan `using`**

**`#define`** adalah macro preprocessor yang melakukan *text substitution* dan tidak memiliki tipe data.

```cpp
#define MAX_SPEED 10
```

Contoh masalah:

```cpp
#define SQR(x) x*x
SQR(1+2)
```

**`using`** diproses oleh compiler, bertipe jelas, dan mengikuti scope.

```cpp
using Speed = double;
```

---

### **2.e. Pointer (`*`) dan address-of (`&`)**

Pointer adalah variabel yang menyimpan alamat memori.

```cpp
int altitude = 100;
int* ptr = &altitude;
```

Digunakan dalam UAV untuk driver sensor, akses register, dan buffer data real-time.

---

### **2.f. Pass by value dan pass by reference**

**Pass by Value:**

```cpp
void process(Data d);
```

**Pass by Reference:**

```cpp
void process(Data& d);
```

---

### **2.g. `std::unique_ptr` dan `std::shared_ptr`**

**`std::unique_ptr`:**

```cpp
std::unique_ptr<IMUSensor> imu = std::make_unique<IMUSensor>();
```

**`std::shared_ptr`:**

```cpp
std::shared_ptr<Map> map = std::make_shared<Map>();
```

---

## **Dasar Pemrograman 3: Multithreading**

### **3.a. Konsep dasar multithreading**

Multithreading adalah kemampuan program menjalankan beberapa alur eksekusi secara bersamaan untuk meningkatkan efisiensi dan mendukung sistem real-time.

Contoh pada UAV:

* Telemetri
* Video stream
* Kontrol & logging

---

### **3.b. Implementasi Program Multithreading**

Contoh file `telemetry.txt`:

```txt
ALT: 100 m
SPD: 12 m/s
GPS: -7.95, 112.61
BAT: 11.1 V
```

Kode C++:

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

---

## **Firmware dan Sistem Benam**

### **1. Firmware dan perannya dalam UAV**

Firmware adalah *low-level software* yang tertanam langsung pada hardware dan berfungsi sebagai penghubung antara hardware dan software tingkat atas.

Firmware merupakan otak utama UAV dan menangani kontrol motor, sensor, flight control loop, serta komunikasi.

---

### **2. Real-Time Operating System (RTOS)**

RTOS menjamin respon deterministik dalam batas waktu tertentu dan sangat penting untuk sistem UAV yang bersifat real-time.

Contoh RTOS:

* FreeRTOS
* NuttX
* Zephyr

---

### **3. Komunikasi Serial dalam UAV (UART, SPI, I2C)**

* **UART:** komunikasi sederhana dan stabil (GPS, telemetry)
* **SPI:** kecepatan tinggi dan latensi rendah (IMU)
* **I2C:** efisien wiring untuk sensor pendukung

Pendekatan ini membuat sistem UAV modular, efisien, dan andal.

---

## **Jawaban Control and Perception (ConCept)**

### **Konsep dasar ROS**

ROS2 membangun sistem sebagai kumpulan node yang berkomunikasi menggunakan topic, service, parameter, dan action.

* **Node:** unit program mandiri
* **Topic:** komunikasi publish–subscribe
* **Service:** request–response
* **Parameter:** konfigurasi runtime
* **Action:** tugas berdurasi panjang


### **Sistem publisher dan subscriber dalam C++**

Pada soal ini dibuat sebuah sistem komunikasi sederhana menggunakan ROS2 Humble dengan mekanisme **publisher–subscriber**. Sistem terdiri dari dua node yang saling berkomunikasi melalui sebuah topic. Tujuan utama dari implementasi ini adalah menunjukkan pemahaman terhadap konsep dasar komunikasi data pada ROS2 menggunakan bahasa C++.

Workspace ROS2 dibuat dengan nama bebas, sedangkan package diberi nama `yapping` sesuai ketentuan soal. Di dalam package tersebut terdapat dua node, yaitu node publisher bernama `clock` dan node subscriber bernama `watch`. Keduanya berkomunikasi melalui sebuah topic bernama `time`.

Node `clock` berperan sebagai publisher yang secara periodik mengambil waktu sistem saat ini, memformatnya ke dalam format ISO 8601, lalu mengirimkannya ke topic `time`. Format ISO 8601 dipilih karena merupakan standar internasional yang tidak ambigu terhadap zona waktu serta umum digunakan dalam sistem terdistribusi seperti UAV dan robotika.

Node `watch` berperan sebagai subscriber yang mendengarkan topic `time`. Setiap kali pesan diterima, node ini akan menampilkan informasi waktu tersebut ke terminal. Komunikasi antar node menggunakan tipe pesan `std_msgs/msg/String`, karena data waktu direpresentasikan dalam bentuk string.

---

**Struktur workspace ROS2 yang digunakan adalah sebagai berikut:**
```css
ros2_ws/
└── src/
    └── yapping/
        ├── CMakeLists.txt
        ├── package.xml
        └── src/
            ├── clock.cpp
            └── watch.cpp
```
File hasil build seperti `build`, `install`, dan `log` tidak disertakan dalam repositori sesuai instruksi soal.

---

**Implementasi Node Publisher (clock.cpp)**
```cpp
#include <rclcpp/rclcpp.hpp>
#include <std_msgs/msg/string.hpp>
#include <chrono>
#include <ctime>
#include <iomanip>
#include <sstream>

class ClockNode : public rclcpp::Node {
public:
    ClockNode() : Node("clock") {
        publisher_ = this->create_publisher<std_msgs::msg::String>("time", 10);

        timer_ = this->create_wall_timer(
            std::chrono::seconds(1),
            std::bind(&ClockNode::publish_time, this)
        );
    }

private:
    void publish_time() {
        auto msg = std_msgs::msg::String();

        auto now = std::chrono::system_clock::now();
        std::time_t now_time = std::chrono::system_clock::to_time_t(now);
        std::tm utc_time = *std::gmtime(&now_time);

        std::stringstream ss;
        ss << std::put_time(&utc_time, "%Y-%m-%dT%H:%M:%SZ");
        msg.data = ss.str();

        publisher_->publish(msg);
    }

    rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
    rclcpp::TimerBase::SharedPtr timer_;
};

int main(int argc, char *argv[]) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<ClockNode>());
    rclcpp::shutdown();
    return 0;
}
```
Node ini menggunakan timer ROS2 untuk mem-publish pesan setiap satu detik. Waktu diformat ke dalam ISO 8601 dengan zona waktu UTC agar konsisten pada sistem terdistribusi.

---

**Implementasi Node Subscriber (watch.cpp)**
```cpp
#include <rclcpp/rclcpp.hpp>
#include <std_msgs/msg/string.hpp>

class WatchNode : public rclcpp::Node {
public:
    WatchNode() : Node("watch") {
        subscription_ = this->create_subscription<std_msgs::msg::String>(
            "time",
            10,
            std::bind(&WatchNode::callback, this, std::placeholders::_1)
        );
    }

private:
    void callback(const std_msgs::msg::String::SharedPtr msg) const {
        RCLCPP_INFO(this->get_logger(), "Current time: %s", msg->data.c_str());
    }

    rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char *argv[]) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<WatchNode>());
    rclcpp::shutdown();
    return 0;
}
```
Node watch akan menerima setiap pesan yang dipublish pada topic time dan mencetak isinya ke terminal menggunakan logger ROS2.

---

**Penjelasan Format Waktu**
Format waktu ISO 8601 dipilih karena:
* Merupakan standar internasional
* Tidak ambigu terhadap zona waktu
* Mudah diparsing pada sistem terdistribusi
* Umum digunakan pada sistem logging dan komunikasi UAV
Contoh pesan yang dikirimkan:
`2026-01-22T03:15:42Z`

---

**Kesimpulan**

Secara keseluruhan, sistem ini merepresentasikan pola komunikasi dasar yang umum digunakan pada ROS2, khususnya pada sistem UAV, di mana satu node bertindak sebagai sumber data dan node lain bertindak sebagai penerima atau pemantau data. Meskipun sederhana, arsitektur ini mencerminkan prinsip modularitas dan loose coupling yang menjadi keunggulan utama ROS2.