# Lab: Unprotected admin functionality

## Deskripsi Soal
This lab has an unprotected admin panel.

Solve the lab by deleting the user  ``carlos``.

## Resources 
https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality

## Step by Step

1. Masuk Akses labnya
<img width="1088" height="841" alt="image" src="https://github.com/user-attachments/assets/12c519e5-4d04-4ca2-af61-06ddc5ec51fb" />

2. Kita coba cari dengan menambahkan URL ``/robots.txt``
<img width="1075" height="345" alt="image" src="https://github.com/user-attachments/assets/8a4fc3e2-29a6-4de8-808a-c5f6c83901a1" />

3. Mencoba dengan ``/adminitrator-panel`` karena ada tulisan dissallow, yang mana aksesnya tentu dibatasi.
<img width="1662" height="747" alt="image" src="https://github.com/user-attachments/assets/0be87071-60e5-4991-8e32-c6cce4b8cccb" />

4. Akhirnya, kita harus delete user ``carlos``
   <img width="1600" height="813" alt="image" src="https://github.com/user-attachments/assets/b2b14be4-95d3-448d-95a1-adc20b3d65ee" />

Akhirnya berhasil untuk solve Broken Acces Control.
