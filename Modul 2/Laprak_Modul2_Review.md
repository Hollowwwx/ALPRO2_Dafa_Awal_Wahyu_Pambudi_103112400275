# <h1 align="center">Laporan Praktikum Modul 2 - Review</h1>
<p align="center">Dafa Awal Wahyu Pambudi - 103112400275</p>


## 2A

### 1. Telusuri Program

Program ini meminta pengguna untuk memasukkan tiga string, lalu mencetaknya dalam urutan awal sebelum menukar nilainya secara rotasi dan mencetak hasil akhir. Pertukaran dilakukan dengan menyimpan nilai satu ke variabel sementara temp, lalu satu diisi dengan dua, dua diisi dengan tiga, dan tiga diisi dengan nilai awal satu dari temp. Sebagai contoh, jika pengguna memasukkan "A", "B", dan "C", program akan mencetak "Output awal = A B C" lalu setelah pertukaran mencetak "Output akhir = B C A". Program ini berfungsi untuk mendemonstrasikan proses rotasi nilai antar variabel dalam pemrograman.

### 2. Tahun Kabisat

```go
package main

import "fmt"

func leap(year int) bool {
    return (year%4 == 0 && year%100 != 0) || year%400 == 0

}
 func main() {
    var year int
    fmt.Print("Masukan tahun: ")
    fmt.Scanln(&year)
    if leap(year) {
        fmt.Println("Kabisat: true")
    } else {
        fmt.Println("Kabisat: false")
    }
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2A\2.go"
Masukan tahun: 2016
Kabisat: true
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2A\2.go"
Masukan tahun: 2018
Kabisat: false
```
Program ini menentukan apakah suatu tahun adalah tahun kabisat dengan menggunakan fungsi leap(year int) bool, yang mengembalikan true jika tahun tersebut habis dibagi 4 tetapi tidak habis dibagi 100, kecuali jika juga habis dibagi 400. Dalam fungsi main(), program meminta pengguna memasukkan sebuah tahun, lalu memanggil fungsi leap(year) untuk mengevaluasi apakah tahun tersebut kabisat atau tidak. Jika hasilnya true, program mencetak "Kabisat: true", dan jika false, mencetak "Kabisat: false".

### 3. Bola

```go
package main

import ("fmt"
		"math"
		)

func main() {
	var rad float64
	pi := math.Pi

	fmt.Print("Masukan jari-jari = ")
	fmt.Scan(&rad)

	vol := 4.0/3.0 * pi * math.Pow(rad, 3)
	LP := 4 * pi * math.Pow(rad, 2)

	fmt.Printf("Bola dengan jejari %.0f memiliki volume %.4f dan luas kulit %.4f\n", rad, vol, LP)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2A\3.go"
Masukan jari-jari = 5
Bola dengan jejari 5 memiliki volume 523.5988 dan luas kulit 314.1593
```
Program ini menghitung volume dan luas permukaan bola berdasarkan jari-jari yang dimasukkan oleh pengguna. Setelah pengguna memasukkan jari-jari, program menggunakan nilai pi untuk menghitung volume dengan mengalikan empat per tiga, pi, dan jari-jari pangkat tiga. Kemudian, program menghitung luas permukaan bola dengan mengalikan empat, pi, dan jari-jari pangkat dua. Hasil perhitungan tersebut ditampilkan dengan empat angka di belakang koma.

### 4. Suhu

```go
package main

import "fmt"

func main() {
	var cel int

	fmt.Print("Temperatur Celcius: ")
	fmt.Scan(&cel)

	far := cel*9/5 + 32
	ream := cel*4/5
	kel := cel + 273

	fmt.Printf("Derajat Reamur: %d\n", ream)
	fmt.Printf("Derajat Fahrenheit: %d\n", far)
	fmt.Printf("Derajat Kelvin: %d\n", kel)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2A\4.go"
Temperatur Celcius: 50
Derajat Reamur: 40     
Derajat Fahrenheit: 122
Derajat Kelvin: 323
```
Program ini mengonversi suhu dari celcius ke reamur, fahrenheit, dan kelvin menggunakan bilangan bulat. Setelah pengguna memasukkan suhu dalam celcius, program menghitung suhu dalam fahrenheit dengan mengalikan sembilan per lima lalu menambahkan tiga puluh dua, dalam reamur dengan mengalikan empat per lima, dan dalam kelvin dengan menambahkan dua ratus tujuh puluh tiga. Hasil konversi ditampilkan dalam bentuk bilangan bulat tanpa angka di belakang koma.

### 5. ASCII

```go
package main

import "fmt"

func main() {
    var a, b, c, d, e int
    var x, y, z rune

    fmt.Scan(&a, &b, &c, &d, &e)
    fmt.Scan(&x, &y, &z)

    fmt.Printf("%c%c%c%c%c\n", a, b, c, d, e)
    fmt.Printf("%c%c%c\n", x, y, z)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2A\tempCodeRunnerFile.go"
66 97 103 117 115
SNO
Bagus
```
Program ini membaca lima angka dan tiga karakter dari input pengguna, lalu mencetaknya sebagai karakter berdasarkan kode ASCII atau Unicode. Lima angka pertama disimpan dalam variabel bilangan bulat, sedangkan tiga karakter berikutnya disimpan dalam variabel bertipe rune. Setelah menerima input, program mencetak lima angka pertama sebagai karakter dalam satu baris, lalu mencetak tiga karakter berikutnya dalam baris terpisah.

## 2B

### 1. Praktikum Kimia

```go
package main

import (
        "bufio"
        "fmt"
        "os"
        "strings"
)

func main() {
        scanner := bufio.NewScanner(os.Stdin)
        successCount := 0

        for i := 1; i <= 5; i++ {
                fmt.Printf("Percobaan %d: ", i)
                scanner.Scan()
                input := scanner.Text()
                colors := strings.Fields(input)

                if len(colors) == 4 &&
                        colors[0] == "merah" &&
                        colors[1] == "kuning" &&
                        colors[2] == "hijau" &&
                        colors[3] == "ungu" {
                        successCount++
                }
        }

        if successCount == 5 {
                fmt.Println("BERHASIL: true")
        } else {
                fmt.Println("BERHASIL: false")
        }
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2B\1.go"
Percobaan 2: merah kuning hijau ungu
Percobaan 3: merah kuning hijau ungu
Percobaan 4: merah kuning ungu hijau
Percobaan 5: merah kuning hijau ungu
BERHASIL: false    
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2B\1.go"
Percobaan 1:  merah kuning hijau ungu
Percobaan 2:  merah kuning hijau ungu
Percobaan 3:  merah kuning hijau ungu
Percobaan 4:  merah kuning hijau ungu
Percobaan 5:  merah kuning hijau ungu
BERHASIL: true
```
Program ini meminta pengguna memasukkan empat warna dalam lima percobaan dan mengevaluasi apakah urutan warna yang dimasukkan benar di setiap percobaan. Pada setiap percobaan, pengguna diminta mengetik empat warna yang dipisahkan oleh spasi, kemudian program memeriksa apakah urutannya sesuai dengan merah, kuning, hijau, dan ungu. Jika semua lima percobaan berhasil, program mencetak berhasil dengan nilai benar, jika tidak, mencetak berhasil dengan nilai salah.
### 2. Pita

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

func main() {
	var flowers []string
	scanner := bufio.NewScanner(os.Stdin)
	fmt.Print("N: ")
	scanner.Scan()
	nInput := scanner.Text()
	var n int
	fmt.Sscanf(nInput, "%d", &n)

	if n > 0 {
		for i := 1; i <= n; i++ {
			fmt.Printf("Bunga %d: ", i)
			scanner.Scan()
			flower := scanner.Text()
			if strings.ToUpper(flower) == "SELESAI" {
				break
			}
			flowers = append(flowers, flower)
		}
	}

	fmt.Println("Pita:", strings.Join(flowers, " - "))
	fmt.Println("Bunga:", len(flowers))
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2B\2.go"
N: 4
Bunga 1: Kertas
Bunga 2: Mawar
Bunga 3: Tulip
Bunga 4: Selesai
Pita: Kertas - Mawar - Tulip
Bunga: 3
```
Program ini meminta pengguna untuk memasukkan sejumlah nama bunga dan menampilkannya dalam format pita dengan jumlah total bunga yang dimasukkan. Pengguna terlebih dahulu memasukkan angka sebagai jumlah bunga yang akan dicatat, lalu memasukkan nama bunga satu per satu. Jika pengguna mengetik "SELESAI" dengan huruf besar, program akan berhenti mencatat meskipun jumlah yang dimasukkan belum mencapai batas. Setelah selesai, program mencetak daftar bunga yang dipisahkan oleh tanda hubung serta jumlah bunga yang berhasil dicatat.

### 3. Berat Belanjaan

```go
package main

import (
	"fmt"
)

func main() {
	var beratKiri, beratKanan float64
	var totalBerat float64 = 0
	
	for {
		fmt.Print("Masukan berat belanjaan di kedua kantong: ")
		fmt.Scan(&beratKiri, &beratKanan)
		
		if beratKiri < 0 || beratKanan < 0 {
			fmt.Println("Proses selesai.")
			break
		}
		
		totalBerat = beratKiri + beratKanan
		oleng := (beratKiri - beratKanan) >= 9 || (beratKanan - beratKiri) >= 9
		fmt.Println("Sepeda motor Pak Andi akan oleng:", oleng)
		
		if totalBerat > 150 || beratKiri >= 9 || beratKanan >= 9 {
			fmt.Println("Proses selesai.")
			break
		}
	}
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2B\3.go"
Masukan berat belanjaan di kedua kantong: 5 10
Sepeda motor Pak Andi akan oleng: false
Proses selesai.
```
Program ini mensimulasikan keseimbangan sepeda motor Pak Andi berdasarkan berat belanjaan yang dimasukkan pengguna. Dalam setiap iterasi, pengguna memasukkan berat belanjaan di kantong kiri dan kanan. Jika salah satu berat bernilai negatif, program berhenti. Program menentukan apakah sepeda motor oleng jika selisih berat antara kedua kantong mencapai sembilan atau lebih, lalu mencetak hasilnya. Program juga berhenti jika total berat belanjaan
melebihi seratus lima puluh atau jika salah satu kantong memiliki berat sembilan atau lebih.

### 4. Nilai K

```go
package main

import (
	"fmt"
)

func main() {
	var k int
	fmt.Print("Nilai K = ")
	fmt.Scan(&k)

	fK := (float64((4*k + 2) * (4*k + 2))) / (float64((4*k + 1) * (4*k + 3)))
	fmt.Printf("Nilai f(K) = %.10f\n", fK)

	approxSqrt2 := 1.0
	for i := 0; i < k; i++ {
		approxSqrt2 *= (float64((4*i + 2) * (4*i + 2))) / (float64((4*i + 1) * (4*i + 3)))
	}
	fmt.Printf("Nilai akar 2 = %.10f\n", approxSqrt2)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2B\tempCodeRunnerFile.go"
Nilai K = 100
Nilai f(K) = 1.0000061880
Nilai akar 2 = 1.4133299615
```
Program ini menghitung dua nilai berdasarkan input bilangan bulat k dari pengguna. Pertama, program menghitung nilai fungsi f(k) menggunakan rumus pecahan dengan operasi perkalian dan pembagian, lalu mencetak hasilnya dengan sepuluh angka di belakang koma. Kedua, program menghitung pendekatan akar dua menggunakan perkalian berulang dengan pola yang mirip dengan f(k), mengalikan hasil sebelumnya dalam setiap iterasi hingga k kali. Setelah perhitungan selesai, program mencetak hasil pendekatan akar dua dengan sepuluh angka di belakang koma.

## 2C

### 1. Biaya POS

```go
package main

import (
	"fmt"
)

func main() {
	var beratParsel int
	fmt.Print("Berat parsel (gram): ")
	fmt.Scan(&beratParsel)

	kg := beratParsel / 1000
	gram := beratParsel % 1000
	totalBiaya := kg * 10000

	if beratParsel > 10000 {
		gram = 0
	}

	if gram >= 500 {
		totalBiaya += gram * 5
	} else {
		totalBiaya += gram * 15
	}

	fmt.Printf("Detail berat: %d kg + %d gr\n", kg, gram)
	fmt.Printf("Detail biaya: Rp. %d + Rp. %d\n", kg*10000, totalBiaya-(kg*10000))
	fmt.Printf("Total biaya: Rp. %d\n", totalBiaya)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2C\1.go"
Berat parsel (gram): 8500
Detail berat: 8 kg + 500 gr
Detail biaya: Rp. 80000 + Rp. 2500
Total biaya: Rp. 82500
```
Program ini menghitung biaya pengiriman berdasarkan berat paket dalam gram. Berat paket dibagi menjadi bagian kilogram dan gram. Setiap kilogram dikenakan biaya tetap, sedangkan bagian gram mendapat biaya tambahan tergantung apakah lebih atau kurang dari setengah kilogram. Jika berat paket melebihi sepuluh kilogram, bagian gram diabaikan. Program kemudian menampilkan rincian berat dan biaya total yang harus dibayar.

### 2. Nilai

```
A. Jika nilai yang dimasukkan adalah 80.1, program akan mengalami kesalahan karena variabel yang menyimpan nilai angka diubah menjadi huruf, yang tidak sesuai dengan tipe data yang ditentukan. Selain itu, program juga tidak menampilkan nilai yang benar karena variabel yang dicetak tidak diperbarui dengan nilai huruf yang sesuai. Oleh karena itu, eksekusi program tidak sesuai dengan spesifikasi soal.

B. Kesalahan dalam program ini antara lain:

- Variabel angka tidak boleh diisi dengan huruf, karena akan menyebabkan error.
- Penggunaan kondisi bertingkat yang tidak benar karena setiap kondisi dieksekusi terpisah, bukan secara eksklusif.
- Program tidak pernah memperbarui variabel yang dicetak sebagai hasil akhir.
- Penggunaan tanda kutip yang salah, karena harus menggunakan tanda kutip ganda yang benar untuk string.
- Penggunaan `fmt.Scanln(&nam)` lebih baik diganti dengan `fmt.Scan(&nam)` untuk   menghindari masalah input.

Alur program yang benar seharusnya adalah:

1. Menerima input nilai akhir.
2. Menentukan huruf berdasarkan rentang nilai dengan kondisi `if-else if` agar hanya satu kondisi yang dieksekusi.
3. Mencetak hasil nilai huruf sesuai input yang diberikan.
```
###### C.
```go
package main

import "fmt"

func main() {
    var nilai float64
    var grade string

    fmt.Print("Nilai akhir mata kuliah: ")
    fmt.Scan(&nilai)

    if nilai > 80 {
        grade = "A"
    } else if nilai > 72.5 {
        grade = "AB"
    } else if nilai > 65 {
        grade = "B"
    } else if nilai > 57.5 {
        grade = "BC"
    } else if nilai > 50 {
        grade = "C"
    } else if nilai > 40 {
        grade = "D"
    } else {
        grade = "E"
    }

    fmt.Println("Nilai mata kuliah:", grade)
}
```
Jika diuji dengan masukan:
- **93.5**, hasilnya adalah **A**.
- **70.6**, hasilnya adalah **B**.
- **49.5**, hasilnya adalah **D**.

### 3. Prima

```go
package main

import (
	"fmt"
)

func main() {
	var b int
	fmt.Print("Bilangan: ")
	fmt.Scan(&b)

	fmt.Print("Faktor: ")
	count := 0

	for i := 1; i <= b; i++ {
		if b%i == 0 {
			fmt.Print(i, " ")
			count++
		}
	}

	isPrime := count == 2
	fmt.Println("\nPrima:", isPrime)
}
```
#### OUTPUT:
```
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2C\3.go"
Bilangan: 12
Faktor: 1 2 3 4 6 12
Prima: false
PS D:\Golang SMT2> go run "d:\Golang SMT2\Module 2\2C\3.go"
Bilangan: 7
Faktor: 1 7 
Prima: true
```
Program ini meminta pengguna memasukkan sebuah bilangan bulat positif, lalu mencari dan menampilkan semua faktor dari bilangan tersebut dengan memeriksa setiap angka dari satu hingga bilangan itu sendiri. Setiap faktor yang ditemukan akan ditampilkan. Setelah itu, program menghitung jumlah faktor yang ditemukan. Jika jumlahnya tepat dua, yaitu satu dan bilangan itu sendiri, maka bilangan tersebut dikategorikan sebagai bilangan prima. Program kemudian menampilkan hasil apakah bilangan tersebut prima atau bukan.