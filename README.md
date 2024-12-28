# Tugas Besar
## Pendahuluan
Repository ini berisi tugas besar unit robotika yang mengimplementasikan robot berbasis URDF (Unified Robot Description Format) dengan kemampuan untuk melakukan aksi sederhana menggunakan algoritma PID (Proportional-Integral-Derivative). Proyek ini dibangun menggunakan ROS (Robot Operating System) dan memiliki sistem simulasi untuk mempelajari kontrol dan pergerakan robot.

## 1. Cara Kerja Proyek
## Deskripsi Sistem
Robot yang dirancang memiliki dua roda penggerak (differential drive) dan satu roda caster untuk keseimbangan. Sistem menggunakan algoritma PID untuk mengontrol kecepatan roda guna mencapai pergerakan yang stabil dan presisi.
Komponen utama sistem:
- URDF Robot Model: Robot dirancang menggunakan URDF dengan deskripsi detail pada elemen fisik seperti dimensi, massa, inersia, dan material visual.
- PID Controller: PID diterapkan pada plugin untuk mengontrol kecepatan roda.
- ROS Nodes: Digunakan untuk komunikasi antar sistem, termasuk node kontrol untuk memberikan perintah kecepatan linear dan angular.
## Cara Kerja Robot
- Inisialisasi Robot: Model URDF dimuat ke dalam simulasi Gazebo.
- Pergerakan Robot: Robot menerima perintah kecepatan dari node ROS. Plugin `diff_drive` mengontrol roda menggunakan PID untuk mencapai kecepatan yang diinginkan.
- Output Simulasi: Robot menghasilkan data odometri yang dipublikasikan ke ROS dan dapat digunakan untuk analisis lebih lanjut.

## 2. Alur Kerja Sistem ROS
## Diagram Alir
[Node Kontrol] --> [Topic: /cmd_vel] --> [Plugin diff_drive] --> [Robot Movement] --> [Topic: /odom] --> [Node Monitoring]
## Penjelasan Alur
- Node Kontrol: Node ini mengirimkan perintah kecepatan (linear dan angular) ke robot melalui topic `cmd_vel`.
- Plugin diff_drive: Plugin membaca perintah `cmd_vel` dan mengontrol roda menggunakan PID untuk mencapai kecepatan yang diminta.
- Robot Movement: Robot bergerak sesuai perintah. Posisi dan orientasi dihitung melalui odometri.
- Node Monitoring: Data odometri diterbitkan ke topic `odom` untuk dianalisis atau digunakan oleh sistem lain.
## Topik yang Digunakan
- `/cmd_vel`: Input kecepatan dari node kontrol.
- `/odom`: Data odometri yang dipublikasikan oleh robot.
- `/tf`: Transformasi posisi dan orientasi.

## Cara Menjalankan Simulasi
### 1.  Build Workspace
    cd <workspace> 
    colcon build --symlink-install
    source install/local_setup.bash
### 2.  Jalankan Simulasi Gazebo
    ros2 launch <launch-file> gazebo.launch.py
### 3.  Kontrol Robot
- Gunakan node kontrol seperti `teleop_twist_keyboard` untuk mengirim perintah ke `/cmd_vel`.
- Monitor odometri menggunakan `rostopic echo /odom`.
## Catatan Tambahan
- Pastikan semua dependensi ROS terinstal.
- Lakukan tuning PID pada plugin untuk mendapatkan performa optimal.

## 3. Video Simulasi Robot
