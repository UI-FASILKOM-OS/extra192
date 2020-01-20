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
TO DO LIST

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

    #Set the channel (frequency) of the host access point
    channel=1
    
    #Set the SSID broadcast by your access point (replace with your own, of course)
    ssid=yourSSIDhere
    
    #This sets the passphrase for your access point (again, use your own)'
    wpa_passphrase=passwordBetween8and64charactersLong
    
    #This is the name of the WiFi interface we configured above
    interface=uap0
    
    #Use the 2.4GHz band (I think you can use in ag mode to get the 5GHz band as well, but I have not tested this yet)
    hw_mode=g
    
    #Accept all MAC addresses
    macaddr_acl=0
    
    #Use WPA authentication
    auth_algs=1
    
    #Require clients to know the network name
    ignore_broadcast_ssid=0
    
    #Use WPA2
    wpa=2
    
    #Use a pre-shared key
    wpa_key_mgmt=WPA-PSK
    wpa_pairwise=TKIP
    rsn_pairwise=CCMP
    driver=nl80211
    
    #I commented out the lines below in my implementation, but I kept them here for reference.
    
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

    #Make sure no uap0 interface exists (this generates an error; we could probably use an if statement to check if it exists first)
    echo "Removing uap0 interface..."
    iw dev uap0 del

    #Add uap0 interface (this is dependent on the wireless interface being called wlan0, which it may not be in Stretch)
    echo "Adding uap0 interface..."
    iw dev wlan0 interface add uap0 type __ap

    #Modify iptables (these can probably be saved using iptables-persistent if desired)
    echo "IPV4 forwarding: setting..."
    sysctl net.ipv4.ip_forward=1
    echo "Editing IP tables..."
    iptables -t nat -A POSTROUTING -s 192.168.70.0/24 ! -d 192.168.70.0/24 -j MASQUERADE

    #Bring up uap0 interface. Commented out line may be a possible alternative to using dhcpcd.conf to set up the IP address.
    #ifconfig uap0 192.168.70.1 netmask 255.255.255.0 broadcast 192.168.70.255
    ifconfig uap0 up

    #Start hostapd. 10-second sleep avoids some race condition, apparently. It may not need to be that long. (?) 
    echo "Starting hostapd service..."
    systemctl unmask hostapd.service
    systemctl start hostapd.service
    sleep 10

    #Start dhcpcd. Again, a 5-second sleep
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
https://wpitchoune.net/tricks/raspberry_pi3_increase_swap_size.html
https://lb.raspberrypi.org/forums/viewtopic.php?t=211542









