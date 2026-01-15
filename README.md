#include <stdio.h>
#include <string.h>

#define MAX 30
#define TUGAS 0
#define UTS   1
#define UAS   2

long long faktorial(int n) {
    if (n <= 1)
        return 1;
    else
        return n * faktorial(n - 1);
}

int fibonacci(int n) {
    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;
    else
        return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    char nim[MAX][15];
    float nilai[MAX][3];
    int jumlah = 0;
    int pilihan, i, j;
    char cariNIM[15];
    int ketemu;

    printf("Masukkan jumlah mahasiswa (maks 30): ");
    scanf("%d", &jumlah);

    for (i = 0; i < jumlah; i++) {
        printf("\nMahasiswa ke-%d\n", i + 1);
        printf("NIM          : ");
        scanf("%s", nim[i]);
        printf("Nilai Tugas  : ");
        scanf("%f", &nilai[i][TUGAS]);
        printf("Nilai UTS    : ");
        scanf("%f", &nilai[i][UTS]);
        printf("Nilai UAS    : ");
        scanf("%f", &nilai[i][UAS]);
    }

    do {
        printf("\n=== MENU PROGRAM ===\n");
        printf("1. Tampilkan seluruh data\n");
        printf("2. Tambah data mahasiswa\n");
        printf("3. Ubah nilai mahasiswa\n");
        printf("4. Hapus data mahasiswa\n");
        printf("5. Hitung dan tampilkan hasil nilai\n");
        printf("6. Fitur rekursif\n");
        printf("7. Keluar\n");
        printf("Pilih menu: ");
        scanf("%d", &pilihan);

        switch (pilihan) {

        case 1:
            printf("\nNIM\t\tTugas\tUTS\tUAS\n");
            for (i = 0; i < jumlah; i++) {
                printf("%s\t%.2f\t%.2f\t%.2f\n",
                       nim[i],
                       nilai[i][TUGAS],
                       nilai[i][UTS],
                       nilai[i][UAS]);
            }
            break;

        case 2:
            if (jumlah >= MAX) {
                printf("Data sudah penuh!\n");
            } else {
                printf("Masukkan NIM        : ");
                scanf("%s", nim[jumlah]);
                printf("Nilai Tugas        : ");
                scanf("%f", &nilai[jumlah][TUGAS]);
                printf("Nilai UTS          : ");
                scanf("%f", &nilai[jumlah][UTS]);
                printf("Nilai UAS          : ");
                scanf("%f", &nilai[jumlah][UAS]);
                jumlah++;
                printf("Data berhasil ditambahkan.\n");
            }
            break;

        case 3:
            printf("Masukkan NIM yang dicari: ");
            scanf("%s", cariNIM);
            ketemu = 0;

            for (i = 0; i < jumlah; i++) {
                if (strcmp(nim[i], cariNIM) == 0) {
                    printf("Nilai Tugas baru: ");
                    scanf("%f", &nilai[i][TUGAS]);
                    printf("Nilai UTS baru  : ");
                    scanf("%f", &nilai[i][UTS]);
                    printf("Nilai UAS baru  : ");
                    scanf("%f", &nilai[i][UAS]);
                    ketemu = 1;
                    break;
                }
            }

            if (!ketemu)
                printf("Data tidak ditemukan.\n");
            break;

        case 4:
            printf("Masukkan NIM yang akan dihapus: ");
            scanf("%s", cariNIM);
            ketemu = 0;

            for (i = 0; i < jumlah; i++) {
                if (strcmp(nim[i], cariNIM) == 0) {
                    for (j = i; j < jumlah - 1; j++) {
                        strcpy(nim[j], nim[j + 1]);
                        nilai[j][0] = nilai[j + 1][0];
                        nilai[j][1] = nilai[j + 1][1];
                        nilai[j][2] = nilai[j + 1][2];
                    }
                    jumlah--;
                    ketemu = 1;
                    printf("Data berhasil dihapus.\n");
                    break;
                }
            }

            if (!ketemu)
                printf("Data tidak ditemukan.\n");
            break;

        case 5: {
            float rata, total;
            float rataTugas = 0, rataUTS = 0, rataUAS = 0;
            float max = -1, min = 101;
            int idxMax = 0, idxMin = 0;

            for (i = 0; i < jumlah; i++) {
                total = nilai[i][TUGAS] + nilai[i][UTS] + nilai[i][UAS];
                rata = total / 3;

                if (rata > max) {
                    max = rata;
                    idxMax = i;
                }
                if (rata < min) {
                    min = rata;
                    idxMin = i;
                }

                rataTugas += nilai[i][TUGAS];
                rataUTS   += nilai[i][UTS];
                rataUAS   += nilai[i][UAS];
            }

            printf("\nRata-rata tiap mahasiswa:\n");
            for (i = 0; i < jumlah; i++) {
                printf("%s : %.2f\n", nim[i],
                       (nilai[i][0] + nilai[i][1] + nilai[i][2]) / 3);
            }

            printf("\nRata-rata Tugas : %.2f\n", rataTugas / jumlah);
            printf("Rata-rata UTS   : %.2f\n", rataUTS / jumlah);
            printf("Rata-rata UAS   : %.2f\n", rataUAS / jumlah);

            printf("\nNilai tertinggi : %s (%.2f)\n", nim[idxMax], max);
            printf("Nilai terendah  : %s (%.2f)\n", nim[idxMin], min);
            break;
        }

        case 6:
            printf("\nFaktorial dari %d = %lld\n", jumlah, faktorial(jumlah));
            printf("Deret Fibonacci (%d): ", jumlah);
            for (i = 0; i < jumlah; i++) {
                printf("%d ", fibonacci(i));
            }
            printf("\n");
            break;

        case 7:
            printf("Program selesai.\n");
            break;

        default:
            printf("Pilihan tidak valid.\n");
        }

    } while (pilihan != 7);

    return 0;
}
<img width="1255" height="938" alt="Cuplikan layar 2026-01-13 212457" src="https://github.com/user-attachments/assets/e062a44f-460c-4f49-b5d3-770eb522a03e" />

