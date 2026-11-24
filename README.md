# 🌿CNN-EfficientNet-B0---Klasifikasi-jenis-rimpang
Proyek ini menerapkan metode Deep Learning berbasis Convolutional Neural Network (CNN) dengan arsitektur EfficientNetB0 untuk mengklasifikasikan empat jenis rimpang, yaitu jahe, kunyit, kencur, dan lengkuas. Model dikembangkan menggunakan Python dan TensorFlow Keras dengan pendekatan Transfer Learning untuk memanfaatkan bobot pretrained dari ImageNet, sehingga proses pelatihan menjadi lebih efisien dan mampu mengenali karakteristik visual dari setiap jenis rimpang. 
Matakuliah JST : Kelompok 8
- Ni Wayan Sinta Maharani 5009231005
- Diarsa Citra Putri 5009231076
- Syarifah Riquhaa Aljannah 5009231156
- Fidora Illahi Faliha 5009231165

# 🧩Arsitektur Model
Model dikembangkan menggunakan pendekatan Transfer Learning dan Fine-Tuning EfficientNetB0, dengan arsitektur sebagai berikut:
- Base Model: EfficientNetB0 (pre-trained pada ImageNet, tanpa top layer).
- Global Average Pooling Layer: Mengubah feature map menjadi representasi fitur berdimensi lebih rendah.
- Batch Normalization Layer: Menstabilkan distribusi nilai fitur selama pelatihan.
- Dense Layer: 128 neuron, aktivasi ReLU.
- Dropout Layer: 0.5 untuk mengurangi risiko overfitting.
- Output Layer: 4 neuron dengan aktivasi Softmax untuk mengklasifikasikan Jahe, Kunyit, Kencur, dan Lengkuas.
Konfigurasi Pelatihan Model
Model dikompilasi menggunakan:
- Optimizer: Adam.
- Learning Rate Tahap 1: 0.001 (Feature Extraction).
- Learning Rate Tahap 2: 0.00001 (Fine-Tuning).
- Loss Function: Sparse Categorical Crossentropy.
- Metrics: Accuracy dan Sparse Top-2 Categorical Accuracy.
- Batch Size: 16.
- Epoch: Maksimal 20 epoch untuk Feature Extraction dan 15 epoch untuk Fine-Tuning.
Tahapan Transfer Learning
1. Feature Extraction: Bobot EfficientNetB0 dibekukan (frozen), kemudian melatih lapisan klasifikasi tambahan.
2. Fine-Tuning: Membuka 30 lapisan terakhir EfficientNetB0 untuk dilatih kembali, kecuali lapisan Batch Normalization yang tetap dibekukan.

# 📊Dataset dan Preprocessing
Dataset terdiri dari empat kelas, yaitu Jahe, Kunyit, Kencur, dan Lengkuas. Pembagian dataset dilakukan secara stratified dengan komposisi:
- 56% data latih (Training)
- 14% data validasi (Validation)
- 30% data pengujian (Testing)
Seluruh gambar melalui preprocessing dengan tahapan:
- Mengubah gambar ke format RGB.
- Mengubah ukuran gambar menjadi 224 × 224 piksel.
- Menggunakan batch size sebesar 16.
Augmentasi data dilakukan pada data latih menggunakan:
- RandomFlip("horizontal") – membalik gambar secara horizontal.
- RandomRotation(0.05) – melakukan rotasi gambar secara acak.
- RandomZoom(0.10) – melakukan pembesaran atau pengecilan gambar.
- RandomTranslation(0.05, 0.05) – menggeser posisi gambar secara horizontal dan vertikal.

# 🚀Callback
Model menggunakan tiga callback untuk mengoptimalkan proses pelatihan dan menyimpan bobot model terbaik:
- EarlyStopping → Menghentikan proses training apabila nilai validation loss tidak mengalami perbaikan selama beberapa epoch, serta mengembalikan bobot terbaik.
- ReduceLROnPlateau → Menurunkan nilai learning rate secara otomatis apabila validation loss tidak mengalami penurunan.
- ModelCheckpoint → Menyimpan model dengan nilai validation loss terbaik selama proses training

# 📈Hasil dan Evaluasi
Model menunjukkan performa yang baik pada dataset rempah-rempah dengan tingkat akurasi tinggi pada data validasi.
(“Akurasi validasi: 88.48%”).
