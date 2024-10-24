## Studi Kasus: Manajemen Daftar Tugas

## Deskripsi
Kamu diminta untuk mengimplementasikan sebuah sistem manajemen daftar tugas (to-do list) menggunakan struktur data **ArrayList**. Setiap pengguna dapat menambah, menghapus, atau melihat daftar tugas yang harus diselesaikan.

Ada empat jenis operasi yang dapat dilakukan pada to-do list:

1. **TAMBAH x**: Menambahkan tugas dengan nama \( x \) ke dalam daftar tugas.
2. **HAPUS n**: Menghapus tugas yang berada pada posisi ke-\( n \) dalam daftar (1-indexed). Jika tugas pada posisi tersebut tidak ada, operasi ini diabaikan.
3. **CEKLIS n**: Menampilkan tugas pada posisi ke-\( n \) dalam daftar (1-indexed). Jika tidak ada tugas pada posisi tersebut, cetak "TIDAK ADA TUGAS".
4. **CEKSEMUA**: Menampilkan semua tugas yang ada dalam daftar. Jika daftar kosong, cetak "DAFTAR KOSONG".

## Input
- Baris pertama berisi sebuah bilangan bulat \( N \) (1 ≤ \( N \) ≤ 1000), yang merupakan jumlah total operasi.
- Setiap baris berikutnya berisi salah satu dari empat operasi: "TAMBAH x", "HAPUS n", "CEKLIS n", atau "CEKSEMUA".

## Output
- Untuk setiap operasi "CEKLIS" dan "CEKSEMUA", cetak hasil sesuai yang diminta.

## Contoh Input
```
7
TAMBAH Belajar
TAMBAH Makan
CEKSEMUA
CEKLIS 1
HAPUS 2
CEKSEMUA
CEKLIS 2
```

## Contoh Output
```
Belajar Makan
Belajar
Belajar
TIDAK ADA TUGAS
```

## Penjelasan
1. Tambahkan tugas "Belajar" ke dalam daftar.
2. Tambahkan tugas "Makan" setelahnya.
3. Saat dicek semua tugas, daftar berisi "Belajar Makan".
4. Saat dicek tugas pada posisi 1, hasilnya "Belajar".
5. Hapus tugas pada posisi 2, yaitu "Makan".
6. Saat dicek semua tugas, daftar hanya berisi "Belajar".
7. Saat dicek tugas pada posisi 2, hasilnya "TIDAK ADA TUGAS" karena posisi 2 sudah dihapus.

## Solusi
```java
import java.util.ArrayList;
import java.util.Scanner;

public class ToDoListArrayList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<String> tasks = new ArrayList<>();

        int N = sc.nextInt();
        sc.nextLine();

        for (int i = 0; i < N; i++) {
            String operation = sc.nextLine();

            if (operation.startsWith("TAMBAH")) {
                String task = operation.split(" ")[1];
                tasks.add(task);
            } else if (operation.startsWith("HAPUS")) {
                int index = Integer.parseInt(operation.split(" ")[1]);
                if (index > 0 && index <= tasks.size()) {
                    tasks.remove(index - 1); // 1-indexed
                }
            } else if (operation.startsWith("CEKLIS")) {
                int index = Integer.parseInt(operation.split(" ")[1]);
                if (index > 0 && index <= tasks.size()) {
                    System.out.println(tasks.get(index - 1));
                } else {
                    System.out.println("TIDAK ADA TUGAS");
                }
            } else if (operation.equals("CEKSEMUA")) {
                if (tasks.isEmpty()) {
                    System.out.println("DAFTAR KOSONG");
                } else {
                    for (String task : tasks) {
                        System.out.print(task + " ");
                    }
                    System.out.println();
                }
            }
        }
    }
}
```
