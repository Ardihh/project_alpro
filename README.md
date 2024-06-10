#include <iostream>
using namespace std;

const int maxValue = 3;
const int maxPesanan = 10;
int totalHarga = 0;
int totalPorsiMakanan[maxPesanan] = {0};
int totalPorsiMinuman[maxPesanan] = {0};
string pesananMakanan[maxPesanan];
int hargaMakanan[maxPesanan];
string pesananMinuman[maxPesanan];
int hargaMinuman[maxPesanan];
int jumlahPesananMakanan = 0;
int jumlahPesananMinuman = 0;
string nama;

struct makanan {
    string nama[maxValue] = {"mie meekow", "udang keju", "rice bowl"};
    int harga[maxValue] = {11500, 10400, 15000};
} Makanan;

struct minuman {
    string nama[maxValue] = {"teh tawar", "teh manis", "green tea"};
    int harga[maxValue] = {4000, 5000, 7000};
} Minuman;

void showMenu();
void strip() {
    cout << "\n---------------------------------------------------------------------------------------------\n";
}

void header(string* nama) {
    cout << "Atas nama: " << *nama;
    cout << "\nPesanan nomor: " << &nama;
    strip();
}

void tampilkanStruk(string* nama) {
    system("cls");
    header(nama);
    cout << "Struk Pembayaran\n";
    cout << "Makanan:\n";
    for (int i = 0; i < jumlahPesananMakanan; i++) {
        cout << "- " << pesananMakanan[i] << " (" << totalPorsiMakanan[i] << " porsi)" << " - Rp. " << hargaMakanan[i] * totalPorsiMakanan[i] << endl;
    }
    cout << "Minuman:\n";
    for (int i = 0; i < jumlahPesananMinuman; i++) {
        cout << "- " << pesananMinuman[i] << " (" << totalPorsiMinuman[i] << " porsi)" << " - Rp. " << hargaMinuman[i] * totalPorsiMinuman[i] << endl;
    }
    int ppn = totalHarga * 0.10;
    cout << "PPN: 10%\n";
    totalHarga += ppn;
    cout << "Total Harga: Rp. " << totalHarga << endl;
}

void pesanMakan(string* nama) {
    system("cls");
    header(nama);
    cout << "Pilih makanan: \n";
    for (int i = 0; i < maxValue; i++) {
        cout << i + 1 << ". " << Makanan.nama[i] << " \t(Rp. " << Makanan.harga[i] << ")\n";
    }
    int pilihan;
    cout << ">> "; cin >> pilihan;
    if (pilihan >= 1 && pilihan <= maxValue) {
        string makananDipilih = Makanan.nama[pilihan - 1];
        int hargaPilihan = Makanan.harga[pilihan - 1];
        cout << "Anda memilih " << makananDipilih << " dengan harga Rp. " << hargaPilihan << "\n";
        int porsi;
        cout << "Berapa porsi? "; cin >> porsi;
        pesananMakanan[jumlahPesananMakanan] = makananDipilih;
        totalPorsiMakanan[jumlahPesananMakanan] = porsi;
        hargaMakanan[jumlahPesananMakanan] = hargaPilihan;
        jumlahPesananMakanan++;
        totalHarga += hargaPilihan * porsi;
        cout << "Saya konfirmasi lagi, pesanan Anda " << makananDipilih << ", untuk " << porsi << " porsi\n";
        char konfir;
        cout << "Apakah sudah benar? (y/n) "; cin >> konfir;
        if (konfir == 'y' || konfir == 'Y') {
            cout << "Apakah ingin tambah pesanan? (y/n) "; cin >> konfir;
            if (konfir == 'y' || konfir == 'Y') {
                pesanMakan(nama);
            } else {
                showMenu();
            }
        } else {
            totalHarga -= hargaPilihan * porsi;
            jumlahPesananMakanan--;
            cout << "Pesanan dibatalkan. Silakan ulangi.\n";
            system("pause");
            pesanMakan(nama);
        }
    } else {
        cout << "Pilihan tidak valid.\n";
    }
}

void pesanMinum(string* nama) {
    system("cls");
    header(nama);
    cout << "Pilih minuman: \n";
    for (int i = 0; i < maxValue; i++) {
        cout << i + 1 << ". " << Minuman.nama[i] << " \t(Rp. " << Minuman.harga[i] << ")\n";
    }
    int pilihan;
    cout << ">> "; cin >> pilihan;
    if (pilihan >= 1 && pilihan <= maxValue) {
        string minumanDipilih = Minuman.nama[pilihan - 1];
        int hargaPilihan = Minuman.harga[pilihan - 1];
        cout << "Anda memilih " << minumanDipilih << " dengan harga Rp. " << hargaPilihan << "\n";
        int porsi;
        cout << "Berapa porsi? "; cin >> porsi;
        pesananMinuman[jumlahPesananMinuman] = minumanDipilih;
        totalPorsiMinuman[jumlahPesananMinuman] = porsi;
        hargaMinuman[jumlahPesananMinuman] = hargaPilihan;
        jumlahPesananMinuman++;
        totalHarga += hargaPilihan * porsi;
        cout << "Saya konfirmasi lagi, pesanan Anda " << minumanDipilih << ", untuk " << porsi << " porsi\n";
        char konfir;
        cout << "Apakah sudah benar? (y/n) "; cin >> konfir;
        if (konfir == 'y' || konfir == 'Y') {
            cout << "Apakah ingin tambah pesanan? (y/n) "; cin >> konfir;
            if (konfir == 'y' || konfir == 'Y') {
                pesanMinum(nama);
            } else {
                showMenu();
            }
        } else {
            totalHarga -= hargaPilihan * porsi;
            jumlahPesananMinuman--;
            cout << "Pesanan dibatalkan. Silakan ulangi.\n";
            system("pause");
            pesanMinum(nama);
        }
    } else {
        cout << "Pilihan tidak valid.\n";
    }
}

void showMenu() {
    int pilih = 0;
    system("cls");
    header(&nama);
    cout << "Silahkan pilih:\n1. Pesan makan\n2. Pesan minum\n3. Selesai memesan\n>> "; cin >> pilih;
    switch (pilih) {
        case 1: pesanMakan(&nama); break;
        case 2: pesanMinum(&nama); break;
        case 3: tampilkanStruk(&nama); break;
        default: cout << "Pilihan tidak valid.\n"; showMenu(); break;
    }
}

int main() {
    cout << "Atas nama siapa ka? "; cin >> nama;
    showMenu();
}
