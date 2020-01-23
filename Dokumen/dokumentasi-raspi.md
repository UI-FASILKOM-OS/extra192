# Raspberry Pi Manual
## Access Point and Wi-fi

### Extra 192:
Aditya Pratama - 1706039490
Hana Dior Novelyne Tobing - 1706025182
Mochamad Naufal Dzulfikar - 1706043903
Sayid Abyan Rizal Shiddiq - 1706022445
Selvy Fitriani - 1706039446

---

### Tujuan 
Modul ini dibuat untuk membantu pembaca untuk melakukan pengaturan Raspberry Pi 3 sebagai <em>access point</em> dan wi-fi. Isi dari modul ini terbagi menjadi cara melakukan <em>flash</em> OS Image ke SD Cards melalui Raspberry Pi, melakukan instalasi Raspbian dan Etcher, menambah dan menghapus <em>user</em> pada Raspberry Pi, dan pengaturan Raspberry Pi menjadi <em>access point</em> dan wifi.
<em>Keywords</em>: Raspberry Pi, raspi, <em>access point</em>

### Spesifikasi 
Hal-hal yang harus Anda siapkan:
* Micro SD card
* Micro USB power supply (2.1 A)
* Raspberry pi (kami menggunakan raspberry pi 3 model B)

Dan untuk menggunakan hal diatas sebagai desktop  komputer, Anda membutuhkan:
* TV or monitor dan HDMI cable
* Keyboard dan mouse

## Metode

### Bagaimana cara melakukan Flash pada Raspberry Pi OS Image ke SD Cards

Untuk memulai, perangkat kita butuh menjalankan sebuah Sistem Operasi  Jadi, kami akan menggunakan sebuah Sistem Operasi resmi yaitu Raspbian.

#### Instalasi raspbian
Untuk melakukan instalasi Raspbian, lakukan tahap-tahap berikut:
* Buka link https://www.raspberrypi.org/downloads/raspbian/ dan pilih versi terakhir Raspbian Buster with desktop.
* Jika anda telah menginstall <em>torrent client</em>, karena waktu unduhnya lebih cepat dibandingkan langsung mengunduh versi zip-nya. Setelah file .torrent berhasil diunduh, silahkan ubah menjadi file .zip dengan <em>torrent client</em> yang Anda miliki. Pilihan lainnya adalah langsung mengunduh versi zip nya.

![text](https://github.com/UI-FASILKOM-OS/extra192/blob/master/Dokumen/Images/raspbian.png)

#### Instalasi Etcher
Selanjutnya, kita **membutuhkan sebuah aplikasi** untuk melakukan flash terhadap image ke sebuah SD Card karena dengan cara inilah, perangkat kita bisa berjalan. Pastikan SD Card Anda sudah dalam bentuk Micro SD.
Aplikasi yang kami gunakan adalah Etcher, silahkan ikuti tahapan berikut:
* Buka link : https://www.balena.io/etcher/ . Pilih versi terakhir yang sesuai dengan Sistem Operasi Anda. Kemudian install.
* Sambungkan SD Card reader dengan SD Card didalamnya.
* Buka balenaEtcher yang sudah ter-install, klik “Select Image” kemudian pilih  Raspberry Pi .img atau .zip yang ingin ditulis pada SD Card.
* Kemudian, klik “Select Drive” untuk memilih SD Card tempat image akan ditulis.
* Periksa kembali file yang dipilih kemudian klik ‘Flash’ untuk memulai menulis data ke SD card.

Sekarang, Anda sudah bisa memasukkan SD Card Anda ke Raspberry pi dan bisa mulai menggunakan Raspbian OS.

### Menambahkan dan Menghapus User 
#### Menambahkan User
Anda bisa menambahkan users pada instalasi Raspbian dengan menggunakan perintah **adduser**.
* Masukkan **sudo adduser [username]**, misalnya username yang akan Anda tambahkan adalah rms46.

        sudo adduser rms46

* Setelah itu, Anda diminta untuk memasukkan password sebanyak 2 kali, sebagai upaya untuk mengonfirmasi <em>password</em> Anda.

#### Memberikan sudo privileges kepada user
Untuk memberikan sudo privileges bagi setiap user, Anda perlu mengakses /etc/sudoers.tmp, lalu tambahkan potongan kode berikut di bawah root

	%sudo ALL=(ALL:ALL) ALL


#### Menghapus User
Anda bisa menghapus users pada sistem Anda dengan menjalankan perintah **userdel**. Gunakan <em>-r flag</em> untuk menghapus folder home mereka.

    sudo userdel -r rms46


#### Menambah User dalam Jumlah Banyak sebagai Script
Untuk menambahkan users dalam jumlah banyak, Anda dapat mengikuti langkah di bawah ini. Pada tahap ini, Anda dapat membuat sebuah script untuk memanggil fungsi tersebut.
    
    sudo nano namascript


Setelah menentukan nama script, maka Anda dapat menambahkan code di bawah ke dalam <em>script</em> tersebut

    #!/bin/bash
    for i in $( cat users.txt ); do
    useradd $i
    echo "user $i added successfully!"
    echo $i:$i"123" | chpasswd
    echo "Password for user $i changed successfully"
    done

### Mengatur Raspberry Pi sebagai Access Point dan Wi-fi Client
#### Meng-update sistem
Untuk melanjutkan ke tahap ini, kita terlebih dahulu melakukan update sistem. Hal ini bertujuan agar sistem yang kita gunakan mendapatkan fitur terbaru.

    sudo apt-get update
    sudo apt-get upgrade

#### Meng-install hostapd dan dnsmasq
Selanjutnya kita meng-install hostapd (sebuah access point daemon) dan dnsmasq dhcp service.

    sudo apt-get install hostapd dnsmasq

#### Meng-edit configuration files
Pada tahap ini kita akan melakukan perubahan terhadap config files untuk dhcps, hostapd, dan dnsmasq agar dapat saling bekerja dengan baik.

Pertama kita pindah ke /etc/dhcpcd.conf lalu di dalamnya kita tambahkan

    interface uap0
        static ip_address=192.168.4.1
        nohook  wpa_supplicant

Selanjutnya kita akan melakukan perubahan terhadap dnsmasq. Pertama kita pindah terlebih dahulu ke config files untuk dnsmasq.

    sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig 

Membuat sebuah /etc/dnsmasq.conf dan menambahkan:

    interface=lo,uap0
    bind-interfaces
    server=8.8.8.8
    domain-needed
    bogus-priv
    dhcp-range=192.168.70.50,192.168.70.150,12h

*Catatan: IP address range yang digunakan dapat sesuai dengan keinginan Anda.*

Membuat sebuah file /etc/hostapd/hostapd.conf dan menambahkan:
Anda boleh untuk menghapus baris komentar (yang diawali oleh tanda #)

    #Melakukan set terhadap channel host access point
    channel=1
    
    #Melakukan set SSID Host
    ssid=yourSSIDhere
    
    #Melakukan set password
    wpa_passphrase=passwordBetween8and64charactersLong
    
    #Nama dari wifi interface yang telah dikonfigurasi sebelumnya
    interface=uap0
    
    #Gunakan 2.4GHz band
    hw_mode=g
    
    #Menerima semua MAC addresses
    macaddr_acl=0
    
    #Gunakan WPA authentication
    auth_algs=1
    
    #Berguna untuk menjamin klien untuk mengetahui nama network
    ignore_broadcast_ssid=0
    
    #Gunakan WPA2
    wpa=2
    
    #Gunakan pre-shared key
    wpa_key_mgmt=WPA-PSK
    wpa_pairwise=TKIP
    rsn_pairwise=CCMP
    driver=nl80211
    
    #Tambahan referensi
    
    #Enable WMM
    #wmm_enabled=1
    #Enable 40MHz channels with 20ns guard interval
    #ht_capab=[HT40][SHORT-GI-20][DSSS_CCK-40]

*Catatan : channel yang ditulis di sini HARUS sesuai dengan channel wifi yang Anda sambungkan dalam client mode (melalui wpa-supplicant). Jika channel untuk Access Point dan  dan STA(stations) Anda tidak cocok, maka salah satu atau keduanya tidak akan berjalan. Hal ini disebabkan karena hanya ada satu antena fisik yang tidak bisa mencakup dua saluran sekaligus.*

Meng-edit file /etc/default/hostapd dan tambahkan script berikut ini setelah #DAEMON_CONF:

    DAEMON_CONF="/etc/hostapd/hostapd.conf" 

Membuat startup script
Tambahkan sebuah file baru /usr/local/bin/wifistart (Anda boleh memilih nama apapun yang Anda suka), kemudian tambahkan:

    systemctl stop hostapd.service
    systemctl stop dnsmasq.service
    systemctl stop dhcpcd.service

    #Pastikan tidak ada uap0 yang dijalankan (hal ini dapat menyebabkan error)
    echo "Removing uap0 interface..."
    iw dev uap0 del

    #Tambahkan uap0 interface (bergantung pada wireless interface bernama wlan0, yang kemungkinan tidak terdapat pada Stretch)
    echo "Adding uap0 interface..."
    iw dev wlan0 interface add uap0 type __ap

    #Modifikasi iptables
    echo "IPV4 forwarding: setting..."
    sysctl net.ipv4.ip_forward=1
    echo "Editing IP tables..."
    iptables -t nat -A POSTROUTING -s 192.168.70.0/24 ! -d 192.168.70.0/24 -j MASQUERADE

    #Jalankan kembali uap0 interface. Baris yang dikomentari dapat menjadi alternatif untuk menggunakan dhcpcd.conf to set up the IP address.
    #ifconfig uap0 192.168.70.1 netmask 255.255.255.0 broadcast 192.168.70.255
    ifconfig uap0 up

    #Jalankan hostapd. 10-second sleep berguna untuk mencegah race condition. Dapat diatur sesuai preferensi 
    echo "Starting hostapd service..."
    systemctl unmask hostapd.service
    systemctl start hostapd.service
    sleep 10

    #Jalankan dhcpcd
    echo "Starting dhcpcd service..."
    systemctl start dhcpcd.service
    sleep 5

    echo "Starting dnsmasq service..."
    systemctl start dnsmasq.service
    echo "wifistart DONE"

Meng-edit local system script
Tambahkan script dibawah ini ke /etc/rc.local diatas exit 0 line
(Perhatikan: ada spasi antara “/bin/bash” dan "/usr/local/bin/wifistart")

Menonaktifkan regular network services
Menonaktifkan artinya memastikan bahwa tidak ada hal yang dijalankan ketika system startup.

    sudo systemctl stop hostapd
    sudo systemctl stop dnsmasq
    sudo systemctl stop dhcpcd
    sudo systemctl disable hostapd
    sudo systemctl disable dnsmasq
    sudo systemctl disable dhcpcd

Reboot
Untuk melakukan reboot, ikuti petunjuk di bawah ini.
(Tidak diwajibkan)

    sudo reboot

Untuk memberi izin untuk eksekusi sebagai script

    chmod +x path to nama_file

### Mengubah *Swap Size* Raspi
Pertama, hentikan *swap*

    sudo dphys-swapfile swapoff

Modifikasi *swap size*

    CONF_SWAPSIZE=1024
    
Lalu, jalankan kembali *swap*
    
    sudo dphys-swapfile swapon


---

## Referensi
Buy a Raspberry Pi 3 Model B – Raspberry Pi. (n.d.). Diambil dari https://www.raspberrypi.org/products/raspberry-pi-3-model-b/

Setting up a Raspberry Pi as a Wireless Access Point. (n.d.). Diambil dari https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md

Installing operating system images. (n.d.). Diambil dari https://www.raspberrypi.org/documentation/installation/installing-images/README.md

Linux users. (n.d.). Diambil dari https://www.raspberrypi.org/documentation/linux/usage/users.md

Raspberry Pi - Increase Swap Size. (n.d). Retrieved from https://wpitchoune.net/tricks/raspberry_pi3_increase_swap_size.html


Pugbot. (2019, February 15). *Raspberry Pi 3 B+ as Access Point and Wifi Client*. Retrieved from https://lb.raspberrypi.org/forums/viewtopic.php?t=211542.

## Source
<em> source </em> dokumentasi ini bisa diakses pada [link](https://hackmd.io/@tehtarikjells/B1J28jfbU/edit) ini