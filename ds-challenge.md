# Resep Makanan

## Deskripsi:
Budi adalah seorang koki yang sedang sibuk menyiapkan beberapa pesanan makanan di restoran. Setiap pesanan makanan tiba dalam antrian berdasarkan waktu pesanan diterima. Namun, beberapa makanan membutuhkan bahan yang harus diambil dari gudang penyimpanan. Bahan-bahan ini disusun di atas rak seperti tumpukan. Budi harus mengambil bahan-bahan dari atas tumpukan sesuai kebutuhan resep. Setelah semua bahan siap, Budi dapat menyelesaikan pesanan dan menghapusnya dari antrian.

Kamu harus membantu Budi menyusun dan menyelesaikan pesanan dengan benar. Setiap pesanan memiliki bahan-bahan yang harus diambil dari tumpukan, dan pesanan diselesaikan sesuai urutan antrian.

## Input Format:
- Baris pertama berisi satu bilangan bulat `n` yang merupakan jumlah pesanan.
- Baris berikutnya berisi `n` baris, masing-masing berisi daftar bahan untuk setiap pesanan yang dipisahkan oleh spasi. Setiap pesanan ditangani dalam urutan antrian.
- Baris terakhir berisi satu bilangan bulat `m` yang merupakan jumlah bahan di tumpukan, diikuti oleh `m` string yang merupakan nama bahan di tumpukan (urutan bahan diinput dari atas ke bawah tumpukan).

## Output Format:
- Cetak "Pesanan [i] selesai" setiap kali pesanan ke-i diselesaikan (dengan bahan-bahan tersedia dari tumpukan). Jika ada bahan yang tidak ditemukan, cetak "Bahan [nama_bahan] tidak tersedia untuk Pesanan [i]".

## Contoh Input:
```
2
telur susu gula
tepung susu
5 telur susu tepung gula garam
```

## Contoh Output:
```
Pesanan 1 selesai
Pesanan 2 selesai
```

## Contoh Input 2:
```
3
telur susu
tepung garam
susu mentega
4 tepung susu gula telur
```

## Contoh Output 2:
```
Pesanan 1 selesai
Bahan garam tidak tersedia untuk Pesanan 2
Bahan mentega tidak tersedia untuk Pesanan 3
```

## Penjelasan:
Untuk test case pertama, tumpukan memiliki bahan-bahan yang dibutuhkan oleh setiap pesanan dalam urutan yang benar. Semua pesanan dapat diselesaikan. Pada test case kedua, bahan "garam" dan "mentega" tidak tersedia, sehingga pesanan kedua dan ketiga tidak bisa diselesaikan.

## Solusi Java:
```java
import java.util.*;

public class ResepMakanan {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        sc.nextLine(); // konsumsi newline

        Queue<List<String>> orders = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            String[] order = sc.nextLine().split(" ");
            orders.add(Arrays.asList(order));
        }

        int m = sc.nextInt();
        Stack<String> stack = new Stack<>();
        for (int i = 0; i < m; i++) {
            stack.push(sc.next());
        }

        for (int i = 1; i <= n; i++) {
            List<String> currentOrder = orders.poll();
            Stack<String> tempStack = new Stack<>();
            boolean canComplete = true;

            for (String item : currentOrder) {
                while (!stack.isEmpty() && !stack.peek().equals(item)) {
                    tempStack.push(stack.pop());
                }

                if (stack.isEmpty()) {
                    System.out.println("Bahan " + item + " tidak tersedia untuk Pesanan " + i);
                    canComplete = false;
                    break;
                } else {
                    stack.pop();
                }

                while (!tempStack.isEmpty()) {
                    stack.push(tempStack.pop());
                }
            }

            if (canComplete) {
                System.out.println("Pesanan " + i + " selesai");
            }
        }
    }
}
```

