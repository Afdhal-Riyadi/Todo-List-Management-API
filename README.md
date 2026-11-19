\# Todo List Management API



RESTful API untuk mengelola daftar tugas (Todo), kategori, autentikasi pengguna, riwayat aktivitas, dan statistik menggunakan Node.js, Express, dan MongoDB.



\## Fitur Utama



\- \*\*Authentication\*\*

&#x20; - Registrasi pengguna.

&#x20; - Login menggunakan email dan password.

&#x20; - Autentikasi menggunakan JSON Web Token (JWT).

&#x20; - Melihat profil pengguna yang sedang login.

&#x20; - Pembatasan akses khusus admin.



\- \*\*Todo Management\*\*

&#x20; - Membuat, melihat, memperbarui, dan menghapus Todo.

&#x20; - Mengatur status dan prioritas tugas.

&#x20; - Menghubungkan Todo dengan kategori.

&#x20; - Filter berdasarkan status, prioritas, dan kategori.

&#x20; - Pencarian, sorting, dan pagination.



\- \*\*Category Management\*\*

&#x20; - Membuat, melihat, memperbarui, dan menghapus kategori.

&#x20; - Pencarian, sorting, dan pagination.



\- \*\*Activity Log\*\*

&#x20; - Melihat riwayat aktivitas pengguna yang sedang login.



\- \*\*Statistics\*\*

&#x20; - Mendapatkan ringkasan statistik Todo.

&#x20; - Menggunakan API Key untuk mengakses endpoint statistik.



\- \*\*API Documentation\*\*

&#x20; - Dokumentasi endpoint menggunakan Swagger UI.



\## Teknologi yang Digunakan



| Teknologi | Kegunaan |

|---|---|

| Node.js | JavaScript runtime |

| Express.js 5 | Framework backend |

| MongoDB | Database NoSQL |

| Mongoose | ODM untuk MongoDB |

| JSON Web Token | Autentikasi |

| bcryptjs | Password hashing |

| express-validator | Validasi input |

| Swagger | Dokumentasi API |

| dotenv | Pengelolaan environment variable |

| Jest | Testing |

| Supertest | HTTP endpoint testing |

| mongodb-memory-server | Database sementara untuk testing |

| Nodemon | Development server |



\## Persyaratan



Pastikan sudah menginstal:



\- Node.js

\- npm

\- MongoDB Atlas atau MongoDB yang dapat diakses oleh aplikasi.

\- Git (opsional).



\## Instalasi



1\. Clone repository:



&#x20;  ```bash

&#x20;  git clone <URL\_REPOSITORY>

&#x20;  ```



2\. Masuk ke folder project:



&#x20;  ```bash

&#x20;  cd Post-Production

&#x20;  ```



3\. Install dependencies:



&#x20;  ```bash

&#x20;  npm install

&#x20;  ```



4\. Buat file `.env` di folder utama project.



5\. Isi konfigurasi environment variable seperti contoh berikut.



\## Environment Variables



Buat file `.env` di root project:



```env

PORT=3000



MONGODB\_URI=your\_mongodb\_connection\_string



JWT\_SECRET=your\_jwt\_secret



JWT\_EXPIRES\_IN=7d



API\_KEY=your\_api\_key

```



Keterangan:



| Variable | Deskripsi |

|---|---|

| PORT | Port untuk menjalankan server |

| MONGODB\_URI | Connection string MongoDB |

| JWT\_SECRET | Secret key untuk JWT |

| JWT\_EXPIRES\_IN | Masa berlaku token JWT |

| API\_KEY | API Key untuk endpoint statistik |



\*\*Catatan keamanan:\*\*

\- Jangan membagikan isi file `.env`.

\- Jangan mengunggah `.env` ke repository Git.

\- Gunakan secret dan API Key yang kuat.



\## Menjalankan Aplikasi



Jalankan server dalam mode development:



```bash

npm run dev

```



Atau mode biasa:



```bash

npm start

```



Jika berhasil, server akan berjalan pada port yang dikonfigurasi, secara default:



```text

http://localhost:3000

```



\## Dokumentasi API



Dokumentasi endpoint tersedia melalui Swagger UI.



Buka browser dan akses:



```text

http://localhost:3000/api-docs

```



Swagger digunakan untuk melihat dokumentasi, parameter, request body, dan mencoba endpoint API.



\## API Endpoints



Base URL:



```text

http://localhost:3000

```



\### 1. Authentication



Base path: `/api/auth`



| Method | Endpoint | Deskripsi | Akses |

|---|---|---|---|

| POST | `/api/auth/register` | Registrasi pengguna | Public |

| POST | `/api/auth/login` | Login pengguna | Public |

| GET | `/api/auth/me` | Melihat profil pengguna | JWT |

| GET | `/api/auth/admin-only` | Endpoint khusus admin | Admin |



\### 2. Todo



Base path: `/api/todos`



| Method | Endpoint | Deskripsi | Akses |

|---|---|---|---|

| POST | `/api/todos` | Membuat Todo | JWT |

| GET | `/api/todos` | Mendapatkan daftar Todo | JWT |

| GET | `/api/todos/:id` | Mendapatkan detail Todo | JWT |

| PATCH | `/api/todos/:id` | Memperbarui Todo | JWT |

| DELETE | `/api/todos/:id` | Menghapus Todo | JWT |



Fitur tambahan pada daftar Todo:

\- Filter berdasarkan `status`.

\- Filter berdasarkan `priority`.

\- Filter berdasarkan `category`.

\- Sorting menggunakan `sortBy` dan `order`.

\- Pagination menggunakan `page` dan `limit`.

\- Pencarian menggunakan `search`.



Status Todo:

\- `pending`

\- `in\_progress`

\- `completed`



Prioritas Todo:

\- `low`

\- `medium`

\- `high`



\### 3. Category



Base path: `/api/categories`



| Method | Endpoint | Deskripsi | Akses |

|---|---|---|---|

| POST | `/api/categories` | Membuat kategori | JWT |

| GET | `/api/categories` | Mendapatkan daftar kategori | JWT |

| GET | `/api/categories/:id` | Mendapatkan detail kategori | JWT |

| PATCH | `/api/categories/:id` | Memperbarui kategori | JWT |

| DELETE | `/api/categories/:id` | Menghapus kategori | JWT |



Fitur tambahan:

\- Pencarian menggunakan `search`.

\- Sorting menggunakan `sortBy` dan `order`.

\- Pagination menggunakan `page` dan `limit`.



\### 4. Activity Log



Base path: `/api/activity-logs`



| Method | Endpoint | Deskripsi | Akses |

|---|---|---|---|

| GET | `/api/activity-logs` | Melihat riwayat aktivitas pengguna | JWT |



\### 5. Statistics



Base path: `/api/stats`



| Method | Endpoint | Deskripsi | Akses |

|---|---|---|---|

| GET | `/api/stats/summary` | Mendapatkan ringkasan statistik Todo | API Key |



Endpoint statistik membutuhkan header:



```http

x-api-key: YOUR\_API\_KEY

```



\## Autentikasi



Endpoint yang membutuhkan login menggunakan Bearer Token.



Tambahkan header berikut pada request:



```http

Authorization: Bearer YOUR\_JWT\_TOKEN

```



Token didapatkan setelah pengguna berhasil login.



Untuk endpoint admin-only, pengguna harus memiliki role admin.



\## Testing



Jalankan seluruh pengujian menggunakan perintah:



```bash

npm test

```



Project menggunakan:

\- Jest untuk menjalankan pengujian.

\- Supertest untuk menguji HTTP endpoint.

\- mongodb-memory-server untuk menyediakan database sementara saat testing.



\## Struktur Project



```text

Post-Production/

│

├── config/

│   ├── db.js

│   └── swagger.js

│

├── controller/

├── middleware/

├── model/

├── routes/

├── service/

├── util/

├── validator/

│

├── tests/

├── postman/

├── .postman/

│

├── app.js

├── server.js

├── package.json

├── package-lock.json

└── .gitignore

```



\## Error Handling



Project menggunakan:

\- AppError untuk pengelolaan error.

\- catchAsync untuk menangani error asynchronous.

\- Global error handler untuk menangani error aplikasi.

\- Validasi request menggunakan express-validator.



\## Keamanan



Beberapa mekanisme keamanan yang digunakan:

\- Password disimpan dalam bentuk hash menggunakan bcryptjs.

\- Autentikasi menggunakan JWT.

\- Pembatasan akses berdasarkan role pengguna.

\- Validasi data request.

\- API Key untuk endpoint statistik.

\- File `.env` dan folder `node\_modules` dikecualikan melalui `.gitignore`.



\## Author



\*\*Muhammad Afdhal Riyadi\*\*



Project: Todo List Management API



\## License



Project ini dibuat untuk keperluan pembelajaran dan pengembangan backend API.

