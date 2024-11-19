# jualjual

- [TUGAS 7](#tugas-7)
- [TUGAS 8](#tugas-8)
- [TUGAS 9](#tugas-9)

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

## TUGAS 9

1. Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?

    Karena model dapat membantu dalam *mapping* data JSON tersebut. Hal ini membantu dalam menjaga struktur data agar tetap konsisten dan tervalidasi.
    Secara garis besar, kita masih bisa bekerja dengan JSON tanpa adanya model, namun perlu langkah yang lebih rumit untuk memetakan data tersebut agar dapat diproses, sehingga lebih rawan terhadap error. Kehadiran model menyediakan cara yang lebih mudah dan terstruktur, sehingga meminimalisir terjadinya error.

2. Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini

    *HTTP* menjadi sarana komunikasi antara aplikasi Flutter dan server Django kita. Melalui HTTP, Flutter bisa mengirimkan *request* seperti `GET`, `POST`, `PUT`, ataupun `DELETE` dari server Django.

3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

    CookieRequest berfungsi dalam mengelola sesi autentikasi pengguna. Dengan adanya CookieRequest, aplikasi bisa secara otomatis mengelola cookie tersebut agar pengguna bisa tetap dalam kondisi terautentikasi.
    Instance CookieRequest harus dibagikan ke semua komponen untuk memastikan pengguna tetap terautentikasi setiap melakukan permintaan HTTP. Sehingga semua bagian aplikasi yang perlu melakukan autentikasi bisa menggunakan instance yang sama, dan tidak perlu melakukan login kembali.

4. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.

    Data input yang diisi oleh pengguna pada aplikasi Flutter dikirimkan ke server Django via HTTP. Kemudian server mengirimkan respons ke Flutter, yang kemudian menampilkan hasilnya ke pengguna.

5. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

    - `Register`

        Pengguna menginput data kredensial, kemudian dikirimkan ke server Django via HTTP. Server memverifikasi data tersebut dengan data dan aturan di database. Jika berhasil, maka server akan membuat pengguna baru dengan kredensial tersebut.

    - `Login`

        Pengguna menginput data kredensial, kemudian dikirimkan ke server Django via HTTP. Server memverifikasi data tersebut dengan data di database. Jika cocok, maka pengguna akan terautentikasi dan aplikasi menyimpan cookie autentikasi untuk sesi tersebut.

    - `Logout`

        Ketika user logout, maka CookieRequest akan menghapus cookie yang menyimpan sesi pengguna, mengakhiri sesi tersebut, dan mengarahkan pengguna ke halaman login.

6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).

    - Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter.

        Membuat halaman register pada aplikasi Flutter yang menerima input username, password, dan konfirmasi password. Kemudian mengirimkan input tersebut ke server Django via HTTP, yang kemudian akan diproses dan diverifikasi oleh server.
        ```dart
        ...
        String username = _usernameController.text;
        String password1 = _passwordController.text;
        String password2 = _confirmPasswordController.text;

        final response = await request.postJson(
            "http://127.0.0.1:8000/auth/register/",
            jsonEncode({
            "username": username,
            "password1": password1,
            "password2": password2,
            }));
        ...
        ```
        
    - Membuat halaman login pada proyek tugas Flutter.

        - Membuat halaman/file baru untuk login tersebut, yang menjadi landing page ketika aplikasi pertama dibuat. `Login page` akan meminta input username dan password. `Login page` juga memiliki tombol untuk diarahkan ke page register, sehingga bisa registrasi terlebih dahulu.

    - Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.

        - Data yang diinput oleh pengguna pada `login page` dikirimkan ke server Django via *HTTP*. Server bertugas untuk menyocokkan data tersebut dengan database yang ada. 
        
        - Jika cocok, maka server akan mengautentikasi pengguna dengan membuatkan cookie untuk sesi tersebut, sehingga pengguna tetap terautentikasi.

    - Membuat model kustom sesuai dengan proyek aplikasi Django.

        - Mengambil data berbentuk json dari projek Django yang sudah ada, kemudian memasukannya pada aplikasi QuickType. Mengkonversikan data yang ada ke sebuah model custom, dan mengcopynya ke file product_entry.dart.

    - Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah kamu deploy. Tampilkan name, price, dan description dari masing-masing item pada halaman ini.

        - Pengambilan seluruh data sudah dilakukan oleh server Django, hanya perlu ditampilkan melalui halaman aplikasi flutter dengan file baru yang berisi kode
        ```dart
        ...
        children: [
            Text(
            product.fields.name,
            style: const TextStyle(
                fontSize: 18.0,
                fontWeight: FontWeight.bold,
            ),
            ),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}"),
            const SizedBox(height: 10),
            Text(product.fields.description),
        ],
        ...

    - Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item. Halaman ini dapat diakses dengan menekan salah satu item pada halaman daftar Item. Tampilkan seluruh atribut pada model item kamu pada halaman ini. Tambahkan tombol untuk kembali ke halaman daftar item.

        - Menambahkan kode tersebut pada halaman daftar produk
        ```dart
        return InkWell( // Membuat elemen menjadi inkwell
            onTap: () {
                Navigator.push( // Redirect ke halaman detail item ketika di click
                context,
                MaterialPageRoute(
                    builder: (context) => ProductDetailPage(product: product),
                ),
                );
            },
        ...
        ```
        - Membuat file baru untuk detail item tersebut yang berisi beberapa kode berikut
        ``` dart
        children: [
            Text(
              product.fields.name,
              style: const TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 16),
            Text(
              product.fields.seller,
              style: const TextStyle(fontSize: 16),
            ), 
            ... // Setiap field item tersebut.
            const Spacer(),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              child: const Text("Back"),
            ), // Tombol kembali
        ],

    -  Melakukan filter pada halaman daftar item dengan hanya menampilkan item yang terasosiasi dengan pengguna yang login.

        - Sudah diimplementasikan pada server Django.