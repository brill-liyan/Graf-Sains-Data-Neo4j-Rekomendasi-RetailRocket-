# UTS Graf Sains Data — Neo4j & Sistem Rekomendasi

Repository ini berisi pengerjaan **UTS Mata Kuliah Graf Sains Data** dengan topik **Python Driver untuk Neo4j dan Rekomendasi**.

## 📌 Deskripsi

Proyek ini menggunakan **RetailRocket Dataset** untuk membangun dan menganalisis graph menggunakan **Neo4j**. Data interaksi pengguna dengan produk digunakan untuk membentuk graph yang terdiri dari node `Visitor` dan `Item`, serta beberapa jenis hubungan berdasarkan aktivitas pengguna.

Analisis kemudian dilanjutkan dengan **Vector Space Model (VSM)**, similarity, dan **K-Nearest Neighbors (KNN)** untuk menghasilkan rekomendasi item.

## 📂 Struktur Repository

```text
UTS-Graf-Sains-Data/
│
├── UTS_GSD_Annotated.ipynb
├── README.md
└── data/
    └── events.csv
```

> **Catatan:** File dataset dapat berukuran besar. Pastikan ukuran file diperiksa terlebih dahulu sebelum diunggah ke GitHub.

## 📊 Dataset

Dataset yang digunakan adalah **RetailRocket Dataset**.

Beberapa atribut utama yang digunakan:

| Atribut | Deskripsi |
|---|---|
| `timestamp` | Waktu terjadinya interaksi |
| `visitorid` | ID pengguna |
| `event` | Jenis interaksi (`view`, `addtocart`, `transaction`) |
| `itemid` | ID item/produk |
| `transactionid` | ID transaksi |

Data interaksi dibagi menjadi dua periode waktu:

- **P1 (Training)** — digunakan untuk membangun graph dan melakukan analisis.
- **P2 (Testing)** — digunakan untuk mengevaluasi hasil rekomendasi.

## 🕸️ Graph Database

Graph dibangun menggunakan **Neo4j** dengan struktur utama:

```text
(Visitor) ──[:VIEWED]──────> (Item)
(Visitor) ──[:ADDED_TO_CART]──> (Item)
(Visitor) ──[:BOUGHT]──────> (Item)
```

Node yang digunakan:

- `Visitor`
- `Item`

Relationship yang digunakan:

- `VIEWED`
- `ADDED_TO_CART`
- `BOUGHT`

Neo4j digunakan untuk menyimpan dan melakukan query terhadap graph hasil interaksi pengguna dan item.

## 🔎 Tahapan Analisis

### 1. Data Preparation

Data RetailRocket difilter berdasarkan periode waktu yang telah ditentukan untuk membentuk data **training (P1)** dan **testing (P2)**.

Data hasil filtering kemudian disimpan dalam format CSV untuk digunakan dalam proses berikutnya.

### 2. Exploratory Data Analysis

Dilakukan analisis terhadap komposisi subgraph, meliputi:

- jumlah node `Visitor`
- jumlah node `Item`
- jumlah relationship
- jenis relationship yang terdapat pada graph

Analisis dilakukan menggunakan **Python** dan **Cypher Query**.

### 3. Vector Space Model (VSM)

VSM digunakan untuk merepresentasikan graph dalam bentuk vektor.

Terdapat dua pendekatan yang dianalisis:

- **VSM pada User/Visitor**
- **VSM pada Item**

Hasil representasi kemudian digunakan untuk membentuk projected graph dan menganalisis hubungan antar-entitas.

### 4. Similarity

Similarity dihitung pada projected graph untuk mengetahui tingkat kemiripan antar node.

Proses ini mencakup:

1. Mengambil beberapa record similarity menggunakan Cypher.
2. Menentukan reference record.
3. Menghitung dan menganalisis nilai similarity menggunakan Python.
4. Menuliskan nilai similarity kembali ke graph Neo4j.
5. Membandingkan kondisi graph sebelum dan sesudah similarity ditambahkan.

### 5. K-Nearest Neighbors (KNN)

KNN digunakan untuk menghasilkan rekomendasi item berdasarkan kemiripan antar pengguna/item.

Parameter yang digunakan:

```text
k = 5
```

Seorang user dipilih secara acak dengan proses yang dibuat **reproducible** menggunakan random seed.

Berdasarkan hasil KNN, dihasilkan **3 item yang direkomendasikan** untuk user tersebut.

### 6. Evaluation

Sistem rekomendasi dievaluasi menggunakan:

- **Hit@5**
- **NDCG@5**

Kedua metrik digunakan untuk mengetahui seberapa baik item yang direkomendasikan dibandingkan dengan item yang terdapat pada data testing.

## 🛠️ Teknologi yang Digunakan

- **Python**
- **Jupyter Notebook**
- **Neo4j**
- **Neo4j Python Driver**
- **Pandas**
- **NumPy**
- **NetworkX**
- **Scikit-learn**
- **Matplotlib**
- **Cypher Query**

## 📓 Notebook

File utama dalam repository:

**`UTS_GSD_Annotated.ipynb`**

Notebook berisi implementasi dan penjelasan setiap tahapan, mulai dari preprocessing data, import data ke Neo4j, pembentukan VSM, similarity, hingga KNN dan evaluasi rekomendasi.

## 🎯 Tujuan

Proyek ini bertujuan untuk menerapkan konsep **Graf Sains Data** dalam pengolahan data interaksi pengguna dan item, serta memanfaatkan struktur graph untuk membangun pendekatan sistem rekomendasi.

---

**Mata Kuliah:** Graf Sains Data  
**Topik:** Python Driver untuk Neo4j dan Rekomendasi  
**Tahun Akademik:** 2026/2027
