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
!

## Data Preparation
## Modeling

## Evaluation

## Referensi
[1] Jackson, R. S. (2008). Wine Science Principles and Applications (Third). Elsevier Inc

[2] OIV. (2020). State of the World Vitivinicultural Sector in 2019 (Issue April). https://www.oiv.int/public/medias/7298/oiv-state-of-the-vitivinicultural-sector-in2019.pdf

[3] Ristic, R., Bindon, K., Francis, L. I., Herderich, M. J., & Iland, P. G. (2010). Flavonoids and C13-norisoprenoids in Vitis vinifera L. cv. Shiraz: relationships between grape and wine composition, wine colour and wine sensory properties. Australian Journal of Grape and Wine Research, 16(3), 369–388. https://doi.org/10.1111/j.1755-0238.2010.00099.x
