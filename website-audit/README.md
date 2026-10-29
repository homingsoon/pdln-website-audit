# Comprehensive Website UI/UX Reconnaissance Report
## Sistem Internal PDLN PNJ (Politeknik Negeri Jakarta)

**Audit Target URL:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Source Repository:** [https://github.com/h3rwthme/iniweb](https://github.com/h3rwthme/iniweb)  
**Inspection Date:** 2026-10-29  
**Reconnaissance Mode:** Evidence-based audit & documentation — **Strictly zero implementation or code modifications.**

---

### Executive Summary

This reconnaissance audit provides an exhaustive, evidence-based inventory of the **Sistem Internal PDLN PNJ** web application. Built for the **Kantor Urusan Internasional (KUI) Politeknik Negeri Jakarta**, the system serves as an institutional pre-screening portal for students (*mahasiswa*) and faculty (*dosen*) applying for official overseas travel (*Perjalanan Dinas Luar Negeri / PDLN*) prior to statutory approval from the Ministry of State Secretariat (*Kemensetneg*).

The documentation has been prepared as technical input for UI/UX recreation using **Google Stitch**, documenting 100% of the rendered pages, component hierarchies, responsive behavior, visual design tokens, interactive states, and modal overlays.

---

### Coverage and Verification Report

| Metric | Total Count | Verification Status | Notes |
| :--- | :---: | :---: | :--- |
| **Total Reachable Pages / Primary Portals** | **5** | 100% Confirmed & Inspected | P01 (Dashboard), P02 (Wizard), P03 (Profile), P04 (Admin), P05 (Auth) |
| **Modal Dialogs & Overlays** | **7** | 100% Confirmed & Inspected | M01 (Profile Flyout), M02 (Visual Guide), M03 (Destinations), M04 (Revision Sheet), M05 (Review Modal), M06 (KUI Request Sheet), M07 (Chatbot) |
| **Interactive Controls Tested** | **38** | 100% Confirmed & Verified | All navigation buttons, tabs, date pickers, mock uploads, filters, and forms |
| **Responsive Viewports Audited** | **4** | 100% Directly Observed | Desktop (1440px), Laptop (1280px), Tablet (768px), Mobile (390px) |
| **Screenshots Captured & Cataloged** | **18** | 100% Stored in Workspace | High-resolution PNGs organized in `screenshots/desktop/`, `tablet/`, `mobile/` |
| **Unverified / Inaccessible Routes** | **0** | Complete Access | Client mock store allows testing both Civitas and Admin portals |

---

### Documentation Map

All audit deliverables are organized in the `website-audit/` directory:

```
website-audit/
├── README.md                     <-- (This Document) Main Overview & Executive Summary
├── page-inventory.md             <-- Complete specification of P01 - P05 & all modal overlays
├── interaction-inventory.md      <-- Exhaustive inventory of 38 interactive controls & triggers
├── user-flows.md                 <-- Multi-step submission, revision loop & review flowcharts
├── design-system.md              <-- Complete color tokens, typography scales, SVG icons & layouts
├── responsive-audit.md           <-- 1440px, 1280px, 768px, and 390px layout behavior & shifts
├── access-limitations.md         <-- Prototype boundaries, RBAC model, and mock simulations
└── screenshots/
    ├── desktop/
    │   ├── P01-dashboard-desktop-1440px.png
    │   ├── P01-dashboard-desktop-scrolled.png
    │   ├── P01-profile-flyout.png
    │   ├── P01-visual-guide-modal.png
    │   ├── P01-destination-picker.png
    │   ├── P01-revision-fix-sheet.png
    │   ├── P01-chatbot-open.png
    │   ├── P02-wizard-step1.png
    │   ├── P02-wizard-step2.png
    │   ├── P02-wizard-step3.png
    │   ├── P03-profile-edit.png
    │   ├── P04-admin-dashboard-1440px.png
    │   ├── P04-admin-split-review-modal.png
    │   ├── P04-admin-revision-request-sheet.png
    │   ├── P05-auth-civitas-login.png
    │   └── P05-auth-admin-login.png
    ├── tablet/
    │   └── P01-dashboard-tablet-768px.png
    └── mobile/
        └── P01-dashboard-mobile-390px.png
```

---

### Core Architecture and Functional Highlights

1. **Information Architecture (Dual Portal Architecture):**
   - **Civitas Portal (Mahasiswa & Dosen):** Sticky 64px navbar, KAI Access-inspired travel route card with segmented selectors, airline boarding-pass dossier ticket, 4-stage visual progress timeline, profile completeness bar, riwayat pengajuan table, and hybrid virtual chatbot.
   - **KUI Operator Portal (`?page=admin`):** 270px fixed dark teal sidebar, live Indonesian timestamp header, 5-metric statistical overview cards, 4-step disposition status, popular destination list, real-time searchable application database, and split-screen review modal with strictly confidential internal notes.
2. **Design Language & Visual Metaphor:**
   - **Metaphor:** High-speed travel ticket / airline boarding pass (`.dossier-ticket`) with flight route arrows, perforated notch borders, and live duration counter.
   - **Color System:** Institutional Navy (`#0f233a`), KUI Teal (`#008c95`), Dark Teal Sidebar (`#06343b`), Quiet Semantic Statuses (Green `#047857`, Sky Blue `#0369a1`, Amber `#b45309`, Rose `#be123c`).
   - **Typography:** `Plus Jakarta Sans` Google Font with structured weights (400, 500, 600, 700, 800).
   - **Tactile UI Elements:** Micro-badges with pulsing status indicators, bottom-sheet sheets with drag handles on mobile, zero-dependency inline SVG feather icons.
3. **Interactive & Responsive Behavior:**
   - **Mobile Conversion:** Below 768px, top navbar minimizes and activates a 60px fixed bottom bar (`Beranda`, `Pengajuan`, `Profil`, `Keluar`).
   - **Adaptive Layout:** Modals transform into mobile bottom-sheets; auth card collapses its visual side on mobile screens; travel route boxes stack vertically.

---

### Screenshot Catalog and Visual Evidence

| ID | View / State | Viewport | Screenshot File Path |
| :--- | :--- | :---: | :--- |
| **P01-1** | Applicant Dashboard Top View | 1440x900 | [P01-dashboard-desktop-1440px.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-dashboard-desktop-1440px.png) |
| **P01-2** | Applicant Dashboard Scrolled (History Table) | 1440x900 | [P01-dashboard-desktop-scrolled.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-dashboard-desktop-scrolled.png) |
| **M01** | User Profile Drawer / Flyout | 1440x900 | [P01-profile-flyout.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-profile-flyout.png) |
| **M02** | Visual Guide & Infographics Modal | 1440x900 | [P01-visual-guide-modal.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-visual-guide-modal.png) |
| **M03** | Destination & Partner University Picker | 1440x900 | [P01-destination-picker.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-destination-picker.png) |
| **M04** | Document Revision Fix Upload Sheet | 1440x900 | [P01-revision-fix-sheet.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-revision-fix-sheet.png) |
| **M07** | Hybrid Chatbot Assistant Panel | 1440x900 | [P01-chatbot-open.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P01-chatbot-open.png) |
| **P02-1** | Application Form Wizard (Step 1: Profil & Rute) | 1440x900 | [P02-wizard-step1.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P02-wizard-step1.png) |
| **P02-2** | Application Form Wizard (Step 2: Kerjasama & Dana) | 1440x900 | [P02-wizard-step2.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P02-wizard-step2.png) |
| **P02-3** | Application Form Wizard (Step 3: Berkas & Konfirmasi) | 1440x900 | [P02-wizard-step3.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P02-wizard-step3.png) |
| **P03** | Academic Profile Editor | 1440x900 | [P03-profile-edit.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P03-profile-edit.png) |
| **P04-1** | KUI Operator Admin Console | 1440x900 | [P04-admin-dashboard-1440px.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P04-admin-dashboard-1440px.png) |
| **M05** | KUI Split-Screen Application Review Modal | 1440x900 | [P04-admin-split-review-modal.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P04-admin-split-review-modal.png) |
| **M06** | KUI Revision Request Sheet | 1440x900 | [P04-admin-revision-request-sheet.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P04-admin-revision-request-sheet.png) |
| **P05-1** | Civitas Single Sign-On (SSO) Login View | 1440x900 | [P05-auth-civitas-login.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P05-auth-civitas-login.png) |
| **P05-2** | KUI Operator Admin Login View | 1440x900 | [P05-auth-admin-login.png](file:///d:/pbl/uiux/website-audit/screenshots/desktop/P05-auth-admin-login.png) |
| **P01-T** | Applicant Dashboard Tablet View | 768x1024 | [P01-dashboard-tablet-768px.png](file:///d:/pbl/uiux/website-audit/screenshots/tablet/P01-dashboard-tablet-768px.png) |
| **P01-M** | Applicant Dashboard Mobile View & Bottom Bar | 390x844 | [P01-dashboard-mobile-390px.png](file:///d:/pbl/uiux/website-audit/screenshots/mobile/P01-dashboard-mobile-390px.png) |

---

### Recreation Guidelines for Google Stitch

When importing this audit into Google Stitch:
1. **Primary Layout:** Use standard responsive flexbox/CSS grid with `Plus Jakarta Sans` as the base font family.
2. **Color Constants:** Implement CSS custom properties directly from [design-system.md](file:///d:/pbl/uiux/website-audit/design-system.md).
3. **State Architecture:** Maintain the dual-portal design (`?` for Civitas, `?page=admin` for KUI Operator) and ensure the confidential notes panel remains strictly isolated from applicant views.
4. **Mobile Navigation:** Implement the 4-tab fixed bottom bar below 768px screen widths.
