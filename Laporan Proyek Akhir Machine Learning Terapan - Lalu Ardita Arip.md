# Laporan Proyek Akhir Machine Learning Terapan - Lalu Ardita Arip
## Domain Proyek

Film merupakan salah satau sarana hiburan yang sangat banyak diminati dizaman sekarang, karena banyak memberikan gambaran atau tayangan yang imajinatif yang membuat penikmatnya menjadi sangat terhibur dan dapat menghabiskan waktunya untuk menikmati sebuah film. filem sendiri terdiri dari berbagai jenis seperti darama, komedi dll. dizaman sekarang semakin banyak perkemabngan yang terjadi pada film dari yang awalnya film hanya berwarna hitam dan putih sekarang memiliki warna sehingga lebih memanjakan mata saat meikmati sebuah film. Adapaun film dapat dinikmati diamna saja baik itu bioskop,TV, maupun hp, sehingga memudahkan untuk meikmati sebuah film. Penonton juga dapat memilih film apa yang akan ditonton atau melihat rekomendasi film yang akan ditonton berdasarkan rating, genre dari film.
Menonton sebuah film yang direkomendasikan berdasarkan hrating sebuah film dapat dilakukan karena adanyanya sistem rekomendasi yang akan membantu merekomendasikan film kepada penonton. Sistem rekomendasi akan merekomendasikan film berdasrkan rating dari film tersebut.

## Business Understanding
### Problem Statements
- Bagaimana cara merekomendasikan film berdasarkan rating dan film yang peranh ditonton oleh orang lain ?
### Goals
- Membuat sistem rekomendasi berdasarkan rating dari sebuah film dan film yang peranh ditonton.

### Solution Statements
Untuk merekomendaiskan film berdasarkan film yang pernah ditonton menggunakan algoritma :
- Content Based Filtering dimana algoritma ini akan merekomendasikan sesuatu dari tanggapan yang telah diberikan.

Dan untuk merekomendaiskan film berdasarkan rating tertinggi menggunkana algoritma :
- Collaborative Filtering merupakan algoritma yang akan merekomendasikan berdasarkan tanggapan komunitas(banyak orang) dan tidak memrlukan atribut untuk setiap itemnnya.

## Data Understanding
 Dataset yang digunakan merupakan dataset yang diambil dari platform kaggel yang dipublikasikan oleh Nezar Abdilah Prakasa. Dataset ini terdiri dari empat buah data yaitu data links.csv, movies.csv, ratings.csv dan tags.csv. Berikut akses link menuju dataset tersebut https://www.kaggle.com/code/nezarabdilahprakasa/big-data-analysis-using-pysprak-movie-recommed/data?select=tags.csv. 
 - links   : berisi daftar link film 
 - movies  : berisi daftar film yang ada
 - ratings : berisi daftar niali dari sebuah filem 
 - tags    : beris daftar id dari film 

Lalu dilakukan Exploratory Data Analysis(EDA).
|    nama variabel    | Jumlah |
|:-------------------:|--------|
|        links        |  9125  |
|        movies       |  9125  |
|  ratings dari user  |   671  |
| ratings dari movie  |  9066  |
|         tags        |   689  |
gambar jumlah data masing-masing variabel
Membaca data dan dari data yang dibaca diperoleh hasil bahwa jumlah data pada links sebanyak 9.125, pada movies sebanyak 9.125, pada rating berdasarkan user sebnyak 576, rating berdasarkan movie sebanyak 8.462 dan pada tags berjumlah 689

1. Nilai pada data links
    |  Column | Non-null  | count    | Dtype |
    |:-------:|----------|----------|-------|
    | movieId |   9125   | non-null | int64 |
    |  imdbId |   9125   | non-null | int64 |
    |  tmdbId |   9112   | non-null | int64 |
    Melihat informasi dari variabel links dan diperolah bahwa terdapat dua type data yaitu int64 yang berjumlah 1 yaitu movieId dana type data object yang berjumlah 2 yaitu title dan genre

2. Nilai pada data movis

    |  Column | Non-null | count    | Dtype  |
    |:-------:|----------|----------|--------|
    | movieId |   9125   | non-null | int64  |
    |  title  |   9125   | non-null | object |
    |  genres |   9125   | non-null | object |
    Melihat informasi dari variabel movies dan diperolah bahwa terdapat dua type data yaitu float64 yang berjumlah 1 yaitu tmdbId dana type data int64 ynag berjumlah 2 yaitu movieId dan imdbId

3. Nilai pada data ratings
    |   Column  | Non-null | count    | Dtype   |
    |:---------:|----------|----------|---------|
    |   userId  |  100004  | non-null |  int64  |
    |  movieId  |  100004  | non-null |  int64  |
    |   rating  |  100004  | non-null | float64 |
    | timestamp |  100004  | non-null |  int64  |
    melihat informasi dari variabel ratings dan diperolah bahwa terdapat dua type data yaitu float64 yang berjumlah 1 yaitu rating dana type data int64 ynag berjumlah 3 yaitu userId, movieId dan timestamp

3. Nilai pada data tags
    |   Column  | Non-null | count    | Dtype  |
    |:---------:|----------|----------|--------|
    |   userId  |   1296   | non-null |  int64 |
    |  movieId  |   1296   | non-null |  int64 |
    |    tag    |   1296   | non-null | object |
    | timestamp |   1296   | non-null |  int64 |
    melihat informasi dari variabel tags diperolah bahwa terdapat dua type data yaitu object yang berjumlah 1 yaitu tag dana type data int64 ynag berjumlah 3 yaitu movieId, userId dan timestamp

melihat sample dengan mengguankan .head() pada dataset yang akan di jadikan acuan
|     |     userId |       movieId |   rating |    timestamp |
|----:|-----------:|--------------:|---------:|-------------:|
|  0  |          1 |            31 |      2.5 |   1260759144 |
|  1  |          1 |          1029 |      3.0 |   1260759179 |
|  2  |          1 |          1061 |      3.0 |   1260759182 |
|  3  |          1 |          1129 |      2.0 |   1260759185 |
|  4  |          1 |          1172 |      4.0 |   1260759205 |

|       |        userId |       movieId |        rating |    timestamp |
|------:|--------------:|--------------:|--------------:|-------------:|
| count | 100004.000000 | 100004.000000 | 100004.000000 | 1.000040e+05 |
|  mean |    347.011310 |  12548.664363 |      3.543608 | 1.129639e+09 |
|  std  |    195.163838 |  26369.198969 |      1.058064 | 1.916858e+08 |
|  min  |      1.000000 |      1.000000 |      0.500000 | 7.896520e+08 |
|  25%  |    182.000000 |   1028.000000 |      3.000000 | 9.658478e+08 |
|  50%  |    367.000000 |   2406.500000 |      4.000000 | 1.110422e+09 |
|  75%  |    520.000000 |   5418.000000 |      4.000000 | 1.296192e+09 |
|  max  |    671.000000 | 163949.000000 |      5.000000 | 1.476641e+09 |
memerikas data pada rating dan di peroleh bahwa pada data rting terdapat empat kompenen yaitu userId, movieId, rating dan timestamp. Dan melihat hubungan yang ada pada dataset rating dan melihat nilai dari data ratings, dan pada data rating diperoleh nilai minimal sebesar 0.5 dan nilai maksimal sebesar 5.
Dan melakukan penggabungan pada seluruh variabel berdasarkan movieId kedalam variabel film dan user berdasarkan userId.


## Data Preparation
Tabel dataframe film  hasil gabungan info_film dan rating 
| userId_x | movieId | rating_x | timestamp_x |     imdbId |   tmdbId |  title |                 genres | userId_y | rating_y | timestamp_y |          tag |     |
|---------:|--------:|---------:|------------:|-----------:|---------:|-------:|-----------------------:|---------:|---------:|------------:|-------------:|-----|
|     0    |       1 |       31 |         2.5 | 1260759144 | 112792.0 | 9909.0 |                    NaN |      NaN |      NaN |         NaN |          NaN | NaN |
|     1    |       1 |       31 |         2.5 | 1260759144 |      NaN |    NaN | Dangerous Minds (1995) |    Drama |      NaN |         NaN |          NaN | NaN |
|     2    |       1 |       31 |         2.5 | 1260759144 |      NaN |    NaN |                    NaN |      NaN |      1.0 |         2.5 | 1.260759e+09 | NaN |
|     3    |       1 |       31 |         2.5 | 1260759144 |      NaN |    NaN |                    NaN |      NaN |      7.0 |         3.0 | 8.518688e+08 | NaN |
|     4    |       1 |       31 |         2.5 | 1260759144 |      NaN |    NaN |                    NaN |      NaN |     31.0 |         4.0 | 1.273542e+09 | NaN |
|    ...   |     ... |      ... |         ... |        ... |      ... |    ... |                    ... |      ... |      ... |         ... |          ... | ... |
|  6609806 |     671 |     6565 |         3.5 | 1074784724 |      NaN |    NaN |                    NaN |      NaN |    509.0 |         4.0 | 1.093278e+09 | NaN |
|  6609807 |     671 |     6565 |         3.5 | 1074784724 |      NaN |    NaN |                    NaN |      NaN |    529.0 |         2.5 | 1.062034e+09 | NaN |
|  6609808 |     671 |     6565 |         3.5 | 1074784724 |      NaN |    NaN |                    NaN |      NaN |    580.0 |         3.5 | 1.165901e+09 | NaN |
|  6609809 |     671 |     6565 |         3.5 | 1074784724 |      NaN |    NaN |                    NaN |      NaN |    654.0 |         4.5 | 1.145391e+09 | NaN |
|  6609810 |     671 |     6565 |         3.5 | 1074784724 |      NaN |    NaN |                    NaN |      NaN |    671.0 |         3.5 | 1.074785e+09 | NaN |
pada gambar diatas menggabungkan data file links, movies, ratings dan tags kedalam dataframe info_film, serta menggabungkan dataframe rating dan info_film berdasarkan movieId.

Tabel cek nilai null
| nama variabel |  jumlah |
|:-------------:|:-------:|
|    userId_x   |       0 |
|    movieId    |       0 |
|    rating_x   |       0 |
|  timestamp_x  |       0 |
|     imdbId    | 6509807 |
|     tmdbId    | 6509878 |
|     title     | 6509807 |
|     genres    | 6509807 |
|    userId_y   |  200008 |
|    rating_y   |  263133 |
|  timestamp_y  |  200008 |
|      tag      | 6546686 |
diperoleh hasil null pada imdbId, tmdbId, title, genres, userId_y, rating_y, timestamp_y, tag.

Tabel grub berdasarkan nilai uinq moveId
| movieId | userId_x | rating_x |    timestamp_x |     imdbId |   tmdbId |   userId_y | rating_y |  timestamp_y |
|--------:|---------:|---------:|---------------:|-----------:|---------:|-----------:|---------:|-------------:|
|    1    | 20906000 | 239125.0 | 68117429794500 | 28333123.0 | 212914.0 | 20778875.0 | 236255.5 | 6.761938e+13 |
|    2    |  3719407 |  39676.0 | 12471487698406 | 12144179.0 | 946308.0 |  3651161.0 |  38948.0 | 1.224265e+13 |
|    3    |  1347551 |  11376.5 |  3477508189719 |  6680452.0 | 920518.0 |  1303369.0 |  11003.5 | 3.363492e+12 |
|    4    |    69330 |    465.0 |   180917035830 |  1493505.0 | 407641.0 |    60086.0 |    403.0 | 1.567948e+11 |
|    5    |  1059876 |  10797.0 |  3293163175649 |  6330296.0 | 664272.0 |  1030120.0 |  10248.0 | 3.189580e+12 |
|   ...   |      ... |      ... |            ... |        ... |      ... |        ... |      ... |          ... |
|  161944 |      861 |     15.0 |     4410503472 |   255313.0 | 159550.0 |      287.0 |      5.0 | 1.470168e+09 |
|  162376 |      219 |     13.5 |     4422766596 |  4574334.0 | 410612.0 |       73.0 |      4.5 | 1.474256e+09 |
|  162542 |     1833 |     15.0 |     4414562001 |  5165344.0 | 392572.0 |      611.0 |      5.0 | 1.471521e+09 |
|  162672 |     1833 |      9.0 |     4414571958 |  3859980.0 | 402672.0 |      611.0 |      3.0 | 1.471524e+09 |
|  163949 |     2188 |     20.0 |     5905676956 |  2531318.0 | 391698.0 |     1094.0 |      5.0 | 2.952838e+09 |
dari hasil penggabungan data berdasarkan niali uniq yaitu movieId di peroleh jumlah sample sebanyak 9.066 data

Tabel penggabungan film_rate dengan variabel ratings
|        | userId | movieId | rating |  timestamp |                        title |                                    genres |        tag |
|-------:|-------:|--------:|-------:|-----------:|-----------------------------:|------------------------------------------:|-----------:|
|    0   |      1 |      31 |    2.5 | 1260759144 |       Dangerous Minds (1995) |                                     Drama |        NaN |
|    1   |      1 |    1029 |    3.0 | 1260759179 |                 Dumbo (1941) |       Animation\|Children\|Drama\|Musical |        NaN |
|    2   |      1 |    1061 |    3.0 | 1260759182 |              Sleepers (1996) |                                  Thriller |  emotional |
|    3   |      1 |    1061 |    3.0 | 1260759182 |              Sleepers (1996) |                                  Thriller |    revenge |
|    4   |      1 |    1061 |    3.0 | 1260759182 |              Sleepers (1996) |                                  Thriller | true story |
|   ...  |    ... |     ... |    ... |        ... |                          ... |                                       ... |        ... |
| 141018 |    671 |    6268 |    2.5 | 1065579370 | Raising Victor Vargas (2002) |                    Comedy\|Drama\|Romance |        NaN |
| 141019 |    671 |    6269 |    4.0 | 1065149201 |                Stevie (2002) |                               Documentary |        NaN |
| 141020 |    671 |    6365 |    4.0 | 1070940363 |  Matrix Reloaded, The (2003) | Action\|Adventure\|Sci-Fi\|Thriller\|IMAX |        NaN |
| 141021 |    671 |    6385 |    2.5 | 1070979663 |           Whale Rider (2002) |                                     Drama |        NaN |
| 141022 |    671 |    6565 |    3.5 | 1074784724 |            Seabiscuit (2003) |                                     Drama |        NaN |
dari hasil penggabungan dari niali uniq yaitu moveId diperoleh jumlah sample data sebanyak 141.023

Tabel cek nilai null
| Nama variabel | Jumlah |
|:-------------:|:------:|
|     userId    |    0   |
|    movieId    |    0   |
|     rating    |    0   |
|   timestamp   |    0   |
|     title     |    0   |
|     genres    |    0   |
|      tag      |  77898 |
diperoleh bahwa niali null terdapat pada variabel tag sebanyak 77890

Tabel melkukan drop pada variabel tag
|        | userId | movieId | rating |  timestamp |                                          title |                                   genres |        tag |
|-------:|-------:|--------:|-------:|-----------:|-----------------------------------------------:|-----------------------------------------:|-----------:|
|    2   |      1 |    1061 |    3.0 | 1260759182 |                                Sleepers (1996) |                                 Thriller |  emotional |
|    3   |      1 |    1061 |    3.0 | 1260759182 |                                Sleepers (1996) |                                 Thriller |    revenge |
|    4   |      1 |    1061 |    3.0 | 1260759182 |                                Sleepers (1996) |                                 Thriller | true story |
|    6   |      1 |    1172 |    4.0 | 1260759205 | Cinema Paradiso (Nuovo cinema Paradiso) (1989) |                                    Drama |   holes80s |
|   20   |      1 |    2968 |    1.0 | 1260759200 |                            Time Bandits (1981) |       Adventure\|Comedy\|Fantasy\|Sci-Fi |    Gilliam |
|   ...  |    ... |     ... |    ... |        ... |                                            ... |                                      ... |        ... |
| 141007 |    671 |    5445 |    4.5 | 1064891627 |                         Minority Report (2002) | Action\|Crime\|Mystery\|Sci-Fi\|Thriller | Tom Cruise |
| 141008 |    671 |    5464 |    3.0 | 1064891549 |                       Road to Perdition (2002) |                             Crime\|Drama |   holes00s |
| 141011 |    671 |    5902 |    3.5 | 1064245507 |                              Adaptation (2002) |                   Comedy\|Drama\|Romance |     boring |
| 141012 |    671 |    5952 |    5.0 | 1063502716 |  Lord of the Rings: The Two Towers, The (2002) |                       Adventure\|Fantasy |     boring |
| 141013 |    671 |    5952 |    5.0 | 1063502716 |  Lord of the Rings: The Two Towers, The (2002) |                       Adventure\|Fantasy |       long |
setelah melakukan drop pada niali null pada variabel tag jumlah data sample yang tersisa adalah 63.125

Tabel cek nilai null
| Nama variabel | Jumlah |
|:-------------:|:------:|
|     userId    |    0   |
|    movieId    |    0   |
|     rating    |    0   |
|   timestamp   |    0   |
|     title     |    0   |
|     genres    |    0   |
|      tag      |    0   |
setelah melakukan pengecekan tidak terdapat lagi nilai null/ missing value pada dataset.

Tabel hasil konversi data seris menjadi list
| nama variabel | jumlah |
|:-------------:|:------:|
|       ID      |   630  |
|     judul     |   630  |
|     genre     |   630  |
melakukan konversi data dari data seris menjadi list menggunakan fungsi tolist() dan diperoleh jumlah data id sebanyak 630, judul sebanyak 630, dan genre sebnyak 630.

Tabel hasil dictianory
|     |     id |                                             title |                                           genre |
|----:|-------:|--------------------------------------------------:|------------------------------------------------:|
|  0  |      1 |                                  Toy Story (1995) | Adventure\|Animation\|Children\|Comedy\|Fantasy |
|  1  |      5 |                Father of the Bride Part II (1995) |                                          Comedy |
|  2  |     47 |                       Seven (a.k.a. Se7en) (1995) |                               Mystery\|Thriller |
|  3  |     50 |                        Usual Suspects, The (1995) |                        Crime\|Mystery\|Thriller |
|  4  |    104 |                              Happy Gilmore (1996) |                                          Comedy |
| ... |    ... |                                               ... |                                             ... |
| 625 | 146501 |                             Land of Storms (2014) |                                           Drama |
| 626 | 146656 |                                      Creed (2015) |                                           Drama |
| 627 | 148626 |                             Big Short, The (2015) |                                           Drama |
| 628 | 156387 |                                Sing Street (2016) |                                           Drama |
| 629 | 163949 | The Beatles: Eight Days a Week - The Touring Y... |                                     Documentary |
membuat dictianory untuk menentukan pasangan key value pada id,title dan genre dari data yang telah disiapkan sebelumnya.
melakukan persiapan untuk melakukan encode pada fitur (user dan userId) dan pada fitur (movie dan movieId). Lalu membagi dataset menjadi dua yaitu data tarin dan validasi dengan komposisi 80:20

## Modeling
- Dalam tahap modeling berikut algoritma yang digunakan dalam pembuatan model machine learning
    - Content Based Filtering
    Content based filtering meruapakan sistem yang memberikan rekomendasi untuk menebak apa yang disukai pengguna berdasarkan aktivitas pengguna tersebut.
    - Collaborative Filtering
    collaborative filtering adalah suatu konsep dimana opini dari pengguna lain yang ada digunakan untuk memprediksi item yang mungkin disukai/diminati oleh seorang pengguna

- Tahapan dalam membuat model
    1. Yang pertama membuat subset produk ynag mungkin disukai atau yang pernah ditonton oleh pengguna.
    2. Melakukan pengurangan terhadap data yang tidak lengkap lalu melakukan pengurutan terhadap daftar rekomendasi ke item yang akan ditampilkan kepada pengguna.
- Hasil dari model
    1. 10 rekomendasi berdasarkan film ynag disukai atau pernah di tonton
        Top 10 rekomendsi filem.
        |   |                                   title |  genre |
        |--:|----------------------------------------:|-------:|
        | 0 |                      In the Loop (2009) | Comedy |
        | 1 |                    Scary Movie 2 (2001) | Comedy |
        | 2 |                      Bridesmaids (2011) | Comedy |
        | 3 |                  I Love You, Man (2009) | Comedy |
        | 4 | Dodgeball: A True Underdog Story (2004) | Comedy |
        | 5 |     Monty Python's Life of Brian (1979) | Comedy |
        | 6 |             Get Him to the Greek (2010) | Comedy |
        | 7 |                      Role Models (2008) | Comedy |
        | 8 |                  What About Bob? (1991) | Comedy |
        | 9 |                        Jerk, The (1979) | Comedy |
    2. 10 rekomendasi berdasarkan rating filem
        Top 10 rekomendasi filem
        ![rekomendasi berdasarkan rating](https://user-images.githubusercontent.com/86635607/191650217-cba7aa68-f51e-450b-a8b3-fb5e730148f3.png)
## Evaluation
1. Evaluasi content based filtering 
    pada algoritma ini untuk mengujinya menggunakan film Bring In Out(2000) seperti berikut: 
    |     |   id |              title |  genre |
    |----:|-----:|-------------------:|-------:|
    | 190 | 3882 | Bring It On (2000) | Comedy |
    sehingga hasil rekomendasi  dari film yang telah ditonton tersebut sebagai berikut :
    |   |                                   title |  genre |
    |--:|----------------------------------------:|-------:|
    | 0 |                      In the Loop (2009) | Comedy |
    | 1 |                    Scary Movie 2 (2001) | Comedy |
    | 2 |                      Bridesmaids (2011) | Comedy |
    | 3 |                  I Love You, Man (2009) | Comedy |
    | 4 | Dodgeball: A True Underdog Story (2004) | Comedy |
    | 5 |     Monty Python's Life of Brian (1979) | Comedy |
    | 6 |             Get Him to the Greek (2010) | Comedy |
    | 7 |                      Role Models (2008) | Comedy |
    | 8 |                  What About Bob? (1991) | Comedy |
    | 9 |                        Jerk, The (1979) | Comedy |
    pada film Bring In Out(2000) yang telah ditonton merupakan film dengan genre komedi sehingga dari 10 film yang direkomendasikan 10 film tersebut bergenre comedi sehingga dpat disimpulkan bahwa precission sistem yang kita miliki sebesar 100%.dan tahap evaluasi tekni yang digunakan adalah teknik precission dimana tekhnik ini memiliki rumus seperti berikut :
    ![sisitem pressision](https://user-images.githubusercontent.com/86635607/191713384-77e9f8d8-f7c9-430f-ae86-591b4591c336.png)
2. Evaluasi collaborativefiltering
    Pada tahap evaluasi, kita menggunakan  Mean Squared Error (MSE) untuk menghitung nilai rata-rata dari jumlah selisih dari rata-rata nilai sebenarnya dengan nilai hasil prediksi.
![rumus MSE](https://user-images.githubusercontent.com/86635607/190569248-4db33849-6e5f-4f48-9422-4be69ad4b636.png)
Keterangan:
n : jumlah dataset
Yi : nilai sebenarnya
Ŷi = nilai prediksi
Adapun hasil visualisasi yang diperoleh dari MSE dari algoritma model machine learning sebagai berikut.
![model matrik](https://user-images.githubusercontent.com/86635607/191650867-246f1a25-b012-4a28-ba25-2343bdd965c8.png)
pada proses ini di peroleh hasil nilai root_mean_squared_error: 0.2002 dan val_root_mean_squared_error: 0.2114 yang memiliki niali tidak jauh berbeda.
lalu untuk memperoleh rekomendasi dapat mengguankan fungsi model.predict() dari library keras yang akan memperoleh hasil sebagi berikut :
![rekomendasi berdasarkan rating](https://user-images.githubusercontent.com/86635607/191650217-cba7aa68-f51e-450b-a8b3-fb5e730148f3.png)
sehingga akan menampilkan 10 rekomendasi film berdasarkan rating dengan film "M (1931)" menjadi film dengan reting tertinggi.
## Kesimpulan

 Kita dapat membuat perogram yang dapat merekomendasikan film berdasarkan film yang pernah ditonton dan rating dari sebuah film, untuk dapat merekomendasikan film dari film yang telah di tonton dapat menggunakan algoritma Content Based Filtering dan untuk merekomendasikan filem berdasarkan rating dari filem dapat menggunakan algoritma Collaborative Filtering

## Referensi

https://doi.org/10.37595/mediainfo.v20i1.54
https://www.kaggle.com/code/nezarabdilahprakasa/big-data-analysis-using-pysprak-movie-recommed/data
https://neptune.ai/blog/recommender-systems-metrics
https://www.researchgate.net/publication/334320752_Penerapan_Metode_Content_Based_Filtering_Dalam_Implementasi_Sistem_Rekomendasi_Tanaman_Pangan




