# User Flows and Multi-Step Workflows
## Sistem Internal PDLN PNJ

**Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Audit Purpose:** Comprehensive mapping of user journeys, form steps, review loops, and administrative approval mechanisms.

---

### Flow 1: End-to-End Civitas PDLN Pre-Submission Journey

This workflow describes the journey of an applicant (Mahasiswa or Dosen) planning travel abroad, selecting their route, configuring partnership & funding details, uploading required documents, and monitoring application progress.

```mermaid
sequenceDiagram
    autonumber
    actor User as Pemohon (Mahasiswa / Dosen)
    participant Dash as P01: Dashboard Civitas
    participant DestModal as M03: Destination Picker
    participant Wizard as P02: 3-Step Wizard
    participant Store as Local Storage / Store State
    participant Toast as Toast Notification

    User->>Dash: Mengakses Portal Beranda
    Dash-->>User: Tampilkan KAI Access Route Card & Dossier Tiket
    opt Ganti Destinasi
        User->>Dash: Klik Box Negara & Mitra Tujuan (#btn-open-dest-sheet)
        Dash->>DestModal: Buka Modal Pilihan Destinasi
        User->>DestModal: Pilih Kampus Mitra (misal: Tokyo Tech, Jepang)
        DestModal->>Dash: Perbarui Rute & Tampilkan Toast
    end
    opt Atur Jadwal
        User->>Dash: Mengubah Tanggal Berangkat & Pulang
        Dash-->>User: Live update durasi dinas ("XX Hari Dinas")
    end
    User->>Dash: Klik "Buat Draf Pengajuan"
    Dash->>Wizard: Transisi ke Wizard Step 1: Konfirmasi Profil & Rute
    Note over Wizard: Data Nama, NIM/NIP ditarik otomatis dari SSO
    User->>Wizard: Verifikasi data rute & Klik "Lanjutkan ➔"
    Wizard->>Wizard: Validasi & Pindah ke Step 2: Kerjasama & Pembiayaan
    User->>Wizard: Pilih Radio MoU (Ya/Tidak), Dokumen MoU, Dropdown Sumber Dana & Nama Sponsor
    User->>Wizard: Klik "Lanjutkan ➔"
    Wizard->>Wizard: Pindah ke Step 3: Unggah Berkas & Tiket
    User->>Wizard: Periksa/Ganti Scan Paspor, LoA Mitra, & SPTJM Bermaterai
    User->>Wizard: Centang Pernyataan Keabsahan Dokumen
    User->>Wizard: Klik "Kirim Pengajuan"
    Wizard->>Store: createApplication() -> Simpan ke Database
    Store->>Toast: Tampilkan Toast Sukses ("Pengajuan PDLN berhasil didaftarkan!")
    Wizard->>Dash: Kembali ke Dashboard (Menampilkan Tiket Pengajuan Baru)
```

---

### Flow 2: Document Revision Request & Resubmission Loop

When KUI finds defects in submitted documents (e.g., passport scan is blurry, expired, or LoA is incomplete), a structured revision feedback loop occurs.

```mermaid
graph TD
    A[Pengajuan Berstatus kui_review] --> B[Operator KUI Memeriksa Berkas di Ruang Tinjau M05]
    B -->|Ada Dokumen Tidak Layak| C[Operator Klik 'Minta Revisi Berkas']
    C --> D[Modal M06: Centang Dokumen Bermasalah misal: Paspor]
    D --> E[Operator Mengisi Catatan Instruksi Revisi Wajib]
    E --> F[Klik 'Kirim Permintaan Revisi']
    F --> G[Status Berubah: revision_required]
    G --> H[Pemohon Membuka Dashboard P01]
    H --> I[Tiket Dossier Berwarna Amber dengan Callout Alert Revisi]
    I --> J[Pemohon Membaca Catatan KUI & Klik 'Unggah Perbaikan Paspor Sekarang']
    J --> K[Modal M04: Perbarui Dokumen Revisi Terbuka]
    K --> L[Pemohon Mengunggah Berkas Baru PDF/JPG]
    L --> M[Pemohon Klik 'Kirim Perbaikan ke KUI']
    M --> N[Status Berubah Kembali: kui_review]
    N --> O[Toast Notifikasi Hijau: 'Dokumen perbaikan telah dikirimkan ke KUI']
    O --> A
```

---

### Flow 3: KUI Operator Review, Confidential Notes & Official Approval

This workflow represents the administrative pre-clearance process handled by KUI PNJ operators before submitting records to the State Secretariat (Kemensetneg).

```mermaid
graph TD
    Start[Operator KUI Login via ?page=admin] --> DashAdmin[P04: Dashboard Kontrol Admin KUI]
    DashAdmin --> Filter[Gunakan Filter Toolbar: Review / Revisi / Siap Setneg atau Kolom Pencarian]
    Filter --> Table[Pilih Pengajuan dari Tabel Database]
    Table --> OpenReview[Klik 'Tinjau Berkas' -> Buka Split Modal M05]
    
    subgraph Split Modal M05
        OpenReview --> DocInspect[Periksa Berkas: Paspor, LoA, SPTJM, Bukti Dana via tombol Pratinjau]
        DocInspect --> NoteSection[Panel Catatan Rahasia Internal KUI]
        NoteSection --> AddNote[Operator Menulis Catatan Koordinasi Tertutup -> Klik Simpan]
        AddNote --> NoteSaved[Catatan Tersimpan dengan Nama & Timestamp Operator]
        
        DocInspect --> Decision{Evaluasi Kelayakan Berkas}
        Decision -->|Berkas Belum Sesuai| ReqRev[Klik 'Minta Revisi Berkas' -> Masuk Alur Flow 2]
        Decision -->|Seluruh Berkas Lengkap & Sah| ApproveBtn[Klik 'Setujui (Siap PDLN Resmi)']
    end
    
    ApproveBtn --> ConfirmDialog[Dialog Konfirmasi Peramban: 'Setujui berkas sebagai SIAP PDLN RESMI?']
    ConfirmDialog -->|Konfirmasi OK| SetReady[Status Berubah: ready_for_official_pdln]
    SetReady --> AuditLog[Tercatat dalam Riwayat Audit Trail Sistem]
    AuditLog --> ToastApprove[Toast: 'Pengajuan disetujui! Berkas siap untuk proses resmi Kemensetneg.']
    ToastApprove --> ExportReady[Data Siap Diekspor ke Format Spreadsheet / CSV untuk Kemensetneg]
```

---

### Flow 4: Role-Based Access Control and Session Navigation

The application isolates views based on query parameters and user session roles:

```mermaid
flowchart TD
    Req[Pengguna Membuka URL Aplikasi] --> CheckRoute{Apakah URL mengandung ?page=admin?}
    
    CheckRoute -->|Tidak - Portal Standar| CheckUser1{Apakah ada sesi pengguna?}
    CheckUser1 -->|Tidak| ShowAuthCivitas[Tampilkan P05: Login Civitas Mahasiswa / Dosen]
    CheckUser1 -->|Ya, role: mahasiswa / dosen| ShowPortalCivitas[Tampilkan P01: Dashboard Civitas + Navbar + Chatbot + Mobile Bar]
    CheckUser1 -->|Ya, role: kui_admin| ForceAdminRedirect[Otomatis redirect ke ?page=admin]
    
    CheckRoute -->|Ya - Admin Route| CheckUser2{Apakah ada sesi pengguna?}
    CheckUser2 -->|Tidak| ShowAuthAdmin[Tampilkan P05: Login Khusus Admin KUI]
    CheckUser2 -->|Ya, role: kui_admin| ShowPortalAdmin[Tampilkan P04: Portal Operator KUI + Sidebar 270px, Navbar & Chatbot Disembunyikan]
    CheckUser2 -->|Ya, role: mahasiswa / dosen| AutoSwitchAdmin[Otomatis ganti sesi ke kui-1 untuk mode pengujian]
    
    ShowAuthCivitas --> QuickDemo1[Pilih Akun Demo: Mahasiswa / Dosen] --> ShowPortalCivitas
    ShowAuthAdmin --> QuickDemo2[Pilih Akun Demo: Operator KUI] --> ShowPortalAdmin
```

---

### Form Field and Validation Rules Summary

#### P02 Form Wizard:
- **Step 1:** All profile and route values are read-only and inherited directly from active session data and route card configuration.
- **Step 2:**
  - `wiz-coop` (Radio): Mandatory choice between MoU vs Non-MoU.
  - `wiz-coop-name` (Text): Required when MoU is selected.
  - `wiz-funding` (Select): Default `sponsor_eksternal`, options: `sponsor_eksternal`, `pnj`, `pribadi`.
  - `wiz-sponsor-name` (Text): Name of funding institution/scholarship.
- **Step 3:**
  - `name-paspor`, `name-loa`, `name-sptjm`: Interactive mock file inputs accepting `.pdf, .jpg, .png` with file size validation (< 5MB).
  - `wiz-consent` (Checkbox): Mandatory legal declaration checkbox.

#### P03 Academic Profile Form:
- Non-editable fields (Institutional source): `NIM / NIP`, `Nama Lengkap`, `Jurusan`, `Program Studi`.
- Editable fields:
  - `Email Kampus`: Disabled (read-only).
  - `No. Telepon / WhatsApp`: Required (`tel`, Indonesian number formatting).
  - `Nomor Paspor`: Optional format (Letter followed by 7-8 digits).
  - `Masa Berlaku Paspor`: Date input (must be at least 6 months after return date per KUI policy).
  - `Nama Kontak Darurat`: Text string.
  - `No. HP Kontak Darurat`: Tel input.

#### M06 KUI Revision Request Sheet:
- Checkboxes: Minimum 1 document must be selected (`paspor`, `surat_undangan`, `sptjm`). Alerts if none selected.
- Instruction textarea: Mandatory non-empty string. Alerts with native prompt if submitted empty.
