# Studi Kasus: Undo-Redo Editor

## Deskripsi
Sebuah aplikasi editor teks memiliki fitur undo dan redo untuk memudahkan penggunanya. Fitur ini dapat direpresentasikan dengan menggunakan struktur data **Stack**. Kamu diminta untuk mengimplementasikan sistem ini untuk melacak perubahan teks yang dilakukan pengguna.

Ada tiga jenis operasi yang dapat dilakukan oleh pengguna:

1. **TAMBAH x**: Menambahkan teks \( x \) ke dalam editor.
2. **UNDO**: Menghapus teks yang terakhir kali ditambahkan ke dalam editor (menggunakan undo).
3. **REDO**: Menambahkan kembali teks yang dihapus oleh operasi undo terakhir (menggunakan redo).
4. **CEKTEKS**: Menampilkan teks yang saat ini ada di editor. Jika editor kosong, cetak "EDITOR KOSONG".

Fitur undo hanya bisa dilakukan pada teks yang telah ditambahkan sebelumnya. Jika tidak ada teks yang bisa di-undo atau di-redo, perintah tersebut diabaikan.

## Input
- Baris pertama berisi sebuah bilangan bulat \( N \) (1 ≤ \( N \) ≤ 1000), yang merupakan jumlah total operasi.
- Setiap baris berikutnya berisi salah satu dari empat operasi: "TAMBAH x", "UNDO", "REDO", atau "CEKTEKS".

## Output
- Untuk setiap operasi "CEKTEKS", cetak teks yang saat ini ada di editor, atau "EDITOR KOSONG" jika tidak ada teks dalam editor.

## Contoh Input
```
8
TAMBAH hello
TAMBAH world
CEKTEKS
UNDO
CEKTEKS
REDO
CEKTEKS
UNDO
```

## Contoh Output
```
hello world
hello
hello world
hello
```

## Penjelasan
1. Tambahkan teks "hello" ke dalam editor.
2. Tambahkan teks "world" setelahnya.
3. Saat dicek, editor berisi "hello world".
4. Undo dilakukan, sehingga "world" dihapus dari editor.
5. Saat dicek, editor hanya berisi "hello".
6. Redo dilakukan, mengembalikan "world" ke editor.
7. Saat dicek, editor kembali berisi "hello world".
8. Undo dilakukan lagi, menghapus "world" dari editor.

## Solusi
```java
import java.util.Scanner;
import java.util.Stack;

public class EditorStack {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Stack<String> undoStack = new Stack<>();
        Stack<String> redoStack = new Stack<>();

        int N = sc.nextInt();
        sc.nextLine(); // Consume newline after reading N

        for (int i = 0; i < N; i++) {
            String operation = sc.nextLine();

            if (operation.startsWith("TAMBAH")) {
                String text = operation.split(" ")[1];
                undoStack.push(text);
                redoStack.clear(); // Clear redo stack after new addition
            } else if (operation.equals("UNDO")) {
                if (!undoStack.isEmpty()) {
                    redoStack.push(undoStack.pop());
                }
            } else if (operation.equals("REDO")) {
                if (!redoStack.isEmpty()) {
                    undoStack.push(redoStack.pop());
                }
            } else if (operation.equals("CEKTEKS")) {
                if (undoStack.isEmpty()) {
                    System.out.println("EDITOR KOSONG");
                } else {
                    System.out.println(String.join(" ", undoStack));
                }
            }
        }
    }
}
```
