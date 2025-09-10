## Lab: SQL injection UNION attack, determining the number of columns returned by the query

# Deskripsi soal in english
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

# Resource Latihan
https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns
https://www.hackthebox.com/files/cheatsheet-sql-injection-fundamentals.pdf --dari HTB
https://portswigger.net/web-security/sql-injection/cheat-sheet --langsung dari laman poertswigger langsung jadi bagus untuk latihan di labs portswigger punya

## Step by step

1. Pertama kita pilih solusi dari portswigger untuk menggunakan burpsuite
<img width="900" height="425" alt="image" src="https://github.com/user-attachments/assets/7add53c2-e30f-48d6-a4e8-8eb21bb0289f" />

2. Akses Lab dan jangan lupa intercept webistenya
<img width="1427" height="912" alt="image" src="https://github.com/user-attachments/assets/3df8f078-3ab3-4476-bfc1-e93734b32658" />

3. Setelah saya intercept dan masuk ke target dari fitur website yaitu ``Gift``
<img width="1707" height="902" alt="image" src="https://github.com/user-attachments/assets/4645a8fc-576f-497e-a1ff-4221b4d75704" />

4. Send ke repeater
<img width="1656" height="898" alt="image" src="https://github.com/user-attachments/assets/57e14080-61e3-4fde-b2b1-a38c6511d340" />

5. Lalu tinggal modify ``catagory``
<img width="1713" height="912" alt="image" src="https://github.com/user-attachments/assets/4dee8ff9-0db0-47e2-a449-77a81fd9afb0" />
Disamping parameter ``catagory`` yaitu  ``'+UNION+SELECT+NULL,NULL--``

Dan hasilnya masih error juga, dan darisini saya mencari tahu penyebabnya ternyata memang adanya ketidakompatibel query yang saya modify dengan backend, jadi say mencoba lagi payload

6. yang awalnya  ``'+UNION+SELECT+NULL,NULL--`` menjadi ``'+UNION+SELECT+NULL,+NULL,+NULL+--``
<img width="1647" height="783" alt="image" src="https://github.com/user-attachments/assets/749f997c-ed53-4cb1-9e43-eb63a9f92d65" />
Yeay akhirnya berhasil

## Tambahan 
Dari Kesimpulan mengerjakan tadi saya tahu bahwa Proses ini secara efektif membuktikan bahwa query pada halaman filter kategori mengambil tepat 3 kolom data.


