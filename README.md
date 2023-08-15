# Final Project - Rakamin Group: peerData

## Dataset
Deskripsi:
Deposito berjangka adalah investasi tunai yang disimpan di bank. Kampanye pemasaran melalui telepon menjadi salah satu cara efektif untuk menjangkau nasabah, namun mereka membutuhkan investasi besar karena pusat panggilan besar disewa untuk melaksanakan kampanye. Oleh karena itu, sangat penting untuk mengidentifikasi nasabah yang kemungkinan besar akan berkonversi terlebih dahulu sehingga mereka dapat ditargetkan secara khusus melalui panggilan.

Dataset :
Memprediksi pelanggan yang berpotensi untuk men-deposito uangnya (berlangganan) atau tidak (tidak berlangganan)

Data :
Setiap satu baris data mewakili satu nasabah bank, satu kolom berisi data dari nasabah tersebut


# EXPLORATORY DATA ANALYSIS

## Descriptive Statistics
Sekilas tentang dataset :
Terdapat 17 kolom (16 kolom fitur dan 1 kolom target)
Terdapat 2 jenis tipe data, yaitu int64 dan object. Semua tipe data sudah sesuai, dengan kolom fitur.
Kolom categorical dengan tipe data object, dan kolom numerical dengan tipe data int64, karena kolom numerical mempunyai nilai yang bulat.
Berdasarkan df.isna( ) diketahui bahwa tidak ada data yang kosong pada dataset yang digunakan, sehingga nilai persentase missing value terhadap keseluruhan data adalah 0
Berdasarkan hasil perhitungan statistika, beberapa variabel nilai mean lebih besar dari median-nya, mengindikasikan bahwa grafik distribusi frekuensi menceng kanan atau kemencengan positif.
Dalam hal nilai minimum, kolom 'balance' memiliki nilai negatif (-8019), yang mungkin tidak sesuai untuk saldo rekening bank. 
Kolom 'duration' memiliki nilai minimum 0, yang mungkin tidak sesuai untuk durasi panggilan. Hal ini mungkin menunjukkan panggilan yang terlewat atau masalah lain.
Kolom pdays memiliki nilai minimum -1, nilai tersebut merupakan representasi nasabah yang belum pernah dihubungi di campaign sebelumnya.
Berdasarkan observasi kolom-kolom categorical, kebanyakan dari nasabah bank adalah orang yang memiliki pekerjaan “blue-collar” atau para pekerja kasar, yang sudah menikah dengan pendidikan menengah.
Para nasabah tersebut sebagian besar memiliki pinjaman rumah, yang dapat dihubungi lewat telepon seluler. Namun, sebagian besar dari para nasabah tersebut tidak mendepositkan uang mereka pada bank sebelumnya.
Dalam hal unique data, tidak ada data yang terlalu beragam (karena tidak ada data id), sehingga masih bagus untuk digunakan semua.
Dalam hal frequency, variabel 'default' memiliki jumlah nilai "no" yang terlalu banyak, hal ini juga terjadi pada variabel 'month', 'poutcome' dan 'y' yang cukup ada ketimpangan data.

## Univariate Analysis
"age" : 
50% dari keseluruhan data terpusat pada usia antara 33 hingga 48 tahun.
Terdapat beberapa outlier pada sisi atas distribusi dengan usia lebih dari 70 tahun.
"balance" : 
Sebagian besar responden memiliki saldo di bawah 1428. 
Terdapat outlier ekstrim pada sisi atas distribusi, menunjukkan adanya responden dengan saldo rekening yang sangat tinggi. 
Saat pre-processing, disarankan untuk mengubah data minus menjadi 0, dan menghapus atau mentransformasi data untuk menangani outliers yang ekstrim
"day": 
Secara umum, distribusi data cenderung normal tanpa terlihat outliers.
"duration": 
50% durasi panggilan sekitar 100 hingga 400 detik
Terdapat banyak outlier dan nilai ekstrem pada sisi atas distribusi
"campaign": 
50% data terpusat pada jumlah campaign antara 1 hingga 4. 
Terdapat banyak outlier dan nilai ekstrem pada sisi atas distribusi, menunjukkan adanya beberapa responden dengan jumlah kontak yang sangat tinggi.  
“pdays": 
Terdapat banyak nilai ekstrem dan outlier pada sisi atas distribusi
Saat melakukan pre-processing data, nilai -1 dapat diganti dengan nilai yang lebih bermakna seperti 0 untuk menandai klien yang tidak pernah dihubungi sebelumnya.
"previous": 
Terdapat beberapa outlier dan nilai ekstrem yang sangat tinggi pada sisi atas distribusi.
Saat melakukan pre-processing data, dapat dilakukan penghapusan outlier yang berada di luar kisaran nilai yang masuk akal.
"age": Distribusi cukup normal, tidak ada indikasi skewness yang signifikan.
"balance": Distribusi sangat skew ke kanan (positively skewed). Perlu dilakukan penghapusan outlier dengan transformasi data (log transformation) atau IQR
"day": Distribusi tidak menunjukkan karakteristik yang mencolok. 
"duration": Distribusi sangat skew ke kanan. Perlu dilakukan penanganan outlier dengan transformasi data (log transformation) atau IQR
"campaign": Distribusi cenderung positively skewed, dengan sebagian besar nasabah menerima panggilan dalam jumlah yang sedikit. Terdapat nilai maksimum yang jauh lebih tinggi dari nilai-nilai lainnya, menunjukkan adanya beberapa nasabah yang menerima panggilan kampanye dalam jumlah yang sangat banyak.
"pdays": Distribusi nilai pdays sangat skew ke kanan. Saat melakukan pra-pemrosesan data, nilai -1 dapat diganti dengan nilai yang lebih bermakna seperti NaN untuk menandai klien yang tidak pernah dihubungi sebelumnya.
"previous": Distribusi sangat skew ke kanan. Perlu dilakukan penghapusan outlier yang berada di luar kisaran nilai.
Feature "job":
Blue-collar  dan management menjadi pekerjaan paling umum dalam dataset ini.
Feature "marital":
Mayoritas responden (60%) dalam dataset ini adalah yang sudah menikah.
Feature "education":
Sekitar setengah dari responden memiliki pendidikan tingkat menengah (secondary)
Feature "default":
Mayoritas responden (98%) tidak memiliki masalah default pada pinjaman atau kredit macet.
Feature "housing":
Lebih dari setengah responden (55%) memiliki kepemilikan rumah (housing).
Feature "loan":
Mayoritas responden (83%) tidak memiliki pinjaman.
Feature "contact":
Sebagian besar komunikasi (64%) dilakukan melalui telepon seluler (cellular) 
Feature "month":
Nasabah paling banyak dihubungi pada bulan Mei (30%) , diikuti oleh bulan Juli, Agustus dan Juni
Saat data pre-processing, pertimbangkan untuk menggabungkan bulan-bulan ke dalam kategori yang lebih luas (misalnya musim atau kuartal) untuk analisis atau pemodelan yang lebih baik.
Feature "poutcome":
Sebagian besar responden(80%) memiliki hasil pemasaran sebelumnya yang tidak diketahui (unknown).
Feature "y":
Mayoritas (88%) responden tidak berlangganan deposito.. 
Saat data pre-processing, memastikan pemrosesan kelas target seperti mengubah nilai "yes" menjadi 1 dan "no" menjadi 0, 
selanjutnya berdasarkan data yang imbalanced, perlu dipertimbangkan juga untuk melakukan undersampling.
Feature "age segmentation":
Mayoritas (46%) responden berada di rentang umur 33-48 tahun

## Multivariate Analysis
Insight:
Berdasarkan conversion-ratenya, persentase tertinggi nasabah yang berlangganan deposit memiliki pekerjaan sebagai pelajar (28.67%).
Berdasarkan conversion-ratenya, pendidikan tertiary memiliki persentase tertinggi (15%).
Semakin tinggi pendidikan nasabah, peluang convertnya akan semakin tinggi.
Nasabah dengan status ‘single’ memiliki persentase conversion rate paling tinggi (14.95%), meskipun selisihnya tidak terlihat signifikan.
Nasabah yang tidak memiliki masalah dengan default atau kredit macet lebih banyak yang berlangganan deposit (11.79%) daripada yang terkena masalah.
Nasabah yang belum pernah mengajukan KPR cenderung lebih banyak berlangganan produk deposit (16.70%).
Conversion rate nasabah yang tidak memiliki KPR memiliki nilai lebih dari 2 kali lipat dari yang memiliki KPR
Nasabah yang belum pernah mengajukan pinjaman pribadi lebih tinggi persentase berlangganannya (12.65%).
Perbedaan persentase yang tidak memiliki pinjaman hampir 2 kali lipat dari nasabah yang memiliki pinjaman.
Jenis kontak melalui seluler memiliki persentase tertinggi (14.91%).
Meskipun tidak berbeda jauh dengan telepon, namun perbedaannya cukup signifikan dibandingkan dengan metode lain atau unknown.
Bulan Maret menjadi bulan terakhir kontak dengan hasil konversi berlangganan tertinggi (51.99%). 
Bulan September, Oktober dan Desember juga cukup tinggi; sisanya rendah.
Hasil sukses pada campaign terakhir menjadi tanda nasabah yang berlangganan deposit (64.72%), memiliki persentase tertinggi dan selisih yang signifikan dari hasil lainnya.
OBSERVATIONS:
Feature 'pdays' dan 'previous' memiliki korelasi yang masuk dalam kategori moderate correlation (0.45), feature lainnya berkorelasi lemah / sangat lemah.
FEATURES SELECTION:
Feature yang perlu dipertahankan:
Previous
Feature yang akan ditakeout:
Pdays : Memiliki banyak outliers yang ekstrim, memiliki nilai mayoritas -1, memiliki standar deviasi yang sangat besar ketimbang 'previous'.
Duration: Memiliki banyak nilai 0 (masih dalam pertimbangan)
OBSERVATIONS:
Korelasi feature 'age' dan 'duration': Semakin lama durasi, kemungkinan deposit menjadi semakin tinggi tidak peduli berapapun usianya.
Korelasi feature 'day' dan 'duration’: Semakin lama durasi semakin tinggi kemungkinan nasabah untuk deposit tidak peduli di hari apa kontak terakhir dilakukan.
Korelasi feature 'age' dan 'campaign': Semakin banyak campaign, semakin kecil kecenderungan nasabah untuk berlangganan deposit tidak peduli berapapun usia nasabah.
Sisanya tidak menunjukkan hubungan dan pola yang menarik terhadap label target.
CONCLUSION:
Selain feature 'pdays' dan 'duration', sisanya cukup relevan untuk dipertahankan.

# BUSINESS INSIGHT & RECOMMENDATION

## Segmentasi dan Personalisasi
Fitur 'job', 'default', 'loan', 'housing' dan 'contact' mengindikasikan bahwa kita bahwa nasabah yang berprofesi sebagai pelajar atau pensiunan yang tidak memiliki kredit macet, pinjaman pribadi, dan KPR jauh lebih tinggi kemungkinannya untuk berlangganan deposito berjangka yang ditawarkan melalui telepon maupun seluler.
Recommendation:
Targetkan upaya marketing kepada kelompok nasabah yang tidak memiliki masalah atau beban pinjaman apapun. 
Untuk target pelajar, buatkan program khusus dan lakukan kerja sama dengan institusi pendidikan.
Untuk pensiunan, ciptakan program tabungan pensiun dengan resiko yang lebih minim dan suku bunga yang lebih besar, serta jangka waktu investasi yang lebih singkat.
Metode kontak bisa dilakukan melalui seluler atau telepon karena masih sangat efektif dari segi conversion rate.

## Analisis Mendalam Durasi Panggilan
Hubungan antara fitur 'duration' dengan fitur 'age' dan 'day' menunjukkan bahwa semakin lama durasi panggilan, lebih tinggi kemungkinan dan cenderung berlangganan deposito berjangka, hal ini mungkin karena nasabah yang tertarik dengan deposito akan lebih banyak bertanya dan melakukan percakapan lebih lama sebelum akhirnya berlangganan.
Recommendation: 
Fokuskan pada peningkatan kualitas dan efisiensi waktu interaksi pelanggan selama panggilan. 
Buatlah guidelines dan skenario interaksi pelanggan yang berfokus pada elemen-elemen yang telah terbukti berhasil (misal menargetkan untuk pembicaraan maksimal 30 menit (1.800 detik) karena berdasarkan persebaran data, cukup banyak nasabah yang tertarik dengan durasi tidak lebih dari 2.000 detik). Dengan ini, diharapkan biaya telepon ataupun seluler juga bisa terpangkas, dan marketer bisa fokus ke nasabah lain tanpa ada pemborosan jumlah marketer yang dibutuhkan.

## Analisis Musiman dan Optimalisasi Kontak
Fitur 'month' menunjukkan pola menarik, dengan beberapa bulan (terakhir dilakukan kontak) memiliki tingkat langganan yang jauh lebih tinggi dibanding yang lainnya.
Hubungan antara fitur 'age' dan fitur 'campaign' menunjukkan bahwa semakin banyak kontak yang dilakukan saat ini berapapun usianya, nasabah cenderung enggan berlangganan.
Fitur 'poutcome' menjadi indikasi bahwa hasil pada campaign sebelumnya mencerminkan keputusan berlangganan.
Recommendation:
Ekstrapolasi analisis di sekitar bulan Maret, September, Oktober dan Desember seperti analisis peristiwa tertentu atau trend ekonomi yang terkait. Pertimbangkan untuk menyesuaikan strategi marketing dan alokasi sumber daya untuk lebih efektif melakukan kontak di bulan-bulan tersebut dan di bulan sebelumnya seperti Februari, Agustus dan November.
Evaluasi efektivitas jumlah kontak dan hasil sebelumnya. Targetkan lebih pada nasabah yang pada campaign sebelumnya memang tertarik atau 'sukses' saat dikontak. Batasi kontak pada rentang 2 bulan, jika tidak berhasil beralih ke nasabah lain di bulan lain yang potensial (memiliki konversi tinggi). Hal ini diharapkan bisa mengurangi intensitas dan frekuensi kontak yang bisa berdampak pada berkurangnya biaya investasi campaign dan meningkatkan conversion rate.

## Maksimalkan Penggunaan Machine Learning Untuk Beberapa Fitur
Untuk variabel numerik, variabel 'pdays' berkorelasi dengan 'previous' sehingga 'pdays' kemungkinan akan di takeout, sedangkan variabel 'duration' masih dalam tahap pertimbangan karena memberikan insight yang cukup menarik terkait karakteristik dan segmentasi calon nasabah. Selebihnya, variabel numerik bisa digunakan untuk analisis ML.
Untuk variabel kategorikal, semua variabel bisa dipakai untuk analisis ML, namun akan dipertimbangkan untuk diencoding, karena variabel 'month', 'loan', 'housing' dan 'default' memberikan info penting bagaimana karakteristik nasabah yang berlangganan.
Recommendation: 
Mencoba menganalisis menggunakan ML dengan memasukkan semua variabel numerik yang tersisa ditambah beberapa variabel kategorikal yang akan di One Hot Encoding. 
Diharapkan gabungan dari variabel-variabel yang akan dipakai modelling ML ini bisa menghasilkan rekomendasi hasil ML yang paling efektif dan efisien untuk mengurangi biaya investasi panggilan, campaign dan karyawan serta meningkatkan conversion rate nasabah yang berlangganan.
