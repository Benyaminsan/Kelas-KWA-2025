<img width="1607" height="943" alt="image" src="https://github.com/user-attachments/assets/94342a14-627f-47e3-9985-c9223fb9ab0d" /># Lab: SQL injection UNION attack, finding a column containing text

## Deskripsi Soal
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a previous lab. The next step is to identify a column that is compatible with string data.
The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

(Intinya cari kolom yang kompatibel dengan data string format)

## Resources
https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text
https://portswigger.net/web-security/sql-injection/union-attacks

## Step by Step

1. Langsung masuk akses lab dan intercept turn on di burpsuite:
<img width="937" height="486" alt="image" src="https://github.com/user-attachments/assets/1bfc518f-7c6c-485f-8427-d7a731c52e62" />

<img width="1087" height="887" alt="image" src="https://github.com/user-attachments/assets/4e3698a7-4bfe-4a15-b332-b0a89c03d497" />

2. Disini saya langsung menuju ke fitur Pets:
<img width="1176" height="863" alt="image" src="https://github.com/user-attachments/assets/92420202-c3a6-4a94-b78a-c49c4a5b0877" />
Karena memang tujuan saya ingin mencari string data format dulu

3. Kemudian saya Modify parameter ``catagory`` dengan ``'+UNION+SELECT+NULL,NULL,NULL--``
   <img width="1607" height="943" alt="image" src="https://github.com/user-attachments/assets/d569ae1e-54da-41f9-b23c-f2000935373a" />
   Disini responnya bagus ``200 OK``

4. Lalu saya ubah lagi payloadnya menjadi ``'+UNION+SELECT+'abcdef',NULL,NULL--`` sehingga saya mencoba untuk mengisi karakter random di setiap ``NULL``(dari solusi di portswigger)
   <img width="1301" height="902" alt="image" src="https://github.com/user-attachments/assets/855a039d-3d8d-4c01-9f7b-7a0493699724" />
Dan Ternyata ada kolom yang tidak kompatibel dengan format data string

5. Dengan begitu saya bisa modify lagi payload menjadi ``'+UNION+SELECT+NULL,'vVALGC',+NULL+--`` Karena saya melihat ada ``hint`` tertentu pada laman yang menandakan string data format.
<img width="1462" height="905" alt="image" src="https://github.com/user-attachments/assets/1de184ed-02e2-4cec-9011-9018b33825e9" />

Saya eksekusi:
<img width="1697" height="1023" alt="image" src="https://github.com/user-attachments/assets/588b6043-7dff-4e6d-895f-ac2e8527c012" />
Voilaa! 

Akhirnya format data string bisa ditemukan di kolom KEDUA.

## Alasan Keberhasilan:
Pendekatan pengujian yang sistematis (cobain satu per satu) memungkinkan saya untuk mengisolasi dan lebih mengkerucutkan dengan tepat kolom mana yang kompatibel. Database akan menghasilkan error atau gagal menampilkan data jika tipe data yang disuntikkan (string) tidak cocok dengan tipe data kolom asli (INT, FLOAT, dll.)
 
