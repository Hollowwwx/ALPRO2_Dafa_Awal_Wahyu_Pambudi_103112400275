<h1 align="center">Laporan Praktikum Modul 7 <br>Struct & Array</h1>
<p align="center">Dafa Awal Wahyu Pambudi - 103112400275</p>
## Unguided

### Soal 1
Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Gunakan tipe bentukan titik untuk menyimpan koordinat, dan tipe bentukan lingkaran untuk menyimpan titik pusat lingkaran dan radiusnya.
Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat.
Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>1 1 5<br>8 8 4<br>2 2</td>
    <td>Titik di dalam lingkaran 1</td>
  </tr>
  <tr>
    <td>2</td>
    <td>1 2 3<br>4 5 6<br>7 8</td>
    <td>Titik di dalam lingkaran 2</td>
  </tr>
  <tr>
    <td>3</td>
    <td>5 10 15<br>-15 4 20<br>0 0</td>
    <td>Titik di dalam lingkaran 1 dan 2</td>
  </tr>
  <tr>
    <td>4</td>
    <td>1 1 5<br>8 8 4<br>15 20</td>
    <td>Titik di dalam lingkaran 1 dan 2</td>
  </tr>
</table>

```go
package main

import (
	"fmt"
	"math"
)

type Titik struct {
	x, y int
}

type Lingkaran struct {
	pusat  Titik
	radius int
}

func jarak(p, q Titik) float64 {
	return math.Sqrt(math.Pow(float64(p.x-q.x), 2) + math.Pow(float64(p.y-q.y), 2))
}

func didalam(c Lingkaran, p Titik) bool {
	return jarak(c.pusat, p) <= float64(c.radius)
}

func main() {
	var (
		cx1, cy1, r1 int
		cx2, cy2, r2 int
		x, y         int
	)

	fmt.Scan(&cx1, &cy1, &r1)
	fmt.Scan(&cx2, &cy2, &r2)
	fmt.Scan(&x, &y)

	lingkaran1 := Lingkaran{Titik{cx1, cy1}, r1}
	lingkaran2 := Lingkaran{Titik{cx2, cy2}, r2}
	titik := Titik{x, y}

	didalam1 := didalam(lingkaran1, titik)
	didalam2 := didalam(lingkaran2, titik)

	if didalam1 && didalam2 {
		fmt.Println("Titik di dalam lingkaran 1 dan 2")
	} else if didalam1 {
		fmt.Println("Titik di dalam lingkaran 1")
	} else if didalam2 {
		fmt.Println("Titik di dalam lingkaran 2")
	} else {
		fmt.Println("Titik di luar lingkaran 1 dan 2")
	}
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go 
1 1 5 
8 8 4 
2 2 
Titik di dalam lingkaran 1 
PS D:\Golang SMT2
```
Program Go ini menentukan posisi sebuah titik terhadap dua buah lingkaran dengan cara mengecek apakah titik tersebut berada di dalam salah satu atau kedua lingkaran. Program menggunakan dua struct, yaitu `Titik` untuk menyimpan koordinat titik dan `Lingkaran` yang berisi titik pusat dan jari-jari. Fungsi `jarak` menghitung jarak antara dua titik menggunakan rumus Euclidean, sedangkan fungsi `didalam` memeriksa apakah jarak titik ke pusat lingkaran kurang dari atau sama dengan jari-jari lingkaran. Di fungsi `main`, data dua lingkaran dan satu titik dibaca dari input, kemudian dicek apakah titik tersebut berada di dalam lingkaran pertama, kedua, keduanya, atau di luar keduanya, lalu hasilnya dicetak sesuai kondisi tersebut.

---
### Soal 2
Sebuah array digunakan untuk menampung sekumpulan bilangan bulat. Buatlah program
yang digunakan untuk mengisi array tersebut sebanyak N elemen nilai. Asumsikan array
memiliki kapasitas penyimpanan data sejumlah elemen tertentu. Program dapat
menampilkan beberapa informasi berikut:
a. Menampilkan keseluruhan isi dari array.
b. Menampilkan elemen-elemen array dengan indeks ganjil saja.
c. Menampilkan elemen-elemen array dengan indeks genap saja (asumsi indek ke-0 adalah
genap).
d. Menampilkan elemen-elemen array dengan indeks kelipatan bilangan x. x bisa diperoleh
dari masukan pengguna.
e. Menghapus elemen array pada indeks tertentu, asumsi indeks yang hapus selalu valid.
Tampilkan keseluruhan isi dari arraynya, pastikan data yang dihapus tidak tampil
f. Menampilkan rata-rata dari bilangan yang ada di dalam array.
g. Menampilkan standar deviasi atau simpangan baku dari bilangan yang ada di dalam array
tersebut.
h. Menampilkan frekuensi dari suatu bilangan tertentu di dalam array yang telah diisi
tersebut.

```go
package main

import (
	"fmt"
	"math"
)

func isiArray(jumlah int) []int {
	array := make([]int, jumlah)
	for i := 0; i < jumlah; i++ {
		fmt.Printf("Masukkan elemen ke-%d: ", i+1)
		fmt.Scan(&array[i])
	}
	return array
}

func ganjilGenap(array []int) ([]int, []int) {
	genap, ganjil := []int{}, []int{}
	for i := 0; i < len(array); i++ {
		if i%2 == 0 {
			genap = append(genap, array[i])
		} else {
			ganjil = append(ganjil, array[i])
		}
	}
	return genap, ganjil
}

func kelipatan(array []int, bilangan int) []int {
	hasil := []int{}
	for i := bilangan; i < len(array); i += bilangan {
		hasil = append(hasil, array[i])
	}
	return hasil
}

func hapusIndeks(array []int, indeks int) []int {
	if indeks < 0 || indeks >= len(array) {
		fmt.Println("Indeks tidak ditemukan")
		return array
	}
	return append(array[:indeks], array[indeks+1:]...)
}

func rataRata(array []int) float64 {
	total := 0
	for i := 0; i < len(array); i++ {
		total += array[i]
	}
	return float64(total) / float64(len(array))
}

func simpanganBaku(array []int) float64 {
	rata := rataRata(array)
	var jumlah float64
	for i := 0; i < len(array); i++ {
		jumlah += math.Pow(float64(array[i])-rata, 2)
	}
	return math.Sqrt(jumlah / float64(len(array)))
}

func frekuensi(array []int, angka int) int {
	jumlah := 0
	for i := 0; i < len(array); i++ {
		if array[i] == angka {
			jumlah++
		}
	}
	return jumlah
}

func main() {
	var jumlah, bilangan, indeks, angka int

	fmt.Print("Masukkan jumlah elemen array: ")
	fmt.Scan(&jumlah)

	if jumlah <= 0 {
		fmt.Println("Program berhenti karena jumlah elemen adalah <=0.")
		return
	}

	array := isiArray(jumlah)
	fmt.Println("\nIsi array yang dimasukkan:", array)
	fmt.Printf("Rata-rata: %.2f\n", rataRata(array))
	fmt.Printf("Simpangan baku: %.2f\n", simpanganBaku(array))

	genap, ganjil := ganjilGenap(array)
	fmt.Println("\nElemen dengan indeks genap:", genap)
	fmt.Println("Elemen dengan indeks ganjil:", ganjil)

	fmt.Print("\nMasukkan nilai kelipatan x: ")
	fmt.Scan(&bilangan)
	hasilKelipatan := kelipatan(array, bilangan)
	fmt.Println("Elemen dengan indeks kelipatan", bilangan, ":", hasilKelipatan)

	fmt.Print("\nMasukkan indeks yang ingin dihapus: ")
	fmt.Scan(&indeks)
	array = hapusIndeks(array, indeks)
	fmt.Println("Array setelah penghapusan:", array)

	fmt.Printf("\nRata-rata setelah penghapusan: %.2f\n", rataRata(array))
	fmt.Printf("Simpangan setelah penghapusan: %.2f\n", simpanganBaku(array))

	fmt.Print("\nMasukkan bilangan untuk mencari frekuensi: ")
	fmt.Scan(&angka)
	fmt.Printf("Frekuensi bilangan %d dalam array: %d\n", angka, frekuensi(array, angka))
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
Masukkan jumlah elemen array: 5 
Masukkan elemen ke-1: 1 
Masukkan elemen ke-2: 2 
Masukkan elemen ke-3: 3 
Masukkan elemen ke-4: 4 
Masukkan elemen ke-5: 5 
Isi array yang dimasukkan: [1 2 3 4 5] 
Rata-rata: 3.00 
Simpangan baku: 1.41 
Elemen dengan indeks genap: [135] 
Elemen dengan indeks ganjil: [24] 
Masukkan nilai kelipatan x: 2 
Elemen dengan indeks kelipatan 2: [35] 
Masukkan indeks yang ingin dihapus: 0 
Array setelah penghapusan: [2 3 4 5] 
Rata-rata setelah penghapusan: 3.50 
Simpangan setelah penghapusan: 1.12 
Masukkan bilangan untuk mencari frekuensi: 2 
Frekuensi bilangan 2 dalam array: 1 
PS D:\Golang SMT2>
```
Program Go ini melakukan berbagai operasi statistik dan manipulasi pada array bilangan bulat yang dimasukkan oleh pengguna. Pertama, program meminta jumlah elemen array lalu mengisi array dengan nilai-nilai dari input. Program menghitung dan menampilkan rata-rata serta simpangan baku dari array tersebut. Kemudian, array dipisah menjadi dua berdasarkan indeks genap dan ganjil. Pengguna dapat memasukkan nilai kelipatan tertentu untuk menampilkan elemen array pada indeks yang merupakan kelipatan nilai tersebut. Selanjutnya, pengguna dapat menghapus elemen berdasarkan indeks, dan program akan memperbarui serta menampilkan rata-rata dan simpangan baku dari array hasil. Terakhir, pengguna dapat memasukkan angka untuk menghitung berapa kali angka tersebut muncul (frekuensinya) dalam array.

---
### Soal 3
Sebuah program digunakan untuk menyimpan dan menampilkan nama-nama klub yang memenangkan pertandingan bola pada suatu grup pertandingan. Buatlah program yang digunakan untuk merekap skor pertandingan bola 2 buah klub bola yang berlaga. Pertama-tama program meminta masukan nama-nama klub yang bertanding, kemudian program meminta masukan skor hasil pertandingan kedua klub tersebut. Yang disimpan dalam array adalah nama-nama klub yang menang saja. Proses input skor berhenti ketika skor salah satu atau kedua klub tidak valid (negatif). Di akhir program, tampilkan daftar klub yang memenangkan pertandingan. Perhatikan sesi interaksi pada contoh berikut ini (teks bergaris bawah adalah input/read)

<table border="1">
  <tr>
    <th>Teks</th>
    <th>Masukan</th>
  </tr>
  <tr>
    <td>Klub A:</td>
    <td>MU</td>
  </tr>
  <tr>
    <td>Klub B:</td>
    <td>INTER</td>
  </tr>
  <tr>
    <td>Pertandingan 1</td>
    <td>2 0</td>
  </tr>
  <tr>
    <td>Pertandingan 2</td>
    <td>1 2</td>
  </tr>
  <tr>
    <td>Pertandingan 3</td>
    <td>2 2</td>
  </tr>
  <tr>
    <td>Pertandingan 4</td>
    <td>0 1</td>
  </tr>
  <tr>
    <td>Pertandingan 5</td>
    <td>3 2</td>
  </tr>
  <tr>
    <td>Pertandingan 6</td>
    <td>1 0</td>
  </tr>
  <tr>
    <td>Pertandingan 7</td>
    <td>5 2</td>
  </tr>
  <tr>
    <td>Pertandingan 8</td>
    <td>2 3</td>
  </tr>
  <tr>
    <td>Pertandingan 9</td>
    <td>-1 2</td>
  </tr>
</table>

```go
package main

import (
	"fmt"
)

func main() {
	var klubA, klubB string
	var skorA, skorB int
	var hasil []string

	fmt.Print("Klub A: ")
	fmt.Scan(&klubA)
	fmt.Print("Klub B: ")
	fmt.Scan(&klubB)

	pertandingan := 1
	for {
		fmt.Printf("Pertandingan %d: ", pertandingan)
		fmt.Scan(&skorA, &skorB)

		if skorA < 0 || skorB < 0 {
			break
		}

		if skorA > skorB {
			hasil = append(hasil, klubA)
		} else if skorA < skorB {
			hasil = append(hasil, klubB)
		} else {
			hasil = append(hasil, "Draw")
		}

		pertandingan++
	}

	for i, pemenang := range hasil {
		fmt.Printf("Hasil %d: %s\n", i+1, pemenang)
	}

	fmt.Println("Pertandingan selesai")
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
Klub A: MU 
Klub B: INTER 
Pertandingan 1: 20 
Pertandingan 2: 1 2 
Pertandingan 3: 22 
Pertandingan 4: 01 
Pertandingan 5: 32 
Pertandingan 6: 10 
Pertandingan 7: 52 
Pertandingan 8: 23 
Pertandingan 9: -1 2 
Hasil 1: MU 
Hasil 2: INTER 
Hasil 3: Draw 
Hasil 4: INTER 
Hasil 5: MU 
Hasil 6: MU 
Hasil 7: MU 
Hasil 8: INTER 
Pertandingan selesai 
PS D:\Golang SMT2>
```
Program Go ini mencatat hasil pertandingan antara dua klub dengan meminta nama Klub A dan Klub B, lalu menerima input skor dari kedua klub dalam beberapa pertandingan. Jika skor negatif dimasukkan, program berhenti. Untuk setiap pertandingan, jika skor Klub A lebih tinggi maka Klub A dianggap menang dan dicatat, jika Klub B lebih tinggi maka Klub B dicatat, dan jika imbang maka dicatat sebagai "Draw". Semua hasil pertandingan disimpan dalam slice dan ditampilkan satu per satu setelah perulangan selesai, diakhiri dengan pesan "Pertandingan selesai".

---
### Soal 4
Sebuah array digunakan untuk menampung sekumpulan karakter, Anda diminta untuk membuat sebuah subprogram untuk melakukan membalikkan urutan isi array dan memeriksa apakah membentuk palindrom.

```go
package main

import "fmt"

const NMAX int = 127
type tabel [NMAX]rune

func isiArray(t *tabel, n *int) {
	*n = 0
	var c rune
	for *n < NMAX {
		fmt.Scanf("%c", &c)
		if c == '.' {
			break
		}
		t[*n] = c
		*n++
	}
}

func cetakArray(t tabel, n int) {
	for i := 0; i < n; i++ {
		fmt.Printf("%c ", t[i])
	}
	fmt.Println()
}

func balikanArray(t *tabel, n int) {
	for i := 0; i < n/2; i++ {
		t[i], t[n-1-i] = t[n-1-i], t[i]
	}
}

func palindrom(t tabel, n int) bool {
	for i := 0; i < n/2; i++ {
		if t[i] != t[n-1-i] {
			return false
		}
	}
	return true
}

func main() {
	var tab tabel
	var m int

	isiArray(&tab, &m)

	fmt.Println("\nTeks: ")
	cetakArray(tab, m)

	balikanArray(&tab, m)

	fmt.Println("\nReverse teks: ")
	cetakArray(tab, m)

	fmt.Println("\nPalindrom: ", palindrom(tab, m))
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
KATAK. 
Teks: 
K A T A K 
Reverse teks: 
K A T A K
Palindrom: true 
PS D:\Golang SMT2>
```
Program Go ini membaca deretan karakter dari input hingga ditemukan tanda titik (`.`), lalu menyimpannya dalam array bertipe `rune`. Setelah input selesai, program mencetak teks asli, membalik urutan karakter dalam array, lalu mencetak hasil pembalikannya. Terakhir, program memeriksa apakah teks tersebut merupakan palindrom (teks yang sama jika dibaca dari depan maupun belakang) dan menampilkan hasil pemeriksaannya sebagai `true` atau `false`.