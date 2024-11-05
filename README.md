# jualjual

## TUGAS 7

1. Jelaskan apa yang dimaksud dengan *stateless widget* dan *stateful widget*, dan jelaskan perbedaan dari keduanya.

    *Stateless widget* tidak memiliki status internal yang dapat berubah sesudah dibangun, sehingga tampilan dan perilakunya tidak dapat diubah oleh pengguna ataupun aplikasi.
    Sebaliknya, *stateful widget* memiliki status internal yang dapat berubah suatu waktu, sehingga *widget* dapat dibangun kembali ketika status diubah. Pengguna ataupun aplikasi dapat menjadi pemicu dari perubahan status ini.

2. Sebutkan *widget* apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.

    - Scaffold: Menyediakan struktur dasar untuk UI aplikasi

    - AppBar: Menampilkan bar di bagian atas layar, biasa berisi judul aplikasi, tombol navigasi, dll

    - Padding: Memberikan ruang di sekitar *widget* untuk kepentingan tampilan

    - Column dan Row: Digunakan untuk menyusun *widget* baik secara horizontal maupun vertikal

    - InfoCard: *Widget* kustom yang menampilkan kartu kecil dengan judul dan konten

    - ItemCard: *Widget* ini menampilkan item individual dengan ikon dan teks

    - InkWell: Menambahkan ripple effect saat user menekan / interaksi dengan ItemCard

    - SnackBar: Menampilkan pesan singkat di bagian bawah layar ketika ItemCard ditekan

    - MaterialApp: Membungkus seluruh aplikasi, menyediakan konfigurasi global seperti tema dan judul aplikasi

    - ThemeData: Mengatur skema warna aplikasi

3. Apa fungsi dari `setState()`? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.

    `setState()` berfungsi untuk memberi tahu *framework* jika terjadi perubahan terhadap suatu variabel yang dapat mempengaruhi *UI* *widget*. *Widget* tersebut kemudian akan di rebuild (jika *Stateful widget*) untuk mencerminkan perubahan tersebut.

    `setState()` mempengaruhi semua variabel yang berada dalam kelas stateful, dan variabel yang memengaruhi tampilan *UI* secara langsung.

4. Jelaskan perbedaan antara *const* dengan *final*.

    - Variabel *const* adalah variabel yang memiliki suatu nilai konstan ketika di kompilasi. Variabel ini bersifat konstan dan tidak dapat berubah di seluruh waktu eksekusi aplikasi.
    - Variabel *final* adalah variabel yang hanya diinisialisasi sekali dan tidak dapat berubah setelahnya. Nilai variabel *final* dapat ditetapkan ketika aplikasi dijalankan, bukan pada waktu kompilasi, sehingga lebih fleksibel dibandingkan *const*.

5. Jelaskan bagaimana cara kamu mengimplementasikan checklist-checklist di atas.

    - Membuat sebuah program Flutter baru dengan tema *E-Commerce* yang sesuai dengan tugas-tugas sebelumnya.
        - Menjalankan command flutter create *jualjual* di terminal pada folder disimpan projek akan disimpan.
    - Membuat tiga tombol sederhana dengan ikon dan teks.
        - Membuat 3 item untuk tombol tersebut pada homepage:
            ```dart
            final List<ItemHomepage> items = [
                ItemHomepage("Lihat Daftar Produk", Icons.mood, Colors.blueAccent),
                ItemHomepage("Tambah Produk", Icons.add, Colors.lightGreen),
                ItemHomepage("Logout", Icons.logout, Colors.teal),
            ];
        - Membuat class baru untuk tombol-tombol tersebut:
            ```dart
            class ItemHomepage {
                final String name;
                final IconData icon;
                final Color color;

                ItemHomepage(this.name, this.icon, this.color);
            }
        - Membuat class itemCard untuk menghandle *view* dan *styling* dari tombol-tombol tersebut
            ```dart
            class ItemCard extends StatelessWidget {
                final ItemHomepage item; 
                const ItemCard(this.item, {super.key}); 
                
                @override
                Widget build(BuildContext context) {
                    return Material(
                    // Menentukan warna latar belakang dari tema aplikasi.
                    color: item.color,
                    // Membuat sudut kartu melengkung.
                    borderRadius: BorderRadius.circular(12),
                    ...
    - Mengimplementasikan warna-warna yang berbeda untuk setiap tombol (`Lihat Daftar Produk`, `Tambah Produk`, dan `Logout`).
        
        Menambahkan elemen baru pada item dengan cara:
        - Menambahkan parameter baru pada class utama item
            ```dart
            class ItemHomepage {
                final String name;
                final IconData icon;
                final Color color;

                ItemHomepage(this.name, this.icon, this.color);
            }
        - Memberikan secara eksplisit warna untuk setiap tombol
            ```dart
            final List<ItemHomepage> items = [
                ItemHomepage("Lihat Daftar Produk", Icons.mood, Colors.blueAccent),
                ItemHomepage("Tambah Produk", Icons.add, Colors.lightGreen),
                ItemHomepage("Logout", Icons.logout, Colors.teal),
            ];
        - Menetapkan warna setiap tombol sesuai dengan warna yang sudah ditentukan.
            ```dart
            @override
            Widget build(BuildContext context) {
            return Material(
                // Menentukan warna latar belakang dari tombol.
                color: item.color,
                // Membuat sudut kartu melengkung.
                borderRadius: BorderRadius.circular(12),
                ...

    - Memunculkan `Snackbar`
        - Ketika tombol diclick (ontap), maka memunculkan snackbar dengan message sesuai dengan nama tombol yang diclick
            ```dart
            onTap: () {
                // Menampilkan pesan SnackBar saat kartu ditekan.
                ScaffoldMessenger.of(context)
                    ..hideCurrentSnackBar()
                    ..showSnackBar(
                    SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
                    );
                },