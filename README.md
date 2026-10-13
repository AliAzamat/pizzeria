# Pizzeria — Vue 3 Storefront

**A pizza-ordering single-page app in Vue 3 with Vuex and Vue Router: a catalog with category filtering, sorting, and search; per-pizza dough type and size selection; a cart that groups identical configurations; and a multi-step admin flow for adding products.** The UI is in Russian.

## Features

- **Catalog** — pizza cards with image, available dough types and sizes, and price per size; category tabs, sort control, and a search bar.
- **Server-side filtering and sorting** — category, sort key, and search are sent as query parameters (`category`, `_sort`, `_order`, `q`) to a json-server-style REST API.
- **Cart** — items are keyed by pizza ID *and* price, so the same pizza in different sizes is tracked separately; increment, decrement (removing at zero), delete, and clear-all with confirmation; totals computed by Vuex getters.
- **Admin screens** — choose a product type (pizza, combo, dessert, drink), then set name, image path, sizes, dough types, prices, rating, category, and list position, with a preview step.
- **Production server** — `server.js` serves the built `dist/` with Express and falls back to `index.html` for client-side routes.

## Tech stack

| | |
|---|---|
| UI | Vue 3, Single-File Components, SCSS |
| State | Vuex 4 (`src/store/index.js`) |
| Routing | Vue Router 4 with hash history: `/`, `/cart`, `/admin`, `/admin/add-product`, `/admin/product-preview` |
| Build | Vue CLI 4 (webpack 4), Babel |
| Serving | Express + `serve-static` |

## Running locally

Requires Node.js. Vue CLI 4 uses webpack 4, which needs the legacy OpenSSL provider on Node 17 and newer:

```bash
git clone https://github.com/AliAzamat/pizzeria.git
cd pizzeria
npm ci

export NODE_OPTIONS=--openssl-legacy-provider   # Node 17+ only
npm run serve        # dev server with hot reload
npm run build        # production build to dist/ (verified to compile)
node server.js       # serve dist/ on $PORT (default 8080)
```

## Data

The app fetches pizzas from a hosted API whose URL is hard-coded in `src/store/index.js`; its current availability wasn't checked. `public/db.json` contains the same catalog (11 pizzas with sizes, types, prices, category, and rating) in the format `json-server` expects, so the store can be pointed at a local `npx json-server public/db.json` instead. Product images are loaded from a third-party CDN.

## Limitations

- **Admin screens are UI only** — they don't send anything to the API, so new products aren't saved.
- The default sort key is spelled `raiting`, while the data field is `rating`, so the initial sort has no effect.
- The initial load requests `/pizzas`, but filter, sort, and search requests go to `/pizzas/pizzas`; only one of these matches a standard json-server setup.
- The cart isn't persisted, and the `start` script in `package.json` is empty — use `node server.js`.
