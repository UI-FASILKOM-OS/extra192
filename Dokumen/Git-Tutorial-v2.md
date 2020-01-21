# Git Tutorial

## How to Set Up Git (Windows Only, untuk OS lainnya, bisa dilihat di https://www.atlassian.com/git/tutorials/install-git)

Langkah-langkah yang perlu dilakukan ialah:

  1.Pastikan Git telah terinstal pada komputer Anda. Anda dapat melihat apakah Git telah terinstal atau belum dengan mengetik *command* git --version pada Command Prompt.
  ```
  $ git --version
  ```
  
  2. Jika telah terinstal, langkah berikutnya adalah menuliskan *command* dibawah ini pada Command Prompt(atau Git Bash jika Anda memilih untuk tidak menggunakan Git pada Command Prompt). Hal ini bertujuan agar sistem mengetahui bahwa akun Anda-lah yang melakukan perubahan pada Git.
  ```
  $ git config --global user.name "nama_user"
  $ git config --global user.email "alamat_email"
  ```
  

## Basic Function 

 1. Git Init
 
Digunakan untuk membuat *repository* baru yang kosong. Untuk memahami mengenai bagaimana penggunaan Git Init, bisa dilihat [disini](https://git-scm.com/docs/git-init).

Contoh pemanfaatan dalam pembuatan *repository* baru dalam suatu direktori:
```
$ cd /path/to/my/codebase
$ git init
```

 2. Git Clone
 
Digunakan untuk melakukan kloning terhadap *repository* yang telah sebelumnya dibuat di Git pada komputer lokal, dengan tujuan agar kita bisa melakukan perubahan dalam git tersebut. Untuk dokumentasi Git Clone dapat dilihat [disini](https://git-scm.com/docs/git-clone).

Contoh pemanfaatan Git Clone dalam melakukan duplikasi:
```
$ git clone 'masukkan link dari git tersebut'
```

 3. Git Add
 
Digunakan untuk memasukkan file baru ke dalam repository, atau memasukkan file lama yang telah diberi perubahan. Dokumentasi mengenai Git Add dapat dilihat [disini](https://git-scm.com/docs/git-add).

Contoh pemanfaatan dari Git Add:
```
$ git add 'nama file'
```

 4. Git Commit
 
Bertujuan untuk memberi komentar pada perubahan yang dilakukan kepada file. Jika hal ini tidak dilakukan, file yang di-add sebelumnya tidak bisa dikirim ke git. Dokumentasi mengenai Git Commit dapat dilihat [disini](https://git-scm.com/docs/git-commit).

Contoh penggunaan Git Commit setelah melakukan Git Add:
```
$ git commit -m "Komentar"
```
5. Git Push

Bertujuan untuk mengirim file ke Git. Untuk dokumentasi Git Push bisa dilihat [disini](https://git-scm.com/docs/git-push).

6. Git Pull

Bertujuan untuk melakukan pengambilan data pada saat perintah dilakukan ke folder lokal. Jika ada *update* terbaru yang dilakukan, tidak bisa melakukan git push sebelum melakukan git pull. Untuk dokumentasi git pull dapat dilihat [disini](https://git-scm.com/docs/git-pull).

7. Membuat Version

Dalam Git, sangat penting dalam memberi version, dengan tujuan agar pengguna dapat melihat apa saja perubahan yang dilakukan pada suatu proyek. Untuk mengetahui cara membuatnya, dapat dilihat [disini](https://help.github.com/en/github/administering-a-repository/creating-releases).

## Tips and Tricks
1. Pahami kodenya secara menyeluruh, jangan setengah-setengah.

2. Jika Anda telah memahami perintah yang digunakan, namun lupa akan syntax, bisa dilihat pada folder pdf yang ditautkan pada bagian *cheatsheet*.

## Learning Git(Complete Version)
1. Youtube git tutorial dari [Udacity](https://www.youtube.com/playlist?list=PLAwxTw4SYaPk8_-6IGxJtD3i2QAu5_s_p)

2. Tutorial Git [petanikode](https://www.petanikode.com/tutorial/git/)

Untuk *cheatsheet*, [bisa dilihat pada tautan berikut ini.](https://education.github.com/git-cheat-sheet-education.pdf)
