# 🚀 Transfer Learning – Pertemuan 1

## Motion Amarine

Dokumen ini berisi panduan **instalasi dan verifikasi ROS 2 Humble** menggunakan **Ubuntu di VMware** sebagai bagian dari **Pertemuan 1 – Transfer Learning** pada divisi **Motion Amarine**.

Tujuan utama dari pertemuan ini adalah memastikan seluruh environment robotika sudah siap sebelum masuk ke materi lanjutan seperti kontrol, simulasi, dan integrasi sistem.

---

## 🎯 Tujuan Pembelajaran

* Memahami setup dasar environment robotika berbasis Linux
* Menginstal dan mengonfigurasi ROS 2 Humble dengan benar
* Memverifikasi instalasi ROS 2 melalui simulasi `turtlesim`

---

## 🖥️ Spesifikasi Lingkungan

* **Host OS**: Windows
* **Virtualization**: VMware Workstation / Player
* **Guest OS**: Ubuntu (disarankan 22.04 LTS)
* **ROS Version**: ROS 2 Humble Hawksbill

---

## 🛠️ Kebutuhan Awal (Prerequisites)

Sebelum masuk ke instalasi ROS 2, **Ubuntu harus benar-benar siap pakai**. Bagian ini menjelaskan proses **dari nol**: apa saja yang dibutuhkan hingga Ubuntu siap digunakan di VMware.

---

## 💿 Instalasi Ubuntu di VMware (Dari Nol)

### 1️⃣ Perangkat & File yang Dibutuhkan

#### Hardware Minimum

* Laptop / PC (64-bit)
* RAM minimal 8 GB (4 GB masih bisa, tapi ngos-ngosan)
* Storage kosong minimal 50 GB
* Virtualization aktif di BIOS (Intel VT-x / AMD-V)

#### Software

* **VMware Workstation** (Windows / Linux)
* **File ISO Ubuntu 22.04 LTS**

> Kenapa 22.04?
> Karena **ROS 2 Humble hanya stabil di Ubuntu 22.04 (Jammy)**. Versi lain bikin hidup tidak tenang.

---

### 2️⃣ Install VMware Workstation

1. Download VMware Workstation Player / Pro dari website resmi VMware
2. Install seperti aplikasi biasa
3. Restart PC jika diminta

Pastikan VMware bisa dibuka tanpa error.

---

### 3️⃣ Buat Virtual Machine Baru

1. Buka **VMware** → klik **Create a New Virtual Machine**
2. Pilih **Installer disc image file (iso)**
3. Pilih file **Ubuntu 22.04 LTS (.iso)**
4. Klik **Next**

Jika muncul menu *Easy Install*, biarkan aktif.

---

### 4️⃣ Konfigurasi Virtual Machine

#### Rekomendasi Setting

* **Guest OS**: Linux → Ubuntu 64-bit
* **CPU**: 2 core atau lebih
* **RAM**: 4 GB minimum (8 GB disarankan)
* **Disk**: 40–50 GB (Single file lebih aman)
* **Network**: NAT

Klik **Finish** untuk membuat VM.

---

### 5️⃣ Proses Instalasi Ubuntu

1. Jalankan VM
2. Tunggu installer Ubuntu muncul
3. Pilih:

   * Language: English
   * Keyboard: English (US)
4. Pilih **Normal Installation**
5. Centang **Install third-party software**
6. Pilih **Erase disk and install Ubuntu**

   * (Ini hanya disk virtual, aman)
7. Atur:

   * Timezone
   * Username & Password

Tunggu hingga instalasi selesai (±10–20 menit).

---

### 6️⃣ First Boot & Setup Awal Ubuntu

Setelah masuk desktop Ubuntu:

1. Buka **Terminal** (`Ctrl + Alt + T`)
2. Update sistem:

```bash
sudo apt update && sudo apt upgrade -y
```

3. (Opsional tapi disarankan) Install VMware Tools jika belum otomatis

Ubuntu sekarang **siap dipakai** untuk instalasi ROS 2.

---

## 🛠️ Persiapan Awal

1. Pastikan Ubuntu sudah berjalan di VMware.
2. Buka **Terminal** dengan shortcut:

   ```bash
   Ctrl + Alt + T
   ```
3. Jika copy–paste dari Windows tidak berfungsi:

   * Gunakan browser **Firefox** di Ubuntu
   * Buka repository / chat ini langsung dari dalam VM

---

## 🔧 Langkah 1: Konfigurasi Locale

Pastikan sistem menggunakan UTF-8 agar ROS berjalan tanpa error.

```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

## 📦 Langkah 2: Menambahkan Repository ROS 2

Langkah ini membuat Ubuntu mengenali sumber paket resmi ROS 2.

```bash
sudo apt install software-properties-common -y
sudo add-apt-repository universe -y

sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 🤖 Langkah 3: Instalasi ROS 2 Humble

Proses ini akan mengunduh paket utama ROS 2 (±2–3 GB).

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install ros-humble-desktop -y
```

⏳ Tunggu hingga proses selesai 100% tanpa error.

---

## 🌱 Langkah 4: Setup Environment ROS

Agar perintah `ros2` otomatis aktif setiap membuka terminal.

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 🐢 Langkah 5: Uji Coba Simulasi (Turtlesim)

Tahap verifikasi bahwa ROS 2 berhasil terpasang.

### Terminal 1

```bash
ros2 run turtlesim turtlesim_node
```

➡️ Akan muncul jendela simulator kura-kura.

### Terminal 2 (Terminal Baru)

```bash
ros2 run turtlesim turtle_teleop_key
```

Gunakan tombol **Panah Atas / Bawah / Kiri / Kanan** pada keyboard untuk menggerakkan kura-kura.

---

## ✅ Indikator Keberhasilan

* Tidak ada error merah saat menjalankan perintah
* Jendela `turtlesim` muncul
* Kura-kura dapat bergerak menggunakan keyboard

Jika semua poin di atas terpenuhi, maka environment ROS 2 di VMware **siap digunakan**.

---

## 📌 Catatan

* Gunakan Ubuntu LTS untuk stabilitas jangka panjang
* Pastikan koneksi internet VM stabil saat instalasi
* Jangan lanjut ke materi berikutnya sebelum tahap ini berhasil

---

---

## 📤 Implementasi: Push Project ROS 2 (Contoh: Turtleboat)

Bagian ini mencontohkan **project ROS 2 nyata** bernama `turtleboat`, lalu bagaimana cara **menyimpannya ke GitHub dengan struktur yang benar**.

---

## 🗂️ Contoh Struktur Project ROS 2

Misalkan kita membuat workspace ROS 2 bernama `ros2_ws` dan package `turtleboat`:

```text
ros2_ws/
├── src/
│   └── turtleboat/
│       ├── package.xml
│       ├── setup.py
│       ├── setup.cfg
│       ├── resource/
│       │   └── turtleboat
│       ├── turtleboat/
│       │   └── turtleboat_node.py
│       └── README.md
└── README.md
```

> Yang di-push ke GitHub adalah **folder workspace atau package**, bukan hasil build.

---

## 1️⃣ Membuat Workspace & Package (Contoh)

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

ros2 pkg create turtleboat --build-type ament_python
```

Kembali ke workspace:

```bash
cd ~/ros2_ws
colcon build
source install/setup.bash
```

Pastikan package bisa dikenali:

```bash
ros2 pkg list | grep turtleboat
```

---

## 2️⃣ Inisialisasi Git pada Project

Masuk ke folder workspace:

```bash
cd ~/ros2_ws
```

Buat file `.gitignore`:

```bash
nano .gitignore
```

Isi dengan:

```text
build/
install/
log/
__pycache__/
*.pyc
```

Simpan, lalu:

```bash
git init
git add .
git commit -m "Initial commit - turtleboat ROS2 project"
```

---

## 3️⃣ Buat Repository di GitHub

1. Login ke GitHub
2. Klik **New Repository**
3. Nama repo contoh: `turtleboat-ros2`
4. Jangan centang README atau .gitignore

---

## 4️⃣ Hubungkan & Push ke GitHub

```bash
git branch -M main
git remote add origin https://github.com/username/turtleboat-ros2.git
git push -u origin main
```

Jika berhasil, seluruh project ROS 2 kamu sekarang **tersimpan aman di GitHub**.

---

## 5️⃣ Best Practice (WAJIB DIPATUHI)

* ❌ Jangan push folder `build/`, `install/`, `log/`
* ✅ Push hanya source code
* ✅ Satu repo = satu project utama
* ✅ README wajib menjelaskan cara build & run

Jika berhasil, project kamu sudah online 🚀

---

## 🏁 Penutup

Setup ini menjadi fondasi utama untuk seluruh aktivitas **Motion Amarine**, termasuk simulasi, kontrol robot, dan pengembangan sistem otonom.

Selamat, kamu resmi siap masuk ke dunia robotika berbasis ROS 2 🚀
