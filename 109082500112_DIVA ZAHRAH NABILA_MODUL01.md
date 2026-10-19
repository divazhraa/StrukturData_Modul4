# <h1 align="center">Laporan Praktikum Modul 4 - SINGLY LINKED LIST (BAGIAN PERTAMA)- ... </h1>
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
### list.h: 

```cpp
#ifndef List_h
#define List_h
#define Nil NULL

#include <iostream>
using namespace std;

struct mahasiswa{
    string nama, nim;
    int umur;
};

typedef mahasiswa dataMahasiswa;
typedef struct node *address;

struct node{
    dataMahasiswa isidata;
    address next;
};

struct linkedlist{
    address first;
};

bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedlist list);
void insertFirst(linkedlist &list, address nodeBaru);
void insertAfter(linkedlist &list, address nodeBaru, address prev);
void insertLast(linkedlist &list, address nodeBaru);

void delFirst(linkedlist &List);
void delLast(linkedlist &List);
void delAfter(linkedlist &List, address nodeHapus, address nodePrev);
int nbList(linkedlist List);
void deleteList(linkedlist &List);
#endif
``` 

### Penjelasan: list.h File header ini berisi deklarasi struktur data dan daftar fungsi yang dipakai program. Struct mahasiswa menyimpan data nama, NIM, dan umur, lalu node membungkus data tersebut bersama pointer next yang menunjuk ke node berikutnya. Struct linkedlist hanya berisi pointer first sebagai penunjuk node pertama. Nil didefinisikan sebagai NULL agar penulisan pointer kosong lebih mudah dibaca. Bagian #ifndef ... #endif mencegah header terbaca dua kali saat kompilasi.


### list.cpp
```cpp
#include "list.h"
#include <iostream>
using namespace std;

bool isEmpty(linkedlist List)
{
    return List.first == Nil;
}

void createList(linkedlist &List)
{
    List.first = Nil;
}

address alokasi(string nama, string nim, int umur)
{
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

void dealokasi(address &node)
{
    node->next = Nil;
    delete node;
    node = Nil;
}

void insertFirst(linkedlist &List, address nodeBaru)
{
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev)
{
    if (Prev != Nil)
    {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    }
}

void insertLast(linkedlist &List, address nodeBaru)
{
    if (isEmpty(List))
    {
        List.first = nodeBaru;
    }
    else
    {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil)
        {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

void delFirst(linkedlist &List)
{
    if (!isEmpty(List))
    {
        address nodeHapus = List.first; 
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    }
    else
    {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List)
{
    address nodeHapus, nodePrev = Nil;
    if (!isEmpty(List))
    {
        nodeHapus = List.first;
        if (nodeHapus->next == Nil)
        {
            List.first = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            while (nodeHapus->next != Nil)
            {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    }
    else
    {
        cout << "List kosong!" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev)
{
    if (isEmpty(List))
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        if (nodePrev != Nil && nodePrev->next != Nil)
        {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next; 
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

void printList(linkedlist list)
{
    if (isEmpty(list))
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        address nodeBantu = list.first;
        while (nodeBantu != Nil)
        {
            cout << "Nama: " << nodeBantu->isidata.nama
                 << ", NIM: " << nodeBantu->isidata.nim
                 << ", Usia: " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

int nbList(linkedlist List)
{
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil)
    {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

void deleteList(linkedlist &List)
{ 
    address nodeBantu = List.first;
    while (nodeBantu != Nil)
    {
        address nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus." << endl;
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

### Penjelasan: File list.cpp berisi implementasi semua operasi pada linked list. Fungsi isEmpty dan createList memeriksa dan menginisialisasi list kosong, sedangkan alokasi membuat node baru dengan new dan dealokasi menghapusnya dengan delete. Untuk penyisipan, insertFirst, insertAfter, dan insertLast menambahkan node di awal, setelah node tertentu, dan di akhir list dengan mengatur ulang pointer next. Untuk penghapusan, delFirst, delLast, dan delAfter melepas node dari awal, akhir, atau setelah node tertentu lalu membebaskan memorinya, dengan menyambungkan kembali pointer agar sisa list tidak terputus. Terakhir, printList menampilkan seluruh isi list, nbList menghitung jumlah node, dan deleteList menghapus semua node hingga list kembali kosong.


### main.cpp:
```cpp
#include "list.h"
using namespace std;

int main()
{
    linkedlist List;
    address nodeA = Nil, nodeB = Nil, nodeC = Nil, nodeD = Nil, nodeE = Nil;
    createList(List);

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "221110014", 21);
    nodeC = alokasi("Rizal", "231110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    delFirst(List);             
    delLast(List);              
    delAfter(List, Nil, nodeC); 

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List); 
    cout << "jumlah node : " << nbList(List) << endl;

    return 0;
}
```
### Penjelasan: Program utama membuat sebuah list kosong, lalu mengalokasikan lima node mahasiswa (Dhimas, Arvin, Rizal, Satrio, Joshua). Kelima node dimasukkan ke list menggunakan kombinasi insertFirst, insertLast, dan insertAfter, sehingga urutannya menjadi Dhimas, Rizal, Satrio, Arvin, Joshua. Isi list dan jumlah node dicetak untuk memastikan proses insert berhasil. Setelah itu program menjalankan delFirst, delLast, dan delAfter untuk menghapus node tertentu, mencetak ulang isi list, dan terakhir memanggil deleteList untuk membebaskan seluruh memori yang tersisa sebelum program selesai.



# Unguided
### 1. Singlylist.h
```cpp
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL

typedef int infotype;
typedef struct ElmList *address;

struct ElmList{
    infotype info;
    address next;
};

struct List{
    address First;
};


void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif 
```

### penjelasan 
[File singlylist.h mendefinisikan struktur singly linked list sederhana yang setiap node-nya menyimpan satu data bertipe int (lewat alias infotype), dengan address sebagai pointer ke node ElmList yang berisi info dan pointer next, serta struct List yang hanya menyimpan pointer First sebagai penunjuk node pertama. Nil dipakai sebagai penanda pointer kosong, dan #ifndef ... #endif mencegah header terbaca dua kali. Header ini mendeklarasikan lima fungsi: createList untuk membuat list kosong, alokasi untuk membuat node baru, dealokasi untuk menghapus node dari memori, printInfo untuk menampilkan isi list, dan insertFirst untuk menyisipkan node di awal list. Karena hanya berisi deklarasi, header ini perlu dilengkapi file .cpp yang berisi definisi fungsinya, lalu dikompilasi bersama.]


### 2. Singlylist.cpp

```cpp
#include <iostream>
#include "Singlylist.h"
using namespace std;

void createList(List &L){
    L.First = Nil;
}

address alokasi(infotype x){
    address P = new ElmList;
    if (P != Nil)
    {
        P->info = x;
        P->next = Nil;
    }
    return P;
}

void dealokasi(address &P){
    delete P;
    P = Nil;
}

void printInfo(List L){
    address P = L.First;
    while (P != Nil)
    {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P){
    if (P != Nil)
    {
        P->next = L.First;
        L.First = P;
    }
}
```


### penjelasan
[File singlylist.cpp ini berisi implementasi dari lima fungsi yang dideklarasikan di header. createList menginisialisasi list kosong dengan mengisi First dengan Nil, sedangkan alokasi membuat node baru menggunakan new, lalu mengisi info dengan nilai x dan next dengan Nil setelah memastikan alokasi berhasil (pointer tidak Nil). dealokasi membebaskan memori node dengan delete dan mengosongkan pointernya agar tidak menjadi dangling pointer. printInfo menelusuri list dari First sampai akhir sambil mencetak setiap info dipisahkan spasi, lalu mencetak baris baru (jika list kosong, hanya baris kosong yang tampil). Terakhir, insertFirst menyisipkan node di awal list dengan membuat next node baru menunjuk ke First lama, lalu menjadikan node tersebut sebagai First, dan hanya dijalankan jika node yang diberikan tidak Nil. Satu hal yang perlu diperhatikan: file ini meng-include "Singlylist.h" (huruf S besar), sehingga nama file headernya harus persis sama. Di Windows hal ini biasanya tidak bermasalah, tetapi di Linux atau macOS akan menimbulkan error No such file or directory jika nama filenya singlylist.h.]



### 3. Singlylist main.cpp

```cpp
#include <iostream>
#include "Singlylist.h"
using namespace std;

int main()
{
    List L;
    address P1, P2, P3, P4, P5;

    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);
    printInfo(L);

    return 0;
}
```
### Output :
![Screenshot Output Unguided 1_!] (https://github.com/divazhraa/StrukturData_Modul4/blob/main/Modul04/output/OUTPUT1.png)


### penjelasan
[File main.cpp ini membuat sebuah list kosong dengan createList, lalu mengalokasikan lima node berturut-turut dengan nilai 2, 0, 8, 12, dan 9, dan setiap node langsung disisipkan di awal list menggunakan insertFirst. Karena insertFirst selalu menaruh node baru di posisi paling depan, urutan di dalam list menjadi terbalik dari urutan pemasukannya, yaitu node yang terakhir dimasukkan (9) berada di depan dan node yang pertama (2) berada di belakang. Setelah itu printInfo dipanggil untuk menampilkan isi list, sehingga output yang muncul adalah 9 12 8 0 2. Program diakhiri dengan return 0, tetapi memori kelima node belum dibebaskan dengan dealokasi sehingga terjadi memory leak kecil (tidak masalah untuk program latihan sederhana ini, namun sebaiknya diperhatikan pada program yang lebih besar). Agar program berhasil dijalankan, ketiga file harus dikompilasi bersama dengan perintah g++ main.cpp Singlylist.cpp -o program, dan penulisan "Singlylist.h" harus sama persis dengan nama file headernya.]


# Kesimpulan
[Kesimpulan dari praktikum ini adalah Praktikum ini membahas implementasi singly linked list dalam C++ dengan pemrograman modular, yaitu dipisah menjadi file header untuk deklarasi, file .cpp untuk implementasi fungsi, dan main.cpp untuk menjalankan program. Program pertama menyimpan data mahasiswa (nama, NIM, umur) dengan operasi lengkap berupa penyisipan di awal, tengah, dan akhir, penghapusan di awal, akhir, dan setelah node tertentu, serta menampilkan, menghitung, dan menghapus seluruh list, sedangkan program kedua menyederhanakannya dengan data int dan operasi dasar seperti createList, alokasi, dealokasi, printInfo, dan insertFirst, yang menghasilkan urutan terbalik (9 12 8 0 2) karena setiap node disisipkan di depan. Dari kedua program dapat disimpulkan bahwa linked list bersifat dinamis karena node dibuat dengan new dan dihapus dengan delete, seluruh operasinya bertumpu pada pengaturan pointer next yang harus teliti agar list tidak terputus dan tidak terjadi memory leak, kasus khusus seperti list kosong dan list satu elemen harus ditangani, serta nama fungsi, signature, dan file harus konsisten dan dikompilasi bersama agar tidak muncul error undefined reference. Pemahaman ini menjadi dasar untuk mempelajari struktur data lanjutan seperti doubly linked list, stack, queue, dan tree. ]


### Referensi
#### Modul pembelajaran


