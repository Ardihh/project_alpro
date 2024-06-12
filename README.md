#include <iostream>
#include <conio.h>
#include <iomanip>
using namespace std;

const int maxMakan = 9, maxPesanan = 10, maxMinum = 14;
int totalHarga = 0, totalPorsiMakanan[maxPesanan] = {0}, totalPorsiMinuman[maxPesanan] = {0};
string pesananMakanan[maxPesanan];
int hargaMakanan[maxPesanan], hargaMinuman[maxPesanan];
string pesananMinuman[maxPesanan], nama;
int jumlahPesananMakanan = 0, jumlahPesananMinuman = 0;
string admin = "admin";

struct makanan {
    string nama[maxMakan] = {"Mie Gacoan lvl 0-4", "Mie Gacoan lvl 6-8", "Mie Hompimpa lvl 0-4", "Mie Hompimpa lvl 6-8", "Lumpia Udang", "Udang Rambutan", "Udang Keju", "Siomay Ayam", "Pangsit Goreng"};
    int harga[maxMakan] = {10500, 11500, 10500, 11500, 10500, 9500, 9500, 9500, 9500};
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
	cout << "|o|=========== WELCOME TO CASH ===========|o|\n";
    cout << "    Atas nama: " << *nama << endl;
    cout << "    Pesanan nomor: " << &nama << endl;
    cout << "|o|=======================================|o|\n\n";
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
    int pilih = 0;
	char input;
	do {
		system("cls");
    	header(nama);
    	cout << "Pilih makanan: \n";
	    for (int i = 0; i < maxMakan; ++i) {
           	if (i == pilih) {
   	            cout << "\x1b[35m=> " << Makanan.nama[i] << "\x1b[0m" << endl;
	        } else {
              	cout << "   " << Makanan.nama[i] << endl;
           	}
       	}
		input = _getch();
		switch (input) {
			case 72: // Panah atas (ASCII value)
                pilih = (pilih == 0) ? maxMakan - 1 : pilih - 1;
                break;
            case 80: // Panah bawah (ASCII value)
                pilih = (pilih == maxMakan - 1) ? 0 : pilih + 1;
                break;
		}
	}while(input != 13);
    if (pilih >= 0 && pilih <= 11) {
        string makananDipilih = Makanan.nama[pilih];
        int hargaPilihan = Makanan.harga[pilih];
        int level;
        if (pilih == 0 || pilih == 1 || pilih == 2 || pilih == 3){
        	cout << "\nLevel Berapa ka? "; cin >> level;
		}
        cout << "Anda memilih " << makananDipilih;
		if (pilih == 0 || pilih == 1 || pilih == 2 || pilih == 3){
			cout << " level " << level;
		}
		cout << " dengan harga Rp. " << hargaPilihan << "\n";
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
    int pilih = 0;
	char input;
	do {
		system("cls");
    	header(nama);
    	cout << "Pilih minuman: \n";
	    for (int i = 0; i < maxMinum; ++i) {
           	if (i == pilih) {
   	            cout << "\x1b[35m=> " << Minuman.nama[i] << "\x1b[0m" << endl;
	        } else {
              	cout << "   " << Minuman.nama[i] << endl;
           	}
       	}
		input = _getch();
		switch (input) {
			case 72: // Panah atas (ASCII value)
                pilih = (pilih == 0) ? maxMinum - 1 : pilih - 1;
                break;
            case 80: // Panah bawah (ASCII value)
                pilih = (pilih == maxMinum - 1) ? 0 : pilih + 1;
                break;
		}
	}while(input != 13);
    if (pilih >= 1 && pilih <= maxMinum) {
        string minumanDipilih = Minuman.nama[pilih];
        int hargaPilihan = Minuman.harga[pilih];
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

void mainMenu(){
	int pilih = 0;
	char input;
	do {
		system("cls");
		header(&nama);
		if (pilih == 0) {
    		cout << "\t\x1b[35m==============================\n\t|         PESAN MAKAN         |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|         PESAN MINUM         |\n\t==============================\n";
			cout << "\t==============================\n\t|           SELESAI           |\n\t==============================\n";
		} else if (pilih == 1) {
			cout << "\t==============================\n\t|         PESAN MAKAN         |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|         PESAN MINUM         |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|           SELESAI           |\n\t==============================\n";
		} else if (pilih == 2) {
			cout << "\t==============================\n\t|         PESAN MAKAN         |\n\t==============================\n";
			cout << "\t==============================\n\t|         PESAN MINUM         |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|           SELESAI           |\n\t==============================\x1b[0m\n";
	    }
		input = _getch();
		switch (input) {
			case 72: //atas
		    	pilih = (pilih == 0) ? 2 : pilih - 1;
	    		break;
			case 80: //bawah
			    pilih = (pilih == 2) ? 0 : pilih + 1;
			    break;
		}
	}while(input != 13);
	if (pilih == 0) pesanMakan(&nama); 
    else if (pilih == 1) pesanMinum(&nama); 
    else if (pilih == 2) tampilkanStruk(&nama);
}

void Admin();

void createMenu() {
    system("cls");
    int choice, index;
    string name;
    int price;
    
    cout << "Tambah Menu:\n1. Makanan\n2. Minuman\n>> ";
    cin >> choice;
    
    if (choice == 1) {
		cout << "Nama Makanan: ";
        cin.ignore();
        getline(cin, name);
        cout << "Harga: ";
   	    cin >> price;
    	Makanan.nama[index] = name;
        Makanan.harga[index] = price;
    } else if (choice == 2) {
        cout << "Nama Minuman: ";
        cin.ignore();
        getline(cin, name);
        cout << "Harga: ";
        cin >> price;
        Minuman.nama[index] = name;
        Minuman.harga[index] = price;
    } else {
        cout << "Pilihan tidak valid.\n";
    }
    
    system("pause");
    Admin();
}

void deleteMenu() {
    system("cls");
    int choice, index;
    char input;
    
    cout << "Hapus Menu:\n1. Makanan\n2. Minuman\n>> ";
    cin >> choice;
    
    if (choice == 1) {
		do {
			system("cls");
    		header(&nama);
	    	cout << "Pilih makanan: \n";
		    for (int i = 0; i < maxMakan; i++) {
        	   	if (i == index) {
   		            cout << "\x1b[35m=> " << Makanan.nama[i] << "\x1b[0m" << endl;
		        } else {
        	      	cout << "   " << Makanan.nama[i] << endl;
    	       	}
	       	}
			input = _getch();
			switch (input) {
				case 72: // Panah atas (ASCII value)
                	index = (index == 0) ? maxMakan - 1 : index - 1;
            	    break;
        	    case 80: // Panah bawah (ASCII value)
    	            index = (index == maxMakan - 1) ? 0 : index + 1;
	                break;
			}
   		} while (input != 13);
        if (index >= 0 && index < maxMakan) {
            Makanan.nama[index] = "";
            Makanan.harga[index] = 0;
        } else {
            cout << "Index tidak valid.\n";
        }
    } else if (choice == 2) {
		do {
			system("cls");
    		header(&nama);
    		cout << "Pilih minuman: \n";
		    for (int i = 0; i < maxMinum; ++i) {
           		if (i == index) {
   	    	        cout << "\x1b[35m=> " << Minuman.nama[i] << "\x1b[0m" << endl;
		        } else {
	              	cout << "   " << Minuman.nama[i] << endl;
           		}
       		}
			input = _getch();
			switch (input) {
				case 72: // Panah atas (ASCII value)
        	        index = (index == 0) ? maxMinum - 1 : index - 1;
    	            break;
	            case 80: // Panah bawah (ASCII value)
                	index = (index == maxMinum - 1) ? 0 : index + 1;
            	    break;
			}
		}while(input != 13);
        if (index >= 0 && index < maxMinum) {
            Minuman.nama[index] = "";
            Minuman.harga[index] = 0;
        } else {
            cout << "Index tidak valid.\n";
        }
    } else {
        cout << "Pilihan tidak valid.\n";
    }
    
    system("pause");
    Admin();
}

void updateMenu() {
    system("cls");
    int choice, index = 0;
    string name;
    int price;
    
    cout << "Edit Menu:\n1. Makanan\n2. Minuman\n>> ";
    cin >> choice;
    
    if (choice == 1) {
	char input;
	do {
		system("cls");
    	header(&nama);
    	cout << "Pilih makanan: \n";
	    for (int i = 0; i < maxMakan; i++) {
           	if (i == index) {
   	            cout << "\x1b[35m=> " << Makanan.nama[i] << "\x1b[0m" << endl;
	        } else {
              	cout << "   " << Makanan.nama[i] << endl;
           	}
       	}
		input = _getch();
		switch (input) {
			case 72: // Panah atas (ASCII value)
                index = (index == 0) ? maxMakan - 1 : index - 1;
                break;
            case 80: // Panah bawah (ASCII value)
                index = (index == maxMakan - 1) ? 0 : index + 1;
                break;
		}
    } while (input != 13);
        if (index >= 0 && index < maxMakan) {
            cout << "Nama Makanan: ";
            cin.ignore();
            getline(cin, name);
            cout << "Harga: ";
            cin >> price;
            Makanan.nama[index] = name;
            Makanan.harga[index] = price;
        } else {
            cout << "Index tidak valid.\n";
        }
    } else if (choice == 2) {
        char input;
	do {
		system("cls");
    	header(&nama);
    	cout << "Pilih minuman: \n";
	    for (int i = 0; i < maxMinum; ++i) {
           	if (i == index) {
   	            cout << "\x1b[35m=> " << Minuman.nama[i] << "\x1b[0m" << endl;
	        } else {
              	cout << "   " << Minuman.nama[i] << endl;
           	}
       	}
		input = _getch();
		switch (input) {
			case 72: // Panah atas (ASCII value)
                index = (index == 0) ? maxMinum - 1 : index - 1;
                break;
            case 80: // Panah bawah (ASCII value)
                index = (index == maxMinum - 1) ? 0 : index + 1;
                break;
		}
	}while(input != 13);
        if (index >= 0 && index < maxMinum) {
            cout << "Nama Minuman: ";
            cin.ignore();
            getline(cin, name);
            cout << "Harga: ";
            cin >> price;
            Minuman.nama[index] = name;
            Minuman.harga[index] = price;
        } else {
            cout << "Index tidak valid.\n";
        }
    } else {
        cout << "Pilihan tidak valid.\n";
    }
    
    system("pause");
    Admin();
}

void readMenu() {
    system("cls");
    cout << "Daftar Menu Makanan:\n";
    for (int i = 0; i < maxMakan; i++) {
        cout << i + 1 << ". " << Makanan.nama[i] << " - " << Makanan.harga[i] << endl;
    }
    cout << "\nDaftar Menu Minuman:\n";
    for (int i = 0; i < maxMinum; i++) {
        cout << i + 1 << ". " << Minuman.nama[i] << " - " << Minuman.harga[i] << endl;
    }
    system("pause");
    Admin();
}

void Admin() {
    int pilih = 0;
	char input;
	strip();
	do {
		system("cls");
		header(&nama);
		if (pilih == 0) {
    		cout << "\t\x1b[35m==============================\n\t|        TAMBAH  MENU        |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|         HAPUS MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         EDIT  MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         LIHAT MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|           KELUAR           |\n\t==============================\n";
		} else if (pilih == 1) {
			cout << "\t==============================\n\t|        TAMBAH  MENU        |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|         HAPUS MENU         |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|         EDIT  MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         LIHAT MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|           KELUAR           |\n\t==============================\n";
		} else if (pilih == 2) {
			cout << "\t==============================\n\t|        TAMBAH  MENU        |\n\t==============================\n";
			cout << "\t==============================\n\t|         HAPUS MENU         |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|         EDIT  MENU         |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|         LIHAT MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|           KELUAR           |\n\t==============================\n";
	    }else if (pilih == 3){
	    	cout << "\t==============================\n\t|        TAMBAH  MENU        |\n\t==============================\n";
			cout << "\t==============================\n\t|         HAPUS MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         EDIT  MENU         |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|         LIHAT MENU         |\n\t==============================\x1b[0m\n";
			cout << "\t==============================\n\t|           KELUAR           |\n\t==============================\n";
		}else if (pilih == 4){
			cout << "\t==============================\n\t|        TAMBAH  MENU        |\n\t==============================\n";
			cout << "\t==============================\n\t|         HAPUS MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         EDIT  MENU         |\n\t==============================\n";
			cout << "\t==============================\n\t|         LIHAT MENU         |\n\t==============================\n";
			cout << "\t\x1b[35m==============================\n\t|           KELUAR           |\n\t==============================\x1b[0m\n";
		}
		input = _getch();
		switch (input) {
			case 72: //atas
		    	pilih = (pilih == 0) ? 4 : pilih - 1;
	    		break;
			case 80: //bawah
			    pilih = (pilih == 4) ? 0 : pilih + 1;
			    break;
		}
	}while(input != 13);
    switch (pilih) {
        case 0: createMenu(); break;
        case 1: deleteMenu(); break;
        case 2: updateMenu(); break;
        case 3: readMenu(); break;
        case 4:
        	system("cls");
			cin.ignore();
			cout << "\tAtas nama siapa ka?\t"; 
			getline(cin, nama);
			mainMenu();
			break;
        default: cout << "Pilihan tidak valid.\n"; Admin(); break;
    }
}

void loginAdmin(){
	string pass;
	system("cls");
   	header(&nama);
    cout << "\tMasukkan password: "; cin >> pass;
   	if (pass == admin){
		Admin();
	}
}
int main() {
	system("cls");
   	cout << "\tAtas nama siapa ka?\t"; getline(cin, nama);
    if (nama == admin){
   		loginAdmin();
	}else{
		cout << "\tAtas nama siapa ka?\t"; 
		getline(cin, nama);
		mainMenu();
	}	
	system("cls");
}
