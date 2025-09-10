# Lab: SQL injection UNION attack, retrieving multiple values in a single column

## Deskripsi Soal

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.
The database contains a different table called ``users``, with columns called ``username`` and ``password.``
To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the ``administrator`` user.

## Resources
https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column
https://portswigger.net/web-security/sql-injection/cheat-sheet
https://portswigger.net/web-security/sql-injection/union-attacks

## Step by Step

1. Saya masuk ke website dan ikuti solusi dari portswigger tersebut.
<img width="925" height="572" alt="image" src="https://github.com/user-attachments/assets/8472261c-2ffc-41ef-810e-4b6705965345" />
Lalu, sperti biasa saya tinggal masukkan link URL yang sudah akses lab ke dalam burpsuite sehingga bisa saya langsung send ke Repeater

<img width="1375" height="938" alt="image" src="https://github.com/user-attachments/assets/3599630a-f68e-4214-964a-595f4286468b" />


3. Masuk ke bagian ``Gifs``
<img width="1295" height="863" alt="image" src="https://github.com/user-attachments/assets/b09c545f-cefa-42c1-b817-156c0ffe55f1" />

4. Setelah itu, saya masukkan query SQL ``'+UNION+SELECT+NULL,'abc'--`` (ini dari payload solusi di portswigger) untuk melakukan modify di parameter ``catagory``
<img width="1588" height="861" alt="image" src="https://github.com/user-attachments/assets/d3d76a53-067c-4559-ba23-f2f5e469fcb5" />

Hasilnya ``200 OK`` yang artinya sudah baik
<img width="1560" height="890" alt="image" src="https://github.com/user-attachments/assets/c08e0634-82a4-47ef-8452-257583f69a66" />

5. Dari sini untuk bisa retrive content ``users`` table, dengan sedikit modifikasi payload ``'+UNION+SELECT+NULL,username||'~'||password+FROM+users--``(sesuai solusi yang ada di portswigger)
<img width="1660" height="992" alt="image" src="https://github.com/user-attachments/assets/de2bd230-8b94-4cea-9605-829419752e94" />

Dan moment menegangkan:
<img width="622" height="750" alt="image" src="https://github.com/user-attachments/assets/1b837be7-7f38-4eb0-a5fe-da0b662eabbe" />

Horee: 
<img width="1351" height="827" alt="image" src="https://github.com/user-attachments/assets/3b0cfa47-9d44-455a-90e8-e79ea2d31090" />

## Alasan Keberhasilan:

1. Aplikasi rentan terhadap SQL Injection UNION.
2. Database backend (kemungkinan Oracle) mendukung operator konkatenasi ||.
3. Saya sudah mengetahui informasi penting sebelumnya (jumlah kolom dan nama tabel/kolom target).

 
