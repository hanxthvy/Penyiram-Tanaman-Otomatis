# 🌱 Sistem Penyiraman Otomatis Arduino
  
<div align="center">

![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Sistem pintar untuk menyiram tanaman secara otomatis berdasarkan kelembaban tanah**

*"Tanamanmu sehat, hidupmu tenang"* 🌿

</div>

---

## 📋 Daftar Isi
- 🎯 [Overview](#-overview)
- ✨ [Fitur Unggulan](#-fitur-unggulan)
- 📦 [Hardware yang Diperlukan](#-hardware-yang-diperlukan)
- 🔌 [Wiring Diagram](#-wiring-diagram)
- 🔧 [Instalasi dan Setup](#-instalasi-dan-setup)
- 🎮 [Cara Penggunaan](#-cara-penggunaan)
- 💻 [Command List](#-command-list)
- 📊 [Penjelasan Kode](#-penjelasan-kode)
- 🚀 [Tips Penggunaan](#-tips-penggunaan)
- 🤝 [Kontribusi](#-kontribusi)
- 📄 [Lisensi](#-lisensi)

---

## 🎯 Overview
Sistem Penyiraman Otomatis ini adalah solusi cerdas untuk menjaga tanaman tetap sehat tanpa harus khawatir lupa menyiram. Dengan sensor kelembaban tanah, pompa air akan otomatis aktif kalau tanah terlalu kering.

---

## 🎨 Visual Sistem Kerja
```
Sensor Baca Kelembaban → Analisis Data → Keputusan Penyiraman → Action Motor
       ↑                      ↑               ↑
   Tanaman Kering?    Threshold Setting    Mode Operation
```

---

## ✨ Fitur Unggulan
- 🌊 **Auto Watering**: Menyiram otomatis sesuai kelembaban
- 💡 **LED Indicator**: 3 warna status (Merah/Kuning/Hijau)
- 📱 **Serial Monitor Control**: Kontrol penuh via Serial
- 💾 **EEPROM Memory**: Threshold tersimpan permanen
- 📊 **Moving Average**: Data sensor lebih akurat
- ⚠️ **Anomaly Detection**: Deteksi error sensor otomatis
- 🔄 **Multiple Modes**: Auto, Manual ON, Manual OFF

---

## 📦 Hardware yang Diperlukan
| Komponen               | Jumlah | Keterangan               |
|-------------------------|--------|--------------------------|
| Arduino Uno             | 1      | Board utama              |
| Soil Moisture Sensor    | 1      | Sensor kelembaban tanah  |
| Relay Module            | 1      | Kontrol pompa air        |
| Water Pump              | 1      | Pompa air mini           |
| LED Merah, Kuning, Hijau| 3      | Indikator status         |
| Resistor 220Ω           | 3      | Untuk LED                |
| Breadboard              | 1      | Tempat rangkai           |
| Kabel Jumper            | -      | Konektor                 |

---

## 🔌 Wiring Diagram
```
Arduino Pin   →   Komponen
A0           →   Soil Sensor Signal
Pin 7        →   Relay IN (kontrol pompa)
Pin 2        →   LED Merah (+ resistor 220Ω)
Pin 3        →   LED Kuning (+ resistor 220Ω)
Pin 4        →   LED Hijau (+ resistor 220Ω)
5V           →   Sensor VCC, Relay VCC
GND          →   Sensor GND, Relay GND, LED Cathode
```

---

## 🔧 Instalasi dan Setup
### 1. Software
1. Download **Arduino IDE** dari [arduino.cc](https://www.arduino.cc/)
2. Install sesuai OS
3. Sambungkan Arduino via USB

### 2. Upload Code
```cpp
// Salin kode utama ke Arduino IDE
// Klik "Verify" (✓) → kompilasi
// Klik "Upload" (→) → unggah ke board
```

### 3. Hardware Setup
- Rangkai sesuai wiring diagram
- Pastikan koneksi benar sebelum menyalakan

### 4. Testing
1. Buka Serial Monitor (9600 baud)
2. Tunggu LED startup animation
3. Sistem siap 🎉

---

## 🎮 Cara Penggunaan
### Mode Otomatis (Default)
```bash
# Sistem otomatis menyiram ketika tanah kering
# Threshold default: 500 (1-1023, makin kecil makin basah)
```

### Monitoring Real-time
```bash
monitor on

[DATA] Sensor: 650 | Kering: 63% -> [AUTO] Kering → Motor ON
[DATA] Sensor: 300 | Kering: 29% -> [AUTO] Basah → Motor OFF
```

### Manual Control
```bash
mode on    # Paksa motor ON
mode off   # Matikan motor
mode auto  # Kembali ke otomatis
```

---

## 💻 Command List
| Command | Contoh | Keterangan |
|---------|--------|------------|
| `set <angka>` | `set 600` | Atur threshold kelembaban |
| `mode <auto/on/off>` | `mode on` | Ganti mode operasi |
| `monitor <on/off>` | `monitor on` | Tampilkan data sensor |
| `delay sensor <ms>` | `delay sensor 2000` | Interval baca sensor |
| `status` | `status` | Cek kondisi sistem |
| `help` | `help` | Lihat semua command |

---

## 📊 Penjelasan Kode
### Struktur Program
```cpp
// Konfigurasi
const int sensorPin = A0;
const int motorPin  = 7;

// Setup awal
void setup() {
  Serial.begin(9600);
}

// Loop utama
void loop() {
  // Baca sensor → Analisis → Kontrol motor
}
```

### Fungsi Penting
- `bacaSensor()` → Baca kelembaban + moving average  
- `printStatus()` → Status real-time ke Serial  
- `cekSerial()` → Baca command user  
- `animasiStartup()` → LED startup  

### Parameter Bisa Disesuaikan
```cpp
int threshold = 500;       // Sensitivitas
int delaySensor = 1000;    // Interval baca sensor (ms)
const int sampleCount = 5; // Moving average sample
```

---

## 🚀 Tips Penggunaan
- 🌱 **Tanaman suka air** → `set 300`
- 🌵 **Tanaman tahan kering** → `set 700`

### Troubleshooting
- ❌ Sensor baca `-1` → Cek kabel sensor  
- ❌ Motor tidak nyala → Cek relay & mode  
- ❌ Serial Monitor error → Pastikan baud 9600  

---

## 🤝 Kontribusi
1. Fork repo ini  
2. Buat branch baru: `git checkout -b feature/NamaFitur`  
3. Commit: `git commit -m "Add fitur"`  
4. Push: `git push origin feature/NamaFitur`  
5. Buat Pull Request  

---

## 📄 Lisensi
Distributed under the **MIT License**.  
Lihat file [LICENSE](LICENSE) untuk detail.

---

<div align="center">

👨‍💻 Developer: **Hanxthc**  
⭐ Jangan lupa kasih bintang kalau project ini bermanfaat!  

💡 *Sistem otomatis membantu, tapi perhatian manusia tetap yang terbaik* 🌟

</div>
