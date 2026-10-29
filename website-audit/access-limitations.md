# Access Limitations and Scope Boundary Report
## Sistem Internal PDLN PNJ

**Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Inspection Date:** 2026-10-29  
**Audit Purpose:** Transparent identification of test barriers, data persistence mechanisms, authentication architecture, and prototype versus live production boundaries.

---

### 1. Architectural Architecture & State Persistence

| Area | Observation | Classification | Impact on UI Recreation |
| :--- | :--- | :--- | :--- |
| **Frontend Framework** | Pure Vanilla ES6 JavaScript (No React/Vue/Angular), zero runtime external library dependencies. | **Direct Fact** | Clean DOM structure; standard HTML tags, CSS classes, and modular classes (`App`, `ApplicantPortal`, `KuiPortal`, `Store`, `ChatbotAssistant`). |
| **Client Routing** | Single-Page Application (SPA) driven by query parameter `?page=admin` and DOM container toggling (`#applicant-portal-root`, `#kui-portal-root`, `#auth-portal-root`). | **Direct Fact** | Browser URL does not change for subviews (e.g., Wizard, Profile Edit); they are controlled via JavaScript state transitions. |
| **Data Persistence** | Browser `localStorage` using key `PDLN_PNJ_DATA_V3_ISOLATED`. Falls back to seed data if key is missing or invalid. | **Direct Fact** | Full state mutations (applications submitted, profiles updated, internal notes added) persist locally within the testing browser session. |
| **Backend Integration** | Mock client-side store simulator. No live HTTP API server or database connected in the static GitHub Pages deployment. | **Direct Fact** | Safe to test all operations (creating applications, submitting revisions, saving confidential notes) without affecting real production records. |

---

### 2. Role-Based Access Control (RBAC) Boundaries

The reference system implements 4 defined roles in its design documentation (`docs/architecture.md`), of which 3 are actively testable in the UI:

| Role ID | Role Name | Testable User | Access Scope in Reference UI |
| :--- | :--- | :--- | :--- |
| `mahasiswa` | Mahasiswa Aktif | `Andi Pratama` (`mhs-1`) | Can fill academic profile, select travel routes, submit 3-step wizard applications, respond to document revisions, view their own dossier ticket and application history. **Cannot** access KUI internal notes or admin console. |
| `dosen` | Dosen Tetap | `Dr. Ir. Hendra Wijaya` (`dosen-1`) | Identical portal capability to Mahasiswa, but displaying official departmental affiliation (Teknik Mesin) and DIPA funding contexts. |
| `kui_admin` | Operator KUI | `Siti Rahmawati, M.Ed.` (`kui-1`) | Full administrative console at `?page=admin`. Can view all incoming applications, inspect submitted PDF/JPG attachments, write strictly confidential internal notes, request document revisions, and approve records for Kemensetneg. |
| `super_admin` | Super Administrator | Inferred from docs (`architecture.md`) | Mentioned in database schema roadmap for system configuration and master data management; **not present as a separate rendered UI view** in this frontend phase. |

---

### 3. Confirmed vs Inferred Capabilities

#### Directly Observed & Confirmed:
1. **Interactive Travel Route Picker:**
   - 4-activity segmented selector (`Student Exchange`, `Konferensi Ilmiah`, `Riset Kolaborasi`, `Pelatihan Vokasi`).
   - Dynamic duration calculation between start and end dates.
   - Destination picker modal with 6 partner universities.
2. **Boarding Pass Dossier Ticket:**
   - Visual flight ticket metaphor with notch perforations.
   - 4-step status progress timeline.
   - Dynamic revision alert banner with direct upload fix trigger.
3. **Form Wizard (3 Steps):**
   - Step 1: Auto-populated verified profile & route metadata.
   - Step 2: MoU radio conditionality & funding dropdowns.
   - Step 3: Mock upload dropzones with file size badges & legal declaration checkbox.
4. **Academic Profile Editor:**
   - Verified PNJ institutional badges.
   - Editable passport and emergency contact fields with 100% completeness update.
5. **KUI Operator Portal:**
   - 270px teal sidebar with operator profile footer.
   - 5-metric stats grid with live counts.
   - Filter pills (Semua, Review, Revisi, Siap Setneg) and live search input.
   - Split-screen review modal with strictly confidential internal notes feed.
   - Revision request sheet with multi-select checkboxes and feedback textarea.
6. **Hybrid Chatbot Assistant:**
   - Floating circular FAB launcher.
   - Automated keyword analysis for status, passport requirements, mandatory documents, and revisions.
7. **Responsive Breakpoints:**
   - 1440px desktop, 1280px laptop, 768px tablet, 390px mobile bottom navigation.

#### Identified Limitations & Inferences:
1. **Real File Uploading:**
   - File upload dropzones simulate file selection via browser file picker (`.mock-file-input`), extracting filename and size to display a green "Siap" badge. No binary files are sent across a network.
2. **Kemensetneg Official Integration:**
   - The button `Ekspor Spreadsheet / CSV` and the final stage `SP Kemensetneg` trigger simulated toast notifications. The actual Kemensetneg portal integration is a Stage 2 external milestone as documented in `docs/architecture.md`.
3. **External Authentication (SSO):**
   - The login form validates against local demo accounts (`20260001`, `kui.admin`) rather than an institutional LDAP/OAuth2 server.
4. **Print Action:**
   - Dossier ticket printing triggers standard native window print dialog (`window.print()`).
