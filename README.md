#include <iostream>
#include <conio.h>
#include <iomanip>
using namespace std;

const int maxMakan = 10, maxPesanan = 10, maxMinum = 14;
int totalHarga = 0, totalPorsiMakanan[maxPesanan] = {0}, totalPorsiMinuman[maxPesanan] = {0};
string pesananMakanan[maxPesanan];
int hargaMakanan[maxPesanan], hargaMinuman[maxPesanan];
string pesananMinuman[maxPesanan], nama;
int jumlahPesananMakanan = 0, jumlahPesananMinuman = 0;

struct makanan {
    string nama[maxMakan] = {"Mie Gacoan lvl 0-4", "Udang Keju", "Mie Gacoan lvl 6-8", "Udang Rambutan", "Mie Hompimpa lvl 0-4", "Lumpia Udang", "Mie Hompimpa lvl 6-8", "Siomay Ayam", "Pangsit Goreng"};
    int harga[maxMakan] = {10500, 11500, 10500, 11500, 10500, 9500, 9500, 9500, 9500, 9500};
} Makanan;

struct minuman {
    string nama[maxMinum] = {"Es Gobak Sodor", "Es Petak Umpet", "Es Sluku Bathok", "Es Teklek", "Air Mineral", "Lemon Tea", "Milo", "Orange", "Es Teh", "Teh Tarik", "Vanilla Latte", "Thai Tea", "Thai Grean Tea", "Es Coklat"};
    int harga[maxMinum] = {8600, 8000, 6000, 6000, 4000, 6000, 8000, 5000, 5500, 6400, 8000, 8000, 8000, 8000};
} Minuman;

void mainMenu();
void strip() {
    cout << "\n------------------------------------------------------------------------------------------\n";
}
      
void header(string* nama) {
	cout << "|o|========= WELCOME TO CASH =========|o|\n";
    cout << "    Atas nama: " << *nama << endl;
    cout << "    Pesanan nomor: " << &nama << endl;
    cout << "|o|===================================|o|\n\n";
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
    //menampilkan menu makan
    int pilih = 0;
	char input;
	do {
		system("cls");
    	header(nama);
    	cout << "Pilih makanan: \n";;
		if (pilih == 0) {
    		cout << "\x1b[35m=> "<< Makanan.nama[0] << "\x1b[0m          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 1) {
			cout <<  "   Mie Gacoan lvl 0-4      " << "\x1b[35m=>  Udang Keju\n";
    		cout <<  "\x1b[0m   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 2) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "\x1b[35m=> Mie Gacoan lvl 6-8          " << "\x1b[0mUdang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 3) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8      " << "\x1b[35m=>  Udang Rambutan\n";
    		cout <<  "   \x1b[0mMie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 4) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "\x1b[35m=> Mie Hompimpa lvl 0-4        " << "\x1b[0mLumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 5) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4    " << "\x1b[35m=>  Lumpia Udang\n";
    		cout <<  "   \x1b[0mMie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 6) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "\x1b[35m=> Mie Hompimpa lvl 6-8\n";
    		cout <<  "   \x1b[0mSiomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 7) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4    " << "\x1b[35m=>  Lumpia Udang\n";
    		cout <<  "   \x1b[0mMie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 8) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "\x1b[35m=> Siomay Ayam\x1b[0m\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 9) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4    " << "\x1b[35m=>  Lumpia Udang\x1b[0m\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		} else if (pilih == 10) {
			cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4        Lumpia Udang\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "\x1b[35m=> Pangsit Goreng\x1b[0m\n";
	    }else if (pilih == 11){
	    	cout <<  "   Mie Gacoan lvl 0-4          Udang Keju\n";
    		cout <<  "   Mie Gacoan lvl 6-8          Udang Rambutan\n";
    		cout <<  "   Mie Hompimpa lvl 0-4    " << "\x1b[35m=>  Lumpia Udang\x1b[0m\n";
    		cout <<  "   Mie Hompimpa lvl 6-8\n";
    		cout <<  "   Siomay Ayam\n";
    		cout <<  "   Pangsit Goreng\n";
		}
		input = _getch();
		switch (input) {
			case 72: // Panah atas (ASCII value)
		    	pilih = (pilih == 0) ? 10 : pilih - 2;
	    		break;
			case 80: // Panah bawah (ASCII value)
			    pilih = (pilih == 10) ? 0 : pilih + 2;
			    break;
			    case 75: //kiri
				pilih = (pilih == 11) ? 0 : pilih - 1;
			    break;
			case 77: //kanan
				pilih = (pilih == 11) ? 11 : pilih + 1;
			    break;
		}
	}while(input != 13);
    if (pilih >= 0 && pilih <= maxMakan) {
        string makananDipilih = Makanan.nama[pilih];
        int hargaPilihan = Makanan.harga[pilih];
    	if (pilih == (7,9,11)){
    		makananDipilih = Makanan.nama[5];
    		hargaPilihan = Makanan.harga[5];
		}
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
    for (int i = 0; i < maxMinum; i++) {
        cout << i + 1 << ". " << Minuman.nama[i] << " \t(Rp. " << Minuman.harga[i] << ")\n";
    }
    int pilihan;
    cout << ">> "; cin >> pilihan;
    if (pilihan >= 1 && pilihan <= maxMinum) {
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
		input = _getche();
		switch (input) {
			case 72: //atas
		    	pilih = (pilih == 0) ? 2 : pilih - 1;
	    		break;
			case 80: //bawah
			    pilih = (pilih == 2) ? 0 : pilih + 1;
			    break;
			case 75: //kiri
				pilih = (pilih == 2) ? 0 : pilih + 1;
			    break;
			case 77: //kanan
				pilih = (pilih == 2) ? 0 : pilih + 1;
			    break;
		}
	}while(input != 13);
	if (pilih == 0) pesanMakan(&nama); 
    else if (pilih == 1) pesanMinum(&nama); 
    else if (pilih == 2) tampilkanStruk(&nama);
}
int main() {
    cout << "\tAtas nama siapa ka?\t"; getline(cin, nama);
    mainMenu();
}
