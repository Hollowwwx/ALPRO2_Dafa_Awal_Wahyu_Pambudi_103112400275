<h1 align="center">Laporan Praktikum Modul 3 <br>Fungsi</h1>
<p align="center">Dafa Awal Wahyu Pambudi - 103112400275</p>
## Unguided

### Soal 1
Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika
diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng
untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian
membantu Jonas?
Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi,
dengan syarat 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑.
Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂
terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑.

```go
package main

import "fmt"

func Faktorial(n int) int {
	var hasil int

	if n == 0 {
		return 1
	}

	hasil = 1
	for i := 1; i <= n; i++ {
		hasil *= i
	}

	return hasil
}

func Permutasi(n, r int) int {
	var hasil int
	hasil = Faktorial(n) / Faktorial(n-r)

	return hasil
}

func Kombinasi(n, r int) int {
	var hasil int
	hasil = Faktorial(n) / (Faktorial(r) * Faktorial(n-r))
	return hasil
}

func main() {
	var a, b, c, d int
	fmt.Scan(&a, &b, &c, &d)

	if a >= c && b >= d {
		fmt.Println(Permutasi(a, c), Kombinasi(a, c))
		fmt.Println(Permutasi(b, d), Kombinasi(b, d))
	}
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
5 10 3 10 
60 10 
3628800 1 
PS D:\Golang SMT2>
```
Program ini menghitung faktorial, permutasi, dan kombinasi berdasarkan input pengguna. Faktorial digunakan sebagai dasar perhitungan, di mana permutasi menghitung jumlah cara menyusun elemen dengan memperhatikan urutan, sedangkan kombinasi menghitung jumlah cara memilih elemen tanpa memperhatikan urutan. Program menerima empat angka sebagai input, lalu memproses apakah nilai yang dimasukkan memenuhi syarat sebelum melakukan perhitungan

### Soal 2
Diberikan tiga buah fungsi matematika yaitu 𝑓 (𝑥) = 𝑥 2 , 𝑔 (𝑥) = 𝑥 − 2 dan ℎ (𝑥) = 𝑥 + 1. Fungsi komposisi (𝑓𝑜𝑔𝑜ℎ)(𝑥) artinya adalah 𝑓(𝑔(ℎ(𝑥))). Tuliskan 𝑓(𝑥), 𝑔(𝑥) dan ℎ(𝑥) dalam bentuk function. Masukan terdiri dari sebuah bilangan bulat 𝑎, 𝑏 dan 𝑐 yang dipisahkan oleh spasi. Keluaran terdiri dari tiga baris. Baris pertama adalah (𝑓𝑜𝑔𝑜ℎ)(𝑎), baris kedua (𝑔𝑜ℎ𝑜𝑓)(𝑏), dan baris ketiga adalah (ℎ𝑜𝑓𝑜𝑔)(𝑐)!

```go
package main

import "fmt"

func f(x int) int {
	var rumus int
	rumus = x * x
	return rumus
}

func g(x int) int {
	var rumus int
	rumus = x - 2
	return rumus
}

func h(x int) int {
	var rumus int
	rumus = x + 1
	return rumus
}

func main() {

	var x1, x2, x3, fogoh, gohof, hofog int
	fmt.Scan(&x1, &x2, &x3)

	fogoh = f(g(h(x1)))
	gohof = g(h(f(x2)))
	hofog = h(f(g(x3)))

	fmt.Println(fogoh, gohof, hofog)

}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
7 2 10 
36 3 65 
PS D:\Golang SMT2>
```
Program Go ini mendefinisikan tiga fungsi sederhana: f(x) mengembalikan kuadrat dari x, g(x) mengembalikan x - 2, dan h(x) mengembalikan x + 1. Di dalam fungsi main, program membaca tiga bilangan bulat dari input pengguna (x1, x2, dan x3), lalu menghitung dan mencetak hasil komposisi fungsi: fogoh = f(g(h(x1))), gohof = g(h(f(x2))), dan hofog = h(f(g(x3))). Program ini pada dasarnya menunjukkan bagaimana fungsi dapat dikomposisikan dan digunakan dalam urutan tertentu untuk memproses input.

### Soal 3
Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

```go
package main

import (
	"fmt"
	"math"
)

func jarak(a, b, c, d float64) float64 {
	return math.Sqrt(math.Pow(a-c, 2) + math.Pow(b-d, 2))
}

func didalam(cx, cy, r, x, y float64) bool {
	return jarak(cx, cy, x, y) <= r
}

func main() {
	var cx1, cy1, r1, cx2, cy2, r2, x, y float64
	var didalam1, didalam2 bool

	fmt.Scan(&cx1, &cy1, &r1)
	fmt.Scan(&cx2, &cy2, &r2)
	fmt.Scan(&x, &y)

	didalam1 = didalam(cx1, cy1, r1, x, y)
	didalam2 = didalam(cx2, cy2, r2, x, y)

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
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go"
1 1 5
8 8 4
2 2
Titik di dalam lingkaran 1 
PS D:\Golang SMT2>
```

Program ini menentukan apakah suatu titik berada di dalam satu atau dua lingkaran berdasarkan input pengguna. Jarak antara titik dan pusat lingkaran dihitung menggunakan rumus Euclidean, dan hasilnya dibandingkan dengan jari-jari lingkaran untuk menentukan posisi titik. Program menerima koordinat pusat dan jari-jari dua lingkaran, serta koordinat titik yang diuji, kemudian mengevaluasi apakah titik tersebut berada dalam satu, kedua, atau di luar lingkaran. Hasil akhirnya ditampilkan dalam bentuk teks sesuai dengan kondisi yang terjadi.