# TikTok Search via GetDL - Node.js TikTok Video Search Scraper

> **GitHub Repository Title**
>
> ```text
> TikTok Search via GetDL - Node.js Video Search Scraper
> ```
>
> **Repository Name**
>
> ```text
> tiktok-search-getdl
> ```
>
> **GitHub Repository Description**
>
> ```text
> Node.js ESM CLI scraper for searching public TikTok videos through GetDL. Returns direct MP4 play URLs, watermark URLs, video stats, author details, music metadata, cover images, region, and cursor pagination in JSON format.
> ```

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js">
  <img src="https://img.shields.io/badge/JavaScript-ESM-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript ESM">
  <img src="https://img.shields.io/badge/TikTok-Video%20Search-000000?style=for-the-badge&logo=tiktok&logoColor=white" alt="TikTok">
  <img src="https://img.shields.io/badge/Creator-SCRIPETEREN-181717?style=for-the-badge&logo=github&logoColor=white" alt="Creator">
</p>

<p align="center">
  <b>Node.js ESM CLI scraper untuk mencari video TikTok publik melalui GetDL.</b><br>
  Mengambil hasil pencarian berdasarkan keyword, direct MP4 play URL, watermark URL, thumbnail, statistik video, author, informasi musik, region, serta cursor pagination dalam format JSON.
</p>

---

## Fitur

- Mencari video TikTok berdasarkan keyword
- Menggunakan GetDL sebagai perantara pencarian
- Membuat session GetDL otomatis melalui endpoint session
- Menyimpan cookie session di memory
- Mengambil cookie `getdl_sid` jika dikirim server
- Mengambil direct `playUrl` video MP4
- Mengambil `wmPlayUrl` atau video watermark jika tersedia
- Mengambil cover dan origin cover video
- Mengambil video ID dan Aweme ID
- Mengambil judul atau caption video
- Mengambil durasi video
- Mengambil region video
- Mengambil statistik video jika tersedia
- Mengambil informasi author
- Mengambil ID author
- Mengambil username author
- Mengambil nickname author
- Mengambil avatar author
- Mengambil informasi music atau audio video
- Mengambil music ID
- Mengambil judul music
- Mengambil author music
- Mengambil duration music
- Mengambil direct music URL jika tersedia
- Mengambil cover music
- Mengubah timestamp video menjadi ISO date
- Mendukung pagination menggunakan cursor
- Mendukung region pencarian
- Mendukung sort type
- Mendukung custom jumlah hasil menggunakan `--limit`
- Menangani retry request HTTP sementara
- Menangani timeout request
- Menangani rate limit `RATE_LIMITED`
- Mendukung verbose log menggunakan `--verbose` atau `-v`
- Output JSON yang siap digunakan untuk bot, API, website, atau aplikasi Node.js
- Dapat digunakan sebagai CLI maupun ESM module

---

## Teknologi

Project ini menggunakan:

- [Node.js](https://nodejs.org/) 18 atau lebih baru
- Native `fetch()` dari Node.js
- `node:util`
- `AbortController`
- ESM Module JavaScript
- GetDL search endpoint
- TikTok public video search data melalui GetDL

Node.js 18+ diperlukan karena script menggunakan global `fetch()` bawaan Node.js.

---

## Struktur Project

```text
tiktok-search-getdl/
├── tiktok.js
├── package.json
├── .gitignore
├── README.md
└── LICENSE
```

---

## Instalasi

Clone repository:

```bash
git clone [https://github.com/SCRIPETEREN/tiktok-search-getdl.git](https://github.com/SCRIPETEREN/tiktok-search-getdl.git)
```

Masuk ke folder project:

```bash
cd tiktok-search-getdl
```

Project ini tidak membutuhkan dependency NPM tambahan karena memakai `fetch()` bawaan Node.js.

Pastikan Node.js yang digunakan minimal versi 18:

```bash
node -v
```

Contoh hasil:

```text
v18.0.0
```

Atau versi yang lebih baru:

```text
v20.x.x
```

```text
v22.x.x
```

---

## package.json

Buat file `package.json` dengan isi berikut agar Node.js membaca file JavaScript sebagai ESM module:

```json
{
  "name": "tiktok-search-getdl",
  "version": "1.0.0",
  "description": "Node.js ESM CLI scraper untuk mencari video TikTok melalui GetDL.",
  "type": "module",
  "main": "tiktok.js",
  "scripts": {
    "start": "node tiktok.js",
    "help": "node tiktok.js"
  },
  "keywords": [
    "tiktok",
    "tiktok-search",
    "tiktok-scraper",
    "getdl",
    "video-search",
    "nodejs",
    "esm",
    "scraper"
  ],
  "author": "SCRIPETEREN",
  "license": "MIT",
  "engines": {
    "node": ">=18.0.0"
  }
}
```

Tidak perlu menjalankan `npm install` untuk script dasar ini karena tidak ada dependency eksternal.

Menjalankan bantuan:

```bash
npm start
```

---

## Cara Penggunaan

Format dasar:

```bash
node tiktok.js search <keyword> [options]
```

Format lengkap:

```bash
node tiktok.js search "<keyword>" --limit <jumlah> --cursor <angka> --region <kode_region> --sortType <angka> --verbose
```

Contoh paling sederhana:

```bash
node tiktok.js search "kucing"
```

Contoh dengan limit hasil:

```bash
node tiktok.js search "kucing" --limit 5
```

Contoh mencari video dengan region Indonesia:

```bash
node tiktok.js search "kucing lucu" --region id --limit 10
```

Contoh mencari video dengan region Amerika Serikat:

```bash
node tiktok.js search "indah alhambra" --region us --cursor 10
```

Contoh menggunakan cursor untuk halaman berikutnya:

```bash
node tiktok.js search "travel jakarta" --limit 10 --cursor 10
```

Contoh menggunakan verbose log:

```bash
node tiktok.js search "kucing" --limit 5 --verbose
```

Atau:

```bash
node tiktok.js search "kucing" --limit 5 -v
```

---

## Command

Script hanya menyediakan command berikut:

| Command | Keterangan | Contoh |
|---|---|---|
| `search <keyword>` | Mencari video TikTok berdasarkan keyword | `node tiktok.js search "kucing"` |

Jika command atau keyword tidak diberikan, script akan menampilkan usage:

```text
Usage:
  node tiktok.js search <keyword> [--limit 10] [--cursor 0] [--region id|us] [--sortType 0]
```

---

## Opsi CLI

| Opsi | Default | Keterangan |
|---|---:|---|
| `--limit` | `10` | Jumlah video yang ingin diminta |
| `--cursor` | `0` | Posisi pagination untuk mengambil hasil berikutnya |
| `--region` | `id` | Kode region pencarian |
| `--sortType` | `0` | Tipe pengurutan hasil sesuai parameter endpoint |
| `--verbose` | `false` | Menampilkan log HTTP ke stderr |
| `-v` | `false` | Alias dari `--verbose` |

Contoh semua opsi:

```bash
node tiktok.js search "kuliner jakarta" --limit 20 --cursor 0 --region id --sortType 0 --verbose
```

---

## Region

Parameter `--region` dapat digunakan untuk menentukan region pencarian.

Contoh region yang dapat dikirim:

| Kode | Region |
|---|---|
| `id` | Indonesia |
| `us` | United States |
| `br` | Brazil |
| `jp` | Japan |
| `cn` | China |
| `gb` | United Kingdom |
| `kr` | South Korea |
| `my` | Malaysia |
| `sg` | Singapore |
| `th` | Thailand |
| `ph` | Philippines |

Contoh pencarian Indonesia:

```bash
node tiktok.js search "makanan viral" --region id
```

Contoh pencarian Jepang:

```bash
node tiktok.js search "anime" --region jp
```

Contoh pencarian Amerika Serikat:

```bash
node tiktok.js search "funny cats" --region us
```

Ketersediaan hasil dapat bergantung pada region yang diterima oleh layanan perantara dan data TikTok saat request dijalankan.

---

## Limit Hasil

Gunakan `--limit` untuk menentukan jumlah hasil yang diminta.

Contoh mengambil 5 video:

```bash
node tiktok.js search "kucing" --limit 5
```

Contoh mengambil 20 video:

```bash
node tiktok.js search "kucing" --limit 20
```

Nilai hasil aktual dapat lebih sedikit dari `--limit` apabila layanan tidak mengembalikan jumlah data yang diminta.

Field jumlah hasil aktual terdapat pada:

```json
{
  "count": 5
}
```

---

## Pagination Cursor

Response menyediakan field pagination berikut:

```json
{
  "cursor": 10,
  "hasMore": true
}
```

Arti field:

| Field | Keterangan |
|---|---|
| `cursor` | Posisi cursor untuk request hasil selanjutnya |
| `hasMore` | Menandakan apakah masih ada hasil berikutnya |

Contoh request pertama:

```bash
node tiktok.js search "kucing" --limit 10 --cursor 0
```

Jika output memiliki:

```json
{
  "cursor": 10,
  "hasMore": true
}
```

Gunakan cursor tersebut untuk request berikutnya:

```bash
node tiktok.js search "kucing" --limit 10 --cursor 10
```

Teruskan proses tersebut sampai `hasMore` bernilai `false`.

---

## Contoh Output

Contoh response sukses:

```json
{
  "keyword": "kucing",
  "count": 1,
  "cursor": 10,
  "hasMore": true,
  "region": "id",
  "videos": [
    {
      "id": "1234567890123456789",
      "awemeId": "1234567890123456789",
      "title": "Contoh video kucing lucu",
      "duration": 15,
      "region": "ID",
      "cover": "[https://example.com/cover.jpg](https://example.com/cover.jpg)",
      "playUrl": "[https://example.com/video.mp4](https://example.com/video.mp4)",
      "wmPlayUrl": "[https://example.com/video-watermark.mp4](https://example.com/video-watermark.mp4)",
      "stats": {
        "playCount": 100000,
        "diggCount": 12000,
        "commentCount": 500,
        "shareCount": 250
      },
      "author": {
        "id": "987654321",
        "username": "username",
        "nickname": "Nama Creator",
        "avatar": "[https://example.com/avatar.jpg](https://example.com/avatar.jpg)"
      },
      "music": {
        "id": "12345",
        "title": "Nama Musik",
        "author": "Nama Penyanyi",
        "duration": 15,
        "playUrl": "[https://example.com/music.mp3](https://example.com/music.mp3)",
        "cover": "[https://example.com/music-cover.jpg](https://example.com/music-cover.jpg)"
      },
      "createdAt": "2026-01-01T12:00:00.000Z"
    }
  ]
}
```

---

## Struktur Response

Response dari function `searchVideos()` memiliki struktur berikut:

```json
{
  "keyword": "string",
  "count": 0,
  "cursor": 0,
  "hasMore": false,
  "region": "string",
  "videos": []
}
```

### Field Utama

| Field | Keterangan |
|---|---|
| `keyword` | Keyword pencarian yang digunakan |
| `count` | Jumlah video yang berhasil diproses |
| `cursor` | Cursor untuk request selanjutnya |
| `hasMore` | Status apakah masih ada hasil berikutnya |
| `region` | Region hasil dari response |
| `videos` | Array hasil video TikTok |

### Field Video

| Field | Keterangan |
|---|---|
| `id` | Video ID |
| `awemeId` | Aweme ID video |
| `title` | Judul atau caption video |
| `duration` | Durasi video dalam detik |
| `region` | Region video |
| `cover` | URL thumbnail atau cover video |
| `playUrl` | Direct URL video MP4 jika tersedia |
| `wmPlayUrl` | URL video dengan watermark jika tersedia |
| `stats` | Statistik video dari response |
| `author` | Informasi creator atau author |
| `music` | Informasi musik atau audio video |
| `createdAt` | Waktu publikasi video dalam ISO string |

### Field Stats

Field `stats` diteruskan langsung dari response layanan. Nama field dapat berbeda sesuai response, tetapi biasanya berhubungan dengan:

| Field Umum | Keterangan |
|---|---|
| `playCount` | Jumlah views |
| `diggCount` | Jumlah likes |
| `commentCount` | Jumlah komentar |
| `shareCount` | Jumlah share |
| `collectCount` | Jumlah favorite atau collect jika tersedia |

### Field Author

| Field | Keterangan |
|---|---|
| `id` | ID author TikTok |
| `username` | Username TikTok |
| `nickname` | Nama tampilan creator |
| `avatar` | URL avatar creator |

### Field Music

| Field | Keterangan |
|---|---|
| `id` | ID musik |
| `title` | Judul musik |
| `author` | Nama artist atau author musik |
| `duration` | Durasi musik dalam detik |
| `playUrl` | URL audio jika tersedia |
| `cover` | URL cover musik |

---

## Verbose Log

Gunakan opsi `--verbose` atau `-v` untuk menampilkan status request HTTP pada terminal.

Contoh:

```bash
node tiktok.js search "kucing" --limit 5 --verbose
```

Contoh output log:

```text
 GET [https://getdl.space/api/session](https://getdl.space/api/session)
 POST [https://getdl.space/api/search/tiktok](https://getdl.space/api/search/tiktok)
```

Verbose log ditulis ke `stderr`, sedangkan hasil JSON tetap ditulis ke `stdout`. Hal ini memudahkan penggunaan command dalam pipeline atau redirect file.

Contoh menyimpan JSON ke file:

```bash
node tiktok.js search "kucing" --limit 10 > result.json
```

Contoh menyimpan hasil sambil melihat verbose log:

```bash
node tiktok.js search "kucing" --limit 10 --verbose > result.json
```

---

## Retry dan Rate Limit

Script memiliki mekanisme retry untuk status HTTP sementara berikut:

```text
403
408
425
429
500
502
503
504
```

Jumlah retry default:

```js
const RETRIES = 3
```

Timeout default:

```js
const TIMEOUT = 25_000
```

Jika server mengembalikan kode:

```text
RATE_LIMITED
```

Script menunggu beberapa detik dan mencoba ulang hingga batas retry tercapai.

Jika tetap gagal, error yang ditampilkan:

```text
Terlalu banyak request, tunggu lalu coba lagi.
```

Untuk mengurangi kemungkinan rate limit:

- Jangan menjalankan request paralel dalam jumlah besar.
- Gunakan delay di antara request pagination.
- Gunakan limit hasil yang wajar.
- Gunakan cursor secara berurutan.
- Tunggu beberapa detik jika layanan mengembalikan `RATE_LIMITED`.

---

## Cara Kerja

Script bekerja dengan tahapan berikut:

1. Memanggil endpoint session GetDL.
2. Menyimpan session ID dari response.
3. Menyimpan cookie dari header response, jika tersedia.
4. Mengirim request POST pencarian TikTok dengan keyword, limit, cursor, region, sort type, dan session ID.
5. Memproses array video dari response.
6. Menyederhanakan data video ke format JSON yang konsisten.
7. Mengembalikan direct play URL, watermark URL, statistik, author, music, dan pagination.

Endpoint yang digunakan oleh script:

```text
GET [https://getdl.space/api/session](https://getdl.space/api/session)
```

```text
POST [https://getdl.space/api/search/tiktok](https://getdl.space/api/search/tiktok)
```

Halaman referer yang digunakan:

```text
[https://getdl.space/id/search/tiktok](https://getdl.space/id/search/tiktok)
```

---

## Penggunaan Sebagai Module

File menggunakan ESM export sehingga dapat langsung di-import pada project Node.js lain.

Contoh file `app.js`:

```js
import { searchVideos } from "./tiktok.js"

async function main() {
  try {
    const result = await searchVideos("kucing", {
      limit: 5,
      cursor: 0,
      region: "id",
      sortType: 0,
      log: console.error
    })

    console.log(JSON.stringify(result, null, 2))
  } catch (error) {
    console.error(error.message)
  }
}

main()
```

Jalankan:

```bash
node app.js
```

Contoh mengambil halaman berikutnya:

```js
import { searchVideos } from "./tiktok.js"

const firstPage = await searchVideos("kucing", {
  limit: 10,
  cursor: 0,
  region: "id"
})

if (firstPage.hasMore) {
  const nextPage = await searchVideos("kucing", {
    limit: 10,
    cursor: firstPage.cursor,
    region: "id"
  })

  console.log(nextPage.videos)
}
```

Export yang tersedia:

```js
export async function searchVideos(...)
```

```js
export default { searchVideos }
```

---

## Error Handling

Script menangani error berikut:

- Keyword kosong
- Command bukan `search`
- Session GetDL gagal dibuat
- Request mengalami timeout
- Request HTTP sementara gagal
- Response bukan JSON valid
- Response tidak memiliki data pencarian
- Layanan mengembalikan status `RATE_LIMITED`
- API mengembalikan field error
- Koneksi jaringan gagal

Contoh menjalankan command tanpa keyword:

```bash
node tiktok.js search
```

Output:

```text
Usage:
  node tiktok.js search <keyword> [--limit 10] [--cursor 0] [--region id|us] [--sortType 0]
```

Contoh error keyword kosong saat dipakai sebagai module:

```js
await searchVideos("")
```

Error:

```text
Kata kunci wajib.
```

Contoh error session:

```text
Gagal membuat session GetDL.
```

Contoh error rate limit:

```text
Terlalu banyak request, tunggu lalu coba lagi.
```

---

## Batasan

- Script bergantung pada endpoint dan struktur response GetDL.
- Endpoint GetDL dapat berubah, dibatasi, atau tidak tersedia kapan saja.
- TikTok dan layanan perantara dapat menerapkan rate limit, proteksi bot, cookie requirement, atau pembatasan region.
- Tidak semua hasil mempunyai `playUrl`, `wmPlayUrl`, data musik, statistik lengkap, atau metadata author lengkap.
- Direct video URL bisa bersifat sementara atau dapat kadaluarsa.
- Hasil pencarian dapat berbeda berdasarkan region, keyword, cursor, atau kondisi layanan.
- Jangan mengirim request dalam jumlah besar atau secara paralel.
- Script ini tidak menjamin video dapat disimpan, diputar, atau tersedia dalam jangka waktu tertentu.

---

## .gitignore

Buat file `.gitignore` dengan isi berikut:

```gitignore
node_modules/
.env
*.log
result.json
results/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.DS_Store
```

---

## License

Project ini menggunakan lisensi MIT.

Buat file `LICENSE`:

```text
MIT License

Copyright (c) 2026 SCRIPETEREN

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to deal in the Software
without restriction, including without limitation the rights to use, copy,
modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Creator

```text
SCRIPETEREN
```

```text
[https://github.com/SCRIPETEREN](https://github.com/SCRIPETEREN)
```

---

## Disclaimer

Repository ini dibuat untuk pembelajaran Node.js, ESM module, HTTP request, session handling, retry logic, JSON parsing, cursor pagination, dan pengolahan metadata video publik.

Gunakan script secara bertanggung jawab. Jangan gunakan untuk melakukan scraping berlebihan, pelanggaran privasi, spam, pengumpulan data tanpa izin, distribusi konten tanpa hak, atau aktivitas yang melanggar ketentuan TikTok, GetDL, dan hukum yang berlaku.

TikTok menyediakan solusi API resmi untuk integrasi developer; penggunaan layanan resmi umumnya memerlukan autentikasi, token, dan scope yang sesuai. [1][2]

<p align="center">
  Made by <a href="https://github.com/SCRIPETEREN">SCRIPETEREN</a>
</p>