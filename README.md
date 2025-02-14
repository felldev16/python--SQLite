# **Laporan Python SQLite📋**
## Fellicia Devina

### Tujuan Aplikasi

### Class Diagram

### Use Case Diagram

![usecase](https://github.com/user-attachments/assets/9ef9a2f6-3ffe-4c3e-9097-62764f073480)


### Sequence Diagram

![sequence](https://github.com/user-attachments/assets/19250ba0-43bc-455b-80ce-05cf16befb90)

🔍 Penjelasan Alur Program

1. Registrasi User

User mengklik tombol "Register".
Sistem menampilkan halaman pendaftaran.
User mengisi username dan password, lalu mengirim data.
Data dikirim ke Controller untuk divalidasi dan disimpan di Database.
Jika berhasil, sistem mengkonfirmasi pendaftaran dan mengarahkan user ke halaman login.
2. Login User

User mengklik tombol "Login".
Sistem menampilkan halaman login.
User memasukkan username dan password, lalu mengirim data.
Controller mengecek data ke Database dan memverifikasi password.
Jika valid, sistem mengkonfirmasi login dan mengarahkan user ke halaman utama.
3. Melihat Daftar Mahasiswa

User mengklik tombol "Students DB".
Sistem meneruskan permintaan ke Controller.
Controller mengambil daftar mahasiswa dari Database.
Sistem menampilkan daftar mahasiswa kepada user.
4. Menambahkan Mahasiswa

User mengisi formulir mahasiswa baru dan mengirimkan data.
Sistem meneruskan data ke Controller untuk disimpan di Database.
Setelah berhasil, sistem mengkonfirmasi dan menampilkan mahasiswa yang baru ditambahkan.
5. Mengedit Data Mahasiswa

User memilih mahasiswa yang ingin diedit.
Sistem menampilkan halaman edit.
User mengubah data lalu menekan tombol "Update".
Sistem meneruskan perubahan ke Controller untuk diperbarui di Database.
Jika berhasil, sistem mengkonfirmasi dan menampilkan data yang telah diperbarui.
6. Menghapus Mahasiswa

User memilih mahasiswa yang ingin dihapus.
Sistem mengirimkan permintaan penghapusan ke Controller.
Controller menghapus data dari Database.
Jika berhasil, sistem mengkonfirmasi dan menghapus data dari daftar tampilan.
7. Logout User

User mengklik tombol "Logout".
Sistem menghapus sesi user dan mengkonfirmasi logout.
User diarahkan kembali ke halaman utama.
