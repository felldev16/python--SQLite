# **Laporan Python SQLite📋**
## Fellicia Devina

## **Analisis Routing & Redirecting Program**
1. Home Route

Code:

![image](https://github.com/user-attachments/assets/d8a7c573-c984-4cc3-9b69-65237aa1e8fa)

### **Penjelasan**
Ketika user membuka halaman utama (/), Flask akan menampilkan halaman `index.html`. Halaman ini adalah tampilan utama dari aplikasi Student Management System.

Di bagian atas, ada judul besar dan tiga tombol utama:
- `Login` → Untuk masuk ke sistem.
- `Register` → Untuk membuat akun baru.
- `Students DB` → Untuk melihat daftar students.

Di bawahnya, terdapat penjelasan singkat tentang keunggulan aplikasi dan footer yang menampilkan hak cipta.

2. Create User

Code:
![image](https://github.com/user-attachments/assets/99ac5677-aa9d-417c-bd71-4bdb68dfa1a7)

### **Penjelasan**
Ketika user tekan tombol `Register` di halaman utama, mereka akan diarahkan ke halaman Create User (`/users/create`).

Flask menampilkan `create_user.html` yang berisi:
- Form Username
- Form Password
- Tombol `Create User` untuk mengirimkan data.
- Tombol `Back to Home` untuk kembali ke halaman utama.

Ketika user mengisi formulir dan menekan tombol `Create User`:

- Flask akan menerima data (username dan password).
- Cek apakah kedua bidang diisi. Jika kosong → muncul pesan error.
- Cek apakah username sudah ada di database. Jika sudah ada, maka akan muncul pesan error. Jika belum:
- ✅ Username & password disimpan di database.
- ✅ Password akan di-hash agar aman.
- ✅ Pengguna dialihkan ke halaman utama dengan pesan sukses.

3. Login

Code:
![](https://github.com/user-attachments/assets/dcbd0896-ee34-40ee-9ac5-7c7ca6c1dc3b)

### **Penjelasan**
Ketika user membuka halaman login, Flask akan menampilkan form login dari file `login.html`.
- User melihat form yang meminta username dan password.
- Ketika tombol login ditekan, browser mengirimkan username dan password ke server menggunakan `POST`.
- Server mencari apakah username yang dimasukkan ada di database.
- Jika username ditemukan, server akan memeriksa apakah password benar menggunakan fungsi `check_password(password)`.
- Jika password benar, server menyimpan `user_id` dalam session, artinya pengguna dianggap sudah login.
- Kemudian, user dialihkan ke halaman `Students DB` (`/students`).
- Jika username tidak ditemukan atau password salah, server akan menampilkan pesan error di halaman `login.html`, dan user mencoba lagi

4. Tampilkan Daftar Students

Code:
![](https://github.com/user-attachments/assets/6267e5b9-4df8-4af6-a776-274e5dd2d6ba)

### **Penjelasan**
- Jika `user_id` tidak ada di session, artinya user belum login.
- Akan muncul pesan peringatan "Please log in to access this page."
- User akan diarahkan ke halaman login (`/login`).
- Jika user sudah login, sistem mengambil semua data students dengan `Student.query.all()`.
- Data students dikirim ke template `student.html` untuk ditampilkan.

`student.html` berisi :
- form agar user bisa menambahkan student baru dengan mengisi Name, Age, dan Grade lalu menekan tombol `Add Student`.
- Data dikirim ke server menggunakan `POST` request ke `/add`.
- Data students diambil dari database dan ditampilkan dalam tabel.
- Setiap student memiliki tombol `Edit`→ mengarah ke `/edit/{id}` untuk mengedit data student dan `Delete`→ mengarah ke `/delete/{id}` untuk menghapus student.

5. Add Student

Code:
![image](https://github.com/user-attachments/assets/772f9377-47c2-4476-85d2-c3ca226ffc8d)

### **Penjelasan**
- Cek jika user sudah login
- Jika sudah login, user akan berada di halaman `student.html`.
- User bisa menambahkan student baru dengan mengisi Name, Age, dan Grade.
- Data akan dikirim ke `/add` menggunakan metode `POST`.
- Tombol `Add Student` akan menambahkan data ke database.

Pada route `/add`:
- `name = request.form['name']` → Mengambil nama student dari input form.
- `age = request.form['age']` → Mengambil umur student dari input form.
- `grade = request.form['grade']` → Mengambil nilai/kelas student dari input form.
- buat objek baru dari model Student, simpan pada `new_student`
- `db.session.add(new_student)` → Menambahkan data student ke database.
- `db.session.commit()` → Menyimpan perubahan ke database.
- Menampilkan pesan berhasil dan mengarahkan user kembali ke halaman Students (`/students`).


6. Edit Student

Code:
![](https://github.com/user-attachments/assets/d22220cc-8537-45fc-a0ec-b9e04c719bad)

### **Penjelasan**
- Jika `user_id` tidak ada di session, artinya user belum login.
- Akan muncul pesan peringatan "Please log in to access this page."
- User akan diarahkan ke halaman login (`/login`).
- Jika user sudah login, sistem mengambil data student berdasarkan id dengan `Student.query.get_or_404(id)`.
- Jika user mengedit data dan menekan tombol Update, perubahan disimpan ke database dan user diarahkan kembali ke halaman Students (`/students`).
- Jika user hanya membuka halaman edit tanpa submit, data student yang sudah ada ditampilkan di form edit (`edit.html`).

`edit.html` berisi:
- Form edit student → menampilkan data Name, Age, dan Grade yang sudah ada.
- User bisa mengubah data dan menekan tombol `Update`.
- Data dikirim ke server menggunakan `POST` request ke `/edit/{id}`.
- Setelah sukses, user diarahkan kembali ke halaman Students (`/students`)

7. Delete Student

Code:
![](https://github.com/user-attachments/assets/97c25fd4-37b0-4178-9a87-c249f8afca0f)

### **Penjelasan**
- Cek jika user sudah login
- Jika sudah login, user akan berada di halaman `student.html`.
- `student.html` berisi memiliki tombol `Delete` di setiap data student yang mengarah ke `/delete/{id}`.
- Cari data student berdasarkan id dengan `Student.query.get_or_404(id)`.
- Jika id tidak ditemukan, tampilkan 404 error.
- Hapus student dari database dengan `db.session.delete(student)`, lalu `db.session.commit()` untuk menyimpan perubahan.
- Tampilkan pesan "Student deleted successfully!" dan arahkan user kembali ke halaman Students (`/students`).

8. Logout

Code:
![](https://github.com/user-attachments/assets/9dd2984c-2975-45e7-9996-786cf95d362b)

### **Penjelasan**
- Menghapus session dengan `session.clear()`, yang berarti semua data session akan dihapus dan user akan kehilangan akses ke halaman yang membutuhkan login.
- Menampilkan pesan "Logged out successfully.".
- Mengalihkan user ke halaman utama (`/index`), sehingga mereka harus login kembali untuk mengakses halaman yang membutuhkan autentikasi.

## **Class Diagram**
![image](https://github.com/user-attachments/assets/d73b3a5a-286d-4c62-a050-f0ba17c78cd7)

### **🗂️Struktur Kelas (Class Diagram) dalam Program**

**🖥️ FlaskApp (Web Service)**

Bertindak sebagai pusat logika program dan mengelola berbagai fungsi utama:
- `login()`, `logout()`, dll → Mengatur otentikasi dan navigasi halaman.
- `add_student()`, `edit_student()`, `delete_student()` → Mengelola data student.
- `create_user_form()` → Membantu dalam pembuatan akun pengguna baru.

**🔑 HTTPBasicAuth (Autentikasi)**

- Bertanggung jawab untuk verifikasi pengguna menggunakan `verify_password(username, password)`.
- Memastikan hanya pengguna yang terdaftar yang dapat mengakses sistem.

**📂 SQLAlchemy (Database Manager)**

- Mengelola sesi database (session: Session).
- Memiliki metode untuk menambah (`add()`), menghapus (`delete()`), dan menyimpan perubahan (`commit()`).
- Digunakan oleh FlaskApp untuk menyimpan dan memperbarui data student serta pengguna.

**👤 User (Model Data Pengguna)**

- Menyimpan informasi pengguna: `id`, `username`, `password_hash`.
Memiliki metode keamanan:
- `set_password(password)` → Menyimpan kata sandi dengan aman menggunakan hashing.
- `check_password(password)` → Memverifikasi kata sandi saat login.
- Terdapat metode `__repr__()` untuk merepresentasikan data pengguna sebagai string.

**🎓 Student (Model Data Student)**

- Menyimpan informasi student seperti `id`, `name`, `age`, dan `grade`.
- Memiliki metode `__repr__()` untuk menampilkan informasi students dalam bentuk string yang lebih mudah dibaca.

## **Use Case Diagram**
![usecase](https://github.com/user-attachments/assets/9ef9a2f6-3ffe-4c3e-9097-62764f073480)

### **🧍‍♂️ Aktor Utama:**
User (pengguna sistem)

### **🗒️ Use Case:**

- User dapat mendaftarkan akun baru dengan mengisi username dan password.
- User dapat masuk ke dalam sistem dengan memasukkan username dan password yang telah terdaftar.
- User dapat melihat daftar students, menambahkan data baru, mengedit data, dan menghapus data dari daftar.
- User dapat melakukan logout dan keluar dari program.

## **Sequence Diagram**

![image](https://github.com/user-attachments/assets/a7a5ca7d-41d9-4d1a-b9e1-0a40cfea0c6e)


### **🔍 Penjelasan Alur Program**

1. Registrasi User

- User mengklik tombol "Register".
- Sistem menampilkan halaman pendaftaran.
- User mengisi username dan password, lalu mengirim data.
- Data dikirim ke Controller untuk divalidasi dan disimpan di Database.
- Jika berhasil, sistem mengkonfirmasi pendaftaran dan mengarahkan user ke halaman login.
  
2. Login User

- User mengklik tombol "Login".
- Sistem menampilkan halaman login.
- User memasukkan username dan password, lalu mengirim data.
- Data akan dicek pada Database dan memverifikasi password.
- Jika valid, sistem mengkonfirmasi login dan mengarahkan user ke halaman Students DB.
  
3. Melihat Daftar Student

- User mengklik tombol "Students DB".
- Sistem meneruskan permintaan ke Controller.
- Controller mengambil daftar students dari Database.
- Sistem menampilkan daftar students kepada user.
  
4. Menambahkan Student

- User mengisi form data baru dan klik "Add Student".
- Sistem meneruskan data ke Controller untuk dikirim dan disimpan pada Database.
- Setelah berhasil, sistem mengkonfirmasi dan menampilkan data yang baru ditambahkan.
  
5. Mengedit Data Student

- User memilih data yang ingin diedit.
- Sistem menampilkan halaman edit.
- User mengubah data pada form lalu menekan tombol "Update".
- Sistem meneruskan perubahan ke Controller untuk diperbarui di Database.
- Jika berhasil, sistem mengkonfirmasi dan menampilkan data yang telah diperbarui.
  
6. Menghapus Student

- User memilih student yang ingin dihapus.
- Sistem mengirimkan permintaan penghapusan ke Controller.
- Controller menghapus data dari Database.
- Jika berhasil, sistem mengkonfirmasi dan menghapus data dari daftar students.

7. Logout User

- User mengklik tombol "Logout".
- Sistem menghapus sesi user dan mengkonfirmasi logout.
- User diarahkan kembali ke halaman utama.
