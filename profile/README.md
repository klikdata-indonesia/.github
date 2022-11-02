# klikcare-services



## Cara Running Development

* Linux
```bash
export SPRING_DATASOURCE_URL=jdbc:mysql//{ip_database:port}/{nama_database}
export SPRING_DATASOURCE_USERNAME={user_db}
export SPRING_DATASOURCE_PASSWORD={password_db}
mvn clean spring-boot:run
```

## Data Model
```plantuml
@startuml

entity Pasien {
    Sring id
    Sring noKk
    Sring nik
    Sring noMr
    Sring noRmLama
    Sring nama
    Sring jk
    Sring tglLahir
    Sring tmpLahir
    Sring golDarah
    Sring email
    Sring noHp
    Long kdProvinsi
    Long kdKabupaten
    Long kdKecamatan
    Long kdDesa
    Sring alamatLengkap
    Boolean stsAlamat
    Long kd_provinsi_1
    Long kd_kota_kab_1
    Long kd_kec_1
    Long kd_desa_1
    Sring alamat_lengkap_1
    Long id_pekerjaan
    Long id_agama
    Long id_pendidikan
    Boolean sts_kawin
    Sring nama_ibu
    LocalDate insert_at
    LocalDate updated_at
    LocalDate delete_at
}

entity Provinsi {
    Long id
    String nama
}

entity Kabupaten {
    Long id
    Long id_prov
    String nama
}

entity Kecamatan {
    Long id
    Long id_kab
    String nama
}

entity Kelurahan {
    Long id
    Long id_kec
    String nama
}

entity Agama {
    Long id
    String nama
}

entity Pendidikan {
    Long id
    String nama
    String singkatan
}

Pasien -> Agama
Pasien -> Pendidikan
Pasien --|> Provinsi
Pasien --|> Kabupaten
Pasien --|> Kecamatan
Pasien --|> Kelurahan
Provinsi <- Kabupaten
Kabupaten <- Kecamatan
Kecamatan <- Kelurahan


entity Asuransi{
Loong id
String nama_asuransi
String singkatan
}

entity Set_Margin {
    Loong id
    Loong id_asuransi
    Varchar uuid_faskes
    String margin_jual
    Boolean sts_bayar
}

Set_Margin -> Asuransi

entity Asuransi_Pasien{
Loong id
Loong 
Loong id_asuransi
Loong id_pasien
String prb
String jnsPeserta
String Kelas
String jnsKelas
}

Asuransi_Pasien -> Pasien
Asuransi_Pasien -> Asuransi

entity Pendaftaran{
    Loong uuid_faskes
Loong no_register
LocalDate tgl_daftar
String kerabat_nama
String Stkerabat_hubungan
String kerabat_hp
no_tiket
no_urut
id_pasien
umur_thn
umur_bln
umur_hri
sts_kunjungan_pasien
sts_kondisi_masuk
id_caradaftar
id_asuransi_dipakai
id_dokter
jam_praktek
keluhan
keterangan
is_katarak
sts_selesai
tgl_pulang
jam_pulang
iscanceled
ket_cancel
user_created
date_created
user_modified
date_modified
}



entity Faskes{
    Loong uuid
    String kdFaskes
    String kdKemkes
    String kdDikes
    String nama_faskes
    Long kdProvinsi
    Long kdKabupaten
    Long kdKecamatan
    Long kdDesa
    Sring alamatLengkap
    String nohp_faskes
    String jenis_faskes
    String user_name_pcare
    String pass_pcare
    String cons_id
    String secret_key
    String user_key
    Boolean enable_pcare
    Boolean pcare_mode
    Boolean post_pendaftaran_pcare   

}

Faskes -> Set_margin
Faskes --|> Provinsi
Faskes --|> Kabupaten
Faskes --|> Kecamatan
Faskes --|> Kelurahan

entity medical_record{
Loong no_register
LocalDate tgl_daftar
LocalDate tgl_masuk
Bolean sts_pencatatan
Loong id_pasien
Loong id_asuransi
Loong id_ruangan
Loong id_dokter
Loong id_kesadaran
String darah_sistol
String darah_diastol
String denyut_nadi
String pernafasan
String badan_suhu
String badan_berat
String badan_tinggi
String anamnese
String pemeriksaan_fisik
String skrining_gizi
String skrining_gizi_ket
String skrining_jatuh
String skrining_jatuh_ket
String skrining_nyeri
String skrining_nyeri_ket
String skala_nyeri
Stringlokasi_nyeri
Loong id_carakeluar
LocalDate tgl_keluar
ket_carakeluar
}

medical_record -> Pendaftaran
Pendaftaran -> Pasien

entity User_Login {
Loong id
String username
String password
Loong id_faskes


}


entity User_Roll {
    Loong id
    String nama_roll

    
}

entity User_Menu{
    Loong id_user


}

```

@enduml

# ICON TOP

## DISPLAY ANTRIAN
## BUKU PANDUAN
## 
# MENU UTAMA
 ## PENDAFTARAN
  ### Data Pasien
  ### Pendaftaran
  ### Pasien Hari Ini
  ### Jadwal Prakter
  ### 

 ## PELAYANAN
 ### Data Pasien Berobat
 ### Persuratan
### Riwayat Pasien
### Report Pelayanan

 ## FARMASI 
### Penjualan
### Penjualan Langsung
### Cetak Etiket
### Pemakaian BHP
### Mutasi Stok
### Adjustment Stok
### Purchase Order
### Pembelian Dari PO
### Pembelian Langsung
### Pembayaran Hutang
### Report Apotik
### Report Stock

 ## KASIR
 ## KEUANGAN
 ## LAPORAN
 ## MASTER
## HELPDESK


# MENU ICON
### display antrian dokter



## Pcare-Api

### 1. Create Signature
### 2. Decrypt
### 3. Diagnosa

#### URL: _{Base URL}_/_{Service Name}_/diagnosa/**{Parameter 1}**/**{Parameter 2}**/**{Parameter 3}**

Fungsi : Get Data Diagnosa

Method :  **GET**

Format :  **Json**

Content-Type:  **application/json; charset=utf-8**

Parameter 1 :  **Kode atau nama diagnosa**

Parameter 2 :  **Row data awal yang akan ditampilkan**

Parameter 3 :  **Limit jumlah data yang akan ditampilkan**

```json
{
  "response": {
    "count": 33,
    "list": [
      {
        "kdDiag": "A001",
        "nmDiag": "Cholera due to vibrio cholerae 01, biovar eltor",
        "nonSpesialis": false
      },
      {
        "kdDiag": "B001",
        "nmDiag": "Herpesviral vesicular dermatitis",
        "nonSpesialis": true
      }
    ]
  },
  "metaData": {
    "message": "OK",
    "code": 200
  }
}
```

## Dokter
### Get Dokter
### _{Base URL}_/_{Service Name}_/dokter/**{Parameter 1}**/**{Parameter 2}**

Fungsi : Get Data Dokter

Method :  **GET**

Format :  **Json**

Content-Type:  **application/json; charset=utf-8**

Parameter 1 :  **Row data awal yang akan ditampilkan**

Parameter 2 :  **Limit jumlah data yang akan ditampilkan**

```json
{
  "response": {
    "count": 19,
    "list": [
      {
        "kdDokter": "001",
        "nmDokter": "dr..."
      },
      {
        "kdDokter": "002",
        "nmDokter": "dr. Muna Hasnita Harahap"
      },
      {
        "kdDokter": "003",
        "nmDokter": "dr. fauzi"
      }
    ]
  },
  "metaData": {
    "message": "OK",
    "code": 200
  }
}
```
Kelompok
Kesadaran
Kunjungan
MCU
Obat
Pendaftaran
## Peserta
### catatan Bridging ini auto fill ketika nik atau no bpjs sudah di isikan, tombol get data di samping form isian nik, form yang bisa di get yaitu

#### 1. noKartu
#### 2. nama

#### 3. sex
#### 4. tglLahir


#### [Get Peserta by Jenis Kartu](https://dvlp.bpjs-kesehatan.go.id:8888/trust-mark/#collapsegetpeserta2)

### _{Base URL}_/_{Service Name}_/peserta/**{Parameter 1}**/**{Parameter 2}**

Fungsi : Get Data Peserta

Method :  **GET**

Format :  **Json**

Content-Type:  **application/json; charset=utf-8**

Parameter 1 :  **Jenis Kartu: nik / noka**

Parameter 2 :  **Nomor NIK atau kartu peserta sesuai dengan Parameter 1**

```json                          
{
  "response": {
    "noKartu": "0001261832477",
    "nama": "TRI ARNI",
    "hubunganKeluarga": "Istri",
    "sex": "P",
    "tglLahir": "29-09-1965",
    "tglMulaiAktif": "09-01-2014",
    "tglAkhirBerlaku": "31-12-2050",
    "kdProviderPst": {
      "kdProvider": "09020107",
      "nmProvider": "KEL. MANGGARAI SELATAN"
    },
    "kdProviderGigi": {
      "kdProvider": null,
      "nmProvider": null
    },
    "jnsKelas": {
      "kode": "3",
      "nama": "KELAS III"
    },
    "jnsPeserta": {
      "kode": "22",
      "nama": "PBI (APBD)"
    },
    "golDarah": "0",
    "noHP": "083876592594",
    "noKTP": "3174016909650001",
    "aktif": true,
    "ketAktif": "AKTIF",
    "asuransi": {
      "kdAsuransi": null,
      "nmAsuransi": null,
      "noAsuransi": null
    },
				"tunggakan": 0
  },
  "metaData": {
    "message": "OK",
    "code": 200
  }
}
```

Poli
Provider
Spesialis
Status Pulang
Tindakan
