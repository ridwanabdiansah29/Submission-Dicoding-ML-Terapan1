# Submission-Dicoding-ML-Terapan1

# Laporan Proyek Machine Learning - Ridwan Abdiansah

## Domain Proyek
Anggur merupakan bahan baku dalam pembuatan wine. Buah anggur menyimpan sebagian besar padatan dalam bentuk gula. Di samping itu, buah anggur juga mengandung
beberapa komponen lain seperti asam, vitamin, mineral, makromolekul (karbohidrat, protein, asam nukleat, dan lemak), serta komponen lain yang berkaitan dengan kualitas
wine, seperti fenol, acetal, lactones, terpenes, komponen mengandung nitrogen, komponen mengandung sulfur, dan beberapa senyawa lainnya [1]
Wine merupakan minuman hasil fermentasi yang cukup populer dan banyak diminati oleh konsumen. Berdasarkan International Organisation of Vine and Wine (OIV), pada tahun 2019, konsumsi wine dunia mencapai 244 mhl [2]. Hasil tersebut dikarenakan semakin tinggi minat dan kualitas dalam pembuatan wine. Di tahun yang sama, terjadi
peningkatan pasar ekspor global sebanyak 1,7% dan 0,9% untuk volume dan nilai ekspor wine [2]. Persaingan pasar yang ketat membuat penelitian terhadap parameter
kualitas wine semakin gencar dilakukan agar dapat menarik minat konsumen. Salah satu atribut wine yang banyak diteliti karena berkontribusi terhadap penerimaan konsumen adalah aroma [3]. Maka dari latar belakang diatas dapat di pastikan kualitas wine dapat dideteksi dengan senyawa yang ada didalamnya.

## Business Understanding

## Problem Statements
Perusahaan pembuat wine membutuhkan model terbaik untuk melakukan prediksi untuk kualitas wine yang berguna menjadi pedoman dalam meningkatkan kualitas barang yang berdampak pada peningkatan pendapatan.

## Goals
Membangun model terbaik untuk melakukan prediksi kualitas wine yang berguna menjadi pedoman dalam meningkatkan kualitas barang yang berdampak pada peningkatan pendapatan.

## Solution statements
Menawarkan solusi sistem prediksi dengan metode regresi. Untuk mendapatkan solusi terbaik, akan digunakan tiga model yang berbeda (KNN, RandomForest, Boosting) dengan hyperparameter tuning GridSearchCV. Selain itu, untuk mengukur kinerja model digunakan metrik Mean Squared Error (MSE) dimana model terbaik nantinya harus memperoleh nilai MSE terkecil dari dataset uji.

## Data Understanding
Berdasarkan sumber dataset: UCI Machine Learning Repository - Wine Quality Dataset diperoleh informasi:
Abstrak: Dua set data disertakan, terkait dengan sampel anggur vinho verde merah dan putih, dari utara Portugal. Tujuannya adalah untuk memodelkan kualitas anggur berdasarkan tes fisikokimia. 
Informasi Dataset
* Data Set Characteristics: Multivariate
* Attribute Characteristics: Real
* Associated Tasks: Classification, Regression
* Number of Instances: 4898
* Number of Attributes: 12
* Missing Values? N/A
* Area: Business

## Variabel-variabel pada WIne Quality Data Set :
Input variables (based on physicochemical tests):
1 - fixed acidity
2 - volatile acidity
3 - citric acid
4 - residual sugar
5 - chlorides
6 - free sulfur dioxide
7 - total sulfur dioxide
8 - density
9 - pH
10 - sulphates
11 - alcohol
Output variable (based on sensory data):
12 - quality (score between 0 and 10)

### Menangani Missing Value

Untuk mendeteksi missing value digunakan fungsi isnull().sum() dan diperoleh:
Tabel 1. Hasil Deteksi Missing Value

Fitur | Jumlah Missing Value
----- | ---------------------
fixed acidity | 0
volatile acidity | 0
citric acid | 0
residual sugar | 0
chlorides | 0
free sulfur dioxide | 0
total sulfur dioxide | 0
density | 0
pH | 0
sulphates | 0
alcohol | 0
quality | 0

Dari Tabel 2. terlihat bahwa setiap fitur tidak memiliki Missing Value (NULL maupun NAN) sehingga dapat dilanjutkan ke tahapan selanjutnya yaitu menangani outliers.

### Menangani Outliers

Pada kasus ini, untuk mendeteksi outliers digunakan teknis visualisasi data (boxplot). Kemudian untuk menangani outliers digunakan metode IQR.

Seltman dalam “Experimental Design and Analysis” [2] menyatakan bahwa outliers yang diidentifikasi oleh boxplot (disebut juga “boxplot outliers”) didefinisikan sebagai data yang nilainya 1.5 IQR di atas Q3 atau 1.5 IQR di bawah Q1.

Berikut persamaannya:

  Batas bawah = Q1 - 1.5 * IQR
  Batas atas = Q3 + 1.5 * IQR
  
Tabel 2. Visualisasi Boxplot Sebelum dan Sesudah Dikenakan Metode IQR.

Cek Outlier Pada Fitur | Setelah Digunakan Metode IQR
---------------------- | ----------------------------
![fixed before](https://user-images.githubusercontent.com/110794445/200461264-a4baa482-5420-4993-aab0-b8d6525a4cf3.png) | ![fixed after](https://user-images.githubusercontent.com/110794445/200462405-b7fc709d-b07d-4097-97c5-724df24dbd3e.png)
![volatile before](https://user-images.githubusercontent.com/110794445/200461352-b5b546a8-0cf2-4a54-9bac-f4977863ce91.png) | ![volatile after](https://user-images.githubusercontent.com/110794445/200462497-51cedf88-8ae2-413b-b7d1-0520ca5d8e42.png)
![citric before](https://user-images.githubusercontent.com/110794445/200461446-76d63d32-f6a2-486f-aed4-17e5816cbce9.png) | ![citric after](https://user-images.githubusercontent.com/110794445/200462592-d7a5bbf7-7639-413e-bfa6-ef457360fc5b.png)
![residual before](https://user-images.githubusercontent.com/110794445/200461475-bd2c378f-296d-49c8-8474-d587e5febe2d.png) | ![residual after](https://user-images.githubusercontent.com/110794445/200462664-3807709a-c796-43f8-b297-04198e4da78e.png)
![chlorides before](https://user-images.githubusercontent.com/110794445/200461539-6c7635ed-9d44-4be9-9f7f-8932d8cddf1c.png) | ![chlorides after](https://user-images.githubusercontent.com/110794445/200462716-5e530b5a-df8c-4413-a4f5-f3b86b68fcab.png)
![free before](https://user-images.githubusercontent.com/110794445/200461564-4a856861-23c9-42f8-a069-b104db7fcc33.png) | ![free after](https://user-images.githubusercontent.com/110794445/200462789-bd2b7625-acf7-4fcd-a414-b95365fd554a.png)
![total before](https://user-images.githubusercontent.com/110794445/200461584-12226d93-76bd-4f0c-a1b6-b82fa8b3f1ae.png) | ![total after](https://user-images.githubusercontent.com/110794445/200462843-36bbf389-4602-4320-87ef-b8987c71221e.png)
![density before](https://user-images.githubusercontent.com/110794445/200461659-68a6181b-7866-466c-9302-ff142eed8ba8.png) | ![density after](https://user-images.githubusercontent.com/110794445/200462895-cbf1391e-fb35-4dac-a3de-4592ea87946d.png)
![pH before](https://user-images.githubusercontent.com/110794445/200461691-f40ddf8c-e072-4964-a12b-86cc4dec4941.png) | ![pH after](https://user-images.githubusercontent.com/110794445/200462938-5b23dba4-ba60-45ab-8b0a-55bd4aaa36f8.png)
![sulphates before](https://user-images.githubusercontent.com/110794445/200461726-337afe62-2581-4f12-823c-8201f75b7ba9.png) | ![sulphates after](https://user-images.githubusercontent.com/110794445/200462983-aab6ec95-2b01-45d5-93f2-c483c35d2ef4.png)
![alcohol before](https://user-images.githubusercontent.com/110794445/200461738-823e6366-941a-4e65-9133-9074ee28b24d.png) | ![alcohol after](https://user-images.githubusercontent.com/110794445/200463037-ae00dcf6-c8f1-4d7d-af04-dcf83d534b42.png)

Dari hasil deteksi ulang outlier dengan boxplot di Tabel 2 di atas, didapat bahwa outlier sudah berkurang pada tiap fitur setelah dibersihkan. Terdapat hanya fitur citric acid yang sudah bersih dari outlier dan hasil dari jumlah data setelah dilakukan pembersihan dari outlier di tabel 3.

Tabel 3. Perbandingan Jumlah Data Sebelum dan Setelah Dibersihkan dari Outlier
Jumlah Data Sebelum Dibersihkan | Jumlah Data Setelah Dibersihkan
------------------------------- | -------------------------------
  1143 |  834
  
 ## Univariate Analysis
 
Selanjutnya, akan dilakukan proses analisis data dengan teknik Univariate EDA. Pada kasus ini semua fiturnya adalah fitur numerik dan tidak ada fitur kategorikal. Sehingga hanya perlu dilakukan analisa terhadap fitur numerik, sebagai berikut:

### Analisa Fitur Numerik

Untuk melihat distribusi data pada tiap fitur akan digunakan visualisasi dengan histogram sebagai berikut:

![histogram](https://user-images.githubusercontent.com/110794445/200467721-f89dcd3e-1f05-48cb-b7b7-821753c86ce4.png)

Dari hasil visualisasi histogram di atas, kita bisa memperoleh beberapa informasi, antara lain:

Distribusi fitur quality (target) cenderung miring ke kanan (right-skewed).

Karena beberapa fitur belum terdistribusi normal hal ini akan berimplikasi pada model, maka selanjutnya kita lakukan transformasi data (non-linear scaling). Namun, sebelum itu kita cek terlebih dahulu hubungan antara fitur numerik tersebut.

## Multivariate Analysis

### Hubungan Antara Fitur Numerik

Untuk mengamati hubungan antara fitur numerik, akan digunakan fungsi pairplot(), dengan output sebagai berikut:

![grafik_pairplot](https://user-images.githubusercontent.com/110794445/200468082-77f8b841-ea58-4bff-934c-d09115b325ff.png)

Gambar 2. Visualisasi Hubungan antara Fitur Numerik dengan pairplot()

Pada pola sebaran data grafik pairplot di atas, terlihat fitur fixed acidity dan citric acid memiliki korelasi kuat (negatif / berkebalikan) dengan fitur quality (target). Sedangkan fitur lainnya yaitu tidak memiliki korelasi positif yang lemah dengan fitur quality.

### Korelasi antara Fitur Numerik

Untuk mengevaluasi skor korelasi hubungan antara fitur numerik, akan digunakan fungsi corr() dengan output sebagai berikut.

![matriks](https://user-images.githubusercontent.com/110794445/200468429-38cb88f4-3106-4003-b152-6285dd99b693.png)

Gambar 3. Korelasi antara Fitur Numerik

Koefisien korelasi berkisar antara -1 dan +1. Semakin dekat nilainya ke 1 atau -1, maka korelasinya semakin kuat. Sedangkan, semakin dekat nilainya ke 0 maka korelasinya semakin lemah.

Dari grafik korelasi di atas, fitur fixed acidity, volatile acidity, citric acid dan pH memiliki korelasi yang kuat (mendekati -1, dibawah -0.85) dengan fitur target auqlity. Sementara itu, fitur residual sugar, chlorides dan sulphates mempunyai korelasi yang rendah dengan fitur target quality.

# Data Preparation
## Train Test Split

Dataset akan dibagi menjadi data latih (train) dan data uji (test). Tujuan langkah ini sebelum proses lainnya adalah agar tidak mengotori data uji dengan informasi yang didapat dari data latih. Contoh pada proses standarisasi dimana jika belum di bagi menjadi data latih dan uji, maka keduanya akan terkena transformasi data yang menggunakan informasi (mean dan standard deviation) dari gabungan data latih dan uji. Hal ini berpotensi menimbulkan kebocoran data (data leakage). Oleh karena itu langkah awal sebelum melakukan tranformasi data adalah membagi dataset terlebih dahulu [3].

Pada kasus ini akan menggunakan proporsi pembagian sebesar 90:10 dengan fungsi train_test_split dari sklearn dengan output sebagai berikut.

Tabel 4. Jumlah Data Latih dan Uji

Jumlah Total Data | Jumlah Data Latih | Jumlah Data Uji
----------------- | ----------------- | ---------------
  834 | 750 | 84

## Standarisasi
Proses standarisasi bertujuan untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Pada kasus ini akan digunakan metode StandarScaler() dari library Scikitlearn.

StandardScaler melakukan proses standarisasi fitur dengan mengurangkan mean kemudian membaginya dengan standar deviasi untuk menggeser distribusi. StandarScaler menghasilkan distribusi deviasi sama dengan 1 dan mean sama dengan 0.

Berikut output yang dihasilkan dari metode StandardScaler dengan menggunakan fungsi describe():

Tabel 5. Hasil Proses Standarisasi Pada Setiap Fitur Pada Data Latih

	| free sulfur dioxide |	total sulfur dioxide | density | alcohol | CFVP
- | ------------------- | -------------------- | ------- | ------- | ----
446 | -0.900488 | -0.413917 | 0.686706 | -1.087267 | 0.474663
685 | 2.330928 | 1.189503 | 0.308333 | -0.984725 | -0.605762
616 | 0.138181 | 1.737012 | 0.611032 | -0.677098 | -0.627900
408 | 0.484405 | 0.016269 | -1.205162 | 1.373748 | -1.332822
121	-1.015896	-0.922318	0.434457	-1.189810	-0.031785

## Reduksi Dimensi dengan PCA
PCA umumnya digunakan ketika variabel dalam data yang memiliki korelasi yang tinggi. Korelasi tinggi ini menunjukkan data yang berulang atau redundant. Sebelumnya sudah dilakukan proses untuk melihat hubungan dan korelasi dengan pairplot(), namun setelah melewati proses transformasi data (standarisasi dan non-linear scaling) dimungkinkan terjadi perubahan korelasi antar fiturnya (meskipun relatif kecil). Untuk itu perlu dicek kembali korelasi antar fitur dengan menggunakan pairplot() dengan output sebagai berikut.

![PCA](https://user-images.githubusercontent.com/110794445/200470283-2422de28-eb69-4c49-96cb-ededaca923f3.png)

Gambar 8. Visualisasi Hubungan antara Fitur Numerik dengan pairplot() pada Data Latih

# Modeling
Pada tahap ini, akan menggunakan tiga algoritma untuk regresi. Kemudian, akan dilakukan evaluasi performa masing-masing algoritma dan menetukan algoritma mana yang memberikan hasil prediksi terbaik. Ketiga algoritma yang akan digunakan, antara lain:

1. K-Nearest Neighbor
Kelebihan algoritma KNN adalah mudah dipahami dan digunakan sedangkan kekurangannya jika dihadapkan pada jumlah fitur atau dimensi yang besar rawan terjadi bias.

2. Random Forest
Kelebihan algoritma Random Forest adalah menggunakan teknik Bagging yang berusaha melawan overfitting dengan berjalan secara paralel. Sedangkan kekurangannya ada pada kompleksitas algoritma Random Forest yang membutuhkan waktu relatif lebih lama dan daya komputasi yang lebih tinggi dibanding algoritma seperti Decision Tree.

3. Boosting Algorithm
Kelebihan algoritma Boosting adalah menggunakan teknik Boosting yang berusaha menurunkan bias dengan berjalan secara sekuensial (memperbaiki model di tiap tahapnya). Sedangkan kekurangannya hampir sama dengan algoritma Random Forest dari segi kompleksitas komputasi yang menjadikan waktu pelatihan relatif lebih lama, selain itu noisy dan outliers sangat berpengaruh dalam algoritma ini.

Langkah pertama membuat DataFrame baru df_models untuk menampung nilai metrik pada setiap model / algoritma. Hal ini berguna untuk melakukan analisa perbandingan antar model. Metrik yang digunakan untuk mengevaluasi model adalah (MSE - Mean Squared Error).

### Model K-Nearest Neighbor
KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih k tetangga terdekat. Pemilihan nilai k sangat penting dan berpengaruh terhadap performa model. Jika memilih k yang terlalu rendah, maka akan menghasilkan model yang overfitting dan hasil prediksinya memiliki varians tinggi. Sedangkan jika memilih k yang terlalu tinggi, maka model yang dihasilkan akan underfitting dan prediksinya memiliki bias yang tinggi [4].

Oleh karena itu, perlu mencoba beberapa nilai k yang berbeda (1 sampai 20) kemudian membandingan mana yang menghasilkan nilai metrik model (pada kasus ini memakai mean squared error) terbaik. Selain itu, akan digunakan metrik ukuran jarak secara default (Minkowski Distance) pada KNeighborsRegressor dari library sklearn.

Tabel 6. Perbandingan Nilai K terhadap Nilai MSE
Nilai K | Nilai MSE
------- | ---------
K1 | 0.6071428571428571
K2 | 0.5
K3 | 0.4391534391534392
K4 | 0.42336309523809523
K5 | 0.36952380952380953
K6 | 0.353505291005291
K7 | 0.36929057337220605
K8 | 0.36811755952380953
K9 | 0.37889476778365666
K10 | 0.3705952380952381
K11 | 0.37682014954742227
K12 | 0.3759093915343915
K13 | 0.37306283460129613
K14 | 0.37263119533527694
K15 | 0.3693650793650794
K16 | 0.36509486607142855
K17 | 0.3617564672927995
K18 | 0.36302175191064073
K19 | 0.35833003561535426
K20 | 0.35613095238095244

Jika divisualisasikan dengan fungsi plot() diperoleh:

![Visualisasi-Nilai-K-terhadap-MSE](https://user-images.githubusercontent.com/110794445/200471344-5373d730-3d3b-4dec-bed3-7ae4a9c0d584.png)
Gambar 9. Visualisasi Nilai K terhadap MSE

Berdasarkan Tabel 6. dan Gambar 9. di atas,  nilai MSE terbaik dicapai ketika k = 6 yaitu sebesar 0.35350. Oleh karena itu kita akan menggunakan k = 6 dan menyimpan nilai MSE nya (terhadap data latih, untuk data uji akan dilakukan pada proses evaluasi) kedalam df_models yang telah kita siapkan sebelumnya.

## Random Forest
Random forest merupakan algoritma supervised learning yang termasuk ke dalam kategori ensemble (group) learning. Pada model ensemble, setiap model harus membuat prediksi secara independen. Kemudian, prediksi dari setiap model ensemble ini digabungkan untuk membuat prediksi akhir. Jenis metode ensemble yang digunakan pada Random Forest adalah teknik Bagging. Metode ini bekerja dengan membuat subset dari data train yang independen. Beberapa model awal (base model / weak model) dibuat untuk dijalankan secara simultan / paralel dan independen satu sama lain dengan subset data train yang independen. Hasil prediksi setiap model kemudian dikombinasikan untuk menentukan hasil prediksi final.

Untuk implementasinya menggunakan RandomForestRegressor dari library scikit-learn dengan base_estimator defaultnya yaitu DecisionTreeRegressor dan parameter-parameter (hyperparameter) yang digunakan antara lain:

n_estimator: jumlah trees (pohon) di forest.
max_depth: kedalaman atau panjang pohon. Ia merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node ke dalam jumlah pengamatan yang diinginkan.
random_state: digunakan untuk mengontrol random number generator yang digunakan.
n_jobs: jumlah job (pekerjaan) yang digunakan secara paralel. Ia merupakan komponen untuk mengontrol thread atau proses yang berjalan secara paralel. n_jobs=-1 artinya semua proses berjalan secara paralel.

Untuk menentukan nilai hyperparameter (n_estimator & max_depth) di atas, kita akan melakukan tuning dengan GridSearchCV. Keuntungan utama dari Grid Search adalah akurasi pembelajaran yang tinggi dan kemampuan pemrosesan paralel pada pelatihan setiap SVM, karena independen satu sama lain[4].

Tabel 7. Hasil Hyperparameter Tuning model GridSearchCV dengan Random Forest
 | Daftar Nilai | Nilai Terbaik
 - | ---------- | --------------
 n_estimators | 10, 20, 30, 40, 50, 60, 70, 80, 90 | 30
 max_depth | 4, 8, 16, 32 | 16
 MSE Data Latih | | 0.049292350984323684
 MSE Data Uji | | 0.39390449661487037
 

Dari hasil output di atas diperoleh nilai MSE terbaik dalam jangkauan parameter params_rf yaitu 0.049292350984323684 (dengan data train) dan 0.39390449661487037 (dengan data test) dengan n_estimators: 30 dan max_depth: 16. Selanjutnya kita akan menggunakan pengaturan parameter tersebut dan menyimpan nilai MSE nya kedalam df_models yang telah kita siapkan sebelumnya.

## Bosting Algorithm
Jika sebelumnya telah digunakan algoritma bagging (Random Forest). Selanjutnya akan menggunakan metode lain dalam model ensemble yaitu teknik Boosting. Algoritma Boosting bekerja dengan membangun model dari data train. Kemudian membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. Model ditambahkan sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum model untuk ditambahkan. Teknik ini bekerja secara sekuensial.

Pada kasus ini akan menggunakan metode Adaptive Boosting. Untuk implementasinya menggunakan AdaBoostRegressor dari library sklearn dengan base_estimator defaultnya yaitu DecisionTreeRegressor hampir sama dengan RandomForestRegressor bedanya menggunakan metode teknik Boosting.

Parameter-parameter (hyperparameter) yang digunakan pada algoritma ini antara lain:

n_estimator: jumlah estimator dan ketika mencapai nilai jumlah tersebut algoritma Boosting akan dihentikan.
learning_rate: bobot yang diterapkan pada setiap regressor di masing-masing iterasi Boosting.
random_state: digunakan untuk mengontrol random number generator yang digunakan.

Untuk menentukan nilai hyperparameter (n_estimator & learning_rate) di atas, kita akan melakukan tuning dengan GridSearchCV.

Tabel 8. Hasil Hyperparameter Tuning model RandomizedSearchCV dengan AdaBoosting
 | Daftar Nilai | Nilai Terbaik
 - | ---------- | --------------
n_estimators | 10, 20, 30, 40, 50, 60, 70, 80, 90 | 90
learning_rate | 0.001, 0.01, 0.1, 0.2 | 0.2
MSE Data Latih | | 0.33116537794773415
MSE Data Uji | | 0.3524856046953491

Dari hasil output di atas diperoleh nilai MSE terbaik dalam jangkauan parameter params_ab yaitu 0.33116537794773415 (dengan data train) dan 0.3524856046953491 (dengan data test) dengan n_estimators: 90 dan learning_rate: 0.2. Selanjutnya kita akan menggunakan pengaturan parameter tersebut dan menyimpan nilai MSE nya kedalam df_models yang telah kita siapkan sebelumnya.

## Model Terbaik berdasarkan Nilai MSE pada Data Latih

Pada tahap ini, hanya dibatasi pada data latih karena penggunaan data uji akan dilakukan pada proses evaluasi model. Berdasarkan DataFrame df_models diperoleh:

Tabel 9. Nilai MSE pada setiap model dengan data latih.
 | KNN | RandomForest | Boosting
- | -- | ------------ | ---------
Train MSE | 0.275889 | 0.050118 | 0.32955

Dari Tabel 9. di atas, perlu diperhatikan bahwa hasil MSE pada tabel sedikit berbeda dengan MSE hasil analisa proses hyperparameter tuning sebelumnya (khususnya pada Random Forest dan Boosting). Hal ini disebabkan model pada proses hyperparameter tuning menggunakan model GridSearchCV berbeda dengan Tabel 9. yang menggunakan model Random Forest dan Boosting. Terlepas dari hal tersebut, model terbaik dipegang oleh Random Forest dengan nilai MSE 0.050118 (terkecil).

## Evaluation
Dari proses sebelumnya, telah dibangun dan dilatih tiga model yang berbeda (KNN, Random Forest, Boosting). Selanjutnya perlu mengevaluasi model-model tersebut menggunakan data uji dan metrik yang digunakan dalam kasus ini yaitu mean_squared_error. Hasil evaluasi kemudian disimpan ke dalam df_models.


![formula-MSE](https://user-images.githubusercontent.com/110794445/200474268-315a6a3b-12bd-43e7-8b0a-17cff8c754b8.png)
Gambar 10. Formula MSE

Keterangan formula MSE pada gambar 10:

MSE = Mean Squared Error
n = banyaknya data point (baris)
Y_i = nilai yang diobservasi (fitur target PE)
Y^_i = hasil prediksi
Cara kerja metrik MSE adalah dengan menghitung selisih hasil prediksi dengan nilai fitur target (PE). Nilai selisih tersebut, disebut juga sebagai nilai eror yang kemudian di kuadratkan untuk menangani nilai selisih negatif, selanjutnya hasil pengkuadratan setiap nilai selisih dijumlahkan dan terakhir dibagi dengan banyak data point (n) untuk memperoleh nilai rata-ratanya. Rata-rata inilah yang disebut Mean Squared Error (MSE). Metrik MSE kerap digunakan untuk mengevaluasi model regresi seperti pada kasus ini.

Berdasarkan DataFrame df_models diperoleh:

Tabel 10. Nilai MSE pada Setiap Model dengan Data Uji
 | KNN | RandomForest | Boosting
 - | -- | ----------- | --------
Test MSE | 0.353505 | 0.377711 | 0.357394

Untuk memudahkan, dilakukan plot hasil evaluasi model dengan bar chart sebagai berikut:
![subplots](https://user-images.githubusercontent.com/110794445/200475859-722643b4-e9cd-4c9d-a76a-328770ff436a.png)
Gambar 11. Bar Chart Hasil Evaluasi Model dengan Data Latih dan Uji

Dari gambar di atas, terlihat bahwa, model RandomForest memberikan nilai eror (MSE) yang paling kecil. Sedangkan model algoritma Boosting memiliki eror yang paling besar. Sebelum memutuskan model terbaik untuk melakukan prediksi Quality pada wine atau besarnya daya yang dihasilkan. Mari kita coba uji prediksi menggunakan beberapa sampel acak (5) pada data uji.

Tabel 11. Hasil Prediksi
index_sample | y_true | prediksi_KNN | prediksi_RF | prediksi_Boosting
------------ | ------ | ------------ | ----------- | -----------------			
229 | 5 | 5.166667 | 5.133333 | 5.302139
283 | 7 | 6.166667 | 6.241667 | 6.061135
658 | 7 | 7.000000 | 6.633333 | 6.316176
50 | 4 | 5.500000 | 5.200000 | 5.303922
42 | 5 | 5.000000 | 5.035294 | 5.280899

## Kesimpulan
Berdasarkan hasil evaluasi model di atas, dapat disimpulkan bahwa model terbaik untuk melakukan prediksi Kualitas Wine adalah Model RandomForest pada Data Latih dengan nilai 0.050118 dan Model terbaik pada Data Uji yaitu Model K-Nearest Neighbor dengan nilai 0.353505. Diharapkan dengan dibangunnya model ini dapat menjadi pedoman perusahaan dalam menentukan kualitas wine yang berdampak pada kenaikan pendapatan.

## Referensi
[1] Jackson, R. S. (2008). Wine Science Principles and Applications (Third). Elsevier Inc

[2] OIV. (2020). State of the World Vitivinicultural Sector in 2019 (Issue April). https://www.oiv.int/public/medias/7298/oiv-state-of-the-vitivinicultural-sector-in2019.pdf

[3] Ristic, R., Bindon, K., Francis, L. I., Herderich, M. J., & Iland, P. G. (2010). Flavonoids and C13-norisoprenoids in Vitis vinifera L. cv. Shiraz: relationships between grape and wine composition, wine colour and wine sensory properties. Australian Journal of Grape and Wine Research, 16(3), 369–388. https://doi.org/10.1111/j.1755-0238.2010.00099.x
