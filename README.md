# **Laporan Python SQLite📋**
## Fellicia Devina

## **Analisis**

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
