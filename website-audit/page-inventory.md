# Page and Route Inventory
## Sistem Internal PDLN PNJ (Politeknik Negeri Jakarta)

**Audit Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Inspection Date:** 2026-10-29  
**Repository Source:** [https://github.com/h3rwthme/iniweb](https://github.com/h3rwthme/iniweb)  
**System Purpose:** Portal administrasi pra-pengajuan (*pre-submission*) dan verifikasi berkas Perjalanan Dinas Luar Negeri (PDLN) civitas akademika Politeknik Negeri Jakarta (PNJ) sebelum diteruskan ke kementerian (Kemensetneg/Kemlu/Kemdikbudristek).

---

### Master Page Inventory Table

| Page ID | Page Name | Route / URL | Access Method & Roles | Main Components | Inspection Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **P01** | **Applicant Dashboard (Portal Civitas)** | `/` or `?` | Public / SSO Auth (Mahasiswa / Dosen default session: `mhs-1`) | Navbar, Brand Logo, Profile Pill, KAI Access Travel Route Card, Boarding Pass Dossier Ticket, Timeline Tracker, Completeness Banner, History Table, Chatbot FAB, Bottom Bar (mobile) | **Confirmed & Visually Verified** |
| **P02** | **Application Form Wizard (3-Step Submission)** | Subview `#applicant-view-wizard` | Click "Buat Draf Pengajuan" on Route Card or Bottom Bar "Pengajuan" | 3-Step Wizard Indicator, Step 1 (Auto-filled Profile & Route), Step 2 (MoU Radio & Funding Fields), Step 3 (Mock Upload Dropzones & Legal Checkbox), Prev/Next Nav Controls | **Confirmed & Visually Verified** |
| **P03** | **Academic Profile Detail & Edit View** | Subview `#applicant-view-profile` | Click "Lengkapi Data" / "Lihat Profil" / Profile Flyout "Edit Profil" | Back Button, Verified PNJ Institutional Grid (4 badges), Editable Fields (Phone, Passport, Passport Expiry, Emergency Contact), Save Button | **Confirmed & Visually Verified** |
| **P04** | **Dedicated KUI Operator Portal** | `?page=admin` | Admin Auth (`kui-1` / `kui_admin` session) | 270px Fixed Teal Sidebar, Topbar with live timestamp & export, Hero Summary Banner, 5-Metric Stats Grid, Disposition Timeline, Top Countries Ranking, Filterable Applications Table | **Confirmed & Visually Verified** |
| **P05** | **Authentication Portal (SSO & Admin Console)** | `#auth-portal-root` (when `sessionUserId: null`) | Log out via Navbar / Flyout / Admin Sidebar | Split Visual Hero (`hero_travel.jpg`), Quick Login Demo Account Chips (`mhs-1`, `dosen-1`, `kui-1`), Identifier/Password Form, Route Switcher Link | **Confirmed & Visually Verified** |

---

### Overlay, Sheet, and Modal Inventory

| Modal ID | Component Name | Trigger Control | Parent View | Key Visual Elements | Verification |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **M01** | **Profile Drawer / Flyout Modal** | Click `#btn-nav-user-profile` or Mobile Nav "Profil" | P01, P02, P03 | Avatar chip, verified institution badge, 7 metadata rows, "Edit Profil" button, "Keluar Akun" button | **Confirmed & Visually Verified** |
| **M02** | **Visual Guide & Infographics Modal** | Click `#btn-open-visual-guide` or Admin Sidebar "Panduan Berkas" | P01, P04 | 4-Step PDLN Workflow Infographic (`guide_workflow.jpg`), 4 Mandatory Documents Checklist (`guide_docs.jpg`), Layperson instructions | **Confirmed & Visually Verified** |
| **M03** | **Destination & Host Institution Picker** | Click Destination Card (`#btn-open-dest-sheet`) | P01 | Modal list of 6 partner universities (SeoulTech, Tokyo Tech, Nanyang Poly, Universiti Malaya, RMIT, TUM) with badges | **Confirmed & Visually Verified** |
| **M04** | **Perbarui Dokumen Revisi Sheet** | Click button "Unggah Perbaikan Paspor Sekarang" (`.btn-fix-revision`) | P01 (Dossier Ticket) | KUI rejection note callout, dashed dropzone with upload simulator, submit revision button | **Confirmed & Visually Verified** |
| **M05** | **KUI Split-Screen Application Review Modal** | Click "Tinjau Berkas" (`.btn-open-review-modal`) | P04 (Admin Table) | Left: Route info & document checklist with status badges & previews; Right: Approval decision actions & Strictly Confidential Internal Notes box | **Confirmed & Visually Verified** |
| **M06** | **KUI Revision Request Sheet** | Click "Minta Revisi Berkas" (`.btn-modal-req-rev`) | M05 (Review Modal) | Multi-select checkboxes for document items needing revision, mandatory instructions textarea, send button | **Confirmed & Visually Verified** |
| **M07** | **Hybrid Chatbot Assistant Panel** | Click Floating Action Button (`#bot-toggle-btn`) | P01, P02, P03 | Bot header, chat feed, typing indicator, 4 quick query chips (`Status Saya`, `Syarat Paspor`, `Dokumen Wajib`, `Alur Revisi`), input field | **Confirmed & Visually Verified** |

---

## Detailed Page Specifications

### P01 — Applicant Dashboard (Portal Civitas)
- **URL Route:** `https://h3rwthme.github.io/iniweb/` (default query `?`)
- **Primary Layout:** Single-page container (`max-width: 1180px; padding: 0 20px;`) with sticky top navbar and responsive footer.
- **Header & Navigation:**
  - Institutional Brand: Official PNJ Crest logo (38x38px), Title `Internal PDLN`, Subtitle `Kantor Urusan Internasional PNJ`.
  - Nav Actions:
    - User Mini Pill (`.user-mini-btn`): Avatar initials badge (`AP`), Name `Andi Pratama`, Role label `Mahasiswa Aktif`, chevron icon.
    - Direct Logout Button (`#btn-nav-logout`): Secondary outline icon button with exit SVG.
- **Section 1: Layperson Visual Guide Banner:**
  - Header: `Portal Pengajuan PDLN` (18px, bold 800) + Subtitle.
  - Action: Button "Panduan Berkas & Alur PDLN" (`#btn-open-visual-guide`) in soft cyan theme (`#f0fbfc`, border `#bfe7ea`, text `#008c95`).
- **Section 2: KAI Access-Inspired Travel Route Card (`.kai-route-card`):**
  - Card style: White background, subtle border `#e4e4e7`, rounded 14px, shadow-sm.
  - Header: Plane vector icon + title `Rencana Perjalanan Dinas Luar Negeri` + badge `Pra-Pengajuan KUI PNJ`.
  - Segmented Activity Selector: 4 pill buttons (`Student Exchange` [active], `Konferensi Ilmiah`, `Riset Kolaborasi`, `Pelatihan Vokasi`).
  - Origin <-> Destination Grid (`.kai-grid`):
    - Left Box (Kampus Asal): Building icon, label, City `PNJ Depok`, Host `Politeknik Negeri Jakarta`.
    - Swap Button: Circular icon button (`#btn-swap-route`) with swap SVG.
    - Right Box (Negara & Mitra Tujuan): MapPin icon, label, City `Seoul (Korea Selatan)`, Host `Seoul National University of Science and Technology`. Clickable trigger to open M03.
  - Date & Duration Bar (`.kai-date-grid`):
    - Tanggal Berangkat date picker (`2026-10-15`).
    - Tanggal Kepulangan date picker (`2027-02-28`).
    - Duration Badge: Clock icon + live calculated days (`136 Hari Dinas`).
  - Footer Action: Primary button "Buat Draf Pengajuan" (240px max width).
- **Section 3: Boarding Pass Dossier Ticket (`.dossier-ticket`):**
  - Visual styling: Flight ticket metaphor with decorative notch perforations (`.dossier-tear`).
  - Top Section: Dual-node flight route `PNJ DEPOK` ➔ `SEOUL / KOREA SELATAN`, status badge with pulsing dot (`Perlu Revisi`).
  - Metadata Grid: 4 columns (Nomor Registrasi: `PDLN-2026-09-001`, Pemohon: `Andi Pratama`, Lembaga Mitra: `SeoulTech`, Jadwal: `2026-10-15 s/d 2027-02-28`).
  - Status Tracker Timeline: 4 steps:
    1. Diajukan (Completed, green check)
    2. Perlu Revisi / Verifikasi KUI (Active state with warning amber dot)
    3. Persetujuan PNJ (Inactive step 3)
    4. SP Kemensetneg (Inactive step 4)
  - Revision Callout Alert (`.alert-revision-clean`): Alert circle icon, KUI reviewer note text, and action button "Unggah Perbaikan Paspor Sekarang".
  - Ticket Action: "Cetak Dossier PDLN" button (`window.print()`).
- **Section 4: Profile Completeness Strip:**
  - Card with user icon box, completeness title `Data Profil PNJ: 85% Lengkap`, description, and button "Lengkapi Data".
- **Section 5: Riwayat Pengajuan (Data Table):**
  - Columns: `ID & Tanggal`, `Tujuan & Lembaga`, `Kegiatan`, `Status`.
  - Table rows with bold IDs, timestamps, partner university, and colored status pill badges.
- **Section 6: Floating Chatbot Assistant & Mobile Bottom Navigation Bar.**
- **Screenshot Evidence:**
  - `screenshots/desktop/P01-dashboard-desktop-1440px.png`
  - `screenshots/desktop/P01-dashboard-desktop-scrolled.png`
  - `screenshots/tablet/P01-dashboard-tablet-768px.png`
  - `screenshots/mobile/P01-dashboard-mobile-390px.png`

---

### P02 — Application Form Wizard (Pengajuan PDLN)
- **URL Route:** Rendered inside `#applicant-portal-root` via DOM subview switch (`#applicant-view-wizard`).
- **Access Method:** Click "Buat Draf Pengajuan" on P01 route card or Mobile Nav "Pengajuan".
- **Layout:** Centered card container (`max-width: 820px;`).
- **Header Progress Indicator:**
  - Step counter badge: `1 / 3`, `2 / 3`, or `3 / 3`.
  - Dynamic step title:
    - Step 1: `Konfirmasi Profil & Rute`
    - Step 2: `Kerjasama & Pembiayaan`
    - Step 3: `Unggah Berkas & Tiket`
  - Action: "Batalkan" button returning to Dashboard.
- **Step 1: Data Pemohon & Rute:**
  - 4 verified information boxes automatically populated from SSO profile:
    - Nama Pemohon (`Andi Pratama` / badge `Profil`)
    - NIM / NIP (`20260001` / badge `Profil`)
    - Tujuan Dinas (`Seoul (Korea Selatan)`)
    - Lembaga Mitra (`Seoul National University of Science and Technology`)
- **Step 2: Aspek Kerjasama & Pendanaan:**
  - Radio button group: "Apakah perjalanan ini bagian dari MoU/MoA resmi PNJ?" (`Ya, terdapat MoU/MoA` vs `Bukan Kerjasama Resmi`).
  - Conditional box: "Nama Dokumen / Nomor MoU Mitra" input field (populated with `MoU PNJ - SeoulTech 2024-2029`).
  - Dropdown: "Sumber Pembiayaan" (`Sponsor / Beasiswa Eksternal`, `DIPA PNJ`, `Mandiri / Pribadi`).
  - Text input: "Nama Lembaga Pendukung / Sponsor" (`Global Korea Scholarship (GKS)`).
- **Step 3: Dokumen Persyaratan PDLN:**
  - Supported format note: `PDF / JPG (Maks. 5MB per berkas)`.
  - 3 mock upload dropzones:
    1. Scan Paspor RI (Aktif min. 6 bulan) + filename preview `Paspor_Aktif.pdf (1.2 MB)` + "Ganti" file input button.
    2. Surat Undangan Resmi / Letter of Acceptance (LoA) + filename preview `LoA_Mitra.pdf (2.4 MB)` + "Ganti" button.
    3. SPTJM Bermaterai Rp10.000 + filename preview `SPTJM_Bermaterai.pdf (850 KB)` + "Ganti" button.
  - Legal Consent Checkbox: Pre-checked statement of truth and compliance with PNJ & Kemensetneg regulations.
- **Wizard Footer Controls:**
  - Button "Sebelumnya" (disabled with 0.5 opacity on step 1).
  - Button "Lanjutkan ➔" (becomes "Kirim Pengajuan" on step 3).
- **Submission Result:** Generates new application record, triggers green toast notification `"Pengajuan PDLN berhasil didaftarkan!"`, and returns to dashboard.
- **Screenshot Evidence:**
  - `screenshots/desktop/P02-wizard-step1.png`
  - `screenshots/desktop/P02-wizard-step2.png`
  - `screenshots/desktop/P02-wizard-step3.png`

---

### P03 — Academic Profile Detail & Edit View
- **URL Route:** Subview `#applicant-view-profile`.
- **Access Method:** Click "Lengkapi Data" banner on P01, or Profile Flyout "Edit Profil" button.
- **Layout:** Centered card container (`max-width: 780px;`).
- **Header:** Title `Profil Akademik Pemohon`, subtitle `Data institusi terverifikasi langsung oleh PNJ, bebas duplikasi input`, and "Kembali" button.
- **Section 1: Data Terverifikasi Kampus PNJ (Non-editable institutional data):**
  - Grid of 4 read-only boxes each accompanied by green check badge `Terverifikasi`:
    1. NIM / NIP: `20260001`
    2. Nama Lengkap: `Andi Pratama`
    3. Jurusan: `Teknik Informatika dan Komputer`
    4. Program Studi: `Teknik Informatika (S1 Terapan)`
- **Section 2: Data Paspor & Kontak Mandiri (Editable Form):**
  - Email Kampus: Disabled input field (`andi.pratama@mhs.pnj.ac.id`).
  - Nomor Telepon / WhatsApp: Required text field (`081234567890`).
  - Nomor Paspor RI: Optional text field (`B7894561`).
  - Masa Berlaku Paspor: Date input (`2028-09-15`).
  - Nama Kontak Darurat: Text field (`Budi Pratama (Ayah)`).
  - No. HP Kontak Darurat: Tel input (`081299887766`).
- **Form Action:** Button "Simpan Profil" (updates completeness to 100%, triggers toast notification, re-renders P01).
- **Screenshot Evidence:**
  - `screenshots/desktop/P03-profile-edit.png`

---

### P04 — Dedicated KUI Operator Portal (Admin Console)
- **URL Route:** `https://h3rwthme.github.io/iniweb/?page=admin`
- **Layout Architecture:** Dedicated Admin Mode replacing navbar with a 270px fixed left sidebar (`.admin-sidebar`) and full-bleed scrollable content area (`.admin-main`).
- **Left Sidebar (270px, Dark Teal `#06343b`):**
  - Brand Header: White circular logo container (40x40px) with PNJ Crest, title `PDLN PNJ`, subtitle `POLITEKNIK NEGERI JAKARTA / Sistem Kontrol Admin`.
  - Main Controller Navigation:
    - `Dashboard Utama` (Active with home icon)
    - `Database Permohonan` (Scrolls to data table with fileText icon)
    - `Panduan Berkas` (Opens M02 Visual Guide with shield icon)
  - Operator Identity Footer: Name `Siti Rahmawati, M.Ed.`, Title `KUI Politeknik Negeri Jakarta`.
  - Session Control: Button "Keluar Sesi Admin" (`#btn-admin-logout`) in red accent (`btn-danger`).
- **Top Bar (`.admin-topbar`):**
  - Left: Title `Halaman Kontrol Administrator` and dynamic Indonesian long timestamp (`Kamis, 29 Oktober 2026`).
  - Right: "Refresh Data" button + "Ekspor Spreadsheet / CSV" primary button.
- **Hero Summary Banner (`.admin-hero`):**
  - Left: Title `Monitoring & Verifikasi Pra-Pengajuan PDLN` + description of institutional pre-filtering before Kemensetneg clearance.
  - Right: Metric card showing big total number (`3`) with label `Total Permohonan Terdaftar`.
- **5-Column Metric Stats Grid (`.admin-stats-grid`):**
  1. Total Data (`3` - Semua Berkas)
  2. Dosen (`1` - Pengajuan Kedinasan)
  3. Mahasiswa (`2` - Exchange / Lomba)
  4. Menunggu Review (`1` - Blue highlight `#0369a1`, border `#bae6fd`)
  5. Siap Setneg (`1` - Green highlight `#047857`, border `#a7f3d0`)
- **Visual Charts & Timeline Grid (2 Columns):**
  - Column 1: `Alur Disposisi Resmi PDLN` (4-step disposition list):
    1. Pengajuan Berkas Pemohon (Status: Siap)
    2. Verifikasi Internal KUI PNJ (Status: 1 Antrean)
    3. Persetujuan Direktur PNJ (Status: Otomatis)
    4. Pengajuan SP Kemensetneg (Status: 1 Siap)
  - Column 2: `Distribusi Negara Destinasi Populer`:
    1. Korea Selatan (SeoulTech - 1 Mahasiswa)
    2. Jepang (Tokyo Tech - 1 Dosen)
    3. Singapura (Nanyang Poly - 1 Mahasiswa)
- **Database Permohonan Pra-PDLN Table Panel (`#admin-table-panel`):**
  - Header: Title, subtitle, and "Cetak Laporan" button.
  - Filter Toolbar:
    - Search field with magnifying glass icon (filters by applicant name, NIM, destination, host).
    - Status Pills: `Semua`, `Review`, `Revisi`, `Siap Setneg`.
  - Data Table:
    - Columns: `Pemohon`, `Tujuan & Lembaga`, `Tanggal Masuk`, `Status`, `Aksi Verifikasi`.
    - Action: Button "Tinjau Berkas" (`.btn-open-review-modal`) triggering split-screen review modal M05.
- **Screenshot Evidence:**
  - `screenshots/desktop/P04-admin-dashboard-1440px.png`
  - `screenshots/desktop/P04-admin-split-review-modal.png`
  - `screenshots/desktop/P04-admin-revision-request-sheet.png`

---

### P05 — Authentication Portal (SSO & Admin Login)
- **URL Route:** Triggered on both `?` and `?page=admin` whenever user session is terminated (`sessionUserId: null`).
- **Layout Architecture:** Two-column split-screen card (`.auth-card`).
- **Left Column: Visual Showcase (`.auth-visual`):**
  - Full-height background image (`assets/hero_travel.jpg`).
  - Dark teal institutional gradient overlay.
  - PNJ crest logo badge with text `POLITEKNIK NEGERI JAKARTA`.
  - Shield badge: `Sistem Pra-Pengajuan & Verifikasi PDLN`.
  - Title:
    - Civitas mode: `Mobilitas Global Mahasiswa & Dosen`
    - Admin mode: `Pusat Kontrol Administrator KUI`
  - Description: Contextual copy explaining the role and pre-submission screening.
  - Institutional copyright footer.
- **Right Column: Login Form (`.auth-form-side`):**
  - Header: Title (`Masuk Akun Civitas` vs `Login Khusus Admin KUI`) and subtitle.
  - Demo Accounts Quick Login Chips:
    - Civitas mode: `Mahasiswa (Andi Pratama)` and `Dosen (Dr. Hendra Wijaya)`.
    - Admin mode: `Operator KUI (Siti Rahmawati)`.
  - Manual Form:
    - Identifier: NIM / NIP / Email (default: `20260001` or `kui.admin`).
    - Password: Password input (default: `password`).
    - Submit Button: `Masuk Portal Civitas` or `Masuk Konsol Admin`.
  - Navigation Switcher Link:
    - On Civitas Login: `Akses Konsol Admin KUI (?page=admin) ➔`
    - On Admin Login: `← Kembali ke Portal Mahasiswa / Dosen`
- **Screenshot Evidence:**
  - `screenshots/desktop/P05-auth-civitas-login.png`
  - `screenshots/desktop/P05-auth-admin-login.png`
