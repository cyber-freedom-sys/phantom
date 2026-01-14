# Phantom - Alat Uji Beban HTTP

`DeepGo` adalah alat bantu baris perintah (CLI) sederhana namun kuat yang ditulis dalam Go untuk melakukan uji beban (load testing) pada endpoint HTTP. Alat ini memungkinkan Anda untuk mengirim sejumlah besar permintaan GET secara bersamaan ke URL target dan mengukur kinerja server.

## Fitur

-   **Uji Beban Konkuren**: Menggunakan goroutine Go untuk mengirim ribuan permintaan secara efisien dan bersamaan.
-   **Dapat Dikonfigurasi**: Semua parameter utama dapat disesuaikan melalui flag command-line.
-   **Statistik Terperinci**: Memberikan ringkasan hasil yang jelas, termasuk jumlah permintaan yang berhasil/gagal, tingkat keberhasilan, dan waktu respons rata-rata.
-   **Mode Verbose**: Opsi untuk melihat status dan durasi setiap permintaan individu secara real-time.
-   **Timeout**: Konfigurasi waktu tunggu (timeout) untuk setiap permintaan guna mencegah proses yang menggantung.

## Prasyarat

-   [Go](https://golang.org/dl/) versi 1.18 atau yang lebih baru.

## Instalasi & Kompilasi

1.  Clone repositori ini atau unduh file `main.go`.
2.  Buka terminal di direktori proyek.
3.  Jalankan perintah berikut untuk mengompilasi aplikasi:
    ```bash
    # Untuk Linux/macOS
    go build -o phantom main.go

    # Untuk Windows (menghasilkan DeepGo.exe)
    go build -o phantom.exe main.go
    ```
    Ini akan membuat file eksekusi bernama `phantom` (atau `phantom.exe` di Windows) di direktori Anda.

## Penggunaan

Jalankan aplikasi dari terminal dengan flag yang diperlukan.

```bash
./phantom [flags]
```

### Flags

| Flag | Tipe | Default | Deskripsi |
|---|---|---|---|
| `-url` | string | `http://localhost:8080` | URL target yang akan diuji. |
| `-n` | int | `100` | Jumlah total permintaan yang akan dikirim. |
| `-c` | int | `10` | Jumlah permintaan konkuren (goroutine) yang berjalan bersamaan. |
| `-timeout` | duration | `30s` | Waktu tunggu untuk setiap permintaan (contoh: `10s`, `1m`). |
| `-v` | bool | `false` | Aktifkan output verbose untuk melihat hasil setiap permintaan. |

## Contoh

#### 1. Uji Dasar
Mengirim 1000 permintaan ke server lokal dengan 50 koneksi konkuren.

```bash
./phantom -url="http://localhost:3000/api/v1/test" -n=1000 -c=50
```

#### 2. Uji dengan Timeout dan Mode Verbose
Mengirim 200 permintaan ke situs publik dengan 20 koneksi konkuren, timeout 5 detik per permintaan, dan mengaktifkan output verbose.

```bash
./phantom -url="https://www.google.com" -n=200 -c=20 -timeout=5s -v
```

## Contoh Output

#### Output Standar
```
===== LOAD TEST RESULTS =====
Target URL:        http://localhost:8080
Total Requests:    100
Concurrency Level: 10
Successful (2xx):  100 (100.00%)
Failed:            0
Avg Response Time: 12ms
=============================
```

#### Output dengan Mode Verbose (`-v`)
Mode ini akan menampilkan hasil setiap permintaan saat selesai, diikuti oleh ringkasan akhir.

```
[SUCCESS] Status: 200 (Duration: 10ms)
[SUCCESS] Status: 200 (Duration: 15ms)
[FAIL] Request error: Get "http://localhost:8080": dial tcp [::1]:8080: connectex: No connection could be made because the target machine actively refused it. (Duration: 2ms)
...

===== LOAD TEST RESULTS =====
Target URL:        http://localhost:8080
Total Requests:    10
Concurrency Level: 2
Successful (2xx):  0 (0.00%)
Failed:            10
=============================
```

## Kontribusi

Kontribusi sangat diterima! Silakan buka *issue* untuk melaporkan bug atau mengajukan fitur baru. Anda juga bisa membuat *pull request* untuk perbaikan atau penambahan fungsionalitas.

## Lisensi

Proyek ini dilisensikan di bawah [Lisensi MIT](LICENSE).
