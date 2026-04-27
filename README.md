# Cyberpunk Artist Portfolio

A premium dark cyberpunk React + Vite static portfolio with a 3D animated background, neon/glow accents, glassmorphism, smooth animations, and a built-in Decap CMS admin panel for editing all content from your browser. Designed to be deployed on **Netlify** in under 5 minutes.

## Stack

- **React 19 + Vite 7 + TypeScript**
- **Tailwind CSS v4** with custom cyberpunk theme tokens (CMS-editable colors)
- **react-three-fiber + drei** — 3D animated hero background (graceful CSS fallback)
- **framer-motion** — page and element animations
- **wouter** — lightweight client-side routing
- **Decap CMS** — git-backed content editing UI at `/admin/`
- **js-yaml + marked** — markdown content parsing at build time

## Quick start (local)

```bash
npm install
npm run dev
```

Open http://localhost:5173

To preview the production build locally:

```bash
npm run build
npm run serve
```

## Deploying to Netlify

You have two options.

### Option A — Connect via Git (recommended, gives you CMS)

1. Push this folder to a new GitHub repo (public or private).
2. Go to https://app.netlify.com → **Add new site** → **Import from Git**.
3. Pick the repo. Netlify auto-detects settings from `netlify.toml`:
   - Build command: `npm install && npm run build`
   - Publish directory: `dist`
4. Click **Deploy**.

### Option B — Netlify Drop (drag-and-drop, fastest)

You can either:
- **Drop the unzipped source folder** at https://app.netlify.com/drop. Netlify will read `netlify.toml`, install deps, run the build, and publish `dist/`. No Git needed.
- **Or build locally first** (`npm install && npm run build`), then drop just the resulting `dist/` folder.

> Note: If you drop only `dist/`, the CMS admin and SPA redirects still work because `netlify.toml` is also bundled into the publish output via the public folder structure. For the admin/CMS to actually save changes, you must use Option A (Git-connected deploy) so Decap CMS can commit content back to your repo.

## Enabling the admin / Decap CMS (5 minutes after first deploy)

The admin panel lives at `https://your-site.netlify.app/admin/`. To activate it:

1. **Enable Identity** — In your Netlify site dashboard: *Site configuration → Identity → Enable Identity*.
2. **Enable Git Gateway** — Same Identity page: scroll to *Services → Git Gateway → Enable*.
3. **Set registration to invite-only** (optional but strongly recommended): *Identity → Registration preferences → Invite only*.
4. **Invite yourself** — *Identity → Invite users → enter your email*.
5. Open the invitation email, set your password, and you'll land on `/admin/` logged in.

You can now edit:
- **Site Settings** — site title, logo, theme colors (primary, secondary, accent), social URLs
- **About page** — bio, profile image, skills, timeline
- **Contact page** — contact details, blurb, contact methods
- **11 Portfolio Categories** — title, description, cover image, slug, order
- **Portfolio Items** — title, category, cover image, gallery (image/video/YouTube/Vimeo), description, featured/visible flags, order

Every edit becomes a Git commit, which triggers a Netlify rebuild — usually live in ~30 seconds.

## Project structure

```
.
├── content/                 # All editable content (CMS commits here)
│   ├── settings/            # site.json — global settings & theme
│   ├── pages/               # about.md, contact.md
│   ├── categories/          # one .md per portfolio category
│   ├── portfolio/           # one .md per portfolio item
│   ├── skills/              # skill chips for About page
│   └── timeline/            # timeline entries for About page
├── public/
│   ├── admin/               # Decap CMS UI (config.yml + index.html)
│   ├── uploads/             # CMS-uploaded images
│   ├── favicon.svg
│   └── opengraph.jpg
├── src/
│   ├── App.tsx              # Routes
│   ├── main.tsx             # App entry
│   ├── index.css            # Cyberpunk theme + global styles
│   ├── pages/               # Home, Portfolio, Category, Item, About, Contact, NotFound
│   ├── components/          # Layout, ThreeBackground, Gallery, etc.
│   ├── lib/                 # content.ts (markdown loader), types.ts
│   └── hooks/               # useDocumentMeta, etc.
├── netlify.toml             # Netlify build & redirect config
├── vite.config.ts
├── tsconfig.json
└── package.json
```

## Editing the CMS schema

The CMS schema lives in `public/admin/config.yml`. You can add, remove, or rename fields and collections. After editing, commit & push — Decap will pick up the new schema on the next admin page load.

## Theming

Theme colors are defined in `content/settings/site.json` under `theme.{primary, secondary, accent}` as hex values. They are applied at runtime as CSS custom properties (`--color-primary`, etc.). You can change them from the CMS without redeploying styles.

## License

Use freely for personal or commercial portfolios.
