# ION NETWORK API STANDARD

Seluruh deskripsi di bawah merupakan standar dari API yang dibuat oleh Ion Network.

## KETENTUAN UMUM
* Menggunakan versi dalam URLnya | contohnya `http://example.com/api/android/v1` 
* URL dibuat dengan menggunakan `kebab-case` | contohnya `http://example.com/api/ios/v1/sample-api-url`
* Menggunakan singular form | contohnya `http://example.com/api/android/v1/table` atau `http://example.com/api/ios/v1/city` 
* Menggunakan id untuk mengakses child object | contohnya `http://example.com/api/android/v1/country/{id}/city`
* Menggunakan pagination untuk mengakses kumpulan object | contohnya `http://example.com/api/ios/v1/city?page=1`
* Memisahkan URL untuk setiap platform yang akan menggunakan API tsb | contohnya `http://example.com/api/android/v1/city?page=1`
* URL publik harus dilindungi dengan menggunakan `X-APP-TOKEN` ( dikirimkan via Header )
* API harus memiliki discovery URL
* Private Token harus dikirimkan melalui Header
* Menggunakan raw parameter berisi JSON untuk non multipart request
* Maksimal waktu response API adalah 250ms untuk data umum / detail dan 400ms untuk kumpulan data

## KETENTUAN PENGEMBALIAN DATA
* Data yang dikembalikan harus menggunakan transformer untuk memastikan konsistensi struktur data
  * Sebaiknya 1 Transformer digunakan untuk 1 endpoint untuk menghindari perubahan struktur / key yang akan mengubah endpoint lain

* Nilai data yang dikembalikan harus sesuai dengan tipenya ( apabila tipenya DOUBLE jangan mengembalikan STRING, apabila tipenya OBJECT jangan mengembalikan ARRAY dll )
* Hindari pengembalian null value apabila sangat tidak terpaksa
* Sebelum pengembalian data, harus ada validasi response untuk memastikan tidak hilangnya data yang dibutuhkan

## List Request

* Data **HARUS** di-paging, ukuran record-per-page dapat menyesuaikan dengan kondisi yang berjalan
* `next` pointer link **HARUS** berupa string, jika current pointer adalah pointer terakhir dari daftar pointer, maka backend cukup mengembalikan string kosong: `""`.

Contoh kembalian data dari List

```json
{
    "data": [],
    "meta": {
        "links": {
            "next": "/relative/url/to/resource",
            "prev": "/relative/url/to/resource"
        },
        "total_data": 100,
        "count": 2,
        "per_page": 10,
        "current_page": 10,
        "total_page": 10
    },
}
```

## READ Request
* Menggunakan HTTP GET Method
* Mengembalikan HTTP Status Code 200 untuk return value dengan data, dan HTTP Status Code 204 untuk return value tanpa data.

Contoh kembalian data READ

```json
{
    "data": {},
    "message": "get data xxx success"
}
```

## CREATE Request 
* Menggunakan HTTP PUT / POST Method
* Mengembalikan HTTP Status Code 201 apabila data berhasil dibuat

## UPDATE Request
* Menggunakan HTTP PUT / PATCH Method
* Mengembalikan HTTP Status Code 200 apabila data berhasil diperbarui

## DELETE Request
* Menggunakan HTTP DELETE Method
* Mengembalikan HTTP Status Code 200 apabila data berhasil dihapus

Contoh kembalian data untuk CREATE UPDATE & DELETE

```json
{
    "message": "pesan yang bersesuaian dengan aksi"
}
```

## RESPONSE UNTUK ERROR
* Error Autentikasi

Harus mengembalikan HTTP Status Code 401 dengan error data sbb

```json
{
    "code": 401.5,
    "message": "error message"
}
```

* Error Validasi

Harus mengembalikan HTTP Status Code 422 dengan error data sbb

```json
{
    "message": "error message",
    "errors": [{
        "field": "foo",
        "message": ["pesan error 1", "pesan error 2"]
    }, {
        "field": "bar",
        "message": ["pesan error 1", "pesan error 2"]
    }]
}
```

* Error URL Tidak Ditemukan

Harus mengembalikan HTTP Status Code 404 dengan error data sbb 

```json
{
    "message": "pesan yang bersesuaian dengan error"
}
```

* Error Server

Harus mengembalikan HTTP Status Code 500 dengan error data sbb

```json
{
    "message": "error message",
    "trace": "string formatted stack trace"
}
```

> `trace` hanya ditampilkan pada saat aplikasi run di staging environment, pada saat aplikasi run di  production environment, `trace` **HARUS** disembunyikan.

# Untuk kondisi lain 

Apabila dijumpai kondisi yang tidak diprediksi, silahkan menggunakan kembalian data

```json
{
    "message": "pesan yang bersesuaian kondisi"
}
```

dengan HTTP Status Code yang sesuai dengan situasi

# CATATAN

## DAFTAR STATUS CODE HTTP

### 1XX - Informational Responses
- `100 Continue`: Server telah menerima header request dan klien dapat melanjutkan mengirim body request
- `101 Switching Protocols`: Server menyetujui pergantian protokol yang diminta klien
- `102 Processing`: Server memproses request, mencegah timeout
- `103 Early Hints`: Memberikan beberapa header sebelum respon final

### 2XX - Successful Responses
- `200 OK`: Request berhasil dan data dikembalikan dengan sukses
- `201 Created`: Request berhasil dan sumber daya baru telah dibuat
- `202 Accepted`: Request diterima untuk diproses, namun belum selesai
- `204 No Content`: Request berhasil namun tidak ada konten untuk dikembalikan

### 3XX - Redirection Responses
- `301 Moved Permanently`: Sumber daya telah dipindahkan secara permanen ke URL baru
- `302 Found`: Sumber daya sementara dialihkan ke URL lain
- `304 Not Modified`: Sumber daya tidak dimodifikasi sejak permintaan terakhir
- `307 Temporary Redirect`: Pengalihan sementara dengan metode HTTP yang sama
- `308 Permanent Redirect`: Pengalihan permanen dengan metode HTTP yang sama

### 4XX - Client Error Responses
- `400 Bad Request`: Server tidak dapat memproses request karena kesalahan klien
- `401 Unauthorized`: Autentikasi diperlukan atau kredensial tidak valid
- `403 Forbidden`: Klien tidak memiliki izin untuk mengakses sumber daya
- `404 Not Found`: Sumber daya yang diminta tidak dapat ditemukan
- `405 Method Not Allowed`: Metode HTTP tidak diizinkan untuk sumber daya
- `408 Request Timeout`: Server tidak menerima request sepenuhnya dalam waktu yang ditentukan
- `422 Unprocessable Entity`: Request yang benar namun tidak dapat diproses karena kesalahan semantik
- `429 Too Many Requests`: Klien telah mengirim terlalu banyak request dalam waktu tertentu

### 5XX - Server Error Responses
- `500 Internal Server Error`: Kesalahan umum pada server
- `501 Not Implemented`: Fungsi yang diminta tidak didukung oleh server
- `502 Bad Gateway`: Server gateway menerima respon tidak valid dari server hulu
- `503 Service Unavailable`: Server sementara tidak dapat menangani request
- `504 Gateway Timeout`: Server gateway tidak menerima respon tepat waktu dari server hulu
- `505 HTTP Version Not Supported`: Versi HTTP tidak didukung oleh server