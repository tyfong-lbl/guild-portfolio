# Bookmark Manager — Design Document

A personal, browser-based bookmark manager for saving, tagging, and searching links.

## Goals

- Save bookmarks with a URL, title, and optional notes
- Organize bookmarks with tags
- Search bookmarks by title, URL, notes, or tag
- No accounts, no login — single-user, local-only
- Learn web fundamentals: HTML, CSS, JavaScript, DOM manipulation, localStorage

## Tech Stack

| Layer       | Choice              | Why                                          |
|-------------|----------------------|----------------------------------------------|
| Markup      | HTML5                | Semantic, accessible, no build step           |
| Styling     | CSS3 (single file)   | Learn layout, responsive design, variables    |
| Logic       | Vanilla JavaScript   | Learn DOM APIs and data handling directly     |
| Storage     | localStorage         | Built into every browser, no server needed    |
| Tooling     | None                 | Open `index.html` in a browser and go         |

No frameworks, no bundlers, no package manager. Three files: `index.html`, `style.css`, `app.js`.

## Data Model

Each bookmark is a plain object stored as a JSON array in `localStorage` under the key `"bookmarks"`.

```json
{
  "id": "a1b2c3",
  "url": "https://example.com",
  "title": "Example Site",
  "notes": "A useful reference for X.",
  "tags": ["reference", "web"],
  "createdAt": "2026-03-25T12:00:00Z"
}
```

- `id` — random string generated with `crypto.randomUUID()`
- `url` — required, validated as a URL
- `title` — required
- `notes` — optional free text
- `tags` — array of lowercase strings, can be empty
- `createdAt` — ISO timestamp, set automatically on creation

## Features

### Core (build these first)

1. **Add bookmark** — form with fields for URL, title, notes, and tags (comma-separated)
2. **List bookmarks** — display all bookmarks, newest first
3. **Delete bookmark** — remove a bookmark from the list
4. **Edit bookmark** — update any field on an existing bookmark
5. **Search** — filter the displayed list by typing in a search box (matches against title, URL, notes, and tags)
6. **Filter by tag** — click a tag to show only bookmarks with that tag
7. **Click a bookmark** — to open the link in a new tab 
### Stretch (build if core is done)

- Import/export bookmarks as JSON file (backup and restore)
- Dark mode toggle
- Keyboard shortcuts (e.g., `/` to focus search)

## UI Layout

Single-page layout with three sections stacked vertically:

```
┌──────────────────────────────────────────┐
│  Bookmark Manager              [search]  │  ← Header
├──────────────────────────────────────────┤
│  URL:   [___________________________]    │
│  Title: [___________________________]    │  ← Add/Edit Form
│  Notes: [___________________________]    │
│  Tags:  [___________________________]    │
│                            [Save]        │
├──────────────────────────────────────────┤
│  Tags: [all] [reference] [tutorial] ...  │  ← Tag filter bar
├──────────────────────────────────────────┤
│  ┌────────────────────────────────────┐  │
│  │ Example Site            [edit][del]│  │
│  │ https://example.com               │  │  ← Bookmark card
│  │ A useful reference for X.         │  │
│  │ #reference  #web                  │  │
│  └────────────────────────────────────┘  │
│                                          │
│  ┌────────────────────────────────────┐  │
│  │ Another Bookmark        [edit][del]│  │
│  │ ...                               │  │
│  └────────────────────────────────────┘  │
└──────────────────────────────────────────┘
```

- **Header**: App title on the left, search input on the right
- **Form**: Collapsible or always-visible. When editing, pre-fills with existing values
- **Tag bar**: Horizontal row of clickable tag pills. "All" resets the filter
- **Bookmark cards**: Stacked list. Each card shows title, URL (as a clickable link), notes, and tags. Edit and delete buttons in the top-right corner

### Responsive behavior

- On narrow screens (< 600px), the form and cards go full-width
- Tag bar wraps to multiple lines if needed

## Project Structure

```
bookmark-manager/
├── index.html      ← page structure
├── style.css       ← all styles
├── app.js          ← all logic
├── DESIGN.md       ← this file
└── README.md       ← (later) how to run and use the app
```

## Key Concepts You'll Practice

- **DOM manipulation**: creating, updating, and removing elements with JavaScript
- **Event handling**: form submissions, clicks, keyboard input
- **localStorage**: reading and writing JSON data that persists across page reloads
- **CSS layout**: flexbox for the tag bar, card layout, and responsive design
- **Data filtering**: searching and filtering an array of objects in JavaScript
- **Form validation**: checking required fields and URL format before saving

## Development Order

Build and test in this sequence:

1. Static HTML structure and CSS (get the layout looking right with fake data)
2. Add bookmark form → saves to localStorage → renders in the list
3. Delete bookmark
4. Edit bookmark (reuse the add form)
5. Search (filter as you type)
6. Tag filter bar
7. Stretch features if desired
