# tugas_3_python_pacmann

## Tujuan Pengerjaan Tugas
Mengimplementasikan Pembelajaran Dasar Python :
1. Test, Debug, Exception
2. Defensive Programming
3. Pembuatan OOP melalui metode Class

## Berikut pertanyaan dan penyelesaian yang dilakukan (untuk hasil output bisa melihat langsung file .ipynb tersebut)
1. Budi ingin membuat sebuah program untuk menghitung banyak elemen bernilai genap dari _list_ berisi sekumpulan bilangan. Contoh dari _input_ dan output yang benar adalah sebagai berikut:\
```input: [1,3,4,5,9,10], output: 2```\
Di bawah ini adalah algoritma yang Budi buat. Ketika Budi mencoba programnya dengan _input_ seperti contoh di atas, program memberikan output yang benar. Namun, ketika Budi mencoba list yang lain, yaitu ```[6,8,11,14,17,18]```, program tidak memberikan output yang benar (seharusnya 4, namun program memberikan output 3). Bahkan, ketika Budi memasukkan list ```[4,6,7,10]```, program Budi _error_. </br>
a. Perbaiki program Budi agar output program sesuai yang diharapkan. </br>
b. Berikan _defense_ pada fungsi untuk memastikan semua bilangan pada `list_bilangan` bertipe `int`. </br>
c. Langkah pada _defense_ adalah mencoba _typecastin_ ke `int`, jika tidak bisa maka `raiseError`

```
#perbaiki program di bawah ini
def jawaban_1(list_bilangan):
    count = 0
    for i in range(len(list_bilangan)):
        if type(list_bilangan[i]) is str:
            raise ValueError('ada string')
        if type(list_bilangan[i]) is not int:
            list_bilangan[i] = int(list_bilangan[i])
        if list_bilangan[i]%2 == 0:
            count+=1
    return count

print(jawaban_1([1,3,4,5,9,10]))
print(jawaban_1([6,8,11,14,17,18]))
print(jawaban_1([4,6,7,10]))
```

2. Buatlah program yang menerima _input_ berupa _list_ berisi bilangan, dan mengeluarkan _output_ berupa elemen terbesar pada _list_ tersebut. Contoh:
```input: [4,9,11,5,8,14,8,5,4,10], output: 14```\
Beri _defense_ untuk program Anda berupa pesan ```'Terjadi kesalahan pada input'``` jika _user_ memasukkan tipe data _integer/float/string_ pada _input_ atau terdapat elemen _list_ yang bukan _integer/float_, dan pesan ```'Panjang list minimal 2'``` jika panjang _list input_ kurang dari 2.

```
def jawaban_2(list_numbers):
    try:
        assert type(list_numbers) == list
        if len(list_numbers) < 2:
            return 'Panjang list minimal 2'
        m = list_numbers[0]
        for i in range(1,len(list_numbers)):
            if m > list_numbers[i]:
                m = list_numbers[i]
        return m
    except AssertionError:
        return("terjadi kesalahan pada input")
    
print(jawaban_2([4,9,11,5,8,14,8,5,4,10]))
print(jawaban_2([15,8,9,11]))
print(jawaban_2([10,5,8,19]))
print(jawaban_2([13]))
print(jawaban_2('sdfuh'))
```

3. Buatlah _class_ `RegularPolygon` yang memiliki atribut `no_of_sides` dan `side_length`. `no_of_sides` adalah _integer_ yang menyatakan banyak sisi yang dimiliki poligon dan `side_length` adalah panjang dari sisi poligon. Objek yang dibentuk oleh _class_ ini adalah poligon sama sisi.\
Buat _method_ pada `RegularPolygon` sebagai berikut:
    * `perimeter` menghitung keliling poligon. 
    * `interior_angle` menghitung besar sudut interior poligon, yaitu $interior\,angle = (n-2)\times 180/n$ (dalam derajat)
    * `exterior_angle` menghitung besar sudut eksterior poligon, yaitu $exterior\,angle = 360/n$ (dalam derajat)
    
    ($n$ pada keterangan rumus adalah banyak sisi yang dimiliki poligon. Keterangan lebih lanjut mengenai sudut interior dan eksterior dapat dilihat [disini](https://www.mathsisfun.com/geometry/regular-polygons.html)).

```
#lengkapi kode di bawah ini
class RegularPolygon:
    def __init__(self, side_length, no_of_sides):
        self.side_length = side_length
        self.no_of_sides = no_of_sides
        
    def perimeter(self):
        keliling = self.side_length*self.no_of_sides
        return keliling
    
    def interior_angle(self):
        sudut_int = (self.no_of_sides-2)*180/self.no_of_sides
        return sudut_int
        
    def exterior_angle(self):
        sudut_ext = 360/self.no_of_sides
        return sudut_ext

segi_300 = RegularPolygon(300,5)

keliling = segi_300.perimeter()
sudut_int = segi_300.interior_angle()
sudut_ext = segi_300.exterior_angle()

jawaban_3 = (keliling,sudut_int,sudut_ext)
print(jawaban_3)
```

4. Buatlah _class_ `Rekening` dengan atribut `saldo`, yaitu saldo yang dimiliki oleh rekening tersebut. Nilai awal/_default_ dari `saldo` adalah 0. `Rekening` memiliki tiga _method_:
* `__str__` : menampilkan sisa saldo rekening.
* `tarik` : menarik sejumlah uang dari saldo rekening sehingga saldo rekening berkurang. _Method_ ini mengembalikan nilai berupa sisa saldo setelah penarikan uang.
* `deposit` : menambahkan sejumlah uang ke saldo rekening sehingga saldo rekening bertambah. _Method_ ini mengembalikan nilai berupa sisa saldo setelah uang ditambahkan.

Buatlah juga _class_ `RekeningKhusus`, yaitu rekening yang mengharuskan pemegang rekening memiliki saldo minimum di dalam rekening tersebut. Pemegang rekening tidak bisa menarik uang jika setelah ditarik sisa saldo rekening tersebut di bawah minimum.
* Buatlah `RekeningKhusus` yang _inherit_ dari `Rekening`, dan tambahkan atribut `saldo_minimum`.
* _Override_ _method_ `tarik` sehingga jika sisa saldo setelah penarikan uang di bawah saldo minimum maka akan keluar pesan `'Saldo tidak boleh di bawah saldo minimum'`.

```
#lengkapi kode di bawah ini
class Rekening:
    def __init__(self, saldo=0):
        self.saldo = saldo
        
    def tarik(self, other_saldo):
        self.saldo = self.saldo - other_saldo
        return Rekening(self.saldo)
    
    def deposit(self, other_saldo):
        self.saldo = self.saldo + other_saldo
        return Rekening(self.saldo)
    
    def __str__(self):
        return "Sisa Saldo Anda:" + " "+ str(self.saldo)

class RekeningKhusus(Rekening):
    def __init__(self, saldo, saldo_minimum):
        Rekening.__init__(self, saldo)
        self.saldo_minimum = saldo_minimum
    
    def tarik(self, other_saldo):
        self.saldo = self.saldo - other_saldo
        if self.saldo < self.saldo_minimum:
            return RekeningKhusus("saldo tidak boleh dibawah saldo minimum", self.saldo_minimum)
        else:
            return RekeningKhusus(self.saldo, self.saldo_minimum)


rek = RekeningKhusus(100_000_000,1_000_000)
rek.deposit(50_000_000)
rek.tarik(109_000_000)
jawaban_4 = rek.tarik(40_500_000)
print(jawaban_4)
```

5. Diketahui bakteri spesies A membelah diri menjadi dua individu setiap satu jam sekali. Sebuah laboratorium melakukan percobaan dengan bakteri A. Setiap tiga jam, 25% dari bakteri dimatikan. Contoh skema banyak bakteri A pada percobaan tersebut adalah sebagai berikut:
- Misalkan mula-mula terdapat 100 bakteri.
- Satu jam pertama, bakteri membelah diri sehingga sekarang menjadi 200 bakteri.
- Satu jam berikutnya, bakteri membelah diri lagi sehingga menjadi 400 bakteri.
- Satu jam berikutnya, bakteri membelah diri lagi menjadi 800 bakteri. Kemudian, 25% dari bakteri dimatikan. Sehingga, pada saat ini akan ada $800 - 25\%(800) = 600$ bakteri.
- Satu jam berikutnya, bakteri membelah diri lagi menjadi $600\times 2 = 1200$ bakteri.\
Dan seterusnya.
Buatlah _generator_ `bakteri(init,hour)` yang meng-_generate_ banyak bakteri di tiap jam (mulai dari jam ke-1) dengan banyak bakteri awal adalah `init` dan lama pengamatan `hour` (dalam jam). Misalnya:

```
#lengkapi kode di bawah ini
def bakteri(init,hour):
    for i in range(1,hour+1):
        init *= 2
        if i % 3 == 0:
            init = int(init - ((1/4)*init))
        yield(init)
    
jawaban_5 = [int(i) for i in bakteri(50,10)]
print(jawaban_5)
```
