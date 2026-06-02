#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
#include <algorithm>
using namespace std;

// [ARRAY STRUCT] - Struct Makanan & Array of Struct
struct Makanan { int id; string nama; int harga; int stok; };

const int MAX = 20;
Makanan daftar[MAX];
int jumlah = 0;

// [ARRAY MULTI DIMENSI] - Riwayat transaksi [baris][kolom]
// kolom: 0=id, 1=qty, 2=total, 3=bayar, 4=kembalian
int transaksi[50][5];
int jmlTransaksi = 0;

// [POINTER] - Update stok lewat pointer
void updateStok(Makanan* m, int qty) { m->stok -= qty; }

// [REKURSIF] - Hitung total belanja secara rekursif
int totalBelanja(int arr[][5], int n) {
    if (n == 0) return 0;
    return arr[n-1][2] + totalBelanja(arr, n-1);
}

// [SORTING] - Bubble sort berdasarkan harga ascending
void sortByHarga() {
    for (int i = 0; i < jumlah-1; i++)
        for (int j = 0; j < jumlah-i-1; j++)
            if (daftar[j].harga > daftar[j+1].harga)
                swap(daftar[j], daftar[j+1]);
}

// Helper toLower & garis pembatas
string toLower(string s) {
    transform(s.begin(), s.end(), s.begin(), ::tolower);
    return s;
}
void garis(char c = '-', int n = 52) { cout << string(n, c) << "\n"; }

// [SEARCHING] - Linear search case-insensitive
int cariMakanan(string nama) {
    for (int i = 0; i < jumlah; i++)
        if (toLower(daftar[i].nama) == toLower(nama)) return i;
    return -1;
}

// [FILE] - Simpan data makanan ke makanan.txt
void simpanFile() {
    ofstream f("makanan.txt");
    f << string(40, '=') << "\n";
    f << "       DATA MENU MAKANAN JADUDUL\n";
    f << string(40, '=') << "\n";
    f << left << setw(5)  << "ID"
              << setw(15) << "NAMA"
              << setw(12) << "HARGA"
              << "STOK\n";
    f << string(40, '-') << "\n";
    for (int i = 0; i < jumlah; i++)
        f << left << setw(5)  << daftar[i].id
                  << setw(15) << daftar[i].nama
                  << setw(12) << ("Rp"+to_string(daftar[i].harga))
                  << daftar[i].stok << "\n";
    f << string(40, '=') << "\n";
    f.close();
}

// [FILE] - Simpan transaksi ke transaksi.txt
void simpanTransaksi() {
    ofstream f("transaksi.txt");
    f << string(56, '=') << "\n";
    f << "          RIWAYAT TRANSAKSI WARUNG JADUDUL\n";
    f << string(56, '=') << "\n";
    f << left << setw(4)  << "No"
              << setw(6)  << "ID"
              << setw(5)  << "Qty"
              << setw(12) << "Total"
              << setw(12) << "Bayar"
              << "Kembalian\n";
    f << string(56, '-') << "\n";
    for (int i = 0; i < jmlTransaksi; i++)
        f << left << setw(4)  << i+1
                  << setw(6)  << transaksi[i][0]
                  << setw(5)  << transaksi[i][1]
                  << setw(12) << ("Rp"+to_string(transaksi[i][2]))
                  << setw(12) << ("Rp"+to_string(transaksi[i][3]))
                  << "Rp" << transaksi[i][4] << "\n";
    f << string(56, '-') << "\n";
    f << "  TOTAL PENDAPATAN : Rp" << totalBelanja(transaksi, jmlTransaksi) << "\n";
    f << string(56, '=') << "\n";
    f.close();
    cout << "  [+] Tersimpan ke transaksi.txt\n";
}

// TAMPIL HEADER & MENU UTAMA
void tampilHeader() {
    cout << "\n";
    garis('*', 52);
    cout << "*" << setw(50) << left << "        ~~~  WARUNG MAKANAN JADUDUL  ~~~" << "*\n";
    cout << "*" << setw(50) << left << "      Klepon | Cenil | Lupis | Getuk | Wajik" << "*\n";
    garis('*', 52);
}

void tampilDaftar() {
    cout << "\n";
    garis('=', 52);
    cout << "  " << left << setw(4) << "No"
                         << setw(18) << "Nama"
                         << setw(14) << "Harga"
                         << "Stok\n";
    garis('-', 52);
    for (int i = 0; i < jumlah; i++)
        cout << "  " << left << setw(4)  << i+1
                             << setw(18) << daftar[i].nama
                             << left << "Rp" << setw(12) << daftar[i].harga
                             << daftar[i].stok << "\n";
    garis('=', 52);
}

// TAMPIL STRUK BELANJA
void tampilStruk(int idx, int qty, int total, int bayar, int kembalian, string metode) {
    cout << "\n";
    garis('=', 52);
    cout << setw(30) << right << "*** STRUK BELANJANYA KAKAAK ***\n";
    garis('-', 52);
    cout << "  Item     : " << daftar[idx].nama << "\n";
    cout << "  Qty      : " << qty << " pcs\n";
    cout << "  Harga    : Rp" << daftar[idx].harga << " / pcs\n";
    garis('-', 52);
    cout << "  Total    : Rp" << total << "\n";
    cout << "  Metode   : " << metode << "\n";
    cout << "  Bayar    : Rp" << bayar << "\n";
    cout << "  Kembalian: Rp" << kembalian << "\n";
    garis('=', 52);
    cout << setw(34) << right << "Terima kasih sudah belanjaaaaaaaaaaaaaaaaaaa!\n";
    garis('=', 52);
}

// TAMBAH MAKANAN BARU
void tambahMakanan() {
    if (jumlah >= MAX) { cout << "  [!] Data penuh!\n"; return; }
    Makanan baru; baru.id = jumlah + 1;
    garis('-', 52);
    cout << "  Nama makanan : "; cin >> baru.nama;
    cout << "  Harga        : Rp"; cin >> baru.harga;
    cout << "  Stok         : "; cin >> baru.stok;
    daftar[jumlah++] = baru;
    simpanFile();
    garis('-', 52);
    cout << "  [+] " << baru.nama << " berhasil ditambahkan!\n";
}

// PROSES BELI + PEMBAYARAN
void beli() {
    string nama; int qty;
    garis('-', 52);
    cout << "  Nama makanan : "; cin >> nama;
    int idx = cariMakanan(nama);   // [SEARCHING]
    if (idx == -1) { cout << "  [!] Makanan ga ada di stok kami ya!\n"; return; }
    cout << "  Jumlah beli  : "; cin >> qty;
    if (qty > daftar[idx].stok) { cout << "  [!] Stoknya ga ada! tersisa: " << daftar[idx].stok << "\n"; return; }

    int total = qty * daftar[idx].harga;
    cout << "\n  Total Bayar  : Rp" << total << "\n";
    garis('-', 52);
    cout << "  Metode Bayar :\n";
    cout << "    [ 1 ] Cash\n";
    cout << "    [ 2 ] Transfer\n";
    cout << "  Pilih        : "; 
    int met; cin >> met;

    int bayar = 0, kembalian = 0;
    string metode;
    if (met == 1) {
        metode = "Cash";
        do {
            cout << "  Uang bayar   : Rp"; cin >> bayar;
            if (bayar < total)
                cout << "  [!] UANG NYA KURANG KAKAAAK Rp" << total - bayar << ",coba masukkan lagi yaa!\n";
        } while (bayar < total);
        kembalian = bayar - total;
    } else {
        metode = "Transfer";
        bayar = total; kembalian = 0;
        cout << "  [+] Transfer Rp" << total << " diterima.\n";
    }

    updateStok(&daftar[idx], qty); // [POINTER]

    // [ARRAY MULTI DIMENSI]
    transaksi[jmlTransaksi][0] = daftar[idx].id;
    transaksi[jmlTransaksi][1] = qty;
    transaksi[jmlTransaksi][2] = total;
    transaksi[jmlTransaksi][3] = bayar;
    transaksi[jmlTransaksi][4] = kembalian;
    jmlTransaksi++;

    simpanFile();
    simpanTransaksi(); // [FILE]
    tampilStruk(idx, qty, total, bayar, kembalian, metode);
}

// INT MAINNYA - TAMPIL MENU & PROSES PILIHAN USER
int main() {
    // [ARRAY STRUCT] Data awal
    daftar[0]={1,"Klepon",2000,20}; daftar[1]={2,"Cenil",1500,15};
    daftar[2]={3,"Lupis",2500,10};  daftar[3]={4,"Getuk",3000,12};
    daftar[4]={5,"Wajik",3500,8};
    jumlah = 5;
    simpanFile(); // [FILE]

    int pilih;
    do {
        tampilHeader();
        tampilDaftar();
        cout << "\n  [ 1 ] Beli Makanan\n";
        cout << "  [ 2 ] Tambah Menu\n";
        cout << "  [ 3 ] Urutkan Harga\n";
        cout << "  [ 4 ] Cari Makanan\n";
        cout << "  [ 5 ] Total Pendapatan\n";
        cout << "  [ 6 ] Keluar\n";
        garis('-', 52);
        cout << "  Pilihan : "; cin >> pilih;

        switch (pilih) {
            case 1: beli(); break;
            case 2: tambahMakanan(); break;
            case 3: // [SORTING + FILE]
                sortByHarga(); simpanFile();
                cout << "  [+] Diurutkan dari harga termurah!\n"; break;
            case 4: {
                string n;
                garis('-', 52);
                cout << "  Cari : "; cin >> n;
                int i = cariMakanan(n); // [SEARCHING]
                garis('-', 52);
                if (i != -1)
                    cout << "  [+] " << left << setw(15) << daftar[i].nama
                         << "Rp" << setw(8) << daftar[i].harga
                         << "Stok: " << daftar[i].stok << "\n";
                else cout << "  [!] Makanan ga ada!.\n";
                break;
            }
            case 5: // [REKURSIF]
                garis('=', 52);
                cout << "  Total Pendapatan : Rp"
                     << totalBelanja(transaksi, jmlTransaksi) << "\n";
                garis('=', 52);
                simpanTransaksi(); break;
            case 0:
                garis('*', 52);
                cout << "*" << setw(44) << right << "Sampai jumpa lagi,,bye byeee!" << "      *\n";
                garis('*', 52);
                break;
        }
    } while (pilih != 6);

    simpanFile();
    simpanTransaksi(); // [FILE]
    return 0;
}
