# Visual Design System Specification
## Sistem Internal PDLN PNJ

**Target:** [https://h3rwthme.github.io/iniweb/](https://h3rwthme.github.io/iniweb/)  
**Extraction Methodology:** Direct source code analysis of `css/main.css`, `css/portal.css`, `css/motion.css`, `js/icons.js`, and browser-rendered DOM styles.

---

### 1. Color Palette Tokens

#### A. Institutional & Brand Accents
| Token Name | Hex Code | RGB | Purpose & Usage |
| :--- | :--- | :--- | :--- |
| `--brand-primary` | `#0f233a` | `rgb(15, 35, 58)` | Primary deep navy institutional blue; headers, primary buttons, brand accents |
| `--brand-hover` | `#173559` | `rgb(23, 53, 89)` | Primary button hover state |
| `--brand-subtle` | `#eef4fa` | `rgb(238, 244, 250)` | Light blue tint background for avatar chips, icon boxes |
| `--brand-accent` | `#1e3a5f` | `rgb(30, 58, 95)` | Secondary brand tone |
| `--kui-sidebar` | `#06343b` | `rgb(6, 52, 59)` | Deep dark teal background for KUI Admin 270px sidebar |
| `--kui-teal` | `#008c95` | `rgb(0, 140, 149)` | Secondary institutional accent; guide buttons, link accents |
| `--kui-teal-soft` | `#12b5bd` | `rgb(18, 181, 189)` | Soft teal highlight color |

#### B. Minimalist Neutral Scale (Zinc / Slate)
| Token Name | Hex Code | Purpose & Usage |
| :--- | :--- | :--- |
| `--neutral-950` | `#09090b` | Highest contrast text, primary titles, brand headers |
| `--neutral-900` | `#18181b` | Primary body text, modal header bars |
| `--neutral-800` | `#27272a` | Secondary dark text |
| `--neutral-700` | `#3f3f46` | Form labels, dark icons |
| `--neutral-600` | `#52525b` | Secondary descriptions, descriptive subtitles |
| `--neutral-500` | `#71717a` | Muted metadata, helper text, inactive step labels |
| `--neutral-400` | `#a1a1aa` | Borders in focus, table subheadings, placeholder text |
| `--neutral-300` | `#d4d4d8` | Secondary borders, dashed upload borders |
| `--neutral-200` | `#e4e4e7` | Standard card borders, table dividers, input borders |
| `--neutral-100` | `#f4f4f5` | Section dividers, pill button backgrounds |
| `--neutral-50` | `#fafafa` | Page background, input disabled background, subtle cards |
| `--white` | `#ffffff` | Pure surface white for cards, modals, and navbar |

#### C. Semantic Status Colors (Quiet & High-Contrast)
| State | Text Color | Background Color | Border Color | Dot / Indicator Color |
| :--- | :--- | :--- | :--- | :--- |
| **Verified / Siap** | `#047857` (`--status-verified-text`) | `#ecfdf5` (`--status-verified-bg`) | `#a7f3d0` | `#10b981` |
| **Review / Menunggu** | `#0369a1` (`--status-review-text`) | `#f0f9ff` (`--status-review-bg`) | `#bae6fd` | `#0284c7` |
| **Revision / Perlu Revisi** | `#b45309` (`--status-revision-text`) | `#fffbeb` (`--status-revision-bg`) | `#fde68a` | `#d97706` |
| **Draft / Disimpan** | `#52525b` (`--status-draft-text`) | `#f4f4f5` (`--status-draft-bg`) | `#e4e4e7` | `#71717a` |
| **Danger / Ditolak / Keluar** | `#be123c` (`--status-danger-text`) | `#fff1f2` (`--status-danger-bg`) | `#fecdd3` | `#ef4444` |

#### D. Strictly Confidential Note Styling (KUI Admin Internal)
- Background: `#fff7ed` (soft amber-orange tint)
- Border: `1px solid #fed7aa`
- Header Text: `#9a3412` (dark rust-amber)
- Confidential Badge: Red background `#fef2f2`, border `#fecaca`, text `#991b1b`, font-size: `10px`, font-weight: `800`.

---

### 2. Typography System

- **Primary Font Family:** `'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`
- **Import URL:** Google Fonts `https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap`
- **Root Font Size:** `14.5px` (scaling basis)
- **Line Height:** `1.5` default

#### Typographic Scale Hierarchy

| Element / Style | Font Size | Font Weight | Line Height | Color | Usage |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Display / Hero H1** | `22px - 24px` | `800` (ExtraBold) | `1.2` | `#07343a` / `#09090b` | Admin Hero title, Login Showcase title |
| **Page Heading H2** | `18px - 20px` | `800` (ExtraBold) | `1.25` | `#09090b` | Section headers ("Portal Pengajuan PDLN") |
| **Section Heading H3** | `15px - 16px` | `700` (Bold) | `1.3` | `#09090b` | Card titles, Dossier route nodes, Navbar brand |
| **Subheading H4** | `13.5px - 14px` | `700` (Bold) | `1.4` | `#18181b` | Table panel titles, modal subheaders |
| **Body Regular** | `13px - 14px` | `400` (Regular) | `1.5` | `#27272a` | General paragraph text, instructions |
| **Body Semibold** | `13px - 13.5px` | `600` (SemiBold) | `1.4` | `#18181b` | Table cell bold text, field values |
| **Form Labels** | `12.5px - 13px` | `600` (SemiBold) | `1.3` | `#3f3f46` | Input field labels, selector labels |
| **Badges & Tags** | `10.5px - 11.5px` | `700` (Bold) | `1.0` | Semantic status | Status badges, institutional tags |
| **Micro Labels & Captions** | `9.5px - 10.5px` | `500` / `600` | `1.2` | `#71717a` | Timestamps, audit actors, sub-captions |

---

### 3. Layout Grid & Dimensional Tokens

| Token / Property | Exact Value | Purpose |
| :--- | :--- | :--- |
| **App Max Width** | `1180px` (`.app-container`) | Main content wrapper for civitas portal |
| **Horizontal Page Padding** | `20px` (Desktop) / `14px` (Mobile) | Container gutter spacing |
| **Navbar Height** | `64px` | Sticky top navigation bar |
| **Admin Sidebar Width** | `270px` | Dedicated KUI Admin controller navigation drawer |
| **Form Wizard Max Width** | `820px` | Centered multistep submission container |
| **Profile Card Max Width** | `780px` | Centered profile editor container |
| **Review Modal Max Width** | `960px` | Split-screen desktop review dialog |
| **Visual Guide Modal Max Width** | `900px` | Layperson infographic viewer dialog |
| **Standard Modal Max Width** | `520px - 600px` | Destination picker, revision sheets |
| **Chatbot Floating Width** | `340px` (Desktop) / `calc(100vw - 28px)` (Mobile) | Floating assistant drawer |

#### Spacing Scale
- `4px`, `6px`, `8px`, `10px`, `12px`, `14px`, `16px`, `18px`, `20px`, `24px`, `28px`, `32px`

#### Elevation & Shadows
- `--shadow-xs`: `0 1px 2px 0 rgba(0, 0, 0, 0.05)`
- `--shadow-sm`: `0 1px 3px 0 rgba(0, 0, 0, 0.08), 0 1px 2px -1px rgba(0, 0, 0, 0.08)`
- `--shadow-md`: `0 4px 6px -1px rgba(0, 0, 0, 0.07), 0 2px 4px -2px rgba(0, 0, 0, 0.05)`
- `--shadow-lg`: `0 10px 15px -3px rgba(0, 0, 0, 0.08), 0 4px 6px -4px rgba(0, 0, 0, 0.04)`

#### Border Radii
- `--radius-sm`: `6px` (Pills, small badges, input fields)
- `--radius-md`: `10px` (Buttons, notification bubbles, verified boxes)
- `--radius-lg`: `14px` (Cards, travel route box, modal dialogs)
- `--radius-xl`: `20px` (Dossier ticket card corners)
- `--radius-full`: `9999px` (Avatar chips, circular FAB buttons, segmented pills)

---

### 4. Component Design Specifications

#### A. Buttons (`.btn`)
- **Primary Button (`.btn-primary`):**
  - Background: `#0f233a`
  - Text: `#ffffff`
  - Padding: `8px 18px` (default) or `6px 14px` (`.btn-sm`)
  - Border-radius: `10px` (`--radius-md`)
  - Hover: Background `#173559`, transform: `translateY(-1px)`
- **Secondary Button (`.btn-secondary`):**
  - Background: `#ffffff`
  - Border: `1px solid #e4e4e7`
  - Text: `#18181b`
  - Hover: Background `#fafafa`, border `#d4d4d8`
- **Danger Button (`.btn-danger`):**
  - Background: `#fff1f2`
  - Border: `1px solid #fecdd3`
  - Text: `#be123c`
  - Hover: Background `#ffe4e6`
- **Icon Button (`.btn-icon`):**
  - Square aspect ratio `36px x 36px` (or `30px x 30px`), centered flex layout

#### B. Badges (`.badge`)
- Display: Inline-flex, items-center, gap `5px`, padding `3px 8px`, border-radius `9999px`, font-size `11px`, font-weight `700`.
- Includes animated pulsating status dot (`.badge-dot`, 6x6px rounded full).

#### C. KAI Access Route Card (`.kai-route-card`)
- Background: White with border `1px solid #e4e4e7`, border-radius `14px`, padding `20px 24px`.
- Origin / Destination Box (`.kai-location-box`):
  - Subtle background `#fafafa`, border `1px solid #e4e4e7`, border-radius `10px`, padding `14px 18px`.
  - Hover effect: Background `#f4f4f5`, border `#a1a1aa`, cursor pointer.
- Swap Button (`.kai-swap-btn`):
  - 36px circular button, centered between origin and destination, border `1px solid #e4e4e7`.

#### D. Boarding Pass Dossier Ticket (`.dossier-ticket`)
- Background: Pure white, border `1px solid #e4e4e7`, border-radius `18px`, overflow hidden.
- Decorative tear notch (`.dossier-tear`): Perforated dashed line with circular cutouts at left and right edges.
- Timeline tracker: 4 circular number/check steps connected by horizontal progress bars.

#### E. Data Table (`.data-table`)
- Width: `100%`, border-collapse `collapse`.
- Table Header (`th`): Background `#fafafa`, text color `#71717a`, text-transform uppercase, font-size `10.5px`, font-weight `700`, padding `12px 16px`, border-bottom `1px solid #e4e4e7`.
- Table Body (`td`): Padding `14px 16px`, border-bottom `1px solid #f4f4f5`, vertical-align middle.
- Row Hover: Background `#fafafa`.

#### F. Form Inputs (`.form-control`)
- Height: `38px - 42px`, padding: `8px 12px`, border: `1px solid #e4e4e7`, border-radius `8px`, background: `#ffffff`, font-size `13px`.
- Focus state: Border color `#0f233a`, outline: `2px solid rgba(15, 35, 58, 0.12)`.
- Disabled state: Background `#fafafa`, color `#a1a1aa`, cursor `not-allowed`.

---

### 5. Vector Iconography System (`js/icons.js`)

All icons in the system are rendered as zero-dependency inline SVGs with standard feather/lucide 24x24 viewBox, stroke-width `1.8` or `2`:

| Icon Key | Function Call | Semantic Meaning |
| :--- | :--- | :--- |
| `shield` | `Icons.shield(size, cls)` | Official verification, security, KUI authority |
| `plane` | `Icons.plane(size, cls)` | International flight, PDLN departure |
| `building` | `Icons.building(size, cls)` | PNJ Campus origin, host university institution |
| `mapPin` | `Icons.mapPin(size, cls)` | Destination country and city |
| `calendar` | `Icons.calendar(size, cls)` | Travel start date, return date, passport expiration |
| `clock` | `Icons.clock(size, cls)` | Travel duration calculation ("136 Hari Dinas"), timestamps |
| `swap` | `Icons.swap(size, cls)` | Swap route origin and destination |
| `user` | `Icons.user(size, cls)` | Applicant identity, profile completeness, student role |
| `fileText` | `Icons.fileText(size, cls)` | Document checklist, spreadsheet export, records |
| `upload` | `Icons.upload(size, cls)` | Document upload dropzone, revision file replacement |
| `ticket` | `Icons.ticket(size, cls)` | Dossier ticket printing, report generation |
| `checkCircle` | `Icons.checkCircle(size, cls)` | Verified status, approved application |
| `alertCircle` | `Icons.alertCircle(size, cls)` | Revision required warning, attention banner |
| `lock` | `Icons.lock(size, cls)` | Strictly confidential internal notes |
| `bot` | `Icons.bot(size, cls)` | Virtual assistant launcher button |
| `search` | `Icons.search(size, cls)` | Real-time database query filter |
| `home` | `Icons.home(size, cls)` | Dashboard home navigation item |
| `logout` | `Icons.logout(size, cls)` | Terminate session control |

---

### 6. Image and Brand Assets

| Asset Filename | Disk Location & URL | Dimensions | File Size | Description & Usage |
| :--- | :--- | :--- | :--- | :--- |
| `logo_pnj.png` | `assets/logo_pnj.png` | 512 x 512 (PNG) | `104 KB` | Official Politeknik Negeri Jakarta crest logo. Displayed in top navbar, admin sidebar, and auth banner. |
| `hero_travel.jpg` | `assets/hero_travel.jpg` | 1920 x 1280 (JPG) | `589 KB` | Airport terminal and international departure concourse visual for authentication split card. |
| `guide_workflow.jpg` | `assets/guide_workflow.jpg` | 1200 x 800 (JPG) | `689 KB` | Infographic illustrating the 4 stages of PDLN clearance (Kampus ➔ KUI ➔ SK Direktur ➔ SP Kemensetneg). |
| `guide_docs.jpg` | `assets/guide_docs.jpg` | 1200 x 800 (JPG) | `631 KB` | Visual checklist illustrating the 4 required pre-submission documents (Passport, LoA, SPTJM, Sponsorship). |
