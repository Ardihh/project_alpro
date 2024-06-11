#include <iostream>
#include <conio.h>
#include <iomanip>
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

void mainMenu();
void strip() {
    cout << "\n------------------------------------------------------------------------------------------\n";
}
      
void header(string* nama) {
	cout << "|o|========= WELCOME TO CASH =========|o|\n";
    cout << "    Atas nama: " << *nama << endl;
    cout << "    Pesanan nomor: " << &nama << endl;
    cout << "|o|===================================|o|\n";
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
    //menampilkan menu makan
    for (int i = 0; i < maxValue; i++) {
        cout << i + 1 << ". " << Makanan.nama[i] << " \t(Rp. " << Makanan.harga[i] << ")\n";
    }
    //pilih makan
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
                mainMenu();
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
                mainMenu();
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

void mainMenu (){
	char jawaban;
	int pilih = 0;
	char input;
	strip();
	do {
		system("cls");
		header(&nama);
		if (pilih == 0) {
    		cout <<  "\x1b[35m" << setw(27) << "=> PILIH MAKAN\n";
    		cout <<  "\x1b[0m" <<  setw(27) << "PILIH MINUM\n";
    		cout <<  setw(25) << "KELUAR\n";
		} else if (pilih == 1) {
			cout << setw(27) << "PILIH MAKAN\n";
	    	cout << "\x1b[35m" << setw(27) << "=> PILIH MINUM\n";
	    	cout << "\x1b[0m"  << setw(25) << "KELUAR\n";
		} else if (pilih == 2) {
			cout << setw(27) << "PILIH MAKAN\n";
			cout << setw(27) << "PILIH MINUM\n";
	    	cout << "\x1b[35m" << setw(29) << "=>    KELUAR\n\x1b[0m";
	    }
		input = _getch();
		switch (input) {
			case 72:
		    	pilih = (pilih == 0) ? 2 : pilih - 1;
	    		break;
			case 80:
			    pilih = (pilih == 2) ? 0 : pilih + 1;
			    break;
		}
	}while(input != 13);
	if (pilih == 0) pesanMakan(&nama); 
    else if (pilih == 1) pesanMinum(&nama); 
    else if (pilih == 3) tampilkanStruk(&nama);
}
int main() {
    cout << "\tAtas nama siapa ka?\t"; getline(cin, nama);
    mainMenu();
}
