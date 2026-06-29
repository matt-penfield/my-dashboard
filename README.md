# Fast Forward Logistics Dashboard

An internal analytics dashboard for **Fast Forward Logistics** that consolidates key operational metrics into a single view. Designed for use in meetings to quickly assess business performance across shipment volume, on-time delivery, regional performance, and open exceptions.

## Features

- **4 KPI summary cards** with trend indicators (up/down arrows showing month-over-month direction)
- **4 bar charts** for monthly breakdowns of each metric with scaled axes
- **Month picker** in the header — filter all cards and charts to a specific month, or view the full year
- **Performance Analysis modal** — explains likely causes behind the open exceptions trend
- **Responsive layout** — adapts from desktop (4-column cards, 2-column charts) down to mobile (single column)

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Vue 3 (Composition API, `<script setup>`) |
| Language | TypeScript |
| UI Library | Vuetify 3 (Material Design components) |
| Charts | Chart.js + vue-chartjs |
| Build Tool | Vite |
| Icons | Material Design Icons (`@mdi/font`) |

## Project Structure

```
src/
├── App.vue                    # Main single-page app (header, layout, filtering logic)
├── main.ts                    # App entry point, Vuetify plugin setup
├── assets/
│   └── main.css               # Global reset and base styles
├── components/
│   ├── AppHeader.vue          # App bar (unused — header is inline in App.vue)
│   ├── AppModal.vue           # Reusable dialog wrapper (v-dialog)
│   ├── ChartCard.vue          # Chart component (bar/line, supports yMin, ySuffix, fill)
│   └── MetricCard.vue         # KPI summary card with trend direction arrow
└── data/
    └── metrics.json           # 12 months of sample logistics data
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or later

### Install and Run

```bash
# Clone the repo
git clone https://github.com/matt-penfield/my-dashboard.git
cd my-dashboard

# Install dependencies
npm install

# Start the dev server
npm run dev
```

Open **http://localhost:5173** in your browser.

### Build for Production

```bash
npm run build
```

Output goes to the `dist/` folder, ready for static hosting.

## Deploying

### Vercel (recommended)

1. Push this repo to GitHub
2. Import it at [vercel.com/new](https://vercel.com/new)
3. Vercel auto-detects Vite — no configuration needed
4. Every push to `main` triggers a new deploy

### Other Static Hosts

Run `npm run build`, then deploy the `dist/` folder to any static host (Netlify, Cloudflare Pages, GitHub Pages, S3, etc.). No server-side runtime is required.

## Data

All data lives in `src/data/metrics.json` — a flat array of 12 monthly records. Each record contains:

| Field | Description |
|-------|------------|
| `month` | Three-letter month abbreviation |
| `shipmentVolume` | Total shipments for the month |
| `onTimeDelivery` | On-time delivery rate (%) |
| `regionalPerformance` | Regional performance score (%) |
| `openExceptions` | Count of open exceptions |

To use your own data, replace this file with the same shape. The dashboard will adapt automatically.

## License

See (LICENSE) for details.
