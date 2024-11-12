# jualjual

- [TUGAS 7](#tugas-7)
- [TUGAS 8](#tugas-8)

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

## TUGAS 8

1. Apa kegunaan *const* di Flutter? Jelaskan apa keuntungan ketika menggunakan *const* pada kode Flutter. Kapan sebaiknya kita menggunakan *const*, dan kapan sebaiknya tidak digunakan?

    *Const* berfungsi untuk membuat suatu objek yang bersifat konstan/*immutable*. *Const* dapat membantu efisiensi penggunaan memori, sebab dengan menggunakan *const* kita bisa menghindari pembuatan objek yang sama berulang kali setiap *UI* di *render*.
    *Const* sebaiknya digunakan jika objek yang didefinisikan tidak akan berubah selama aplikasi berjalan, sehingga tidak bergantung terhadap keadaan aplikasi.
    *Const* sebaiknya tidak digunakan jika objek bergantung terhadap keadaan aplikasi, dan bisa berubah berdasarkan keadaan tersebut.

2. Jelaskan dan bandingkan penggunaan *Column* dan *Row* pada *Flutter*. Berikan contoh implementasi dari masing-masing layout widget ini!

    Keduanya berfungsi untuk menata widget dalam suatu container, *Column* untuk menatanya secara vertikal, sedangkan *Row* untuk menatanya secara horizontal.
    Contoh implementasi:
    - *Column* : 
        ```flutter
        Column(
            children: <Widget>[
                Text('Item 1'),
                Text('Item 2'),
                Text('Item 3'),
            ],
        )
    Kode ini akan menata 3 teks tersebut secara vertikal.
    - *Row*:
        ```flutter
        Row(
            children: <Widget>[
                Icon(Icons.star),
                Icon(Icons.favorite),
                Icon(Icons.home),
            ],
        )
    Kode ini akan menata 3 ikon tersebut secara horizontal.

3. Sebutkan apa saja elemen input yang kamu gunakan pada halaman *form* yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!

    - Elemen input yang digunakan:
        - TextFormField
            
            Untuk menerima nama, harga, dan prediksi produk.
        - ElevatedButton

            Tombol untuk menyimpan data yang sudah diinput pengguna pada 3 TextFormField di atas.
    
    - Elemen input yang tidak digunakan
        - Checkbox

            Input untuk pilihan ya/tidak.
        - Radio Button

            Input untuk memilih 1 dari beberapa daftar pilihan.
        - Switch

            Input untuk memilih antara 2 keadaan *(on/off)*.
        - DropdownButton

            Input untuk memilih 1 opsi dari daftar dropdown.
        - Slider

            Input untuk memilih suatu nilai (numerik) dari rentang yang ditentukan.
        - DatePicker
            
            Input untuk memilih tanggal dari suatu kalender.

4.  Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?

    Dengan menggunakan fitur dari flutter yaitu ThemeData untuk diterapkan pada alikasi. Tema ini menghandle agar aplikasi konsisten dalam styling widget ataupun halamannya.
    Saya sendiri menggunakan fitur tersebut untuk mengatur konsistensi warna dari aplikasi saya.

5. Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?

    Saya menangani navigasi dalam aplikasi menggunakan *widget* `Navigator`. *Widget* ini bersifat layaknya sebuah *stack*, sehingga penanganan *view* yang ditampilkan dilakukan melalui fungsi seperti `push()`, `pop()`, dan `pushReplacement()`.