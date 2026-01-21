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
[1] B. Stroustrup, The C++ Programming Language, 4th ed., Addison-Wesley, 2013.
[2] R. C. Martin, Clean Code, Prentice Hall, 2008.
[3] https://en.cppreference.com/w/, “C++ Classes and Object-Oriented Programming”.
[4] P. Deitel and H. Deitel, C++ How to Program, Pearson, 2017.
[5] ROS 2 Documentation, https://docs.ros.org/en/humble/