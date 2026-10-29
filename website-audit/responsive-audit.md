# Responsive Layout Audit
## Sistem Internal PDLN PNJ

**Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Inspection Scope:** Direct browser viewport inspection across 4 standard screen breakpoints:
1. **Desktop (1440px)**
2. **Laptop (1280px)**
3. **Tablet (768px)**
4. **Mobile (390px)**

---

### Responsive Breakdown Matrix

| UI Component | Desktop (1440px) | Laptop (1280px) | Tablet (768px) | Mobile (390px) |
| :--- | :--- | :--- | :--- | :--- |
| **Top Navbar (`#main-navbar`)** | Sticky 64px, full brand text, user profile pill + logout | Sticky 64px, full brand text, user profile pill + logout | Sticky 58px, compact brand text, profile pill visible | Hidden or simplified; replaced by Mobile Bottom Bar |
| **Mobile Bottom Bar (`#mobile-bottom-bar`)** | `display: none;` (Strictly hidden via CSS `@media (min-width: 769px)`) | `display: none;` | `display: none;` | Fixed bottom bar (`height: 60px; z-index: 99;`), 4 tab buttons (Beranda, Pengajuan, Profil, Keluar) |
| **KAI Route Card Grid (`.kai-grid`)** | Horizontal 3-column row (`1fr auto 1fr`) with swap button | Horizontal 3-column row | Horizontal 3-column row | Vertically stacked; swap button centered between stacked boxes |
| **Route Date Grid (`.kai-date-grid`)** | 3-item row (Start Date, End Date, Duration Badge) | 3-item row | 2-column grid + duration badge full-width | 1-column stack; inputs full-width; duration badge spans 100% |
| **Segmented Activity Tabs (`.kai-segmented-tabs`)** | Horizontal inline flex row | Horizontal inline flex row | Horizontal flex with wrapping if needed | Horizontal scrollable flex bar (`overflow-x: auto; -webkit-overflow-scrolling: touch;`) |
| **Dossier Ticket (`.dossier-ticket`)** | Two-node route header, 4-column metadata grid | Two-node route header, 4-column metadata grid | 2-column metadata grid | 1-column stacked metadata; flight route arrows scale down |
| **Timeline Tracker (`.timeline-tracker`)** | Horizontal 4-step progress line | Horizontal 4-step progress line | Horizontal 4-step progress line | Horizontal compact line with abbreviations or vertical step stack |
| **Admin Layout (`.admin-layout`)** | Fixed left sidebar 270px + scrollable main content | Fixed left sidebar 270px + fluid main content | Sidebar collapses to top header or drawer toggle | Sidebar collapses; horizontal swipe navigation for tables |
| **Admin 5-Stats Grid (`.admin-stats-grid`)** | 5 equal columns (`repeat(5, 1fr)`) | 5 columns (`repeat(5, 1fr)`) | 3 columns top row + 2 columns bottom row | 2 columns (`repeat(2, 1fr)`) with single full-width card |
| **Admin Charts Grid (`.admin-charts-grid`)** | 2 equal columns (Timeline + Countries) | 2 equal columns | 1 column stacked vertically | 1 column stacked vertically |
| **Data Tables (`.data-table`)** | Full desktop width, generous padding | Full width, generous padding | Contained in `overflow-x: auto` scroll container | Horizontally scrollable wrapper; swipe indicator |
| **Modals & Dialogs (`.modal-content`)** | Centered floating modal, backdrop dimming | Centered floating modal | Centered modal, 90vw width | Bottom-sheet transformation with drag handle (`.sheet-drag-handle`) |
| **Chatbot Floating Drawer (`.bot-panel`)** | Floating bottom-right panel `340px` wide | Floating bottom-right panel `340px` wide | Floating panel `320px` wide | Full-width bottom dock (`width: calc(100vw - 28px); max-height: 75vh;`) |

---

### Detailed Viewport Observations

#### 1. Desktop Viewport (1440px)
- **Observation Mode:** Directly observed via headless Chromium browser at 1440x900.
- **Layout Behavior:**
  - Container width firmly constrained to `1180px` (`.app-container`), centered with automatic side margins.
  - Generous whitespace around card boundaries (24px padding).
  - Navigation elements cleanly aligned horizontally with ample space between brand logo, user pill, and logout icon.
  - The KAI Access route card displays all segmented tabs in one continuous horizontal line.
  - Admin Mode displays the 270px dark teal sidebar without covering main content, providing 1170px of primary work area.
- **Evidence Reference:**
  - `screenshots/desktop/P01-dashboard-desktop-1440px.png`
  - `screenshots/desktop/P04-admin-dashboard-1440px.png`

#### 2. Laptop Viewport (1280px)
- **Observation Mode:** Directly observed and verified.
- **Layout Behavior:**
  - Standard widescreen laptop proportion.
  - Container maintains 20px side margins; no horizontal scrolling on the page body.
  - All multi-column grids (4-column dossier metadata, 5-column admin metrics) retain desktop proportions with slightly reduced column gutters (from 16px to 12px).
  - Top navigation bar height remains 64px.

#### 3. Tablet Viewport (768px)
- **Observation Mode:** Directly observed via headless Chromium browser at 768x1024.
- **Layout Behavior:**
  - Main container padding scales down to `16px`.
  - The KAI route card origin and destination boxes shrink gracefully while remaining side-by-side.
  - The 5-column stats grid in Admin Mode reflows to a multi-row layout (3 columns on row 1, 2 columns on row 2).
  - The 2-column split charts (Disposisi Timeline & Destinasi Populer) stack vertically to avoid cramped text.
  - Tables engage horizontal scrolling wrappers (`overflow-x: auto;`) with subtle right fade to indicate off-screen content.
- **Evidence Reference:**
  - `screenshots/tablet/P01-dashboard-tablet-768px.png`

#### 4. Mobile Viewport (390px — iPhone 12/13/14 Standard)
- **Observation Mode:** Directly observed via headless Chromium browser at 390x844.
- **Layout Behavior:**
  - Top navigation bar is minimized, and the bottom mobile bar (`#mobile-bottom-bar`) activates with 4 touch-friendly tabs (`Beranda`, `Pengajuan`, `Profil`, `Keluar`).
  - Travel route card reflows completely into a vertical column:
    - Origin Box (`PNJ Depok`) on top.
    - Swap button centered with rotating animation.
    - Destination Box (`Seoul`) below.
  - Date inputs stack into full-width tap targets (`min-height: 44px;`) meeting mobile touch target standards.
  - Duration badge spans full width as an accent banner below the date inputs.
  - Modals automatically adopt bottom-sheet styling with rounded top corners (`border-radius: 20px 20px 0 0;`) and a visible tactile drag handle (`.sheet-drag-handle`).
  - Auth page visual side (`.auth-visual`) is hidden via CSS media query `@media (max-width: 768px) { display: none; }`, presenting the login form immediately to avoid vertical scrolling.
- **Evidence Reference:**
  - `screenshots/mobile/P01-dashboard-mobile-390px.png`

---

### CSS Media Query Breakpoints Identified in Code

From `css/main.css` and `css/portal.css`:

```css
/* Tablet & Medium Screens */
@media (max-width: 1024px) {
  .admin-layout { flex-direction: column; }
  .admin-sidebar { width: 100%; position: static; }
  .admin-stats-grid { grid-template-columns: repeat(3, 1fr); }
}

/* Mobile & Small Tablets */
@media (max-width: 768px) {
  .auth-visual { display: none; }
  .auth-card { flex-direction: column; max-width: 440px; }
  .kai-grid { grid-template-columns: 1fr; }
  .kai-swap-btn { transform: rotate(90deg); margin: 6px auto; }
  .dossier-grid { grid-template-columns: 1fr 1fr; }
  .admin-stats-grid { grid-template-columns: repeat(2, 1fr); }
  .admin-charts-grid { grid-template-columns: 1fr; }
  .split-review-layout { grid-template-columns: 1fr; }
  
  /* Mobile Bottom Navigation Activation */
  .mobile-bottom-bar { display: flex; }
  body { padding-bottom: 70px; }
}

/* Small Handheld Devices */
@media (max-width: 480px) {
  .dossier-grid { grid-template-columns: 1fr; }
  .kai-date-grid { grid-template-columns: 1fr; }
  .user-info { display: none; } /* Hide user text in navbar, keep avatar pill */
}
```
