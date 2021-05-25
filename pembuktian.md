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

### Pembangkitan Kunci
Ada tiga kemungkinan:

1. Panjang kunci sudah sesuai dengan panjang input untuk SHA1 (64 bit), sehingga tidak perlu dilakukan normalisasi kunci. Misalnya:
    ```
    `)DUpP{I@}sILmugg#X_G<*DFnF&J1J,D_4mdh>(p63F0v=<_~11eMpOfq)gXHClF`
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