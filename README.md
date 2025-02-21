## 1. Rumus Qubit & Superposisi
Qubit bisa dituliskan dalam bentuk:

∣
𝜓
⟩
=
𝛼
∣
0
⟩
+
𝛽
∣
1
⟩
∣ψ⟩=α∣0⟩+β∣1⟩
artinya:

∣
0
⟩
∣0⟩ dan 
∣
1
⟩
∣1⟩ adalah dua keadaan dasar (kayak 0 dan 1 di komputer biasa).

𝛼
α dan 
𝛽
β adalah angka yg menunjukkan seberapa besar peluang qubit jadi 0 atau 1 ketika diukur.

Probabilitas total harus 1, jadi:

∣
𝛼
∣
2
+
∣
𝛽
∣
2
=
1
∣α∣ 
2
 +∣β∣ 
2
 =1
Contoh rumus dalam angka
kalau:

∣
𝜓
⟩
=
1
2
∣
0
⟩
+
1
2
∣
1
⟩
∣ψ⟩= 
2
​
 
1
​
 ∣0⟩+ 
2
​
 
1
​
 ∣1⟩
maka:

𝛼
=
1
2
α= 
2
​
 
1
​
  → peluang 0 adalah 
(
1
2
)
2
=
0.5
( 
2
​
 
1
​
 ) 
2
 =0.5 (50%).
𝛽
=
1
2
β= 
2
​
 
1
​
  → peluang 1 juga 50%.
jadi kalau diukur banyak kali, setengahnya bakal jadi 0, setengahnya bakal jadi 1.

2. Gerbang Hadamard (H-Gate) untuk Superposisi
Hadamard adalah gerbang kuantum yg mengubah |0⟩ atau |1⟩ jadi superposisi.

rumus dalam bentuk matriks:

𝐻
=
1
2
[
1
1
1
−
1
]
H= 
2
​
 
1
​
 [ 
1
1
​
  
1
−1
​
 ]
kalau di terapkan ke |0⟩, hasilnya:

𝐻
∣
0
⟩
=
1
2
(
∣
0
⟩
+
∣
1
⟩
)
H∣0⟩= 
2
​
 
1
​
 (∣0⟩+∣1⟩)
(jadi superposisi dgn peluang 50% jadi 0 dan 50% jadi 1).

kalau di terapkan ke |1⟩, hasilnya:

𝐻
∣
1
⟩
=
1
2
(
∣
0
⟩
−
∣
1
⟩
)
H∣1⟩= 
2
​
 
1
​
 (∣0⟩−∣1⟩)
(ini juga superposisi, tapi dengan perbedaan fase).



### Kode Python :
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
