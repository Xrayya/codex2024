# Perkebunan Buah Prima

## Deskripsi:
Tono memiliki perkebunan dengan beberapa jenis pohon buah yang ditanam secara berbaris. Setiap pohon diberi nomor sesuai posisinya di barisan. Tono hanya ingin memetik buah dari pohon-pohon yang nomornya adalah bilangan prima, dan Tono juga ingin menghitung berapa banyak pohon yang bisa dipetik dari pohon-pohon dengan nomor yang merupakan faktor dari sebuah bilangan `n`.

Bantu Tono untuk menentukan jumlah pohon yang nomornya adalah bilangan prima hingga `n` dan juga jumlah pohon yang bisa dipetik karena nomornya merupakan faktor dari `n`.

## Input Format:
- Satu bilangan bulat `n` yang merupakan jumlah pohon dalam barisan.

## Output Format:
- Cetak dua angka. Angka pertama adalah jumlah pohon dengan nomor bilangan prima hingga `n`. Angka kedua adalah jumlah pohon yang nomornya merupakan faktor dari `n`.

## Contoh Input:
```
10
```

## Contoh Output:
```
4 4
```

## Contoh Input 2:
```
15
```

## Contoh Output 2:
```
6 4
```

## Penjelasan:
Untuk test case pertama, bilangan prima dari 1 hingga 10 adalah [2, 3, 5, 7], sehingga ada 4 pohon dengan nomor prima. Faktor dari 10 adalah [1, 2, 5, 10], sehingga ada 4 pohon yang bisa dipetik karena nomornya merupakan faktor dari 10.

## Solusi Java:

### Solusi 1: Menggunakan Brute-Force untuk Bilangan Prima dan Faktor
```java
import java.util.*;

public class BuahPrima {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        // Menghitung bilangan prima
        int primeCount = 0;
        for (int i = 2; i <= n; i++) {
            if (isPrime(i)) {
                primeCount++;
            }
        }

        // Menghitung faktor dari n
        int factorCount = 0;
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) {
                factorCount++;
            }
        }

        System.out.println(primeCount + " " + factorCount);
    }

    public static boolean isPrime(int num) {
        if (num < 2) return false;
        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

### Solusi 2: Menggunakan Sieve of Eratosthenes untuk Bilangan Prima
```java
import java.util.*;

public class BuahPrimaSieve {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        // Menghitung bilangan prima menggunakan Sieve of Eratosthenes
        boolean[] isPrime = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;

        for (int i = 2; i * i <= n; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= n; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        int primeCount = 0;
        for (int i = 2; i <= n; i++) {
            if (isPrime[i]) {
                primeCount++;
            }
        }

        // Menghitung faktor dari n
        int factorCount = 0;
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) {
                factorCount++;
            }
        }

        System.out.println(primeCount + " " + factorCount);
    }
}
```
