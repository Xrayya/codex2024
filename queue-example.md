# Studi Kasus: Manajemen Antrian Vaksinasi

## Deskripsi
Sebuah pusat vaksinasi sedang melakukan layanan kepada masyarakat dengan mengelola antrian pendaftaran vaksinasi. Setiap orang yang datang akan mendapatkan nomor antrian, dan layanan akan memproses orang-orang yang berada dalam antrian satu per satu.

Ada tiga jenis operasi yang dapat dilakukan oleh pusat vaksinasi:

1. **DAFTAR x**: Orang dengan nomor ID \( x \) mendaftar dan masuk ke dalam antrian.
2. **LAYANI**: Orang yang berada di depan antrian mendapatkan vaksinasi dan keluar dari antrian.
3. **CEKDEPAN**: Lihat nomor ID orang yang berada di depan antrian. Jika antrian kosong, cetak "ANTRIAN KOSONG".

Sebagai seorang pengelola IT pusat vaksinasi, kamu diminta untuk membantu memproses semua operasi ini dan memberikan hasil dari setiap operasi **CEKDEPAN**.

## Input
- Baris pertama berisi sebuah bilangan bulat \( N \) (1 ≤ \( N \) ≤ 1000), yang merupakan jumlah total operasi.
- Setiap baris berikutnya berisi salah satu dari tiga operasi: "DAFTAR x", "LAYANI", atau "CEKDEPAN".

## Output
- Untuk setiap operasi "CEKDEPAN", cetak nomor ID orang yang berada di depan antrian, atau cetak "ANTRIAN KOSONG" jika tidak ada orang dalam antrian.

## Contoh Input
```
7
DAFTAR 101
DAFTAR 202
CEKDEPAN
LAYANI
CEKDEPAN
LAYANI
CEKDEPAN
```

## Contoh Output
```
101
202
ANTRIAN KOSONG
```

## Penjelasan
1. Orang dengan ID 101 mendaftar ke dalam antrian.
2. Orang dengan ID 202 mendaftar setelahnya.
3. Saat dicek, orang dengan ID 101 berada di depan antrian.
4. Orang dengan ID 101 dilayani dan keluar dari antrian.
5. Saat dicek kembali, orang dengan ID 202 berada di depan.
6. Orang dengan ID 202 dilayani dan keluar dari antrian.
7. Antrian kosong ketika dicek terakhir.

## Solusi
```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class VaksinQueue {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Queue<Integer> queue = new LinkedList<>();

        int N = sc.nextInt();
        sc.nextLine();

        for (int i = 0; i < N; i++) {
            String operation = sc.nextLine();

            if (operation.startsWith("DAFTAR")) {
                int x = Integer.parseInt(operation.split(" ")[1]);
                queue.add(x);
            } else if (operation.equals("LAYANI")) {
                if (!queue.isEmpty()) {
                    queue.poll();
                }
            } else if (operation.equals("CEKDEPAN")) {
                if (queue.isEmpty()) {
                    System.out.println("ANTRIAN KOSONG");
                } else {
                    System.out.println(queue.peek());
                }
            }
        }
    }
}
```
