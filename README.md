Nama       : Jehian Athaya Tsani Az Zuhry

NIM        : H1D022006

Shift Baru : D


# Proses Passing Data dari Form ke Tampilan

## 1. Pengumpulan Data di FormData

`TextEditingController` digunakan untuk mengelola input dari user:

```dart
final _namaController = TextEditingController();
final _nimController = TextEditingController();
final _tahunController = TextEditingController();
```

Setiap controller ini terhubung ke `TextFormField` masing-masing. `TextFormField` menggunakan controller untuk menyimpan dan memperbarui nilai input user secara otomatis.

## 2. Validasi dan Pengiriman Data

Ketika user menekan button "Simpan", method `_submitForm()` dipanggil:

```dart
void _submitForm() {
  if (_formKey.currentState!.validate()) {
    String nama = _namaController.text;
    String nim = _nimController.text;
    int tahun = int.parse(_tahunController.text);
    
    Navigator.of(context).push(
      PageRouteBuilder(
        pageBuilder: (context, animation, secondaryAnimation) => 
          TampilData(nama: nama, nim: nim, tahun: tahun),
        transitionsBuilder: (context, animation, secondaryAnimation, child) {
          return FadeTransition(opacity: animation, child: child);
        },
      ),
    );
  }
}
```

Proses ini melibatkan:
1. Validasi form `_formKey.currentState!.validate()`.
2. Jika valid, nilai dari setiap controller diambil dan disimpan dalam variabel.
3. Nilai `tahun` dikonversi dari String ke int menggunakan `int.parse()`.

## 3. Navigasi dan Passing Data

Setelah data dikumpulkan, `Navigator.of(context).push()` digunakan untuk berpindah ke halaman `TampilData`. Data dikirim sebagai parameter konstruktor:

```dart
TampilData(nama: nama, nim: nim, tahun: tahun)
```

Yang artinya akan membuat instance baru dari `TampilData` dengan data yang telah dikumpulkan dari form.

## 4. Penerimaan Data di TampilData

`TampilData` didefinisikan untuk menerima data melalui konstruktornya:

```dart
class TampilData extends StatelessWidget {
  final String nama;
  final String nim;
  final int tahun;

  const TampilData({
    super.key,
    required this.nama,
    required this.nim,
    required this.tahun,
  });

}
```

## 5. Penggunaan Data

Method `build` dari `TampilData` menggunakan data yang diterima untuk menampilkan informasi:

```dart
@override
Widget build(BuildContext context) {
  final int umur = DateTime.now().year - tahun;

  _buildInfoRow(context, "Nama", nama),
  _buildInfoRow(context, "NIM", nim),
  _buildInfoRow(context, "Umur", "$umur tahun"),

}
```

Data `nama` dan `nim` langsung ditampilkan, sedangkan `tahun` digunakan untuk menghitung umur.

# Demo
![](https://github.com/send0moka/Tugas2Praktikum2024/blob/main/demo.gif)
