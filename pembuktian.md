# Pembuktian Enkripsi dan HMAC-SHA1

Link = https://github.com/deovaliandro/pembuktian/blob/main/pembuktian.md

## Pesan

Misalnya pesan adalah:

```
ABCEDABADEAAABECAEDEAAABBBEDCBACBEADDDDAEBCBCBAERBACRCBDAEDAEACBECDAEDEABCBBBCDAEACBDCCDBAEABCEACEEC
```

dalam ASCII (dalam bentuk desimal):

```
65 66 67 69 68 65 66 65 68 69 65 65 65 66 69 67 65 69 68 69 65 65 65 66 66 66 69 68 67 66 65 67 66 69 65 68 68 68 68 65 69 66 67 66 67 66 65 69 82 66 65 67 82 67 66 68 65 69 68 65 69 65 67 66 69 67 68 65 69 68 69 65 66 67 66 66 66 67 68 65 69 65 67 66 68 67 67 68 66 65 69 65 66 67 69 65 67 69 69 67
```

Setiap suatu angka, merupakan suatu indeks array. Misalnya `arr[0] = 65`, `arr[1] = 66`, dst.

Ini digunakan untuk menghitung RSA.

## HMAC

Didefinisikan terdapat dua parameter, yaitu:

```
IPAD = 0x36
OPAD = 0x5c
```

masing-masing memiliki panjang 64 byte (nilainya di ulang-ulang).

### Pembangkitan Kunci
Ada tiga kemungkinan:

1. Panjang kunci sudah sesuai dengan panjang input untuk SHA1 (64 bit), sehingga tidak perlu dilakukan normalisasi kunci. Misalnya:
    ```
    <>j}.2W,}lw8LqB:7V^Ju=J~ds3=.$@eKk;~G2du0:lq&81<-68_0l#6907C3Vz.
    ```
2. Panjang kunci kurang dari 64 bit, misalnya:

    ```
    qwertyuiop
    ```
    Untuk normalisasi, dilakukan penambahan padding yaitu `0`, sehingga mencapai ukuran 64 bit.
    Hasilnya
    ```
    qwertyuiop000000000000000000000000000000000000000000000000000000
    ```

3. Panjang kunci lebih dari 64 bit, misalnya (100 byte):

    ```
    1835680838382434351145939143193828632331920341628866896842923618141316070322011739557891761769367175
    ```
    Untuk normalisasi, dilakukan perhitungan SHA1 pada kunci tersebut, sehingga menghasilkan 40 byte (hasil dari operasi SHA1).

    Operasi SHA1 pada kunci diatas menghasilkan
    ```
    b18e4143150a6c859f324cb66692ecd6ffdc0ce1
    ```

    Kemudian, ditambahkan padding `0` sehingga panjangnya menjadi 64:

    ```
    b18e4143150a6c859f324cb66692ecd6ffdc0ce100000000000000000000
    ```

Dalam pembuktian ini, kita menggunakan kunci yang ada pada nomor 1 dengan anggapan jika kunci memiliki panjang 64 byte.

### HMAC

Langkah pertama adalah melakukan operasi xor antara kunci dan IPAD.

Key =

```
<>j}.2W,}lw8LqB:7V^Ju=J~ds3=.$@eKk;~G2du0:lq&81<-68_0l#6907C3Vz.
```

Diuraikan sebagai berikut:

```
Indeks ke 0 = < atau 60 dalam ASCII xor 54 = 10
Indeks ke 1 = > atau 62 dalam ASCII xor 54 = 8
Indeks ke 2 = j atau 106 dalam ASCII xor 54 = 92
Indeks ke 3 = } atau 125 dalam ASCII xor 54 = 75
Indeks ke 4 = . atau 46 dalam ASCII xor 54 = 24
Indeks ke 5 = 2 atau 50 dalam ASCII xor 54 = 4
Indeks ke 6 = W atau 87 dalam ASCII xor 54 = 97
Indeks ke 7 = , atau 44 dalam ASCII xor 54 = 26
Indeks ke 8 = } atau 125 dalam ASCII xor 54 = 75
Indeks ke 9 = l atau 108 dalam ASCII xor 54 = 90
Indeks ke 10 = w atau 119 dalam ASCII xor 54 = 65
Indeks ke 11 = 8 atau 56 dalam ASCII xor 54 = 14
Indeks ke 12 = L atau 76 dalam ASCII xor 54 = 122
Indeks ke 13 = q atau 113 dalam ASCII xor 54 = 71
Indeks ke 14 = B atau 66 dalam ASCII xor 54 = 116
Indeks ke 15 = : atau 58 dalam ASCII xor 54 = 12
Indeks ke 16 = 7 atau 55 dalam ASCII xor 54 = 1
Indeks ke 17 = V atau 86 dalam ASCII xor 54 = 96
Indeks ke 18 = ^ atau 94 dalam ASCII xor 54 = 104
Indeks ke 19 = J atau 74 dalam ASCII xor 54 = 124
Indeks ke 20 = u atau 117 dalam ASCII xor 54 = 67
Indeks ke 21 = = atau 61 dalam ASCII xor 54 = 11
Indeks ke 22 = J atau 74 dalam ASCII xor 54 = 124
Indeks ke 23 = ~ atau 126 dalam ASCII xor 54 = 72
Indeks ke 24 = d atau 100 dalam ASCII xor 54 = 82
Indeks ke 25 = s atau 115 dalam ASCII xor 54 = 69
Indeks ke 26 = 3 atau 51 dalam ASCII xor 54 = 5
Indeks ke 27 = = atau 61 dalam ASCII xor 54 = 11
Indeks ke 28 = . atau 46 dalam ASCII xor 54 = 24
Indeks ke 29 = $ atau 36 dalam ASCII xor 54 = 18
Indeks ke 30 = @ atau 64 dalam ASCII xor 54 = 118
Indeks ke 31 = e atau 101 dalam ASCII xor 54 = 83
Indeks ke 32 = K atau 75 dalam ASCII xor 54 = 125
Indeks ke 33 = k atau 107 dalam ASCII xor 54 = 93
Indeks ke 34 = ; atau 59 dalam ASCII xor 54 = 13
Indeks ke 35 = ~ atau 126 dalam ASCII xor 54 = 72
Indeks ke 36 = G atau 71 dalam ASCII xor 54 = 113
Indeks ke 37 = 2 atau 50 dalam ASCII xor 54 = 4
Indeks ke 38 = d atau 100 dalam ASCII xor 54 = 82
Indeks ke 39 = u atau 117 dalam ASCII xor 54 = 67
Indeks ke 40 = 0 atau 48 dalam ASCII xor 54 = 6
Indeks ke 41 = : atau 58 dalam ASCII xor 54 = 12
Indeks ke 42 = l atau 108 dalam ASCII xor 54 = 90
Indeks ke 43 = q atau 113 dalam ASCII xor 54 = 71
Indeks ke 44 = & atau 38 dalam ASCII xor 54 = 16
Indeks ke 45 = 8 atau 56 dalam ASCII xor 54 = 14
Indeks ke 46 = 1 atau 49 dalam ASCII xor 54 = 7
Indeks ke 47 = < atau 60 dalam ASCII xor 54 = 10
Indeks ke 48 = - atau 45 dalam ASCII xor 54 = 27
Indeks ke 49 = 6 atau 54 dalam ASCII xor 54 = 0
Indeks ke 50 = 8 atau 56 dalam ASCII xor 54 = 14
Indeks ke 51 = _ atau 95 dalam ASCII xor 54 = 105
Indeks ke 52 = 0 atau 48 dalam ASCII xor 54 = 6
Indeks ke 53 = l atau 108 dalam ASCII xor 54 = 90
Indeks ke 54 = # atau 35 dalam ASCII xor 54 = 21
Indeks ke 55 = 6 atau 54 dalam ASCII xor 54 = 0
Indeks ke 56 = 9 atau 57 dalam ASCII xor 54 = 15
Indeks ke 57 = 0 atau 48 dalam ASCII xor 54 = 6
Indeks ke 58 = 7 atau 55 dalam ASCII xor 54 = 1
Indeks ke 59 = C atau 67 dalam ASCII xor 54 = 117
Indeks ke 60 = 3 atau 51 dalam ASCII xor 54 = 5
Indeks ke 61 = V atau 86 dalam ASCII xor 54 = 96
Indeks ke 62 = z atau 122 dalam ASCII xor 54 = 76
Indeks ke 63 = . atau 46 dalam ASCII xor 54 = 24
```

Kemudian dilakukan juga xor antara OPAD dengan kunci:

```
Indeks ke 0 = < atau 60 dalam ASCII xor 92 = 96
Indeks ke 1 = > atau 62 dalam ASCII xor 92 = 98
Indeks ke 2 = j atau 106 dalam ASCII xor 92 = 54
Indeks ke 3 = } atau 125 dalam ASCII xor 92 = 33
Indeks ke 4 = . atau 46 dalam ASCII xor 92 = 114
Indeks ke 5 = 2 atau 50 dalam ASCII xor 92 = 110
Indeks ke 6 = W atau 87 dalam ASCII xor 92 = 11
Indeks ke 7 = , atau 44 dalam ASCII xor 92 = 112
Indeks ke 8 = } atau 125 dalam ASCII xor 92 = 33
Indeks ke 9 = l atau 108 dalam ASCII xor 92 = 48
Indeks ke 10 = w atau 119 dalam ASCII xor 92 = 43
Indeks ke 11 = 8 atau 56 dalam ASCII xor 92 = 100
Indeks ke 12 = L atau 76 dalam ASCII xor 92 = 16
Indeks ke 13 = q atau 113 dalam ASCII xor 92 = 45
Indeks ke 14 = B atau 66 dalam ASCII xor 92 = 30
Indeks ke 15 = : atau 58 dalam ASCII xor 92 = 102
Indeks ke 16 = 7 atau 55 dalam ASCII xor 92 = 107
Indeks ke 17 = V atau 86 dalam ASCII xor 92 = 10
Indeks ke 18 = ^ atau 94 dalam ASCII xor 92 = 2
Indeks ke 19 = J atau 74 dalam ASCII xor 92 = 22
Indeks ke 20 = u atau 117 dalam ASCII xor 92 = 41
Indeks ke 21 = = atau 61 dalam ASCII xor 92 = 97
Indeks ke 22 = J atau 74 dalam ASCII xor 92 = 22
Indeks ke 23 = ~ atau 126 dalam ASCII xor 92 = 34
Indeks ke 24 = d atau 100 dalam ASCII xor 92 = 56
Indeks ke 25 = s atau 115 dalam ASCII xor 92 = 47
Indeks ke 26 = 3 atau 51 dalam ASCII xor 92 = 111
Indeks ke 27 = = atau 61 dalam ASCII xor 92 = 97
Indeks ke 28 = . atau 46 dalam ASCII xor 92 = 114
Indeks ke 29 = $ atau 36 dalam ASCII xor 92 = 120
Indeks ke 30 = @ atau 64 dalam ASCII xor 92 = 28
Indeks ke 31 = e atau 101 dalam ASCII xor 92 = 57
Indeks ke 32 = K atau 75 dalam ASCII xor 92 = 23
Indeks ke 33 = k atau 107 dalam ASCII xor 92 = 55
Indeks ke 34 = ; atau 59 dalam ASCII xor 92 = 103
Indeks ke 35 = ~ atau 126 dalam ASCII xor 92 = 34
Indeks ke 36 = G atau 71 dalam ASCII xor 92 = 27
Indeks ke 37 = 2 atau 50 dalam ASCII xor 92 = 110
Indeks ke 38 = d atau 100 dalam ASCII xor 92 = 56
Indeks ke 39 = u atau 117 dalam ASCII xor 92 = 41
Indeks ke 40 = 0 atau 48 dalam ASCII xor 92 = 108
Indeks ke 41 = : atau 58 dalam ASCII xor 92 = 102
Indeks ke 42 = l atau 108 dalam ASCII xor 92 = 48
Indeks ke 43 = q atau 113 dalam ASCII xor 92 = 45
Indeks ke 44 = & atau 38 dalam ASCII xor 92 = 122
Indeks ke 45 = 8 atau 56 dalam ASCII xor 92 = 100
Indeks ke 46 = 1 atau 49 dalam ASCII xor 92 = 109
Indeks ke 47 = < atau 60 dalam ASCII xor 92 = 96
Indeks ke 48 = - atau 45 dalam ASCII xor 92 = 113
Indeks ke 49 = 6 atau 54 dalam ASCII xor 92 = 106
Indeks ke 50 = 8 atau 56 dalam ASCII xor 92 = 100
Indeks ke 51 = _ atau 95 dalam ASCII xor 92 = 3
Indeks ke 52 = 0 atau 48 dalam ASCII xor 92 = 108
Indeks ke 53 = l atau 108 dalam ASCII xor 92 = 48
Indeks ke 54 = # atau 35 dalam ASCII xor 92 = 127
Indeks ke 55 = 6 atau 54 dalam ASCII xor 92 = 106
Indeks ke 56 = 9 atau 57 dalam ASCII xor 92 = 101
Indeks ke 57 = 0 atau 48 dalam ASCII xor 92 = 108
Indeks ke 58 = 7 atau 55 dalam ASCII xor 92 = 107
Indeks ke 59 = C atau 67 dalam ASCII xor 92 = 31
Indeks ke 60 = 3 atau 51 dalam ASCII xor 92 = 111
Indeks ke 61 = V atau 86 dalam ASCII xor 92 = 10
Indeks ke 62 = z atau 122 dalam ASCII xor 92 = 38
Indeks ke 63 = . atau 46 dalam ASCII xor 92 = 114
```

Hasil IPAD xor kunci kemudian digabung dengan pesan (dalam ASCII), menjadi:

```
1089275244972675906514122711161219610412467111247282695112418118831259313721134826761290711614710270141056902101561117596762465666769686566656869656565666967656968696565656666666968676665676669656868686865696667666766656982666567826766686569686569656766696768656968696566676666666768656965676668676768666569656667696567696967
```

Kemudian dilakukan perhitungan hash terhadap penggabungan ini, menghasilkan:

```
b2d45029d89dd4c587a84a55899c209afd046ff7
```

Langkah selanjutnya adalah penggabungan hasil hash pertama diatas dengan hasil dari xor antar OPAD dan kunci, namun sebelumnya, dilakukan perubahan nilai pada hash yang semula adalah bentuk hex diubah menjadi desimal untuk menyeragamkan dengan nilai hasil xor OPAD dengan kunci. Dengan menggunakan tabel ASCII, dikonversi menjadi:

```
b = 98
2 = 50
d = 100
4 = 52
5 = 53
0 = 48
2 = 50
9 = 57
d = 100
8 = 56
9 = 57
d = 100
d = 100
4 = 52
c = 99
5 = 53
8 = 56
7 = 55
a = 97
8 = 56
4 = 52
a = 97
5 = 53
5 = 53
8 = 56
9 = 57
9 = 57
c = 99
2 = 50
0 = 48
9 = 57
a = 97
f = 102
d = 100
0 = 48
4 = 52
6 = 54
f = 102
f = 102
7 = 55
```

Lalu kemudian digabungkan menjadi:


```
9850100525348505710056571001005299535655975652975353565757995048579710210048525410210255969854331141101111233484310016453010210710222419722345647111971141202857235510334271105641108102484512210010996113106100310848127106101108107311111038114
```

Langkah terakhir adalah dengan menghitung nilai hash dari hasil penggabungan kedua diatas:

```
6d24541c463591d0977685c7c042145e0f490258
```

Hasil HMAC-SHA1 = `6d24541c463591d0977685c7c042145e0f490258`

## RSA (Pembangkitan Kunci dan Enkripsi)

### Pembangkitan Kunci
Misalnya diambil

p = `31`
q = `67`

```
n = p * q
n = 31 * 67
n = 2077
```

kemudian

```
tot(n)  = (p − 1) ∗ (q − 1)
        = (31 − 1) ∗ (67 − 1)
        = 1980
```

Untuk membangkitkan e, dipilih suatu nilai, dimana 1 < e < n − 1, dan e relatif prima dengan tot(n).
Misalnya dipilih e = 203, karena 

```
gcd(203, 1980) = 1
```

Untuk membangkitkan d, dipilih suatu nilai yang memenuhi

```
d.e ≡ 1(mod tot(n))
```

misalnya dipilih d = `1307`, karena:

```
1307 * 203 ≡ 1 (mod 1980)
```

Pasangan kunci `e = (203, 2077)`, dan `d = (1307, 2077)`.

### Enkripsi

Setiap indeks array dilakukan operasi:

```
c = m^e mod n
```

`c = hasil enkripsi`

`m = isi dari indeks array 0, 1, 2 ...`

Sehingga menghasilkan:

`arr[i] = nilai = hasil enkripsi`

```
arr[0] = 65 = 1375
arr[1] = 66 = 870
arr[2] = 67 = 335
arr[3] = 69 = 568
arr[4] = 68 = 336
arr[5] = 65 = 1375
arr[6] = 66 = 870
arr[7] = 65 = 1375
arr[8] = 68 = 336
arr[9] = 69 = 568
arr[10] = 65 = 1375
arr[11] = 65 = 1375
arr[12] = 65 = 1375
arr[13] = 66 = 870
arr[14] = 69 = 568
arr[15] = 67 = 335
arr[16] = 65 = 1375
arr[17] = 69 = 568
arr[18] = 68 = 336
arr[19] = 69 = 568
arr[20] = 65 = 1375
arr[21] = 65 = 1375
arr[22] = 65 = 1375
arr[23] = 66 = 870
arr[24] = 66 = 870
arr[25] = 66 = 870
arr[26] = 69 = 568
arr[27] = 68 = 336
arr[28] = 67 = 335
arr[29] = 66 = 870
arr[30] = 65 = 1375
arr[31] = 67 = 335
arr[32] = 66 = 870
arr[33] = 69 = 568
arr[34] = 65 = 1375
arr[35] = 68 = 336
arr[36] = 68 = 336
arr[37] = 68 = 336
arr[38] = 68 = 336
arr[39] = 65 = 1375
arr[40] = 69 = 568
arr[41] = 66 = 870
arr[42] = 67 = 335
arr[43] = 66 = 870
arr[44] = 67 = 335
arr[45] = 66 = 870
arr[46] = 65 = 1375
arr[47] = 69 = 568
arr[48] = 82 = 1538
arr[49] = 66 = 870
arr[50] = 65 = 1375
arr[51] = 67 = 335
arr[52] = 82 = 1538
arr[53] = 67 = 335
arr[54] = 66 = 870
arr[55] = 68 = 336
arr[56] = 65 = 1375
arr[57] = 69 = 568
arr[58] = 68 = 336
arr[59] = 65 = 1375
arr[60] = 69 = 568
arr[61] = 65 = 1375
arr[62] = 67 = 335
arr[63] = 66 = 870
arr[64] = 69 = 568
arr[65] = 67 = 335
arr[66] = 68 = 336
arr[67] = 65 = 1375
arr[68] = 69 = 568
arr[69] = 68 = 336
arr[70] = 69 = 568
arr[71] = 65 = 1375
arr[72] = 66 = 870
arr[73] = 67 = 335
arr[74] = 66 = 870
arr[75] = 66 = 870
arr[76] = 66 = 870
arr[77] = 67 = 335
arr[78] = 68 = 336
arr[79] = 65 = 1375
arr[80] = 69 = 568
arr[81] = 65 = 1375
arr[82] = 67 = 335
arr[83] = 66 = 870
arr[84] = 68 = 336
arr[85] = 67 = 335
arr[86] = 67 = 335
arr[87] = 68 = 336
arr[88] = 66 = 870
arr[89] = 65 = 1375
arr[90] = 69 = 568
arr[91] = 65 = 1375
arr[92] = 66 = 870
arr[93] = 67 = 335
arr[94] = 69 = 568
arr[95] = 65 = 1375
arr[96] = 67 = 335
arr[97] = 69 = 568
arr[98] = 69 = 568
arr[99] = 67 = 335
```

Hasil tiap indeks kemudian diubah menjadi hex dan ditambahkan padding `0` didepannya sehingga panjangnya fix menjadi 4 byte.

```
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
568 = 238 , ditambah padding = 0238
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
1375 = 55f , ditambah padding = 055f
336 = 150 , ditambah padding = 0150
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
1375 = 55f , ditambah padding = 055f
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
568 = 238 , ditambah padding = 0238
335 = 14f , ditambah padding = 014f
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
336 = 150 , ditambah padding = 0150
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
1375 = 55f , ditambah padding = 055f
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
870 = 366 , ditambah padding = 0366
870 = 366 , ditambah padding = 0366
568 = 238 , ditambah padding = 0238
336 = 150 , ditambah padding = 0150
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
1375 = 55f , ditambah padding = 055f
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
336 = 150 , ditambah padding = 0150
336 = 150 , ditambah padding = 0150
336 = 150 , ditambah padding = 0150
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
1538 = 602 , ditambah padding = 0602
870 = 366 , ditambah padding = 0366
1375 = 55f , ditambah padding = 055f
335 = 14f , ditambah padding = 014f
1538 = 602 , ditambah padding = 0602
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
568 = 238 , ditambah padding = 0238
335 = 14f , ditambah padding = 014f
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
336 = 150 , ditambah padding = 0150
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
870 = 366 , ditambah padding = 0366
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
336 = 150 , ditambah padding = 0150
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
335 = 14f , ditambah padding = 014f
870 = 366 , ditambah padding = 0366
336 = 150 , ditambah padding = 0150
335 = 14f , ditambah padding = 014f
335 = 14f , ditambah padding = 014f
336 = 150 , ditambah padding = 0150
870 = 366 , ditambah padding = 0366
1375 = 55f , ditambah padding = 055f
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
870 = 366 , ditambah padding = 0366
335 = 14f , ditambah padding = 014f
568 = 238 , ditambah padding = 0238
1375 = 55f , ditambah padding = 055f
335 = 14f , ditambah padding = 014f
568 = 238 , ditambah padding = 0238
568 = 238 , ditambah padding = 0238
335 = 14f , ditambah padding = 014f
```

Hasil akhir adalah penggabungan nilai enkripsi dengan nilai HMAC:

```
055f0366014f02380150055f0366055f01500238055f055f055f03660238014f055f023801500238055f055f055f03660366036602380150014f0366055f014f03660238055f0150015001500150055f02380366014f0366014f0366055f023806020366055f014f0602014f03660150055f02380150055f0238055f014f03660238014f0150055f023801500238055f0366014f036603660366014f0150055f0238055f014f03660150014f014f01500366055f0238055f0366014f0238055f014f02380238014f1bfe5b0bc0b391bf8cae729de7ea73c8e6517bf3
```

# Pembuktian Dekripsi dan Verifikasi

Pesan yaitu:

```
055f0366014f02380150055f0366055f01500238055f055f055f03660238014f055f023801500238055f055f055f03660366036602380150014f0366055f014f03660238055f0150015001500150055f02380366014f0366014f0366055f023806020366055f014f0602014f03660150055f02380150055f0238055f014f03660238014f0150055f023801500238055f0366014f036603660366014f0150055f0238055f014f03660150014f014f01500366055f0238055f0366014f0238055f014f02380238014f1bfe5b0bc0b391bf8cae729de7ea73c8e6517bf3
```

dibagi menjadi 2 bagian, yaitu pesan terenkripsi dan nilai hash, nilai hash diambil dari 40 byte akhir pesan dengan asumsi bahwa panjang hasil HMAC-SHA1 adalah 40 byte yang disimpan di bagian akhir.

Hasilnya:

1. Pesan terenkripsi
    ```
    055f0366014f02380150055f0366055f01500238055f055f055f03660238014f055f023801500238055f055f055f03660366036602380150014f0366055f014f03660238055f0150015001500150055f02380366014f0366014f0366055f023806020366055f014f0602014f03660150055f02380150055f0238055f014f03660238014f0150055f023801500238055f0366014f036603660366014f0150055f0238055f014f03660150014f014f01500366055f0238055f0366014f0238055f014f02380238014f
    ```

2. Nilai HMAC-SHA1 (tanda tangan)
    ```
    1bfe5b0bc0b391bf8cae729de7ea73c8e6517bf3
    ```

## Dekripsi

Dengan menggunakan kunci privat, yaitu `d = (1307, 2077)`, dilakukan operasi dekripsi pada pesan.

Langkah pertama adalah mengubah array pesan dari hex menjadi desimal.

```
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0238 = 568 didekripsi = 69 = E
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
055f = 1375 didekripsi = 65 = A
0150 = 336 didekripsi = 68 = D
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
055f = 1375 didekripsi = 65 = A
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
0238 = 568 didekripsi = 69 = E
014f = 335 didekripsi = 67 = C
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
0150 = 336 didekripsi = 68 = D
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
055f = 1375 didekripsi = 65 = A
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
0366 = 870 didekripsi = 66 = B
0366 = 870 didekripsi = 66 = B
0238 = 568 didekripsi = 69 = E
0150 = 336 didekripsi = 68 = D
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
055f = 1375 didekripsi = 65 = A
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
0150 = 336 didekripsi = 68 = D
0150 = 336 didekripsi = 68 = D
0150 = 336 didekripsi = 68 = D
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
0602 = 1538 didekripsi = 82 = R
0366 = 870 didekripsi = 66 = B
055f = 1375 didekripsi = 65 = A
014f = 335 didekripsi = 67 = C
0602 = 1538 didekripsi = 82 = R
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
0238 = 568 didekripsi = 69 = E
014f = 335 didekripsi = 67 = C
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
0150 = 336 didekripsi = 68 = D
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
0366 = 870 didekripsi = 66 = B
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0150 = 336 didekripsi = 68 = D
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
014f = 335 didekripsi = 67 = C
0366 = 870 didekripsi = 66 = B
0150 = 336 didekripsi = 68 = D
014f = 335 didekripsi = 67 = C
014f = 335 didekripsi = 67 = C
0150 = 336 didekripsi = 68 = D
0366 = 870 didekripsi = 66 = B
055f = 1375 didekripsi = 65 = A
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
0366 = 870 didekripsi = 66 = B
014f = 335 didekripsi = 67 = C
0238 = 568 didekripsi = 69 = E
055f = 1375 didekripsi = 65 = A
014f = 335 didekripsi = 67 = C
0238 = 568 didekripsi = 69 = E
0238 = 568 didekripsi = 69 = E
014f = 335 didekripsi = 67 = C
```

atau:

```
ABCEDABADEAAABECAEDEAAABBBEDCBACBEADDDDAEBCBCBAERBACRCBDAEDAEACBECDAEDEABCBBBCDAEACBDCCDBAEABCEACEEC
```

Kemudian untuk memverifikasi, dilakukan proses yang sama dengan proses HMAC dengan menggunakan kunci yang sama.

Hasilnya adalah:

```
1bfe5b0bc0b391bf8cae729de7ea73c8e6517bf3
```

Nilai ini kemudian dibandingkan dengan nilai HMAC-SHA1 yang didapatkan dari pesan, dan didapati nilainya sama. Hal ini mengindikasikan pesan terverifikasi.