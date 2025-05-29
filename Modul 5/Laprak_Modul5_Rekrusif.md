<h1 align="center">Laporan Praktikum Modul 5<br>Rekrusif</h1>
<p align="center">Dafa Awal Wahyu Pambudi - 103112400275</p>
## Unguided

### Soal 1
Deret fibonacci adalah sebuah deret dengan nilai suku ke-0 dan ke-1 adalah 0 dan 1, dan nilai suku ke-n selanjutnya adalah hasil penjumlahan dua suku sebelumnya. Secara umum dapat diformulasikan 𝑆𝑛 = 𝑆𝑛−1 + 𝑆𝑛−2 . Berikut ini adalah contoh nilai deret fibonacci hingga suku ke-10. Buatlah program yang mengimplementasikan fungsi rekursif pada deret fibonacci tersebut.

```go
package main

import "fmt"

func fibonacci(n int) int {
	if n < 2 {
		return n
	}
	return fibonacci(n-1) + fibonacci(n-2)
}

func cetakFibonacci(i, n int) {
	fmt.Print(fibonacci(i), " ")
	if i < n {
		cetakFibonacci(i+1, n)
	}
}

func main() {
	var n int
	fmt.Scan(&n)
	cetakFibonacci(0, n)
}
```
![[Pasted image 20250529121512.png]]
Program Go ini menghitung dan mencetak deret Fibonacci dari indeks 0 hingga `n` (inklusif) yang dimasukkan oleh pengguna. Fungsi `fibonacci(n int)` menggunakan pendekatan rekursif untuk menghitung nilai ke-`n` dalam deret Fibonacci, di mana `fibonacci(0) = 0` dan `fibonacci(1) = 1`. Fungsi `cetakFibonacci(i, n int)` secara rekursif mencetak nilai Fibonacci mulai dari indeks `i` hingga `n`, dengan memanggil dirinya sendiri sambil menaikkan `i`. Di fungsi `main`, pengguna memasukkan sebuah bilangan bulat `n`, dan program mencetak deret Fibonacci dari `fibonacci(0)` sampai `fibonacci(n)`.

### Soal 2
Buatlah sebuah program yang digunakan untuk menampilkan pola bintang berikut ini dengan menggunakan fungsi rekursif. N adalah masukan dari user.

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>5</td>
    <td>*<br>**<br>***<br>****<br>*****</td>
  </tr>
  <tr>
    <td>2</td>
    <td>1</td>
    <td>*</td>
  </tr>
  <tr>
    <td>3</td>
    <td>3</td>
    <td>*<br>**<br>***</td>
  </tr>
</table>

```go
package main

import "fmt"

func bintang(n int) {
	if n != 0 {
		fmt.Print("*")
		bintang(n - 1)
	}
}

func pola(n, baris int) {
	if baris <= n {
		bintang(baris)
		fmt.Println()
		pola(n, baris+1)
	}
}

func main() {
	var n int
	fmt.Scan(&n)
	pola(n, 1)
}
```
![[Pasted image 20250529121658.png]]
Program Go ini mencetak pola segitiga bintang yang terdiri dari `n` baris menggunakan rekursi. Fungsi `bintang(n int)` mencetak `n` buah karakter `*` secara rekursif dalam satu baris. Fungsi `pola(n, baris int)` mencetak pola dari baris 1 hingga `n`, di mana setiap baris berisi jumlah bintang sebanyak nomor barisnya (baris ke-1 satu bintang, baris ke-2 dua bintang, dan seterusnya). Di fungsi `main`, pengguna memasukkan nilai `n`, dan program memulai pencetakan pola dari baris pertama hingga ke-`n`. Hasilnya adalah segitiga bintang dengan tinggi `n`.

### Soal 3
Buatlah program yang mengimplementasikan rekursif untuk menampilkan faktor bilangan dari suatu N, atau bilangan yang apa saja yang habis membagi N. Masukan terdiri dari sebuah bilangan bulat positif N. Keluaran terdiri dari barisan bilangan yang menjadi faktor dari N (terurut dari 1 hingga N ya).

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>5</td>
    <td>1 5</td>
  </tr>
  <tr>
    <td>2</td>
    <td>12</td>
    <td>1 2 3 4 6 12</td>
  </tr>
</table>

```go
package main

import "fmt"

func faktorBilangan(n, i int) {
	if i <= n {
		if n%i == 0 {
		fmt.Print(i, " ")
		}
		faktorBilangan(n, i+1)
	}
}

func main() {
	var n int
	fmt.Scan(&n)
	faktorBilangan(n, 1)
}
```
![[Pasted image 20250529121855.png]]
Program Go ini digunakan untuk menampilkan semua faktor dari sebuah bilangan bulat `n` yang dimasukkan oleh pengguna. Fungsi `faktorBilangan(n, i int)` bekerja secara rekursif, dimulai dari `i = 1` hingga `i = n`. Pada setiap langkah, jika `n` habis dibagi `i` (`n % i == 0`), maka `i` dicetak sebagai salah satu faktor dari `n`. Fungsi ini terus memanggil dirinya sendiri dengan `i+1` hingga seluruh faktor ditemukan. Di fungsi `main`, program membaca input `n` dari pengguna, lalu memanggil `faktorBilangan(n, 1)` untuk mencetak seluruh faktor dari `n`.

### Soal 4
Buatlah program yang mengimplementasikan rekursif untuk menampilkan barisan bilangan tertentu. Masukan terdiri dari sebuah bilangan bulat positif N. Keluaran terdiri dari barisan bilangan dari N hingga 1 dan kembali ke N.

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>5</td>
    <td>5 4 3 2 1 2 3 4 5</td>
  </tr>
  <tr>
    <td>2</td>
    <td>9</td>
    <td>9 8 7 6 5 4 3 2 1 2 3 4 5 6 7 8 9</td>
  </tr>
</table>

```go
package main

import "fmt"

func barisan(n, angka int) {
	fmt.Print(angka, " ")
	if angka > 1 {
		barisan(n, angka-1)
		fmt.Print(angka, " ")
	}
}

func main() {

	var n int
	fmt.Scan(&n)
	barisan(n, n)

}
```
![[Pasted image 20250529122004.png]]
Program Go ini mencetak pola angka secara rekursif dengan efek simetris. Fungsi `barisan(n, angka int)` mencetak angka dari nilai `angka` turun ke 1, lalu naik kembali ke nilai semula, membentuk pola cermin. Saat fungsi dipanggil, angka saat ini dicetak, lalu jika `angka > 1`, fungsi memanggil dirinya dengan `angka-1`, dan setelah itu mencetak kembali `angka`. Di `main`, pengguna memasukkan bilangan bulat `n`, lalu fungsi `barisan(n, n)`

### Soal 5
Buatlah program yang mengimplementasikan rekursif untuk menampilkan barisan bilangan ganjil. Masukan terdiri dari sebuah bilangan bulat positif N. Keluaran terdiri dari barisan bilangan ganjil dari 1 hingga N. Contoh masukan dan keluaran:

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>5</td>
    <td>1 3 5</td>
  </tr>
  <tr>
    <td>2</td>
    <td>20</td>
    <td>1 3 5 7 9 11 13 15 17 19</td>
  </tr>
	</table>

```go
package main

import "fmt"

func cetakGanjil(i, n int) {
	if i <= n {
		fmt.Print(i, " ")
		cetakGanjil(i+2, n)
	}
}

func main() {
	var n int
	fmt.Scan(&n)
	cetakGanjil(1, n)
}
```
![[Pasted image 20250529122143.png]]
Program Go ini mencetak semua **bilangan ganjil** dari 1 hingga `n` menggunakan rekursi. Fungsi `cetakGanjil(i, n int)` mencetak nilai `i` jika masih kurang dari atau sama dengan `n`, kemudian memanggil dirinya sendiri dengan `i+2` (melompati satu angka untuk menjaga agar hanya ganjil yang dicetak). Di fungsi `main`, pengguna memasukkan sebuah bilangan bulat `n`, lalu program mencetak deret ganjil mulai dari 1 sampai `n`.\

### Soal 6
Buatlah program yang mengimplementasikan rekursif untuk mencari hasil pangkat dari dua buah bilangan. Masukan terdiri dari bilangan bulat x dan y. Keluaran terdiri dari hasil x dipangkatkan y. Catatan: diperbolehkan menggunakan asterik "", tapi dilarang menggunakan import "math". Contoh masukan dan keluaran:

<table border="1">
  <tr>
    <th>No</th>
    <th>Masukan</th>
    <th>Keluaran</th>
  </tr>
  <tr>
    <td>1</td>
    <td>2 2</td>
    <td>4</td>
  </tr>
  <tr>
    <td>2</td>
    <td>5 3</td>
    <td>125</td>
  </tr>
	</table>

```go
package main

import "fmt"

func pangkat(x, y int) int {
	if y == 0 {
		return 1
	}

	return x * pangkat(x, y-1)
}

func main() {
	var x, y int
	fmt.Scan(&x, &y)
	fmt.Println(pangkat(x, y))
}
```
![[Pasted image 20250529122256.png]]
Program Go ini menghitung hasil pemangkatan x^y secara rekursif melalui fungsi pangkat(x, y int), di mana jika y sama dengan 0 maka akan mengembalikan 1, dan jika tidak maka akan mengembalikan x dikalikan dengan hasil pemanggilan fungsi pangkat dengan y dikurangi 1. Pada fungsi main, dua bilangan bulat x dan y dibaca dari input, kemudian hasil pemangkatan tersebut dicetak ke layar.
