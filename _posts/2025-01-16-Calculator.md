---
title: Calculator
date: 2025-01-16 00:00:00 +0800
categories: Mini Project
tags: Phyton without numpy
---

hello everyone, i'm gladys.
this is my second project in my first year which is to make a matrix calculator with python without using numphy and sympy

```python
def hitung_matrix(matriks):
    for baris in matriks:
        print(" ".join(map(str, baris)))

def proses_penjumlahan_matrix(matriks1, matriks2):
    jawab = [[matriks1[i][j] + matriks2[i][j] for j in range(len(matriks1[0]))] for i in range(len(matriks1))]
    return jawab

def proses_pengurangan_matrix(matriks1, matriks2):
    jawab = [[matriks1[i][j] - matriks2[i][j] for j in range(len(matriks1[0]))] for i in range(len(matriks1))]
    return jawab

def proses_perkalian_matrix(matriks1, matriks2):
    jawab = [[0 for _ in range(len(matriks2[0]))] for _ in range(len(matriks1))]
    for i in range(len(matriks1)):
        for j in range(len(matriks2[0])):
            for k in range(len(matriks2)):
                jawab[i][j] += matriks1[i][k] * matriks2[k][j]
    return jawab

def proses_determinan_2x2(matriks):
    return matriks[0][0] * matriks[1][1] - matriks[0][1] * matriks[1][0]

def proses_determinant_3x3(matriks):
    det = (matriks[0][0] * (matriks[1][1] * matriks[2][2] - matriks[1][2] * matriks[2][1]) -
           matriks[0][1] * (matriks[1][0] * matriks[2][2] - matriks[1][2] * matriks[2][0]) +
           matriks[0][2] * (matriks[1][0] * matriks[2][1] - matriks[1][1] * matriks[2][0]))
    return det

def proses_determinant_4x4(matriks):
    det = 0
    for i in range(4):
        minor = [[matriks[m][n] for n in range(4) if n != i] for m in range(1, 4)]
        cofactor = matriks[0][i] * proses_determinant_3x3(minor)
        det += cofactor if i % 2 == 0 else -cofactor
    return det

def proses_transpose_matrix(matriks):
    return [[matriks[j][i] for j in range(len(matriks))] for i in range(len(matriks[0]))]

def inverse_matrix(matrix):
    n = len(matrix)
    luas_matriks = [row + [1 if i == j else 0 for j in range(n)] for i, row in enumerate(matrix)]
    
    # Eliminasi Gauss-Jordan
    for i in range(n):
        # Pivot
        if luas_matriks[i][i] == 0:
            for j in range(i + 1, n):
                if luas_matriks[j][i] != 0:
                    luas_matriks[i], luas_matriks[j] = luas_matriks[j], luas_matriks[i]
                    break
            else:
                print("Invers tidak dapat dihitung untuk matriks dengan determinan 0.")
                return None
        
        # Normalize pivot row
        pivot = luas_matriks[i][i]
        for j in range(2 * n):
            luas_matriks[i][j] /= pivot
        
        # Eliminate other rows
        for k in range(n):
            if k != i:
                factor = luas_matriks[k][i]
                for j in range(2 * n):
                    luas_matriks[k][j] -= factor * luas_matriks[i][j]
    
    # Extract inverse matrix
    inverse = [row[n:] for row in luas_matriks]
    return inverse

def main():
    print("PENGOPRASIAN MATRIKS (MAKS 4X4)")
    print("Pilih Opsi:")
    print("1.Penjumlahan")
    print("2.Pengurangan")
    print("3. Perkalian")
    print("4. Determinan")
    print("5. Transpose")
    print("6. Invers")
    choice = input("jenis pengoprasian apa: ")
    
    baris_matriks = int(input("masukkan jumlah baris (max 4): "))
    kolom_matriks = int(input("masukkan jumlah kolom (max 4): "))

    print("masukkan angka matrix pertama:")
    matriks1 = [[int(input(f"Element [{i+1}][{j+1}]: ")) for j in range(kolom_matriks)] for i in range(baris_matriks)]

    print("masukkan angka matriks kedua:")
    matriks2 = [[int(input(f"Element [{i+1}][{j+1}]: ")) for j in range(kolom_matriks)] for i in range(baris_matriks)]

    if choice == '1':
        result = proses_penjumlahan_matrix(matriks1, matriks2)
        print("jawaban:")
        hitung_matrix(result)

    elif choice == '2':
        result = proses_penjumlahan_matrix(matriks1, matriks2)
        print("jawaban:")
        hitung_matrix(result)

    elif choice == '3':
        if baris_matriks == kolom_matriks:
            result = proses_perkalian_matrix(matriks1, matriks2)
            print("jawaban:")
            hitung_matrix(result)

    elif choice == '4':
        if baris_matriks == kolom_matriks:
            if baris_matriks == 2:
                result = proses_determinan_2x2(matriks1)
            elif baris_matriks == 3:
                result = proses_determinant_3x3(matriks1)
            elif baris_matriks == 4:
                result = proses_determinant_4x4(matriks1)
            print(f"hasil Determinan Matriks: {result}")
        
    elif choice == '5':
        result = proses_transpose_matrix(matriks1)
        print("Transpose dari matriks pertama adalah:")
        hitung_matrix(result)

    elif choice == '6':
        if baris_matriks == kolom_matriks:
            result = inverse_matrix(matriks1)
            if result:
                print("Invers Matriks:")
                hitung_matrix(result)

    else:
        print("silahkan input ulang, terjadi kesalahan pada penginputan angka pada matriks")


if __name__ == "__main__":
    main()
```