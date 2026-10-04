# Travel Studio — CEO Business Plan & Technical Architecture Specification
**Product Vision:** *"A Private Concierge in Every Traveler's Pocket — Even at 4,400m Altitude with Zero Cell Signal."*
**Status:** MVP Built & Live (`https://youngapple.github.io/travel-studio/`)
**Flagship Case Studies:**
- **Case Study #1 (`global` profile):** [South America 2026 — Patagonia, Glaciers, Amazon & Iguazú (15 Days, 39 Stops)](https://youngapple.github.io/south-america-2026/)
- **Case Study #2 (`cn_domestic` profile):** [Yunnan 2026 — Lijiang, Haba, Shangri-La, Meili & Nanjiluo (11 Days, Private Group)](https://youngapple.github.io/yunnan-2026/)

---

## 1. Executive Summary & The Core Insight

When a private travel group (family expedition, friends' self-drive/charter tour, luxury bespoke agency group, or executive retreat) embarks on a high-stakes journey—whether trekking **Fitz Roy and Perito Moreno Glacier in Patagonia** or crossing **4,292m Baima Snow Mountain Pass into Meili & Nanjiluo in Yunnan**—their actual in-field experience breaks down at the exact moment they leave the hotel Wi-Fi:

1. **Static PDFs & Word Docs Are Dead Weight in the Field**: Nobody wants to pinch-zoom a 25-page PDF on a windy trailhead to find out whether the 14:30 cutoff to Feilai Temple is still achievable.
2. **WeChat / WhatsApp Group Chat Entropy**: Critical reminders, hotel locations, driver contacts, altitude protocols, and Plan A vs. Plan B decisions get buried under hundreds of photos and voice messages.
3. **Generic Consumer Trip Apps Fail on Two Fronts**:
   - They are **empty CRUD shells** (requiring manual entry of every POI without deep local insider context, trail elevation profiles, photography golden hours, or hard cutoff warnings).
   - They **break across network boundaries and offline dead zones**: Google Maps, Wikipedia, and foreign CDNs fail completely for domestic travelers inside China (`cn_domestic`), while online-only apps fail at 4,000m mountain passes, glaciers, and rainforest lodges where cell signal drops to zero.

### The Solution: Travel Studio (`Agenda ──► Pre-Compiled Offline Bespoke Web App`)
**Travel Studio** is an AI-powered **Bespoke Offline Travel Companion Compiler & Hosting Platform**.
Given a simple 10–20 line raw itinerary (dates, stops, hotels, key constraints), Travel Studio **pre-compiles** a tailored, zero-dependency, **100% offline-capable Progressive Web App (PWA)** specifically for that private group, and deploys it in one click to a permanent, shareable URL (starting with **GitHub Pages** for zero-cost global/domestic static hosting, extensible to Cloudflare Pages / Aliyun OSS+CDN).

---

## 2. The 10-Star Product Experience (`/plan-ceo-review` Framing)

- **1-Star Experience**: A text message or Excel/PDF itinerary sent in a group chat.
- **3-Star Experience**: A generic itinerary app (Wanderlog / TripIt) that lists flight/hotel times but requires internet, has no local insider soul, and fails inside China or offline in Patagonia.
- **5-Star Experience**: A custom interactive web page with a map of the stops and daily schedule.
- **10-Star Experience (Travel Studio Standard)**:
  1. **Zero-Friction Input**: The trip organizer pastes a rough 12-line agenda (including unresolved forks like *"D6–D9 Plan A Yubeng trekking vs. Plan B Nanjiluo + Cizhong Church"* or *"Must depart Shangri-La by 14:30"*).
  2. **Total Pre-Marked Spatial Intelligence**: Every single stop, hotel, viewpoint, trailhead, ferry pier, and intermediate pass is pre-marked on an interactive map with **connected day-by-day route polylines**, **segment transport badges (drive km / hike hours / flight)**, and **interactive elevation profiles**.
  3. **In-Field Pocket Guidebook**: Tapping any stop opens a rich drawer with **local insider tips, photography golden-hour angles, must-order local dishes, altitude/safety checklists, timed hard-cutoff alerts**, and curated deep links.
  4. **Region-Native Network Stack (`cn_domestic` vs. `global`)**:
     - For **China Domestic (`cn_domestic`)**: Automatically compiles with **Gaode AMap tiles (`autonavi.com`)**, **GCJ-02 coordinate projection**, one-tap **Gaode/Baidu Maps URI navigation**, **Baidu Baike** encyclopedia entries, **Xiaohongshu (RED)** photo/guide deep links, and **Ctrip/Dianping** restaurant/hotel links—with **zero** blocked Google/Wikipedia/foreign CDN dependencies.
     - For **Global (`global`)**: Compiles with **Carto Voyager / OSM tiles**, **WGS-84 coordinates**, **Google Maps Universal Cross-Platform links**, **Wikipedia / AllTrails / TripAdvisor** deep links, and downloadable **KML layers** for Google My Maps / Organic Maps.
  5. **True Offline-First Pre-Compilation (`sw.js` + `manifest.webmanifest` + LocalStorage)**:
     - The entire HTML, CSS, JS, structured itinerary database, local guides, checklists, and core assets are **pre-compiled into a self-contained bundle** backed by a **Service Worker (`sw.js`)** that caches the app shell AND visited map tiles (`CacheStorage`), plus `localStorage` persistence for group checklists and Plan A/B selections. Open it once at the hotel or airport, and it works **anytime, anywhere with zero bars of signal**.

---

## 3. Business Model & Go-To-Market Strategy

### 3.1 Target Customer Segments
1. **B2B2C — Bespoke Travel Agencies & Private Tour Operators (高定旅行机构 / 私家团定制师 / 户外俱乐部)** *(Primary Revenue Engine)*:
   - Thousands of boutique agencies in China (Yunnan, Xinjiang, Tibet, Sichuan, Qinghai) and globally (Patagonia, Iceland, Safari, Japan, Dolomites) charge **$3,000–$25,000+ per private group**, yet still hand clients a PDF or a generic H5 link.
   - Travel Studio gives them a **white-labeled, agency-branded Offline Companion Web App** generated in 60 seconds from their existing quotation sheet—instantly elevating their perceived service quality and win rate on high-ticket proposals.
2. **B2B — Corporate Retreats, Executive Offsites & Luxury Family Offices**:
   - High-touch group travel where every attendee needs offline schedules, logistics contacts, dietary/safety notes, and pre-marked maps without downloading a bloated native app from the App Store.
3. **B2C Pro — Independent Group Organizers ("The Trip Captain")**:
   - Every group of 4–10 friends or family members has one "Trip Captain" (like `yangshuguo` for South America 2026 or the friend organizing Yunnan 2026). They gladly pay **$9.90–$19.90 per trip** (or **$49/year Unlimited**) to turn their messy notes into a stunning offline web app for their travel companions.

### 3.2 Pricing & Unit Economics
- **COGS per Compiled Trip App**:
  - LLM enrichment + geocoding + static hosting on GitHub Pages / Cloudflare Pages = **~$0.08 – $0.15 per trip**.
- **Pricing Tiers**:
  - **Explorer (Free / Viral Loop)**: 1 active trip up to 5 days, "Built with Travel Studio" badge in footer (drives viral organic acquisition from every group member who opens the link!).
  - **Trip Captain Pro ($15 / trip or $49 / year)**: Unlimited days, Plan A/B branch comparison, full offline Service Worker tile pre-warming, KML export, custom cover photos.
  - **Agency Studio B2B ($199 / month or $15 / client group)**: White-label custom domain (`trips.youragency.com`), agency logo & concierge WhatsApp/WeChat one-tap button, batch PDF/Word-to-App ingestion, live emergency broadcast banner when online.
- **Gross Margin**: **>95%** (pure software compilation + static edge hosting).

---

## 4. Technical Architecture: The 4-Stage Compiler Pipeline

```
┌────────────────────────┐    ┌──────────────────────────┐    ┌────────────────────────────┐    ┌────────────────────────────┐
│ Stage 1: Agenda Parser │───►│ Stage 2: Geo & Guide     │───►│ Stage 3: Region-Adaptive   │───►│ Stage 4: Offline PWA       │
│ (Raw Text / JSON / MD) │    │ Enrichment Engine        │    │ Compiler (CN vs. Global)   │    │ Packager & GitHub Publisher│
└────────────────────────┘    └──────────────────────────┘    └────────────────────────────┘    └────────────────────────────┘
```

### Stage 1: Multi-Format Agenda Parser (`generator.py`)
- Accepts either:
  1. **Raw human-written agenda text** (e.g., `D1 11/21 丽江 宿丽江`, `D3 11/23 14:30前从香格里拉出发去飞来寺`, `D6-D9 方案A雨崩 / 方案B南极洛`), or
  2. **Structured Trip Spec JSON** (`trip_spec.json`).
- Extracts:
  - Day index, date, title, region/hub, overnight hotel;
  - Hard time constraints (`14:30` cutoff, sunrise windows, flight check-ins);
  - Route forks (`Plan A` vs. `Plan B` alternative tracks);
  - Group reminders (altitude sickness protocol, border/visa rules, cash/gear checklists).

### Stage 2: Spatial, Elevation & Local Guide Enrichment
- Resolves every destination and intermediate waypoint into:
  - **Dual Coordinates**: WGS-84 (`lat`, `lng`) + GCJ-02 (`gcjLat`, `gcjLng`) for seamless switching between international and Chinese map engines.
  - **Elevation & Transport Telemetry**: Altitude (`meters`), daily elevation gain/loss, driving distance/time, or trekking distance/duration.
  - **Curated Insider Dossier**:
    - `mustDo` / `highlights`: What actually matters on the ground;
    - `photoTip`: Exact viewpoint & golden-hour timing (e.g., *Feilai Temple 06:45–07:30 Kawagebo Sunrise Golden Peak*);
    - `foodTip`: Authentic local specialties (e.g., *Nixie Black Pottery Tibetan Yak Hotpot*, *Patagonian Cordero al Palo*);
    - `warning`: Actionable safety/logistics alerts (e.g., *Do not wash hair on Day 1 above 3,200m*, *Bring physical passport for Brazilian side of Iguazú*).

### Stage 3: Dual-Network Region Adapter (`cn_domestic` vs. `global`)
The compiler strictly enforces a **Region Profile Contract** at build time:

- **`region_profile = "cn_domestic"` (For China Trips & Domestic Users)**:
  - **Map Tiles**: Gaode AMap Vector/Road (`https://webrd0{1-4}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}`) + Esri World Imagery satellite toggle.
  - **Navigation Deep Links**:
    - Gaode Maps (`https://uri.amap.com/marker?position={gcjLng},{gcjLat}&name={name}`)
    - Baidu Maps (`https://api.map.baidu.com/marker?location={lat},{lng}&title={name}&output=html`)
  - **Knowledge & Discovery Links**:
    - Encyclopedia: **Baidu Baike** (`https://baike.baidu.com/item/{query}`)
    - Visual/Field Guides: **Xiaohongshu (小红书)** (`https://www.xiaohongshu.com/search_result?keyword={query}`)
    - Reviews/Booking: **Ctrip / Dianping** (`https://you.ctrip.com/SearchSite/Default/Destination?keyword={query}`)
  - **CDN & Fonts**: Domestic Staticfile / BootCDN (`cdn.staticfile.net`) + system CJK font stack (`PingFang SC`, `HarmonyOS Sans SC`, `Microsoft YaHei`) — **0 bytes** loaded from `googleapis.com`, `google.com`, or `wikipedia.org`.

- **`region_profile = "global"` (For International Trips)**:
  - **Map Tiles**: CartoDB Voyager (`basemaps.cartocdn.com`) + OpenTopoMap / Esri Satellite.
  - **Navigation Deep Links**: Google Maps Universal URL (`https://www.google.com/maps/search/?api=1&query={lat},{lng}`).
  - **Knowledge & Discovery Links**: Wikipedia (`en.wikipedia.org` / `zh.wikipedia.org`), AllTrails, TripAdvisor, plus downloadable **KML files** for Google My Maps / Organic Maps.

### Stage 4: Offline-First PWA Packager & 1-Click GitHub Pages Publisher
Every compiled output directory contains:
1. **`index.html`**: Self-contained single-page application with all trip data, guides, reminders, checklists, and elevation SVGs pre-compiled directly into the document (zero external API calls required to render the trip).
2. **`sw.js` (Offline Service Worker)**:
   - Pre-caches `index.html`, `manifest.webmanifest`, KML/JSON files, and the map library on install (`install` event with `skipWaiting()`).
   - Intercepts runtime requests with a **Stale-While-Revalidate / Cache-First** strategy—including opportunistic caching of map tiles (`autonavi.com` / `cartocdn.com`) in a dedicated `travel-studio-tiles-v1` cache so panning the map over Wi-Fi automatically caches the tiles for offline use in the mountains!
3. **`manifest.webmanifest`**: Allows one-tap **"Add to Home Screen"** on iOS Safari and Android Chrome/WeChat, launching fullscreen like a native app.
4. **1-Click GitHub Pages Deployment (`generator.py --publish-github <owner>/<repo>`)**:
   - Automatically creates or updates the target GitHub repository, pushes the compiled bundle to `main`, enables GitHub Pages via `gh api`, and returns the live `https://<owner>.github.io/<repo>/` URL.

---

## 5. Validation via Flagship Case Studies

### Case Study #1: South America 2026 (`global` Profile)
- **Live URL**: `https://youngapple.github.io/south-america-2026/`
- **Scope**: 15 Days (Sep 30 – Oct 15, 2026), 5 Regions (Buenos Aires, El Calafate & El Chaltén Glaciers, Puerto Iguazú AR/BR, Manaus Amazon Rainforest, Rio de Janeiro), 39 pre-marked POIs, 5 downloadable KML layers, interactive day-by-day route map, bilingual local guides, and field-tested updates from Patagonia.

### Case Study #2: Yunnan 2026 (`cn_domestic` Profile)
- **Live URL**: `https://youngapple.github.io/yunnan-2026/`
- **Scope**: 11 Days (Nov 21 – Dec 1, 2026) private group itinerary for Lijiang, Haba Snow Mountain (Baishuitai + Tiger Leaping Gorge), Shangri-La (Songzanlin + Napa Lake), Meili Snow Mountain (Feilai Temple), and an interactive **Plan A (Yubeng Trekking) vs. Plan B (Nanjiluo Alpine Lakes + Cizhong Church)** switcher, complete with `14:30` departure hard-cutoff alerts, high-altitude acclimatization checklists, and 100% China-domestic map/guide links (Gaode AMap, Baidu Baike, Xiaohongshu, Ctrip).
