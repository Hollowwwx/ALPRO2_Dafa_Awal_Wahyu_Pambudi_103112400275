<h1 align="center">Laporan Praktikum Modul 4<br>Prosedur</h1>
<p align="center">Dafa Awal Wahyu Pambudi - 103112400275</p>
## Unguided

### Soal 1
Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian membantu Jonas? (tidak tentunya ya :p) Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi, dengan syarat 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑. Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂 terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑. Catatan: permutasi (P) dan kombinasi (C) dari 𝑛 terhadap 𝑟 (𝑛 ≥ 𝑟) dapat dihitung dengan menggunakan persamaan berikut! 𝑃(𝑛, 𝑟) = 𝑛! (𝑛−𝑟)! , sedangkan 𝐶(𝑛, 𝑟) = 𝑛! 𝑟!(𝑛−𝑟)!

```go
package main

import "fmt"

func factorial(n int, hasil *int) {
	*hasil = 1
	for i := 1; i <= n; i++ {
		*hasil *= i
	}
}

func permutation(n, r int, hasil *int) {
	var faktorialN, faktorialNR int

	factorial(n, &faktorialN)
	factorial(n-r, &faktorialNR)
	*hasil = faktorialN / faktorialNR
}

func combination(n, r int, hasil *int) {
	var faktorialN, faktorialR, faktorialNR int

	factorial(n, &faktorialN)
	factorial(r, &faktorialR)
	factorial(n-r, &faktorialNR)
	*hasil = faktorialN / (faktorialR * faktorialNR)
}

func main() {
	var a, b, c, d, permutationA, permutationB, combinationA, combinationB int
	fmt.Scan(&a, &b, &c, &d)

	if a >= c && b >= d {
		permutation(a, c, &permutationA)
		combination(a, c, &combinationA)
		permutation(b, d, &permutationB)
		combination(b, d, &combinationB)
		fmt.Println(permutationA, combinationA)
		fmt.Println(permutationB, combinationB)
	} else {
		fmt.Print("Input tidak valid")
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
### Penjelasan
Ketika program berjalan, program akan meminta untuk memasukan 4 bilangan asli yang masing-masing disimpan pada variabel a, b, c dan d, dan ada beberapa syarat yang harus dipenuhi, yaitu 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑. Kemudian akan terdapat beberapa proses, yaitu faktorial, permutasi dan kombinasi. Untuk output yang dihasilkan adalah permutasi dan kombinasi a terhadap c, sedangkan baris kedua adalah hasil permutasi dan kombinasi b terhadap d.
### Soal 2
Kompetisi pemrograman tingkat nasional berlangsung ketat. Setiap peserta diberikan 8 soal yang harus dapat diselesaikan dalam waktu 5 jam saja. Peserta yang berhasil menyelesaikan soal paling banyak dalam waktu paling singkat adalah pemenangnya. Buat program gema yang mencari pemenang dari daftar peserta yang diberikan. Program harus dibuat modular, yaitu dengan membuat prosedur hitungSkor yang mengembalikan total soal dan total skor yang dikerjakan oleh seorang peserta, melalui parameter formal. Pembacaan nama peserta dilakukan di program utama, sedangkan waktu pengerjaan dibaca di dalam prosedur. prosedure hitungSkor(in/out soal, skor : integer) Setiap baris masukan dimulai dengan satu string nama peserta tersebut diikuti dengan adalah 8 integer yang menyatakan berapa lama (dalam menit) peserta tersebut menyelesaikan soal. Jika tidak berhasil atau tidak mengirimkan jawaban maka otomatis dianggap menyelesaikan dalam waktu 5 jam 1 menit (301 menit). Satu baris keluaran berisi nama pemenang, jumlah soal yang diselesaikan, dan nilai yang diperoleh. Nilai adalah total waktu yang dibutuhkan untuk menyelesaikan soal yang berhasil diselesaikan.

```go
package main

import "fmt"

func hitungSkor(soal, skor *int) {
	var time int

	*soal = 0
	*skor = 0

	for i := 0; i < 8; i++ {
		fmt.Scan(&time)
		if time < 301 {
			*soal++
			*skor += time
		}
	}
}

func main() {

	var nama, pemenang string
	var soal, skor, maksimumSoal, minimumSkor int

	maksimumSoal = -1
	minimumSkor = 99999

	for {
		fmt.Scan(&nama)

		if nama == "Selesai" || nama == "selesai" {
			break
		}

		hitungSkor(&soal, &skor)

		if soal > maksimumSoal || (soal == maksimumSoal && skor < minimumSkor) {
			maksimumSoal = soal
			minimumSkor = skor
			pemenang = nama
		}
	}

	fmt.Println(pemenang, maksimumSoal, minimumSkor)
}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
Astuti 20 50 301 301 61 71 75  10  
Bertha 25  47  301  26  50  60  65  21  
selesai  
Bertha 7 294  
PS D:\Golang SMT2>
```
### Penjelasan
Program ini akan menentukan pemenang dari sebuah kompetisi pemrograman berdasarkan jumlah soal dan waktu pengerjaan. Terdapat perulangan yang berhenti ketika sudah 8 kali perulangan, yaitu sesuai dengan jumlah soal yang dikerjakan masing-masing peserta, yaitu 8 soal. Dan untuk batas pengerjaan masing-masing soal adalah 5 jam, dan di program terangkan bahwa jika lebih dari 300 menit, maka dianggap sudah melebihi batas waktu yang ditentukan.

### Soal 3
Skiena dan Revilla dalam Programming Challenges mendefinisikan sebuah deret bilangan.
Deret dimulai dengan sebuah bilangan bulat n. Jika bilangan n saat itu genap, maka suku
berikutnya adalah ½n, tetapi jika ganjil maka suku berikutnya bernilai 3n+1. Rumus yang sama
digunakan terus menerus untuk mencari suku berikutnya. Deret berakhir ketika suku terakhir
Halaman 9 | M o d u l P r a k t i k u m A l g o r i t m a P e m r o g r a m a n
bernilai 1. Sebagai contoh jika dimulai dengan n=22, maka deret bilangan yang diperoleh
adalah:
22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1
Untuk suku awal sampai dengan 1000000, diketahui deret selalu mencapai suku dengan nilai 1. Buat program skiena yang akan mencetak setiap suku dari deret yang dijelaskan di atas untuk
nilai suku awal yang diberikan. Pencetakan deret harus dibuat dalam prosedur cetakDeret
yang mempunyai 1 parameter formal, yaitu nilai dari suku awal.
prosedure cetakDeret(in n : integer )
Masukan berupa satu bilangan integer positif yang lebih kecil dari 1000000.
Keluaran terdiri dari satu baris saja. Setiap suku dari deret tersebut dicetak dalam baris yang
dan dipisahkan oleh sebuah spasi.

```go
package main

import "fmt"

func cetakDeret(n int) {
	for {
		fmt.Print(n, " ")
		if n == 1 {
			break
		}

		if n%2 == 0 {
			n /= 2
		} else {
			n = n*3 + 1
		}
	}
}

func main() {

	var n int
	fmt.Scan(&n)

	if n > 0 && n < 1000 {
		cetakDeret(n)
	}

}
```

```
PS D:\Golang SMT2> go run "d:\Golang SMT2\cok.go" 
22 
22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 
PS D:\Golang SMT2>
```
#### Penjelasan
Program ini digunakan untuk mencetak deret angka berdasarkan aturan ketika genap, maka bilangan atau nilai n akan dikali dengan 1/2, jika ganjil dengan 3n + 1. Program diawali dengan membaca sebuah bilangan bulat positif n dari input, dengan batasan 1 hingga 999. Jika input memenuhi syarat, prosedur cetakDeret dipanggil untuk mencetak deretnya. Deret akan dicetak dari nilai n hingga 1. 