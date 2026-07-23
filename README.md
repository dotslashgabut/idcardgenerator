# ID Card Generator

A single-file, client-side web app for designing and mass-producing ID cards (or any card-style layout) from a CSV/Excel data source. Everything runs in the browser — no backend, no upload of your data anywhere — and the whole tool lives in one HTML file (`idcard-generator.html`).

Available in Indonesian (default) and English, with a light/dark theme toggle.

## Key Features

- **Bulk data import** — Load a CSV or XLSX file (first row = column headers) to drive card generation, one card per row.
- **Photo matching** — Bulk-upload photos and auto-match them to rows via a chosen "matching" column (filename without extension). Supports multiple photo sources for different image elements (e.g. ID photo + signature).
- **Visual card editor** — Drag, resize, rotate, and skew elements on a WYSIWYG canvas:
  - Text fields (bound to data columns or static)
  - Data-bound photos
  - Static images (including SVG/PDF as vector sources)
  - QR codes
  - Shapes: rectangle, rounded rectangle, ellipse, triangle, right triangle, diamond, trapezoid, parallelogram, pentagon, hexagon, star, line, single/double arrows
- **Card setup** — Standard CR80 size or custom width/height, portrait/landscape swap, single or double-sided cards, bleed/extra size for trimming, adjustable export DPI.
- **Custom fonts** — Upload your own font files (.ttf/.otf/.woff/.woff2), load a font from a URL, or pull any Google Font by name.
- **Background control** — Upload a background image per side, choose Cover/Contain/Stretch fit, zoom, drag-to-position on canvas, alignment shortcuts, and arrow-key nudging (1 mm, or 0.1 mm with Shift).
- **Element tools** — Multi-select, copy/paste (including paste-to-other-side), alignment tools (left/center/right, top/middle/bottom), undo/redo (Ctrl+Z / Ctrl+Y).
- **Print layout & export**:
  - Export a single card as PNG
  - Export all cards as a ZIP of PNGs
  - Export a print-ready PDF with all data rows laid out on a chosen paper size, with configurable margins, gaps, fill order (row-first/column-first), auto/portrait/landscape orientation, card rotation, front/back combining (side-by-side or stacked, with optional 180° flip and mirroring for duplex printing), and cut guides (corner marks or full lines)
  - Choice between flattening each card to a single raster image or exporting as vector + layered PDF (text stays selectable, SVG/PDF sources and QR codes stay vector) for smaller, sharper output
- **Save/load layout** — Save the entire card design as a JSON file and reload it later to continue editing or reuse with new data.

## How It Works (Typical Workflow)

1. Upload your CSV/XLSX data file.
2. Upload the photos referenced by your data (optional).
3. Configure card size, sides, and background(s).
4. Add and arrange text, photo, image, QR, and shape elements on the canvas, binding text/photo elements to data columns.
5. Configure the print layout (paper size, margins, orientation, etc.).
6. Export as PDF (all cards, print-ready), ZIP of PNGs, or a single PNG.
7. Optionally save your layout as JSON to reuse for a future batch.

## Libraries Used

All libraries are loaded from public CDNs — no build step or install required.

| Library | Version | Purpose |
|---|---|---|
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | Generating the print-ready PDF output |
| [svg2pdf.js](https://github.com/yWorks/svg2pdf.js) | 2.7.0 | Converting SVG content (vector elements/shapes) into PDF drawing operations |
| [JSZip](https://stuk.github.io/jszip/) | 3.10.1 | Bundling exported card PNGs into a downloadable ZIP archive |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18.5 | Parsing uploaded CSV/XLSX data files |
| [pdf-lib](https://pdf-lib.js.org/) | 1.17.1 | Embedding source PDF files (used as backgrounds/images) as native vector pages in the exported PDF |
| [pdf.js](https://mozilla.github.io/pdf.js/) | 3.11.174 | Rendering/reading PDF files used as image or background sources |
| qrcode (bundled inline, not CDN-loaded) | — | Generating QR code elements |
| Google Fonts (DM Mono, Syne, Roboto, Montserrat, Open Sans, Poppins, Oswald) | — | Default UI/card typography, plus support for adding any additional Google Font by name |

## Notes

- Everything (data, photos, rendering, export) happens client-side in the browser; no data is sent to a server.
- Theme and language preferences are remembered locally via `localStorage`.
- Best used in a modern desktop browser given the density of the editing UI, though it includes a mobile tab layout (Settings / Card Editor).
