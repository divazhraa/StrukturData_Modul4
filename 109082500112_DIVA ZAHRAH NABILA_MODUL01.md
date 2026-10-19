# <h1 align="center">Laporan Praktikum Modul 3 - ABSTRACT DATA TYPE (ADT)- ... </h1>
<p align="center">[Diva Zahrah Nabila] - [109082500112]</p>

## Unguided 

# Dasar Teori
## A.	Abstract Data Type (ADT)
###     Abstract Data Type (ADT) adalah definisi statik yang mencakup sebuah tipe data (TYPE) beserta sekumpulan operasi dasar atau primitif yang dapat memanipulasi tipe data tersebut. ADT yang terstruktur dan lengkap biasanya juga menyertakan definisi invarian dari tipe dan aksioma-aksioma terkait. Sebuah definisi ADT dapat bersifat kompleks, artinya di dalamnya dapat memuat definisi dari ADT lain (contohnya, ADT SEGI4 dapat dibentuk dari dua buah ADT POINT).

## B.	Implementasi Modular pada ADT
###     Dalam standar software engineering, ADT diimplementasikan menggunakan arsitektur modular yang memecah program menjadi tiga file utama, yaitu:
###     1. Berkas Header (.h): Memuat deklarasi atau spesifikasi tipe struct serta bentuk prototipe (header) dari primitif (fungsi dan prosedur) tanpa menjabarkan isi prosesnya.   
###     2. Berkas Body/Realisasi (.cpp): Memuat implementasi kode murni (body) dari primitif fungsi/prosedur yang telah dideklarasikan di bagian header.   
###     3. Berkas Program Utama/Driver (main.cpp): Merupakan antarmuka utama program yang dipanggil oleh sistem (memuat fungsi int main()) untuk menggunakan tipe data bentukan tersebut.



# GUIDED 1
### Source code: 

```cpp
#include <iostream>
using namespace std;
struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
int main()
{
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata - rata = " << rata2(mhs);
    return 0;
}
void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> m.nim;
    cout << "input nilai = ";
    cin >> m.nilai1;
    cout << "input nilai2 = ";
    cin >> m.nilai2;
}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
``` 

### Penjelasan: Program ini menggunakan tipe data bentukan (struct) bernama mahasiswa untuk mengelompokkan data secara rapi, yaitu NIM, nilai 1, dan nilai 2. Seluruh kode pada program ini ditulis di dalam satu file tunggal. Di dalamnya terdapat dua fungsi pendukung: prosedur inputMhs() yang bertugas meminta pengguna memasukkan data, dan fungsi rata2() untuk menghitung nilai rata-rata dari kedua nilai tersebut. Fungsi main() kemudian akan memanggil kedua fungsi itu secara berurutan agar hasilnya bisa tampil di layar.



### GUIDED 2	
### Source code: 

### mahasiswa.h
```cpp
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif
```
### mahasiswa.cpp
```cpp
#include <iostream>
#include "mahasiswa.h"
using namespace std;
void inputMhs(mahasiswa &m){
    cout << "input nama = ";
    cin >> (m).nim;
    cout << "input nilai =";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
```
### guided2.main.cpp
```cpp
#include <iostream>
#include "mahasiswa.h"
using namespace std;
int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata - rata = " << rata2(mhs);
    return 0;
}
```

### Penjelasan: Program ini adalah contoh penerapan Abstract Data Type (ADT) di mana satu program sengaja dipecah menjadi tiga file. File mahasiswa.h berfungsi sebagai kerangka dasar untuk mengenalkan nama tipe data dan fungsi. File mahasiswa.cpp berisi isi atau logika cara kerja dari fungsi-fungsi tersebut. Terakhir, file guided2.cpp adalah program utamanya yang bertugas memanggil file-file tadi agar hasilnya bisa tampil di layar.




# Unguided
### 1. Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3*uts+0.4*uas+0.3*tugas.
```cpp
#include <iostream>
using namespace std;

struct Mahasiswa{
    string nama, nim;
    float uts, uas, tugas, nilai_akhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas){
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

int main(){
    Mahasiswa mhs[10]; 
    int jumlah;
    cout << "Masukkan jumlah mahasiswa (Maks 10): ";
    cin >> jumlah;
    if (jumlah > 10)
        jumlah = 10;
    for (int i = 0; i < jumlah; i++){
        cout << "\nData Mahasiswa ke-" << i + 1 << endl;
        cout << "Nama  : ";
        cin >> mhs[i].nama;
        cout << "NIM   : ";
        cin >> mhs[i].nim;
        cout << "UTS   : ";
        cin >> mhs[i].uts;
        cout << "UAS   : ";
        cin >> mhs[i].uas;
        cout << "Tugas : ";
        cin >> mhs[i].tugas;
        mhs[i].nilai_akhir = hitungNilaiAkhir(mhs[i].uts, mhs[i].uas, mhs[i].tugas);
    }

    cout << "\n=== HASIL REKAP NILAI MAHASISWA ===" << endl;
    for (int i = 0; i < jumlah; i++){
        cout << "Nama: " << mhs[i].nama << " | NIM: " << mhs[i].nim
             << " | Nilai Akhir: " << mhs[i].nilai_akhir << endl;
    }
    return 0;
}
```
### Output 1
![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/SOAL1.png)

![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/SOAL1(JAM).png)


### penjelasan unguided 1
[Program ini menggunakan tipe data array of struct untuk menyimpan data maksimal 10 mahasiswa. Rumus nilai dipisah ke dalam fungsi bernama hitungNilaiAkhir(). Fungsi ini mengambil nilai UTS, UAS, dan tugas, menghitung hasilnya, lalu menyimpan hasil hitungan tersebut langsung ke dalam data milik masing-masing mahasiswa.]


### 2. Buatlah ADT pelajaran sebagai berikut di dalam file “pelajaran.h”:

### pelajaran.h
```cpp
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct pelajaran{
    string namaMapel;
    string kodeMapel;
};
pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran pel);
#endif
```

### pelajaran.cpp
```cpp
#include <iostream>
#include "pelajaran.h"
using namespace std;
pelajaran create_pelajaran(string namapel, string kodepel){
    pelajaran pel;
    pel.namaMapel = namapel;
    pel.kodeMapel = kodepel;
    return pel;
}

void tampil_pelajaran(pelajaran pel){
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```

### soal2.main.cpp
```cpp
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main(){
    string namapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```
### Output Unguided 2 :
![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/pelajaran.h.png)

![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/pelajaran.cpp.png)

![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/SOAL2.png)



### penjelasan unguided 2
[Program ini adalah contoh penerapan Abstract Data Type (ADT) di mana satu program dipecah menjadi tiga file. File pelajaran.h berfungsi sebagai kerangka dasar untuk mengenalkan nama tipe data dan fungsi. File pelajaran.cpp berisi isi atau logika cara kerja dari fungsi-fungsi tersebut. Terakhir, file soal2.main.cpp adalah program utamanya yang bertugas memanggil file-file tadi agar hasilnya bisa tampil di layar.]

### 3. Buatlah program dengan ketentuan :
#### - 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
#### - fungsi/prosedur yang menampilkan isi sebuah array integer 2D
#### - fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
#### - fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer

### source code unguided 3
```cpp
#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]){
    for (int i = 0; i < 3; i++){
        for (int j = 0; j < 3; j++){
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

void tukarIsiArray(int arr1[3][3], int arr2[3][3], int row, int col){
    int temp = arr1[row][col];
    arr1[row][col] = arr2[row][col];
    arr2[row][col] = temp;
}

void tukarPointer(int *ptr1, int *ptr2){
    int temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
}

int main(){
    int array1[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int array2[3][3] = {{9, 8, 7}, {6, 5, 4}, {3, 2, 1}};

    int var1 = 15, var2 = 50;
    int *p1 = &var1;
    int *p2 = &var2;

    cout << "=== SEBELUM DITUKAR ===" << endl;
    cout << "Array 1:" << endl;
    tampilArray(array1);
    cout << "Array 2:" << endl;
    tampilArray(array2);
    tukarIsiArray(array1, array2, 1, 1);

    cout << "\n=== SESUDAH ARRAY DITUKAR (Posisi [1][1]) ===" << endl;
    cout << "Array 1:" << endl;
    tampilArray(array1);
    cout << "Array 2:" << endl;
    tampilArray(array2);

    cout << "\n-----------------------------------" << endl;

    cout << "=== SEBELUM POINTER DITUKAR ===" << endl;
    cout << "Isi P1 = " << *p1 << ", Isi P2 = " << *p2 << endl;
    
    tukarPointer(p1, p2);

    cout << "\n=== SESUDAH POINTER DITUKAR ===" << endl;
    cout << "Isi P1 = " << *p1 << ", Isi P2 = " << *p2 << endl;

    return 0;
}
```
### Output Unguided 3 :
![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul3/blob/main/MODUL03/output/SOAL3.png)


### penjelasan unguided 3
[Program ini menunjukkan cara menukar data menggunakan array dua dimensi dan pointer. Fungsi tukarIsiArray() dibuat untuk menukar isi dari dua buah array (berukuran 3x3) pada posisi baris dan kolom tertentu. Sedangkan fungsi tukarPointer() berguna untuk menukar nilai dari dua variabel secara langsung dengan cara mengakses alamat memorinya menggunakan bantuan tanda bintang (*).]


# Kesimpulan
[Kesimpulan dari praktikum ini adalah pentingnya pemahaman mengenai tipe data bentukan dan modularitas program. Melalui penerapan Abstract Data Type (ADT), kita belajar bahwa memecah kode program menjadi beberapa file terpisah (seperti header .h dan body .cpp) membuat kode jauh lebih rapi, terstruktur, dan mudah untuk dikembangkan. Selain itu, penggunaan struct yang dipadukan dengan array terbukti sangat efektif untuk mengelompokkan dan menyimpan banyak data sekaligus secara efisien. Praktikum ini juga melatih kita dalam memanfaatkan fungsi, prosedur, dan pointer untuk memecah logika yang rumit serta memanipulasi data di dalam memori secara langsung, yang semuanya merupakan bekal penting untuk pengembangan perangkat lunak di dunia nyata.]


### Referensi
#### Modul pembelajaran


