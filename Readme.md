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

## 🏁 Penutup

Setup ini menjadi fondasi utama untuk seluruh aktivitas **Motion Amarine**, termasuk simulasi, kontrol robot, dan pengembangan sistem otonom.

Selamat, kamu resmi siap masuk ke dunia robotika berbasis ROS 2 🚀
