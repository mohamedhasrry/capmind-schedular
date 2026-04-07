# CapMinds — Practice Dashboard

A clean, fully client-side appointment scheduling dashboard for medical practices. Built with pure HTML5, CSS3, and vanilla JavaScript — no frameworks, no dependencies.

---

## Overview

CapMinds is a lightweight practice management interface that allows clinic staff to book, view, edit, and delete patient appointments through an interactive calendar and list dashboard. All data is persisted in the browser's `localStorage`, making it ready to use instantly without any backend or build step.

---

## Features

### Appointment Management
- Book new appointments with patient name, doctor, hospital, specialty, date, and time
- Edit existing appointments via the calendar or dashboard table
- Delete appointments with a confirmation dialog to prevent accidental removal
- Conflict detection — prevents double-booking a doctor at the same date and time

### Calendar View
- Monthly grid calendar with navigation (previous/next month)
- Click any date cell to pre-fill the booking modal with that date
- Up to 2 appointments shown per cell with a `+N more` overflow button
- Jump to any date using a native date picker or the month dropdown
- Today's date is visually highlighted

### Dashboard View
- Tabular list of all appointments with sorting by date and time
- Filter by patient name, doctor name, and date range
- Mobile-friendly card layout that replaces the table on small screens
- Live result count and total appointment badge

### Form Validation
- Required field checks for all core fields
- Patient name must be alphabetic (no digits) and at least 2 characters
- Past dates are rejected when creating new appointments (allowed when editing)
- Inline error messages appear beside each invalid field

### UI & Accessibility
- Responsive layout: collapsible sidebar on desktop, drawer on mobile
- ARIA roles, labels, and live regions throughout
- Keyboard navigable — modals close on `Escape`, calendar events respond to `Enter`/`Space`
- Toast notifications for success and error feedback
- Bottom-sheet modal animation on mobile devices
- Touch-friendly tap targets (minimum 44×44px) on mobile

---

## Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Markup     | HTML5 (semantic, accessible)      |
| Styling    | CSS3 (custom properties, flexbox, grid, media queries) |
| Logic      | Vanilla JavaScript ES6+ (no frameworks) |
| Storage    | Browser `localStorage`            |
| Icons      | Inline SVG                        |
| Font       | System font stack (`-apple-system`, `Segoe UI`, etc.) |

**Zero external dependencies.** No npm, no CDN links, no build tools required.

---

## Project Structure

```
capminds/
├── index.html      # App shell, layout, modal markup
├── styles.css      # All styling — variables, components, responsive breakpoints
└── script.js       # Application logic — state, calendar, dashboard, modal, validation
```

### JavaScript Architecture

The JavaScript is organized into self-contained IIFE modules, each with a single responsibility:

| Module           | Responsibility                                              |
|------------------|-------------------------------------------------------------|
| `CONFIG`         | App-wide constants (storage key, durations, labels)         |
| `State`          | Centralized reactive state (appointments, filters, month)   |
| `Storage`        | `localStorage` read/write with seed data fallback           |
| `Utils`          | Helpers — UID generation, time conversion, date formatting, debounce |
| `Validator`      | Form validation logic and error rendering                   |
| `AppointmentOps` | CRUD operations (add, update, delete, getById)              |
| `Toast`          | Timed success/error notification bar                        |
| `Confirm`        | Promise-based confirmation dialog                           |
| `Layout`         | Sidebar toggle, view switching, responsive behavior         |
| `Calendar`       | Monthly grid rendering, date navigation, event display      |
| `Dashboard`      | Appointment table/card rendering, filter handling           |
| `Modal`          | Booking/edit form — open, close, pre-fill, save             |

---

## Getting Started

No installation or build step is needed.

1. Download or clone the repository.
2. Open `index.html` directly in any modern browser.

```bash
git clone https://github.com/your-org/capminds.git
cd capminds
open index.html   # macOS
# or double-click index.html on Windows/Linux
```

The app loads with two sample appointments pre-seeded so the calendar and dashboard are populated on first launch. Once you create your own appointments, they are saved to `localStorage` and persist across page refreshes.

---

## Browser Support

| Browser        | Support |
|----------------|---------|
| Chrome 90+     | ✅      |
| Firefox 88+    | ✅      |
| Safari 14+     | ✅      |
| Edge 90+       | ✅      |

Requires a browser with `localStorage`, `ES6+` (arrow functions, async/await, destructuring), and the native `<input type="date">` picker.

---

## Data Model

Each appointment is stored as a plain object:

```js
{
  id:        "1718000000000-abc12",   // Unique ID (timestamp + random)
  patient:   "Henry James",
  doctor:    "James Marry",
  hospital:  "Salus Center (General Hospital)",
  specialty: "Dermatology",
  date:      "2025-12-18",            // ISO format YYYY-MM-DD
  time:      "09:00 AM",              // 12-hour format
  reason:    "Routine check-up"       // Optional
}
```

All appointments are serialized as a JSON array under the `localStorage` key `capminds_appointments`.

---

## Customization

**Adding doctors** — Edit the `<select id="appt-doctor">` options in `index.html`.

**Adding hospitals or specialties** — Edit the respective `<select>` elements in `index.html`.

**Adding patients to the autocomplete** — Edit the `<datalist id="patient-list">` options in `index.html`.

**Changing the accent color** — Update `--color-primary` in the `:root` block of `styles.css`.

---

## License

MIT — free to use, modify, and distribute.
