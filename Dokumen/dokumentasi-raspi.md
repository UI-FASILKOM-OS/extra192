# Raspberry Pi Manual
## Access Point and Wi-fi

### Extra 192:
* Aditya Pratama - 1706039490
* Hana Dior Novelyne Tobing - 1706025182
* Mochamad Naufal Dzulfikar - 1706043903
* Sayid Abyan Rizal Shiddiq - 1706022445
* Selvy Fitriani - 1706039446

---

### Tujuan 
Modul ini dibuat untuk membantu pembaca untuk melakukan pengaturan Raspberry Pi 3 sebagai <em>access point</em> dan wi-fi. Isi dari modul ini terbagi menjadi cara melakukan <em>flash</em> OS Image ke SD Cards melalui Raspberry Pi, melakukan instalasi Raspbian dan Etcher, menambah dan menghapus <em>user</em> pada Raspberry Pi, dan pengaturan Raspberry Pi menjadi <em>access point</em> dan wifi.
<em>Keywords</em>: Raspberry Pi, raspi, <em>access point</em>

### Spesifikasi 
Hal-hal yang harus Anda siapkan:
* Micro SD card (kami menggunakan ukuran 8 GB)
![micro sd](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/micro_sd_card.jpeg)
* Micro USB power supply (2.5 A)
![micro usb power supply](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/micro-usb-power-supply.jpg)
* Raspberry pi (kami menggunakan raspberry pi 3 model B)
![raspberry pi 3 b](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/Raspberry_Pi_3_buyapi-1__20242.1539127615.jpg)

Dan untuk menggunakan spesifikasi di atas sebagai *desktop*  komputer, Anda membutuhkan:
* TV or monitor dan HDMI cable  
![monitor](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/monitor.jpg)  

![hdmi](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/hdmi.jpg)

* Keyboard dan mouse  
![keyboard and mouse](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/81Z882NR-ZL._AC_SX466_.jpg)

## Metode

### Bagaimana cara melakukan Flash pada Raspberry Pi OS Image ke SD Cards

Untuk memulai, perangkat kita butuh menjalankan sebuah Sistem Operasi  Jadi, kami akan menggunakan sebuah Sistem Operasi resmi yaitu Raspbian.

#### Instalasi raspbian
Untuk melakukan instalasi Raspbian, lakukan tahap-tahap berikut:
* Buka link https://www.raspberrypi.org/downloads/raspbian/ dan pilih versi terakhir Raspbian Buster with desktop.
![raspberry pi os](https://raw.githubusercontent.com/UI-FASILKOM-OS/extra192/master/Dokumen/Images/download-raspberry.JPG)
* Jika anda telah menginstall <em>torrent client</em>, karena waktu unduhnya lebih cepat dibandingkan langsung mengunduh versi zip-nya. Setelah file .torrent berhasil diunduh, silahkan ubah menjadi file .zip dengan <em>torrent client</em> yang Anda miliki. Pilihan lainnya adalah langsung mengunduh versi zip nya.

#### Instalasi Etcher
Selanjutnya, kita **membutuhkan sebuah aplikasi** untuk melakukan *flash* terhadap *image* ke sebuah SD Card karena dengan cara inilah, perangkat kita bisa berjalan. Pastikan SD Card Anda sudah dalam bentuk Micro SD.
Aplikasi yang kami gunakan adalah Etcher, silahkan ikuti tahapan berikut:
* Buka link : https://www.balena.io/etcher/ . Pilih versi terakhir yang sesuai dengan Sistem Operasi Anda. Kemudian *install*.
* Sambungkan SD Card *reader* dengan SD Card didalamnya.
* Buka balenaEtcher yang sudah ter-*install*, klik “Select Image” kemudian pilih  Raspberry Pi .img atau .zip yang ingin ditulis pada SD Card.
* Kemudian, klik “Select Drive” untuk memilih SD Card tempat *image* akan ditulis.
* Periksa kembali file yang dipilih kemudian klik ‘Flash’ untuk memulai menulis data ke SD card.

Sekarang, Anda sudah bisa memasukkan SD Card Anda ke Raspberry pi dan bisa mulai menggunakan Raspbian OS.

---
Pada tahapan selanjutnya, Anda dibebaskan untuk memilih melakukannya dengan mengikuti langkah-langkah yang disusun oleh Tim Extra 192 atau melakukan *cloning scripts* yang tersedia pada Github Tim Extra 192.

## Set up raspberry pi
Sebelum anda melakukan apapun pada raspberry pi, anda harus melakukan set up awal pada raspberry pi. Anda perlu set up untuk Localization, termasuk basaha dan keyboard, password untuk akun pi, dan seterusnya.

### Set up localization
Tekan tombol "Next" pada window pertama yang anda hadapi.
Kami berasumsi anda tinggal di Indonesia, sehingga silahkan pilih negara Indonesia pada tab "Country". Setelah anda lakukan itu harusnya tab "Language" dan "Timezone" akan otomatis berubah ke "Indonesia" dan "Jakarta". Setelah itu jangan lupa untuk mentik box "Use English Language" dan box "Use US Keyboard". Karena itu yang akan kita pakai pada tutorial ini.
Tekan tombol "Next".

### Change Password
Pada window ini anda harus menentukan password untuk akun pi, yaitu akun root anda. Masukan password anda pada tab "Enter new password", lakukan lagi pada tab di bawahnya.
Jika sudah, tekan tombol "Next".

### Select WiFi Network
Di sini anda disarankan memilih WiFi yang memiliki koneksi internet sehingga Raspberry Pi dapat meng-update pada window selanjutnya. Pilih WiFi yang anda miliki lalu tekan tombol "Next". Masukan password WiFi tersebut pada tab "Password", jika sudah benar tekan tombol "Next".

### Check For Updates
Di sini anda boleh memilih untuk melakukan update, namun ini akan memakan waktu yang cukup lama sehingga langsung tekan tombol "Next".

### Reboot
Tekan tombol "Reboot".
Raspberry Pi anda telah siap digunakan.

## Melakukan *cloning*  dari Github Extra 192
Pertama, lakukan git clone pada link ini https://github.com/UI-FASILKOM-OS/extra192

    git clone https://github.com/UI-FASILKOM-OS/extra192
    
### Menambah *user* dalam jumlah banyak
Setelah proses *cloning* selesai anda pindah ke direktori /extra192/Proyek/addUsers dengan

    cd extra192/Proyek/addUsers/
    
Pada direktori tersebut, tambahkan satu *file* untuk menampung daftar *username* yang akan Anda gunakan.

    sudo nano namafile

di dalamnya tambahkan *usernames* yang akan anda pakai dipisahkan dengan *new line*.
    
Lanjutkan dengan melakukan perintah ls, maka akan terlihat salah satu *file* yang *executable* yaitu appendusers. Yang Anda perlu lakukan sekarang hanyalah menajalankannya dengan

    sudo ./appendusers namafile
    
Tunggu proses hingga selesai lalu Anda dapat menambahkan *users* dalam jumlah banyak.

### Melakukan *set-up* Raspberry Pi sebagai *access point hotspot*
Setelah proses *cloning* selesai anda pindah ke direktori /extra192/Proyek/extraAuto dengan

    cd extra192/Proyek/extraAuto/
    
Pada direktori tersebut, lakukan perintah ls, maka akan terlihat salah satu *file* yang *executable* yaitu starthotspot. Yang Anda perlu lakukan sekarang hanyalah menajalankannya dengan

    sudo ./starthotspot
    
Tunggu proses hingga selesai lalu Anda dapat menggunakan Raspi sebagai *hotspot* dengan ssid "extraos" dan password "extraos192".

### Menambahkan sudo privilege pada user
Setelah proses *cloning* selesai anda pindah ke direktori /extra192/Proyek/addsudoers
    
    cd /extra192/Proyek/addsudoers/
    
Jalankan file addsudoers dengan cara 

    sudo ./addsudoers
    
Masukkan nama user yang ingin anda berikan *sudo privileges* 

**Peringatan**: user yang ingin Anda tambahkan sudo privileges-nya harus ada dalam sistem.

### Meng-generate password untuk banyak users
Setelah proses *cloning* selesai anda pindah ke direktori /extra192/Proyek/generatePassword
    
    cd /extra192/Proyek/generatePassword/

Tambahkan username yang ingin anda buatkan password secara random pada file baru dipisahkan dengan new line dengan cara

    nano namafile
    
Jalankan file generatepassword dengan cara 

    ./generatepassword namafile
    
Setelah file selesai *running*, maka akan muncul file *users.txt* yang berisi "*username* *random passwords*". 
    
## Tutorial
### Menambahkan dan Menghapus User
#### Menambahkan User
Anda bisa menambahkan *users* pada instalasi Raspbian dengan menggunakan perintah **adduser**.
* Masukkan **sudo adduser [username]**, misalnya username yang akan Anda tambahkan adalah rms46.

        sudo adduser rms46

* Setelah itu, Anda diminta untuk memasukkan password sebanyak 2 kali, sebagai upaya untuk mengonfirmasi <em>password</em> Anda.

#### Memberikan sudo privileges kepada user
Untuk memberikan sudo privileges bagi setiap user, Anda perlu membuat file sesuai dengan nama user yang ingin diberikan privileges pada /etc/sudoers.d/, lalu isi file tersebut dengan  
     
    nama_user ALL=(ALL:ALL) ALL

catatan : nama_user diganti dengan *username* yang ingin ditambahkan

#### Menghapus User
Anda bisa menghapus *users* pada sistem Anda dengan menjalankan perintah **userdel**. Gunakan <em>-r flag</em> untuk menghapus folder *home* mereka.

    sudo userdel -r rms46
    


#### Menambah User dalam Jumlah Banyak sebagai Script
Untuk menambahkan *users* dalam jumlah banyak, Anda dapat mengikuti langkah di bawah ini. Pada tahap ini, Anda dapat membuat sebuah *script* untuk memanggil fungsi tersebut.
    
    sudo nano namascript


Setelah menentukan nama *script*, maka Anda dapat menambahkan *code* di bawah ke dalam <em>script</em> tersebut

    #!/bin/bash
    IFS=$'\n'   
    for line in $(cat $1); do
        username=`(echo $line | awk '{print $1}')`
        password=`(echo $line | awk '{print $2}')`
        adduser --disabled-password --gecos "" $username
        echo $username:$password | chpasswd
    done
    unset IFS

Setelah membuat *script* tersebut, Anda perlu memberikan *permission* untuk dieksekusi dengan cara 
    
    sudo chmod +x path_to_namascript
    
### Mengatur Raspberry Pi sebagai Access Point dan Wi-fi Client
Pada tahap ini, kami menyediakan dua alternatif cara untuk mengatur raspi sebagai *access point* dan *wi-fi client*.

**Meng-update sistem**
Untuk melanjutkan ke tahap ini, kita terlebih dahulu melakukan *update* sistem. Hal ini bertujuan agar sistem yang kita gunakan mendapatkan fitur terbaru.

    sudo apt-get update
    sudo apt-get upgrade

**Meng-install hostapd dan dnsmasq**
Selanjutnya kita meng-*install* hostapd (sebuah access point daemon) dan dnsmasq dhcp service.

    sudo apt-get install hostapd dnsmasq

**Meng-edit configuration files**
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
    dhcp-range=192.168.4.1,192.168.4.50,24h

*Catatan: IP address range yang digunakan dapat sesuai dengan keinginan Anda.*

Membuat sebuah *file* /etc/hostapd/hostapd.conf dan menambahkan:
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

Meng-*edit* file /etc/default/hostapd dan tambahkan *script* berikut ini setelah #DAEMON_CONF:

    DAEMON_CONF="/etc/hostapd/hostapd.conf" 

**Membuat startup script**
Tambahkan sebuah *file* baru /usr/local/bin/wifistart (Anda boleh memilih nama apapun yang Anda suka), kemudian tambahkan:

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

**Meng-edit local system script**
Tambahkan *script* dibawah ini ke /etc/rc.local di atas *exit 0*
(Perhatikan: ada spasi antara “/bin/bash” dan "/usr/local/bin/wifistart")

**Menonaktifkan regular network services**
Menonaktifkan artinya memastikan bahwa tidak ada hal yang dijalankan ketika *system startup*.

    sudo systemctl stop hostapd
    sudo systemctl stop dnsmasq
    sudo systemctl stop dhcpcd
    sudo systemctl disable hostapd
    sudo systemctl disable dnsmasq
    sudo systemctl disable dhcpcd

**Reboot**
Untuk melakukan *reboot*, ikuti petunjuk di bawah ini.
(Tidak diwajibkan)

    sudo reboot

Untuk memberi izin untuk eksekusi sebagai *script*

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







