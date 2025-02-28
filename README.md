# 1. Rumus Qubit & Superposisi
### Kode Python :

- Linear accuracy
```python
# ini adlaah module dari IBM utnuk mesimulasikan konsep Quantum Computing
from qiskit import QuantumCircuit, Aer, execute

# membuat sirkuit kuantum dengan 1 qubit
qc = QuantumCircuit(1)

# menerapkan gerbang Hadamard (membuat superposisi)
qc.h(0)

# menambahkan pengukuran
qc.measure_all()

# menjalankan simulasi
simulator = Aer.get_backend('aer_simulator')
job = execute(qc, simulator, shots=1000)
result = job.result()
counts = result.get_counts()

print(counts)  # hasilnya harus mendekati {'0': 500, '1': 500}
```


- Visualisasi
```python
from qiskit import QuantumCircuit

qc = QuantumCircuit(2)  # memuat quantum circuit dengan 2 qubit
qc.h(0)  # memberi gerbang Hadamard ke qubit pertama (superposisi)
qc.cx(0, 1)  # entanglement antara qubit 0 dan 1
qc.measure_all()  # mengukur semua qubit

print(qc)
```

maka ouputnya akan seperti ini 
```bash
        ┌───┐      ░ ┌─┐   
   q_0: ┤ H ├──■───░─┤M├───
        └───┘┌─┴─┐ ░ └╥┘┌─┐
   q_1: ─────┤ X ├─░──╫─┤M├
             └───┘ ░  ║ └╥┘
meas: 2/══════════════╩══╩═
                      0  1
```


# Qubit dan Superposisi dalam Komputasi Kuantum

## Konsep Dasar Qubit

Qubit (quantum bit) adalah e;emen dasar informasi kuantum, analog dengan bit klasik namun dengan properti kuantum yang beda. Berbeda dengan bit klasik yang hanya dapat berada dalam keadaan 0 atau 1, qubit dapat berada dalam superposisi keduanya.

### Representasi Matematis Qubit

Secara matematis, keadaan qubit dapat direpresentasikan sebagai vektor keadaan dalam ruang Hilbert dua dimensi. dengan cara menggunakan notasi Dirac, basis komputasi standar yg bisa di tulskan seperti ini:

- |0⟩ = [1, 0]ᵀ (analog dengan bit klasik 0)
- |1⟩ = [0, 1]ᵀ (analog dengan bit klasik 1)

Keadaan umum sebuah qubit dapat dituliskan sebagai kombinasi linear dari basis komputasi:

|ψ⟩ = α|0⟩ + β|1⟩

dimana α dan β adalah bilangan kompleks yang memenuhi syarat normalisasi:

|α|² + |β|² = 1

Koefisien α dan β menentukan amplitudo probabilitas. Ketika qubit diukur dalam basis komputasi standar:
- Probabilitas mendapatkan hasil |0⟩ adalah |α|²
- Probabilitas mendapatkan hasil |1⟩ adalah |β|²

### Representasi Geometris: Menggunakan konsep Bola

Keadaan murni sebuah qubit dapat divisualisasikan pada bola, dimana:

|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩

dengan:
- θ adalah sudut polar (0 ≤ θ ≤ π)
- φ adalah sudut azimuthal (0 ≤ φ < 2π)

Keadaan klasik(komputer klasik) |0⟩ dan |1⟩ berada pada kutub utara dan selatan bola, sedangkan superposisi berada di tempat lain pada permukaan bola.

## Superposisi Kuantum

Superposisi adalah keadaan kuantum dimana sistem berada dalam beberapa keadaan basis secara simultan sampai saat pengukuran.

### Properti Matematika Superposisi

Kalau |ψ₁⟩, |ψ₂⟩, ..., |ψₙ⟩ adalah keadaan kuantum yang mungkin, maka superposisi linear mereka:

|ψ⟩ = c₁|ψ₁⟩ + c₂|ψ₂⟩ + ... + cₙ|ψₙ⟩

juga merupakan keadaan kuantum yang valid, dengan syarat normalisasi |c₁|² + |c₂|² + ... + |cₙ|² = 1.

### Contoh Penting Superposisi

1. **Keadaan Bell**:
   Keadaan terbelit maksimal antara dua qubit:
   |Φ⁺⟩ = (|00⟩ + |11⟩)/√2

2. **Keadaan Superposisi Merata**:
   Dibuat dengan menerapkan gerbang Hadamard pada keadaan |0⟩:
   H|0⟩ = (|0⟩ + |1⟩)/√2

3. **Keadaan GHZ**:
   Superposisi multi-qubit:
   |GHZ⟩ = (|000...0⟩ + |111...1⟩)/√2

4. **Keadaan W**:
   Superposisi dengan satu qubit dalam keadaan |1⟩:
   |W⟩ = (|100...0⟩ + |010...0⟩ + ... + |000...1⟩)/√n

### Menciptakan Superposisi

Salah satu cara paling mudah buat menciptakan superposisi itu menggunakan gerbang Hadamard:

1. Mulai dengan qubit dalam keadaan basis |0⟩
2. Terapkan gerbang Hadamard (H) untuk mendapatkan:
   H|0⟩ = (|0⟩ + |1⟩)/√2

Untuk membuat superposisi dari n qubit, kita harusmenerapkan gerbang Hadamard pada semua qubit:
H⊗ⁿ|0⟩⊗ⁿ = (1/√2ⁿ) ∑ₓ |x⟩

dimana jumlahan dilakukan atas semua 2ⁿ string biner x.

## Register Qubit dan Pengukuran

### Register Qubit

Register qubit terdiri dari beberapa qubit yg beroperasi bersama. Keadaan register Nqubit berada dalam ruang Hilbert 2ⁿ dimensi, yang memungkinkan superposisinya eksponensial.

Keadaan umum register n-qubit:

|ψ⟩ = ∑ₓ cₓ|x⟩

dimana x berjalan melalui semua 2ⁿ string biner dan ∑ₓ |cₓ|² = 1.

### Proses Pengukuran

Saat pengukuran dilakukan pada qubit dalam superposisi:

1. Keadaan kuantum "kolaps" ke salah satu keadaan basis
2. Hasil pengukuran bersifat probabilistik
3. Informasi superposisi hilang setelah pengukuran

Untuk keadaan |ψ⟩ = α|0⟩ + β|1⟩, pengukuran menghasilkan:
- |0⟩ dengan probabilitas |α|²
- |1⟩ dengan probabilitas |β|²

### Fenomena

1. **Interferensi Kuantum**:
   Amplitudo probabilitas bisa saling memperkuat atau meniadakan, menghasilkan pola interferensi yg tidak ada padanannya dalam komputer klasik.

2. **Entanglement (Keterbelitan)**:
   Keadaan dua atau lebih qubit yang tidak dapat dideskripsikan secara terpisah. Contohnya:
   |Φ⁺⟩ = (|00⟩ + |11⟩)/√2

3. **Paralelisme Kuantum**:
   Kemampuan untuk mengevaluasi fungsi pada superposisi input, secara efektif melakukan banyak perhitungan secara simultan.

## Rumus

### Produk Tensor

Untuk menggabungkan sistem qubit, gunakan produk tensor:
|ψ₁⟩ ⊗ |ψ₂⟩ = |ψ₁ψ₂⟩

Contoh: (α|0⟩ + β|1⟩) ⊗ (γ|0⟩ + δ|1⟩) = αγ|00⟩ + αδ|01⟩ + βγ|10⟩ + βδ|11⟩

### Evolusi Kuantum

Evolusi keadaan kuantum diberikan oleh operator uniter U:
|ψ(t)⟩ = U|ψ(0)⟩

Dalam kasus kontinu:
i·ħ·∂|ψ(t)⟩/∂t = H|ψ(t)⟩

dimana H ini adalah operator Hamiltonian sistem.

### Operator Densitas

Untuk sistem campuran, keadaan dapat direpresentasikan dengan operator densitas:
ρ = ∑ᵢ pᵢ|ψᵢ⟩⟨ψᵢ|

dimana pᵢ adalah probabilitas klasik bahwa sistem berada dalam keadaan |ψᵢ⟩.

## Hubungan dengan Algoritma Kuantum

Konsep qubit & superposisi adalah fondasi bagi algoritma kuantum seperti Deutsch Jozsa, Grover, dan Shor:

1. **Algoritma Deutsch-Jozsa**:
   Memanfatkan superposisi untuk mengevaluasi fungsi f(x) pada semua input secara simultan.

2. **Algoritma Grover**:
   Menggunakan superposisi dan interferensi kuantum buat mempercepat pencarian dalam database yg tidak terurut.

3. **Algoritma Shor**:
   Memanfaatkan transformasi Fourier kuantum yang bekerja pada superposisi untuk faktorisasi bilangan besar.



# Materi 2: Entanglement (Keterkaitan Kuantum)
1️⃣ Apa Itu Entanglement? Entanglement (keterkaitan kuantum) adalah fenomena di mana dua qubit menjadi saling terhubung, sehingga mengubah satu qubit akan langsung mempengaruhi qubit lainnya, meskipun mereka berjauhan.

💡 Contoh Analoginya:
Bayangkan kamu dan temanmu masing2 punya sebuah kotak ajaib.

Kalau kamu buka kotakmu dan isinya bola merah, maka temanmu pasti juga menemukan bola merah di kotaknya, meskipun dia ada di tempat yang sangat jauh. Kalau kamu buka dan isinya bola biru, maka temanmu juga akan menemukan bola biru. Ini terjadi tanpa ada koneksi langsung antara kedua kotak! Itulah entanglement. Begitu satu qubit diukur, qubit lainnya langsung "tertentu" hasilnya, meskipun sebelumnya masih dalam superposisi.

2️⃣ Cara Membuat Entanglement dengan Qiskit Kita bisa membuat dua qubit ter entangle dengan menggunakan dua gerbang kuantum utama:

Hadamard (H-Gate) → Membuat superposisi. CNOT (CX-Gate) → Menghubungkan dua qubit agar ter-entangle.

```python
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator  
from qiskit import transpile

# membuat quantum circuit dengan 2 qubit
qc = QuantumCircuit(2)

# gerbang Hadamard ke qubit pertama (superposisi)
qc.h(0)

# menerapkan gerbang CNOT (menghubungkan qubit 0 dan qubit 1)
qc.cx(0, 1)

# menambahkan pengukuran
qc.measure_all()

# sirkuitnya
print(qc)

# simulator nya
simulator = AerSimulator()
compiled_circuit = transpile(qc, simulator)  
result = simulator.run(compiled_circuit, shots=1000).result()

print(result.get_counts())
```
result :
```
        ┌───┐      ░ ┌─┐   
   q_0: ┤ H ├──■───░─┤M├───
        └───┘┌─┴─┐ ░ └╥┘┌─┐
   q_1: ─────┤ X ├─░──╫─┤M├
             └───┘ ░  ║ └╥┘
meas: 2/══════════════╩══╩═
                      0  1 
{'11': 497, '00': 503}
```

# Entanglement (Keterkaitan Kuantum)

Entanglement atau keterkaitan kuantum adalah salah satu fenomena paling misterius dan fundamental dalam mekanika kuantum. Fenomena ini menjadi dasar bagi berbagai aplikasi kuantum modern termasuk komputasi kuantum, kriptografi kuantum, dan teleportasi kuantum.

## Konsep Dasar Entanglement

Entanglement terjadi ketika dua atau lebih partikel berinteraksi sedemikian rupa sehingga keadaan kuantum masing2 partikel tidak dapat dijelaskan secara independen. Sebagai gantinya, keadaan kuantum harus dijelaskan sebagai keadaan sistem secara keseluruhan, bahkan ketika partikel2 tersebut dipisahkan oleh jarak yang sangat jauh.

### Definisi Matematis

Secara matematis, keadaan terbelit (entangled state) adalah keadaan kuantum dari sistem multi-partikel yang tidak dapat ditulis sebagai produk tensor dari keadaan individual partikel:

$$|\psi_{AB}\rangle \neq |\psi_A\rangle \otimes |\psi_B\rangle$$

dengan $|\psi_{AB}\rangle$ adalah keadaan sistem secara keseluruhan, dan $|\psi_A\rangle$ dan $|\psi_B\rangle$ adalah keadaan subsistem A dan B.

## Keadaan Bell: Contoh Entanglement Paling Sederhana

Keadaan Bell adalah contoh paling sederhana dari keadaan terbelit maksimal antara dua qubit. Terdapat empat keadaan Bell yang membentuk basis ortonormal dalam ruang Hilbert dimensi empat dari sistem dua qubit:

$$|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$$

$$|\Phi^-\rangle = \frac{1}{\sqrt{2}}(|00\rangle - |11\rangle)$$

$$|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$$

$$|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$$

Keadaan $|\Psi^-\rangle$ dikenal sebagai keadaan singlet dan memiliki sifat yang sangat istimewa dalam berbagai aplikasi kuantum.

## Menciptakan Keadaan Terbelit

### Rangkaian Bell

Rangkaian Bell adalah cara standar untuk menciptakan keadaan Bell $|\Phi^+\rangle$ dari keadaan dasar $|00\rangle$:

```
q₀: ───H───●───
           │
q₁: ───────X───
```

Rangkaian ini terdiri dari gerbang Hadamard pada qubit pertama diikuti oleh gerbang CNOT dengan qubit pertama sebagai kontrol dan qubit kedua sebagai target.

Analisis matematisnya adalah sebagai berikut:

1. Keadaan awal: $|00\rangle$
2. Setelah Hadamard pada q₀: $\frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)$
3. Setelah CNOT: $\frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) = |\Phi^+\rangle$

### Rangkaian untuk Keadaan Bell Lainnya

Untuk menciptakan keadaan Bell lainnya, kita dapat memodifikasi rangkaian Bell dasar:

- Untuk $|\Phi^-\rangle$: Tambahkan gerbang Z pada q₁ setelah CNOT
- Untuk $|\Psi^+\rangle$: Tambahkan gerbang X pada q₁ sebelum CNOT
- Untuk $|\Psi^-\rangle$: Tambahkan gerbang X pada q₁ sebelum CNOT dan gerbang Z pada q₁ setelah CNOT

## Sifat-Sifat Entanglement

### Korelasi Non-Lokal

Ketika dua partikel terbelit, pengukuran pada satu partikel secara instan memengaruhi hasil pengukuran pada partikel lain, terlepas dari jarak yang memisahkan keduanya. Inilah yang disebut Einstein sebagai "spooky action at a distance" (aksi hantu pada jarak jauh).

Misalnya, kalau kita memiliki keadaan Bell $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$:

- Jika q₀ diukur dan hasilnya |0⟩, maka q₁ juga akan terukur sebagai |0⟩
- Jika q₀ diukur dan hasilnya |1⟩, maka q₁ juga akan terukur sebagai |1⟩

Korelasi ini bersifat probabilistik tapo sempurna, dan melanggar gagasan klasik kalau informasi tidak dapat berpindah lebih cepat dari kecepatan cahaya.

### Paradoks EPR dan Pertidaksamaan Bell

Albert Einstein, Boris Podolsky, dan Nathan Rosen (EPR) memperkenalkan paradoks yang menantang kelengkapan mekanika kuantum. Mereka berpendapat bahwa entanglement menunjukkan bahwa mekanika kuantum tidak lengkap, dan harus ada "variabel tersembunyi" yang menentukan hasil pengukuran.

John Bell kemudian merumuskan pertidaksamaan matematis (Bell's inequalities) yang malah menunjukkan kalau prediksi mekanika kuantum tidak kompatibel dengan teori variabel tersembunyi lokal. Eksperimen yang dilakukan sejak saat itu secara konsisten melanggar pertidaksamaan Bell, mendukung prediksi mekanika kuantum dan menunjukkan bahwa entanglement adalah fenomena nyata.

Pertidaksamaan Bell yang paling sederhana adalah pertidaksamaan CHSH:

$$|E(a,b) - E(a,b') + E(a',b) + E(a',b')| \leq 2$$

di mana $E(a,b)$ adalah nilai ekspektasi dari pengukuran dengan setting $a$ dan $b$.

Mekanika kuantum memprediksi nilai maksimum $2\sqrt{2} \approx 2.82$, yang telah dikonfirmasi oleh berbagai eksperimen.

## Pengukuran pada Sistem Terbelit

### Proyeksi Keadaan

Ketika pengukuran dilakukan pada satu qubit dari pasangan terbelit, keadaan kedua qubit akan mengalami "proyeksi" atau "kolaps" sesuai dengan hasil pengukuran qubit pertama.

Misalnya, untuk keadaan Bell $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$:

- Jika q₀ diukur dalam basis komputasi dan hasilnya |0⟩, keadaan sistem akan berubah menjadi |00⟩
- Jika q₀ diukur dalam basis komputasi dan hasilnya |1⟩, keadaan sistem akan berubah menjadi |11⟩

### Matriks Densitas dan Entanglement

Matriks densitas adalah cara yang berguna untuk menganalisis entanglement, terutama dalam sistem campuran. Untuk sistem murni dua qubit, matriks densitasnya adalah:

$$\rho_{AB} = |\psi_{AB}\rangle\langle\psi_{AB}|$$

Matriks densitas tereduksi dari subsistem A diperoleh dengan melakukan partial trace terhadap subsistem B:

$$\rho_A = \text{Tr}_B(\rho_{AB})$$

Jika keadaan terbelit, maka $\rho_A$ dan $\rho_B$ akan menjadi keadaan campuran, bukan keadaan murni.

### Ukuran Entanglement

Beberapa ukuran entanglement yang umum digunakan:

1. **Entropi von Neumann**: $S(\rho_A) = -\text{Tr}(\rho_A \log_2 \rho_A)$
   - Untuk keadaan terbelit maksimal, $S(\rho_A) = 1$
   - Untuk keadaan terpisah, $S(\rho_A) = 0$

2. **Concurrence**: $C(\rho) = \max\{0, \lambda_1 - \lambda_2 - \lambda_3 - \lambda_4\}$
   - Di mana $\lambda_i$ adalah akar kuadrat dari eigenvalue dari $\rho(\sigma_y \otimes \sigma_y)\rho^*(\sigma_y \otimes \sigma_y)$ dalam urutan menurun

3. **Negativity**: Jumlah eigenvalue negatif dari partial transpose matriks densitas

## Aplikasi Entanglement dalam Komputasi Kuantum

### Teleportasi Kuantum

Teleportasi kuantum memungkinkan transfer keadaan kuantum dari satu lokasi ke lokasi lain menggunakan pasangan terbelit dan komunikasi klasik. Protokolnya melibatkan:

1. Persiapan pasangan terbelit antara pengirim (Obama) dan penerima (Nabila)
2. Pengirim melakukan operasi Bell pada qubit yang akan diteleportasikan dan bagian pasangan terbelitnya
3. Pengirim mengukur kedua qubit dan mengirimkan hasil pengukuran (2 bit klasik) ke penerima
4. Penerima melakukan koreksi pada qubitnya berdasarkan informasi yang diterima

Rangkaian kuantum untuk teleportasi:

```
         ┌───┐     ┌─┐
q₀: ──■──┤ H ├──■──┤M├───────────────── (qubit yang diteleportasikan)
     │  └───┘  │  └─┘
q₁: ─┼─────────┼────┤M├─────────────── (qubit Obama dari pasangan terbelit)
     │         │    └─┘  ┌───┐ ┌───┐
q₂: ─X─────────X─────────┤ X ├─┤ Z ├─ (qubit Nabila dari pasangan terbelit)
                          └───┘ └───┘
                           │     │
                      kontrol kontrol
                       dari   dari
                      hasil  hasil
                       q₀     q₁
```

### Kriptografi Kuantum (QKD)

Protokol BB84 dan E91 memanfaatkan entanglement untuk membuat kunci kriptografi yang aman secara teoritis. E91 secara khusus menggunakan pasangan terbelit untuk mendeteksi kehadiran penyadap.

### Komputasi Kuantum Terdistribusi

Entanglement memungkinkan komputasi kuantum terdistribusi, dimana sumber daya kuantum dapat dibagi dan dioperasikan dari lokasi yang berbeda.

## Entanglement Multi-Partite

### Keadaan GHZ

Keadaan Greenberger Horne Zeilinger (GHZ) adalah generalisasi keadaan Bell untuk tiga atau lebih qubit:

$$|GHZ\rangle = \frac{1}{\sqrt{2}}(|00...0\rangle + |11...1\rangle)$$

### Keadaan W

Keadaan W adalah jenis entanglement multi partite lain dengan sifat keterberadaan yang berbeda:

$$|W\rangle = \frac{1}{\sqrt{n}}(|10...0\rangle + |01...0\rangle + ... + |00...1\rangle)$$

### Klasifikasi Entanglement Multi-Partite

Entanglement multi partite memiliki struktur yang lebih kaya dan kompleks dibandingkan entanglement dua partite. Klasifikasi lengkap masih menjadi subjek penelitian aktif.

## Algoritma Kuantum yang Memanfaatkan Entanglement

### Algoritma Deutsch-Jozsa

Algoritma ini memanfaatkan superposisi dan entanglement untuk menentukan apakah fungsi boolean bersifat konstan atau seimbang dengan satu evaluasi.

### Algoritma Grover

Algoritma pencarian Grover menciptakan entanglement antar qubit yang memungkinkan amplifikasi amplitudo keadaan target, mempercepat pencarian dalam database yg tidak terurut.

### Algoritma Shor

Algoritma Shor untuk faktorisasi bilangan besar memanfaatkan entanglement dalam transformasi Fourier kuantum, yang merupakan bagian kunci dari algoritma.


# Materi 3: Interferensi Kuantum
1. Apa Itu Interferensi Kuantum? Dalam mekanika kuantum, interferensi terjadi ketika gelombang kuantum saling memperkuat atau saling membatalkan.

➡ Interferensi Konstruktif → Menguatkan probabilitas hasil tertentu. ➡ Interferensi Destruktif → Menghilangkan probabilitas hasil tertentu.

💡 Analogi:

Bayangkan dua orang melempar batu ke kolam air.
Jika gelombang air bertemu dalam fase yang sama, gelombang akan semakin besar (interferensi konstruktif). Jika gelombang bertemu dalam fase berlawanan, mereka akan saling membatalkan (interferensi destruktif). Dalam komputasi kuantum, interferensi digunakan untuk meningkatkan kemungkinan jawaban yang benar dan mengurangi kemungkinan jawaban yang salah.

2️. Gerbang Kuantum yang Menggunakan Interferensi Beberapa gerbang kuantum memanfaatkan interferensi kuantum, di antaranya:

Hadamard (H-Gate) → Membuat superposisi dan menciptakan pola interferensi. Gerbang Fase (S, T, dan Z-Gate) → Mengubah fase qubit untuk mengontrol interferensi. Gerbang Hadamard Ganda (H-Gate Dua Kali) → Membatalkan superposisi dan mengembalikan qubit ke keadaan awal.

```python
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator  
from qiskit import transpile

# membuat quantum circuit dengan 1 qubit
qc = QuantumCircuit(1)

# gerbang Hadamard dua kali
qc.h(0)  # hadamard pertama
qc.h(0)  # hadamard kedua

# pengukuran
qc.measure_all()

# ini sirkuitnya
print(qc)

# simulator untuk menjalankan sirkuit
simulator = AerSimulator()
compiled_circuit = transpile(qc, simulator)  
result = simulator.run(compiled_circuit, shots=1000).result()
print(result.get_counts())
```
result :
```
        ┌───┐┌───┐ ░ ┌─┐
     q: ┤ H ├┤ H ├─░─┤M├
        └───┘└───┘ ░ └╥┘
meas: 1/══════════════╩═
                      0 
{'0': 1000}
```
Bagaimana jika hadamard berkali kali?
```python
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator
from qiskit import transpile

qc = QuantumCircuit(1)

# menerapkan Hadamard sebanyak 6 kali
for _ in range(1):
    qc.h(0)

# Tambahkan pengukuran
qc.measure_all()

# mencetak sirkuitnya
print(qc)

# menggunakan simulator untuk menjalankan sirkuit
simulator = AerSimulator()
compiled_circuit = transpile(qc, simulator)
result = simulator.run(compiled_circuit, shots=1000).result()

print(result.get_counts())
```
result :
```
        ┌───┐ ░ ┌─┐
     q: ┤ H ├─░─┤M├
        └───┘ ░ └╥┘
meas: 1/═════════╩═
                 0 
{'1': 493, '0': 507}
```
🔹 Hadamard 1x → Membuat superposisi.

🔹 Hadamard 2x → Mengembalikan qubit ke keadaan awal (|0⟩).

🔹 Hadamard 3x → Sama seperti 1x (superposisi).

🔹 Hadamard 4x → Sama seperti 2x (kembali ke |0⟩).

🔹 Hadamard 6x → Sama seperti 2x dan 4x, hasilnya tetap |0⟩.

 jadi, kalau Hadamard diterapkan genap kali (2, 4, 6, 8, ...), qubit kembali ke keadaan awal. alias Hadamard seperti saklar.


# Materi 4: Algoritma Kuantum (Deutsch & Grover)
Komputer kuantum bisa menyelesaikan masalah tertentu lebih cepat dari komputer klasik. Di sini, kita akan belajar dua algoritma kuantum penting:

Algoritma Deutsch → Menentukan tipe fungsi dalam 1 langkah saja.
Algoritma Grover → Mencari data lebih cepat dengan √N pencarian (daripada N pencarian di komputer klasik). 
Algoritma Deutsch
- Masalah yang Diselesaikan Kita punya fungsi f(x) yang menerima 0 atau 1, lalu mengembalikan 0 atau 1.
- Fungsi bisa bersifat konstan (hasil selalu sama) atau seimbang (hasil bisa berbeda).
- Fungsi f(x) f(0) f(1) Tipe f₁(x) 0 0 Konstan f₂(x) 1 1 Konstan f₃(x) 0 1 Seimbang f₄(x) 1 0 Seimbang Komputer klasik perlu cek dua kali (f(0) dan f(1)). Komputer kuantum hanya butuh 1 langkah dengan superposisi & interferensi kuantum saja

```python
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer 

# membuat quantum circuit dengan 2 qubit (1 input, 1 output)
qc = QuantumCircuit(2)

# menerapkan Hadamard ke kedua qubit
qc.h(0)
qc.h(1)

# menerapkan gerbang CNOT untuk membuat fungsi seimbang
qc.cx(0, 1)  # fungsi ini membuat f(x) seimbang

# menerapkan Hadamard lagi ke qubit pertama
qc.h(0)

# menambahkan pengukuran
qc.measure_all()

# ini sirkuitnya
print(qc)

# menggunakan simulator Aer
simulator = Aer.get_backend('aer_simulator')
compiled_circuit = transpile(qc, simulator)

# simulasi dengan execute
result = simulator.run(compiled_circuit, shots=1000).result()

print(result.get_counts())
```
result
```

        ┌───┐     ┌───┐ ░ ┌─┐   
   q_0: ┤ H ├──■──┤ H ├─░─┤M├───
        ├───┤┌─┴─┐└───┘ ░ └╥┘┌─┐
   q_1: ┤ H ├┤ X ├──────░──╫─┤M├
        └───┘└───┘      ░  ║ └╥┘
meas: 2/═══════════════════╩══╩═
                           0  1 
{'00': 529, '10': 471}
```

- H|0⟩ = (|0⟩ + |1⟩)/√2
- H|1⟩ = (|0⟩ - |1⟩)/√2

Dalam bentuk matriks, gerbang Hadamard direpresentasikan seperti ini:

```
H = 1/√2 [ 1  1 ]
         [ 1 -1 ]
```

### Gerbang CNOT (Controlled-NOT)

Gerbang CNOT adalah gerbang kuantum dua qubit yang melakukan operasi NOT pada qubit target kalau qubit kontrol berada dalam keadaan |1⟩. Secara matematis:

- CNOT|00⟩ = |00⟩
- CNOT|01⟩ = |01⟩
- CNOT|10⟩ = |11⟩
- CNOT|11⟩ = |10⟩

Matriks yang merepresentasikan gerbang CNOT adalah:

```
CNOT = [ 1 0 0 0 ]
       [ 0 1 0 0 ]
       [ 0 0 0 1 ]
       [ 0 0 1 0 ]
```

Gerbang CNOT itu sangat penting karena:
1. Menciptakan entanglement (keterkaitan) antar qubit
2. Bersama dengan gerbang satu qubit (seperti Hadamard), dapat membentuk set gerbang universal untuk komputasi kuantum

## Algoritma Deutsch

Algoritma Deutsch adalah salah satu algoritma kuantum yang paling sederhana yang mendemonstrasikan keunggulan kuantum dibandingkan komputasi klasik. Algoritma ini mampu menentukan apakah suatu fungsi boolean *f*: {0,1} → {0,1} bersifat konstan atau seimbang dengan hanya dgn satu evaluasi fungsi.

### Tahapan Algoritma Deutsch

1. Inisialisasi dua qubit dalam keadaan |0⟩|1⟩
2. Terapkan gerbang Hadamard pada kedua qubit, menghasilkan keadaan (|0⟩ + |1⟩)/√2 ⊗ (|0⟩ - |1⟩)/√2
3. Terapkan oracle U<sub>f</sub> yang mengkodifikasi fungsi f: U<sub>f</sub>|x⟩|y⟩ = |x⟩|y ⊕ f(x)⟩
4. Terapkan gerbang Hadamard pada qubit pertama
5. Ukur qubit pertama. Jika hasilnya |0⟩, maka fungsi f bersifat konstan; jika |1⟩, maka fungsi f bersifat seimbang

### Rangkaian Kuantum Algoritma Deutsch

```
|0⟩ ─── H ─── U<sub>f</sub> ─── H ─── Measurement
|1⟩ ─── H ───────────────────── (tidak diukur)
```

### Peranan CNOT dan Hadamard dalam Algoritma Deutsch

- **Gerbang Hadamard**: Membuat superposisi yang memungkinkan evaluasi paralel pada semua input fungsi sekaligus
- **CNOT**: Digunakan sebagai bagian dari implementasi oracle U<sub>f</sub>, terutama untuk fungsi f(x) = x atau f(x) = x ⊕ 1

## Algoritma Grover

Algoritma Grover adalah algoritma pencarian kuantum yg dapat menemukan elemen daoam database tidak terurut dengan kompleksitas O(√N), dibandingkan dengan algoritma komputer klasik yang memerlukan O(N) operasi.

### Tahapan Algoritma Grover

1. Inisialisasi n qubit dalam keadaan |0⟩ dan terapkan gerbang Hadamard untuk membuat superposisi merata dari semua kemungkinan keadaan:
   |ψ⟩ = 1/√N ∑<sub>x=0</sub><sup>N-1</sup> |x⟩

2. Ulangi langkah-langkah berikut sebanyak O(√N) kali:
   - Terapkan operator oracle (O) yang membalik amplitudo keadaan target
   - Terapkan operator difusi (D) yang membalik amplitudo semua keadaan terhadap rata-rata amplitudo

3. Ukur register qubit untuk mendapatkan keadaan target dengan probabilitas tinggi

### Rangkaian Kuantum Algoritma Grover

```
|0⟩⊗ⁿ ─── H⊗ⁿ ─── (O─D)^r ─── Measurement
```

di mana r ≈ π/4 · √N adalah jumlah iterasi optimal.

### Peranan CNOT dan Hadamard dalam Algoritma Grover

- **Gerbang Hadamard**: Digunakan untuk menciptakan superposisi awal yg merata dari semua basis komputasi, serta sebagai komponen dalam operator bagian difusi (D)
- **CNOT**: ini diigunakan dalam implementasi oracle buat mendeteksi keadaan target dan dalam operator difusi untuk mengimplementasikan refleksinya



# Materi 5 : Analisis Rangkaian: Hadamard → CNOT → Hadamard

Dalam dokumen ini, kita akan menganalisis rangkaian kuantum dengan urutan operasi sebagai berikut:
1. Gerbang Hadamard pada q₀ (menciptakan superposisi)
2. Gerbang CNOT dengan q₀ sebagai kontrol dan q₁ sebagai target
3. Gerbang Hadamard pada q₁

## Diagram Rangkaian

```
q₀: ─────H─────●─────────────
                │
q₁: ─────────────X─────H─────
```

## Representasi Matematis Gerbang
```python
from qiskit import QuantumCircuit, transpile, Aer, execute

# 🔹 Membuat quantum circuit
qc = QuantumCircuit(2, 2)

qc.h(0)        # Hadamard di q0 → superposisi
qc.cx(0, 1)    # CNOT (q0 mengontrol q1) → entanglement
qc.h(1)        # Hadamard kedua di q1
qc.measure(0, 0)
qc.measure(1, 1)

# 🔹 Simulasikan eksperimen
simulator = Aer.get_backend('aer_simulator')

compiled_qc = transpile(qc, simulator)

result = simulator.run(compiled_qc, shots=1000).result()

# 🔹 Tampilkan hasilnya
print("Hasil pengukuran:")
print(result.get_counts())


```

Result :
```
{'00': ~500, '10': ~500}  # (kurang lebih seimbang)
```

### Gerbang Hadamard (H)

$$H = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

Transformasi basis:
$$H|0\rangle = \frac{|0\rangle + |1\rangle}{\sqrt{2}}$$
$$H|1\rangle = \frac{|0\rangle - |1\rangle}{\sqrt{2}}$$

### Gerbang CNOT

$$\text{CNOT} = \begin{pmatrix} 
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 
\end{pmatrix}$$

Transformasi basis:
$$\text{CNOT}|00\rangle = |00\rangle$$
$$\text{CNOT}|01\rangle = |01\rangle$$
$$\text{CNOT}|10\rangle = |11\rangle$$
$$\text{CNOT}|11\rangle = |10\rangle$$

## Penjelassn Langkah demi Langkah

### Keadaan Awal
Kita mulai dengan keadaan awal dua qubit:
$$|\psi_0\rangle = |00\rangle$$

### Langkah 1: Hadamard pada q₀
Aplikasi gerbang Hadamard pada qubit pertama (q₀):

$$|\psi_1\rangle = (H \otimes I)|00\rangle = (H|0\rangle) \otimes (I|0\rangle)$$

Substitusi dengan definisi H:
$$|\psi_1\rangle = \frac{|0\rangle + |1\rangle}{\sqrt{2}} \otimes |0\rangle = \frac{|00\rangle + |10\rangle}{\sqrt{2}}$$

Pada titik ini, kita memiliki superposisi dari dua keadaan basis: $|00\rangle$ dan $|10\rangle$ dengan amplitudo yang sama.

### Langkah 2: CNOT dengan q₀ sebagai kontrol dan q₁ sebagai target
Aplikasi gerbang CNOT:

$$|\psi_2\rangle = \text{CNOT} \cdot |\psi_1\rangle = \text{CNOT} \cdot \frac{|00\rangle + |10\rangle}{\sqrt{2}}$$

Kita dapat menghitung ini suku per suku:
$$|\psi_2\rangle = \frac{\text{CNOT}|00\rangle + \text{CNOT}|10\rangle}{\sqrt{2}} = \frac{|00\rangle + |11\rangle}{\sqrt{2}}$$

Keadaan ini adalah keadaan Bell $|\Phi^+\rangle$, salah satu dari keadaan terbelit maksimal.

### Langkah 3: Hadamard pada q₁
Mengaplikasi gerbang Hadamard pada qubit kedua (q₁):

$$|\psi_3\rangle = (I \otimes H)|\psi_2\rangle = (I \otimes H) \cdot \frac{|00\rangle + |11\rangle}{\sqrt{2}}$$

Kita dapat memecah perhitungan ini:

$$(I \otimes H)|00\rangle = |0\rangle \otimes H|0\rangle = |0\rangle \otimes \frac{|0\rangle + |1\rangle}{\sqrt{2}} = \frac{|00\rangle + |01\rangle}{\sqrt{2}}$$

$$(I \otimes H)|11\rangle = |1\rangle \otimes H|1\rangle = |1\rangle \otimes \frac{|0\rangle - |1\rangle}{\sqrt{2}} = \frac{|10\rangle - |11\rangle}{\sqrt{2}}$$

Sehingga:

$$|\psi_3\rangle = \frac{1}{\sqrt{2}} \left( \frac{|00\rangle + |01\rangle}{\sqrt{2}} + \frac{|10\rangle - |11\rangle}{\sqrt{2}} \right)$$

$$|\psi_3\rangle = \frac{1}{2} \left( |00\rangle + |01\rangle + |10\rangle - |11\rangle \right)$$

## Analisis Probabilitas Pengukuran

Setelah rangkaiannya lengkap, keadaan akhir sistemnya jadi:

$$|\psi_\text{final}\rangle = \frac{1}{2} \left( |00\rangle + |01\rangle + |10\rangle - |11\rangle \right)$$

Kalau kita melakukan pengukuran pada kedua qubit dalam basis komputasi standar, probabilitas mendapatkan masing2 hasil adalah:

$$P(|00\rangle) = \left| \frac{1}{2} \right|^2 = \frac{1}{4}$$
$$P(|01\rangle) = \left| \frac{1}{2} \right|^2 = \frac{1}{4}$$
$$P(|10\rangle) = \left| \frac{1}{2} \right|^2 = \frac{1}{4}$$
$$P(|11\rangle) = \left| -\frac{1}{2} \right|^2 = \frac{1}{4}$$

## Mendapatkan Hasil Hanya |00⟩ dan |10⟩

### Menggunakan Pengukuran dan Post-Selection

Untuk mendapatkan hanya keadaan $|00\rangle$ dan $|10\rangle$, kita bisa mengukur qubit kedua (q₁) terlebih dahulu.

Kalau kita mengukur q₁ dan mendapatkan hasil $|0\rangle$, keadaan akan menjadi:

$$|\psi_\text{collapse}\rangle = \frac{|00\rangle + |10\rangle}{\sqrt{2}}$$

Ini terjadi karena saat mengukur q₁ dan mendapatkan $|0\rangle$, keadaan akan mengalami kolaps menjadi superposisi dari semua keadaan yang memiliki q₁ = $|0\rangle$, yaitu $|00\rangle$ dan $|10\rangle$.

Probabilitas mendapatkan q₁ = $|0\rangle$ adalah:
$$P(q_1 = |0\rangle) = P(|00\rangle) + P(|10\rangle) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$$

### Menggunakan Modifikasi Rangkaian

Alternatif lain, kalau tujuan kita hanya ingin mendapatkan superposisi dari $|00\rangle$ dan $|10\rangle$, kita bisa menggunakan rangkaian yang lebih sederhana:

```
q₀: ─────H─────
q₁: ─────────── (tetap |0⟩)
```

Rangkaian ini langsung menghasilkan keadaan:
$$|\psi\rangle = \frac{|00\rangle + |10\rangle}{\sqrt{2}}$$

## Kesimpulan

Rangkaian Hadamard-CNOT-Hadamard menghasilkan keadaan:
$$|\psi\rangle = \frac{1}{2} \left( |00\rangle + |01\rangle + |10\rangle - |11\rangle \right)$$

Yang memiliki amplitudo yang sama untuk semua basis komputasi (meskipun dengan fase berbeda untuk $|11\rangle$).

Untuk mendapatkan hanya keadaan $|00\rangle$ dan $|10\rangle$:
1. Lakukan pengukuran pada q₁ dan pilih hasil $|0\rangle$ (post-selection)
2. Atau gunakan rangkaian yang lebih sederhana dengan hanya mengaplikasikan Hadamard pada q₀

