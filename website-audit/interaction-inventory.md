# Interaction and Component Inventory
## Sistem Internal PDLN PNJ

**Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Audit Scope:** All discoverable navigation links, buttons, inputs, segmented controls, modal triggers, drawers, floating action buttons, and form state changes.

---

### Master Interaction Table

| Page / Component ID | Element Name & Location | Initial State | Trigger Action | Resulting State & Visual Feedback | URL Change | Modal / Overlay Appeared | Reversible? | Verification Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **P01-NAV-01** | User Profile Mini Button (`#btn-nav-user-profile`) | Closed pill showing initials "AP", Name, Role | Click | Opens Profile Flyout (M01) with backdrop dimming | No | Yes (M01 Profile Flyout) | Yes (Click close icon or backdrop) | **Confirmed & Verified** |
| **P01-NAV-02** | Navbar Logout Button (`#btn-nav-logout`) | Icon button in top navbar | Click | Logs out user session; switches view to P05 Auth Portal; shows toast notification "Anda telah keluar." | No | No (Switches root view) | Yes (Log in again) | **Confirmed & Verified** |
| **P01-ACT-01** | Visual Guide Button (`#btn-open-visual-guide`) | Soft cyan secondary button | Click | Opens Visual Guide Modal (M02) showing 2 large infographics & text | No | Yes (M02 Visual Guide) | Yes (Click close icon or backdrop) | **Confirmed & Verified** |
| **P01-ACT-02** | Activity Selector Segments (`.kai-segment-btn`) | "Student Exchange" selected (`.active`) | Click on another segment (e.g. "Konferensi Ilmiah") | Active class shifts to clicked button; updates `routeData.purpose` and `routeData.purposeLabel` | No | No | Yes (Click original segment) | **Confirmed & Verified** |
| **P01-ACT-03** | Route Destination Box (`#btn-open-dest-sheet`) | Displays "Seoul (Korea Selatan)" & SeoulTech | Click | Opens Destination Picker Modal (M03) with 6 partner universities | No | Yes (M03 Destination Picker) | Yes (Close or pick item) | **Confirmed & Verified** |
| **P01-ACT-04** | Route Swap Button (`#btn-swap-route`) | Circular button between Origin & Destination | Click | Displays informative toast: "Rute terkonfirmasi pulang-pergi (Depok - Tujuan)." | No | No (Toast notification) | N/A | **Confirmed & Verified** |
| **P01-ACT-05** | Date Pickers (`#kai-input-start`, `#kai-input-end`) | Defaults: `2026-10-15` & `2027-02-28` | Change dates | Live recalculates and updates duration badge (`#kai-duration-display`), e.g. "136 Hari Dinas" | No | No | Yes (Change dates back) | **Confirmed & Verified** |
| **P01-ACT-06** | "Buat Draf Pengajuan" Button (`#btn-start-kai-apply`) | Primary button at bottom of Route Card | Click | Transitions view to P02 Form Wizard Step 1; syncs selected rute & dates | No (DOM Subview) | No | Yes (Click "Batalkan") | **Confirmed & Verified** |
| **P01-ACT-07** | Revision Action Button (`.btn-fix-revision`) | Primary small button in amber revision alert | Click | Opens Revision Fix Sheet (M04) with file upload dropzone | No | Yes (M04 Revision Fix Sheet) | Yes (Click Batal or close) | **Confirmed & Verified** |
| **P01-ACT-08** | Print Dossier Button (`.btn-print-ticket`) | Secondary button on Dossier Ticket | Click | Triggers native browser print dialog (`window.print()`) | No | System Print Dialog | Yes (Cancel print dialog) | **Confirmed & Verified** |
| **P01-ACT-09** | Completeness Button (`.btn-nav-profile`) | Secondary button on Profile Completeness Strip | Click | Transitions view to P03 Academic Profile Edit page | No (DOM Subview) | No | Yes (Click "Kembali") | **Confirmed & Verified** |
| **P01-BOT-01** | Chatbot Launcher FAB (`#bot-toggle-btn`) | Floating circular button at bottom right | Click | Toggles open Chatbot Assistant Panel (`#bot-panel`); focuses text input | No | Yes (Chat Panel overlay) | Yes (Click close or FAB) | **Confirmed & Verified** |
| **P01-BOT-02** | Chatbot Quick Query Chips (`.chip-query`) | 4 chips: Status Saya, Syarat Paspor, Dokumen Wajib, Alur Revisi | Click (e.g. "Syarat Paspor") | Appends user message to feed; shows typing indicator (400ms); renders bot automated response | No | No (Inside Chat Panel) | Yes (Ask other questions) | **Confirmed & Verified** |
| **P01-BOT-03** | Chatbot Input Bar (`#bot-input-text` + `#bot-send-trigger`) | Placeholder: "Tanya regulasi berkas PDLN..." | Type text and press Enter or click "Kirim" | Sends custom query, bot analyzes keywords and outputs response or KUI office contact info | No | No (Inside Chat Panel) | Yes | **Confirmed & Verified** |
| **P01-MOB-01** | Mobile Bottom Nav Items (`.mobile-nav-item`) | "Beranda" active (`.active`) | Tap "Pengajuan" / "Profil" / "Keluar" | Switches active state; "Pengajuan" opens Wizard, "Profil" opens M01 Flyout, "Keluar" logs out | No | Yes (on Profil) | Yes (Tap "Beranda") | **Confirmed & Verified** |
| **P02-WIZ-01** | Wizard Next Button (`.btn-wiz-next`) | Step 1 active; button text: "Lanjutkan ➔" | Click | Validates current step, animates forward to Step 2, updates step badge to `2 / 3` | No | No | Yes (Click "Sebelumnya") | **Confirmed & Verified** |
| **P02-WIZ-02** | Wizard Prev Button (`.btn-wiz-prev`) | Disabled on Step 1 (0.5 opacity) | Click (when on Step 2 or 3) | Returns to previous step; updates step badge and title | No | No | Yes (Click "Lanjutkan") | **Confirmed & Verified** |
| **P02-WIZ-03** | MoU Radio Toggle (`input[name="wiz-coop"]`) | "Ya, terdapat MoU/MoA" checked | Toggle to "Bukan Kerjasama Resmi" | Toggles visibility/state of MoU document name field | No | No | Yes (Toggle back to "Ya") | **Confirmed & Verified** |
| **P02-WIZ-04** | Mock File Inputs (`.mock-file-input`) | Initial filename: e.g. `Paspor_Aktif.pdf` | Choose a new file | Updates filename text label with selected file name, size, and green badge "Siap" | No | Native file picker | Yes (Choose different file) | **Confirmed & Verified** |
| **P02-WIZ-05** | Wizard Submit Button (`.btn-wiz-next` on Step 3) | Text: "Kirim Pengajuan" | Click | Appends new application to Store; triggers green toast; switches view back to P01 Dashboard | No | No | Yes (Data persists in store) | **Confirmed & Verified** |
| **P02-WIZ-06** | Wizard Cancel Button (`.btn-back-dashboard`) | "Batalkan" secondary button in top step card | Click | Cancels wizard; returns directly to P01 Dashboard | No | No | Yes (Click "Buat Draf" again) | **Confirmed & Verified** |
| **P03-PRF-01** | Profile Save Form (`#form-edit-profile`) | Pre-populated user contact & passport data | Submit form with changes | Updates user profile in Store (sets completeness to 100%); triggers green toast; returns to P01 | No | No | Yes (Edit again anytime) | **Confirmed & Verified** |
| **P03-PRF-02** | Profile Back Button (`.btn-back-dashboard`) | Secondary button in header | Click | Discards uncommitted inputs and returns to P01 Dashboard | No | No | Yes | **Confirmed & Verified** |
| **P04-ADM-01** | Admin Nav DB Button (`#btn-admin-nav-db`) | Sidebar navigation item | Click | Smooth-scrolls viewport down directly to `#admin-table-panel` | No | No | Yes | **Confirmed & Verified** |
| **P04-ADM-02** | Admin Nav Guide Button (`#btn-admin-nav-guide`) | Sidebar navigation item | Click | Opens Visual Guide Modal (M02) | No | Yes (M02 Visual Guide) | Yes (Click close) | **Confirmed & Verified** |
| **P04-ADM-03** | Admin Refresh Button (`#btn-admin-refresh`) | Secondary button in topbar | Click | Re-renders stats & table; shows toast "Data diperbarui secara live." | No | No | N/A | **Confirmed & Verified** |
| **P04-ADM-04** | Admin Export Button (`.btn-export-all`) | Primary button in topbar | Click | Triggers toast "Data permohonan diekspor dalam format spreadsheet/CSV." | No | No | N/A | **Confirmed & Verified** |
| **P04-ADM-05** | Admin Search Input (`#admin-search-input`) | Empty text input | Type query (e.g. "Hendra", "Seoul") | Dynamically filters table rows in real-time matching applicant, ID, country, or host | No | No | Yes (Clear input) | **Confirmed & Verified** |
| **P04-ADM-06** | Admin Filter Pills (`[data-f]`) | "Semua" active | Click "Review", "Revisi", or "Siap Setneg" | Re-filters table rows by status; updates active button styling | No | No | Yes (Click "Semua") | **Confirmed & Verified** |
| **P04-ADM-07** | Admin Review Button (`.btn-open-review-modal`) | Primary button in each table row | Click | Opens KUI Split-Screen Review Modal (M05) for that specific application | No | Yes (M05 Review Modal) | Yes (Click close) | **Confirmed & Verified** |
| **P04-ADM-08** | Admin Logout Button (`#btn-admin-logout`) | Danger button at bottom of sidebar | Click | Clears admin session; redirects window location to base path (clears `?page=admin`); renders P05 Auth | Yes (`?page=admin` -> `/`) | No | Yes (Log in again) | **Confirmed & Verified** |
| **M01-FLY-01** | Flyout Edit Profile (`#btn-flyout-edit-prof`) | Secondary button in flyout footer | Click | Closes flyout; transitions view to P03 Academic Profile Edit | No | Closes M01 | Yes (Return to Dashboard) | **Confirmed & Verified** |
| **M01-FLY-02** | Flyout Logout (`#btn-flyout-logout`) | Danger button in flyout footer | Click | Closes flyout; logs out user session; renders P05 Auth Portal | No | Closes M01 | Yes (Log in again) | **Confirmed & Verified** |
| **M03-DST-01** | Destination University Item (`.dest-option-item`) | List of 6 destination cards | Click an item (e.g. "Tokyo, Jepang") | Sets destination city, country, and host; updates P01 display; closes modal; shows toast | No | Closes M03 | Yes (Re-open and select other) | **Confirmed & Verified** |
| **M04-REV-01** | Revision File Select (`#rev-file-picker`) | Dashed dropzone with upload button | Click and choose file | Displays filename with green checkmark (`✓ Paspor_Baru.pdf`) | No | Native file picker | Yes (Pick another file) | **Confirmed & Verified** |
| **M04-REV-02** | Revision Submit (`#btn-submit-rev-file`) | Primary button: "Kirim Perbaikan ke KUI" | Click | Updates application status from `revision_required` to `kui_review`; closes sheet; shows success toast | No | Closes M04 | Yes | **Confirmed & Verified** |
| **M05-REV-01** | KUI Split Review Approve (`.btn-modal-approve`) | Green-styled primary button | Click | Prompts native confirmation (`confirm()`); if OK, sets status to `ready_for_official_pdln`; closes modal; shows toast | No | Native confirmation dialog | Yes | **Confirmed & Verified** |
| **M05-REV-02** | KUI Split Review Request Revision (`.btn-modal-req-rev`) | Secondary button | Click | Closes M05; immediately opens KUI Revision Request Sheet (M06) | No | Closes M05, Opens M06 | Yes (Cancel sheet) | **Confirmed & Verified** |
| **M05-REV-03** | KUI Save Confidential Note (`#btn-save-modal-note`) | Secondary button below textarea | Type text and click | Appends internal note to application record with author name and timestamp; updates confidential feed | No | No (Updates M05 DOM) | Yes | **Confirmed & Verified** |
| **M06-REQ-01** | KUI Send Revision Request (`#btn-send-req-sheet`) | Danger button: "Kirim Permintaan Revisi" | Click | Validates checkboxes and explanation text; sets app status to `revision_required`; closes sheet; shows toast | No | Closes M06 | Yes | **Confirmed & Verified** |
| **P05-ATH-01** | Demo Account Chip (`.demo-chip-btn`) | Chip buttons for Quick Login | Click (e.g. "Mahasiswa", "Dosen", "Operator KUI") | Immediately authenticates designated user; renders target portal; shows welcome toast | No (or redirect to `?page=admin` if admin) | No | Yes (Log out anytime) | **Confirmed & Verified** |
| **P05-ATH-02** | Manual SSO Form (`#form-login-manual`) | Pre-filled identifier & password inputs | Click "Masuk Portal Civitas" | Authenticates credentials; matches role; routes to either Civitas Portal or KUI Admin Console | No | No | Yes | **Confirmed & Verified** |
| **P05-ATH-03** | Console Switcher Link | Anchor text at bottom of form | Click | Navigates between `?` (Civitas SSO) and `?page=admin` (Admin Console) | Yes (`?page=admin` <-> `?`) | No | Yes | **Confirmed & Verified** |

---

### Toast Notification System (`#toast-root`)
- **Container Location:** Fixed at top-right on desktop (`top: 24px; right: 24px; z-index: 9999;`).
- **Variants Observed:**
  - `toast-success`: Green border, check circle icon, auto-dismiss in 3.2s.
  - `toast-warning`: Amber border, alert circle icon, auto-dismiss in 3.2s.
  - `toast-info`: Blue border, file text icon, auto-dismiss in 3.2s.
- **Entry & Exit Animation:** CSS slide-in (`toast-enter`, 200ms cubic-bezier) and fade-out (`toast-exit`, 220ms).
