package Pemlan;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Penumpang {
    private String nama;

    public Penumpang(String nama) {
        this.nama = nama;
    }

    public String getNama() {
        return nama;
    }
}

class Driver {
    private String nama;

    public Driver(String nama) {
        this.nama = nama;
    }

    public String getNama() {
        return nama;
    }
}

class Kendaraan {
    public String platNomor;
    public int maxPenumpang;
    public List<Penumpang> daftarPenumpang;
    public Driver driver;

    public Kendaraan(String pn, int max) {
        this.platNomor = pn;
        this.maxPenumpang = max;
        this.daftarPenumpang = new ArrayList<>();
    }

    public void cekPenumpang() {
        System.out.println("Penumpang saat ini: " + this.daftarPenumpang.size());
    }

    public void penumpangNaik() {
        System.out.println("Ada penumpang naik.");
        if (this.daftarPenumpang.size() >= this.maxPenumpang) {
            System.out.println("Maaf, penumpang melebihi kapasitas.");
        } else {
            this.daftarPenumpang.add(new Penumpang("Penumpang"));
            System.out.println("Penumpang berhasil naik.");
        }
        cekPenumpang();
    }

    public void penumpangNaik(String namaPenumpang) {
        System.out.println("Penumpang " + namaPenumpang + " naik.");
        if (this.daftarPenumpang.size() >= this.maxPenumpang) {
            System.out.println("Maaf, penumpang melebihi kapasitas.");
        } else {
            this.daftarPenumpang.add(new Penumpang(namaPenumpang));
            System.out.println("Penumpang berhasil naik.");
        }
        cekPenumpang();
    }

    public void turunPenumpang() {
        if (this.daftarPenumpang.isEmpty()) {
            System.out.println("Tidak ada penumpang yang bisa turun.");
        } else {
            this.daftarPenumpang.remove(this.daftarPenumpang.size() - 1);
            System.out.println("Penumpang berhasil turun.");
        }
        cekPenumpang();
    }

    public void setDriver(Driver driver) {
        this.driver = driver;
    }

    public void infoDriver() {
        if (driver != null) {
            System.out.println("Driver: " + driver.getNama());
        } else {
            System.out.println("Belum ada driver.");
        }
    }
}

public class LK02 {
    public static void main(String[] args) throws Exception {
        int pilihanKendaraan = 0;
        Scanner scanner = new Scanner(System.in);

        System.out.println("Pilih jenis kendaraan:");
        System.out.println("1. Bus");
        System.out.println("2. Truk");
        System.out.print("Masukkan pilihan : ");
        pilihanKendaraan = scanner.nextInt();

        Kendaraan kendaraan = null;

        switch (pilihanKendaraan) {
            case 1:
                kendaraan = new Bus("B 1234 AB", 25);
                break;
            case 2:
                kendaraan = new Truk("T 5678 CD", 40);
                break;
            default:
                System.out.println("Pilihan tidak valid.");
                return;
        }

        int pilihan = 0;
        while (pilihan != 5) {

            System.out.println("\nMenu:");
            System.out.println("1. Penumpang Naik (tanpa nama) : ");
            System.out.println("2. Penumpang Naik (dengan nama) : ");
            System.out.println("3. Penumpang Turun");
            System.out.println("4. Cek Jumlah Penumpang");
            System.out.println("5. Nama Driver");
            System.out.println("6. Keluar");

            System.out.print("Pilih menu (masukkan angka): ");
            pilihan = scanner.nextInt();

            switch (pilihan) {
                case 1:
                    kendaraan.penumpangNaik();
                    break;
                case 2:
                    System.out.println("Masukkan nama penumpang:");
                    scanner.nextLine(); // Consume newline character
                    String namaPenumpang = scanner.nextLine();
                    kendaraan.penumpangNaik(namaPenumpang);
                    break;
                case 3:
                    kendaraan.turunPenumpang();
                    break;
                case 4:
                    kendaraan.cekPenumpang();
                    break;
                case 5:
                    System.out.println("Masukkan nama driver:");
                    scanner.nextLine(); // Consume newline character
                    String namaDriver = scanner.nextLine();
                    kendaraan.setDriver(new Driver(namaDriver));
                    kendaraan.infoDriver();
                    break;
                case 6:
                    System.out.println("Terima kasih. Program berhenti.");
                    break;
                default:
                    System.out.println("Pilihan tidak valid. Silakan pilih antara 1-6.");
            }
        }
        scanner.close();
    }
}

class Bus extends Kendaraan {
    int jumlahKursi;

    public Bus(String pn, int jumlahKursi) {
        super(pn, jumlahKursi);
        this.jumlahKursi = jumlahKursi;
    }

    public void berhentiDiTerminal() {
        System.out.println("Bus berhenti di terminal.");
    }
}

class Truk extends Kendaraan {
    double tonase;

    public Truk(String pn, int max) {
        super(pn, max);
    }
    public void kirimBarang() {
        System.out.println("Truk mengirim barang.");
    }
}
