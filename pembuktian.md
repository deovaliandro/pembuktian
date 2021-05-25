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

### Key xor IPAD

Key =

```
<>j}.2W,}lw8LqB:7V^Ju=J~ds3=.$@eKk;~G2du0:lq&81<-68_0l#6907C3Vz.
```

Key (dalam hex)=
```
3C3E6A7D2E32572C7D6C77384C71423A37565E4A753D4A7E6473333D2E2440654B6B3B7E47326475303A6C712638313C2D36385F306C23363930374333567A2E
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

## RSA

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
