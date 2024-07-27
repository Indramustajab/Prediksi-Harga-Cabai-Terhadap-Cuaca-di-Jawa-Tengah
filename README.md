># Prediksi Harga Cabai Terhadap Cuaca di Jawa Tengah
>>Analisis data (Pemodelan Prediktif Regresi Linear & Evaluation Mean Squared Error (MSE))

## Permasalahan utama dalam bisnis cabai di Jawa Tengah dan juga di daerah lain di Indonesia adalah fluktuasi harga yang tinggi. 

Fluktuasi harga ini bisa terjadi karena kondisi cuaca seperti cuaca ekstrem seperti banjir, kekeringan, dan badai dapat merusak tanaman cabai dan mengurangi hasil panen. Hal ini menyebabkan pasokan cabai menurun, yang pada gilirannya menyebabkan harga naik. Sebaliknya, kondisi cuaca yang baik dan panen melimpah dapat menyebabkan kelebihan pasokan dan penurunan harga.


## Data Collection and Understanding
Identifikasi data
- Data Harga Cabai dari Badan Pusat Statistik (BPS) dan Portal Harga Komoditas Pangan

- Data Cuaca dari BPS per Kota/Kabupaten di Jawa Tengah, mencakup data historis curah hujan, suhu, dan faktor cuaca lainnya

Pemahaman data
- Memeriksa apakah semua periode waktu tercakup/tidak ada data yang hilang
- Menangani missing values dengan imputasi data atau metode statistik lainnya

Analisis
- Memahami distribusi data dengan perhitungan statistik dasar seperti rata-rata, median, standar deviasi, dan varians.
- Standar deviasi harga cabai membantu memahami fluktuasi harga dalam periode tertentu.

Identifikasi Outlier
- Menemukan kejadian luar biasa yang mempengaruhi harga cabai, seperti bencana alam atau gangguan distribusi.
- Membantu memahami fenomena khusus.

Tren Musiman

- Memahami pola musiman harga cabai, seperti kenaikan harga menjelang musim panen atau penurunan harga setelah panen melimpah.
- Membantu meramalkan pergerakan harga dan membuat prediksi lebih akurat.

## Data Preparation
Cleaning Data 
- Menghapus Missing Values (Jika jumlah missing values kecil, baris atau kolom yang memiliki missing values dapat dihapus/jika banyak missing values, metode imputasi seperti mean/median atau mode imputation digunakan)
- Menghapus Duplikasi (Identifikasi duplikasi dengan mencari baris yang memiliki nilai yang sama di semua kolom atau kolom tertentu/menghapus baris duplikat untuk mencegah bias dalam analisis dan model)

## Hasil Data Latih dan Data Uji
```
Data Latih:
 Januari_curah_hujan  Februari_curah_hujan  Maret_curah_hujan  April_curah_hujan  Mei_curah_hujan  Juni_curah_hujan  Juli_curah_hujan  Agustus_curah_hujan  September_curah_hujan  Oktober_curah_hujan  November_curah_hujan  Desember_curah_hujan  Januari_harga  Februari_harga  Maret_harga  April_harga  Mei_harga  Juni_harga  Juli_harga  Agustus_harga  September_harga  Oktober_harga  November_harga  Desember_harga
               353.5                 274.7              611.0              252.3            222.3             222.3              29.8                 85.8                  134.7                303.5                 360.0                 287.0          45789           48026        51195        36928      28647       16095       19952          15525            14318          23850           32590           37478
               290.0                 255.0              357.0              402.0            258.0             236.0             319.0                356.0                  420.0                620.0                 530.0                 523.0          30833           31571        44545        26666      41666       67500       83333          53333            60789          45947           32045           36176
               109.0                 196.0              288.0              185.0            132.0             129.0              89.0                 12.0                   15.0                300.0                 241.0                 345.0          43122           47315        43326        31261      23095       17904       18204          12090            72000          72000           72000           28900
               270.0                 227.0              287.0              253.0            113.0              63.0               2.0                 20.0                   36.0                230.0                 379.0                 433.0          23190           26230        32500        24636      32200       62600       76875          58250            59050          40190           26714           30809
               371.0                 309.0              309.0              152.0            167.0              56.0             162.0                 40.0                  155.0                239.0                 182.0                 223.0          25000           32000        47142        38600      35625       66250       79454          60000            53777          50000           28142           33850

Data Uji:
 Januari_curah_hujan  Februari_curah_hujan  Maret_curah_hujan  April_curah_hujan  Mei_curah_hujan  Juni_curah_hujan  Juli_curah_hujan  Agustus_curah_hujan  September_curah_hujan  Oktober_curah_hujan  November_curah_hujan  Desember_curah_hujan  Januari_harga  Februari_harga  Maret_harga  April_harga  Mei_harga  Juni_harga  Juli_harga  Agustus_harga  September_harga  Oktober_harga  November_harga  Desember_harga
              311.00                185.00             321.00             238.00           153.00            120.00            151.00                17.00                  64.00               139.00                279.00                208.00          41190           46700        40500        33789      30072       30417       32295          36650            60125          46476           32772           36045
              384.00                189.74             306.21             238.16           113.53            220.79             28.79                90.68                  92.79               290.11                259.37                256.68          22412           26268        37849        28363      36033       66878       75571          54318            55242          35190           23068           27293
              471.93                511.53             263.53             184.14           310.00            189.53            130.13                96.87                 104.17               412.87                188.67                439.87          40873           40350        36174        32157      39715       25838       27075          32181            57411          41364           27452           29750
              268.00                337.00             348.00             193.00           226.00            194.00             40.00                54.00                 100.00               223.00                295.00                136.00          45283           48745        46485        34642      26071       17444       18651          13810            51781          42500           31000           34100
              157.00                195.00             176.00             221.00           105.00            103.00             34.00                29.00                  29.00               399.00                350.00                286.00          19000           28700        35527        31261      29000       84678       77269          64277            64083          48411           30605           23800
```

## Hasil MSE Evaluation
5 Data bulan
```
Prediksi untuk Januari_harga:
[[28026.16840285]
 [27515.03258711]
 [26899.35899425]
 [28327.2484039 ]
 [29104.45491825]]
Mean Squared Error: 114232698.12305021

Prediksi untuk Februari_harga:
[[33572.54176046]
 [33599.06346899]
 [35399.57414181]
 [34423.02692864]
 [33628.49473205]]
Mean Squared Error: 72012371.82454905

Prediksi untuk Maret_harga:
[[41350.88356968]
 [41180.26288878]
 [40687.89705641]
 [41662.36148614]
 [39678.13179614]]
Mean Squared Error: 11286444.503058085

Prediksi untuk April_harga:
[[30553.85173005]
 [30555.00451356]
 [30165.79598175]
 [30229.63136849]
 [30431.36848235]]
Mean Squared Error: 7311178.027302129

Prediksi untuk Mei_harga:
[[34206.70371097]
 [34369.70038642]
 [33558.35108755]
 [33905.24038925]
 [34404.92616908]]
Mean Squared Error: 28237494.888882816

```

## Plot Regresi Linear

<table>
  <tr>
    <td><img src="https://github.com/Indramustajab/Prediksi-Harga-Cabai-Terhadap-Cuaca-di-Jawa-Tengah/blob/main/Grafik%20Plot/download%20(1).png" width="1500" height="600" /></td>

  </tr>
</table>
Penyebaran Data:
- Dengan membandingkan titik-titik biru (actual) dan titik-titik merah (predicted), kita bisa melihat seberapa baik model regresi linier memprediksi harga cabe berdasarkan curah hujan.
- Jika titik-titik merah mendekati titik-titik biru, berarti model memiliki performa yang baik dalam memprediksi harga cabe.
Kesalahan Prediksi:

- Jarak antara titik biru dan merah menunjukkan seberapa besar kesalahan prediksi (prediction error). Semakin dekat titik merah dengan titik biru, semakin kecil kesalahan prediksi untuk bulan tersebut.
  
Kecenderungan:
- Plot ini juga dapat menunjukkan kecenderungan atau pola antara curah hujan dan harga cabe. Misalnya, apakah harga cabe cenderung naik atau turun dengan bertambahnya curah hujan.

Variasi Data:

- Plot juga membantu kita memahami variasi dalam data curah hujan dan harga cabe untuk setiap bulan. Misalnya, kita bisa melihat apakah ada bulan dengan variasi curah hujan atau harga cabe yang lebih besar dibandingkan bulan lainnya.
<br></br>

