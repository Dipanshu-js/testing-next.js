<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the **DevEvent** Next.js App Router project. Here's a summary of all changes made:

- **`instrumentation-client.ts`** (new) — Client-side PostHog initialization using the recommended Next.js 15.3+ pattern. Initializes `posthog-js` with a reverse proxy host (`/ingest`), exception capture for automatic error tracking, and debug mode in development.
- **`next.config.ts`** (updated) — Added reverse proxy rewrites so PostHog ingestion and static asset requests are routed through `/ingest/*` on the same origin, improving ad-blocker resistance and data quality.
- **`components/ExploreBtn.tsx`** (updated) — Added `posthog.capture('explore_events_clicked')` inside the existing click handler to track top-of-funnel hero button engagement.
- **`components/EventCard.tsx`** (updated) — Added `"use client"` directive and `posthog.capture('event_card_clicked')` with rich event metadata (title, slug, location, date, time) to track which specific events users show interest in.
- **`components/Navbar.tsx`** (updated) — Added `"use client"` directive and `posthog.capture('nav_link_clicked')` with `nav_label` and `nav_href` properties on all navigation links to understand navigation patterns.
- **`.env.local`** (new) — PostHog API key and host added as `NEXT_PUBLIC_POSTHOG_KEY` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables.

## Tracked events

| Event Name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicked the 'Explore Events' hero button | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicked an event card; includes title, slug, location, date, time | `components/EventCard.tsx` |
| `nav_link_clicked` | User clicked a navbar link; includes label and href | `components/Navbar.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- 📊 **Dashboard — Analytics basics**: https://us.posthog.com/project/319723/dashboard/1297358
- 📈 **Explore & Event Card Clicks Over Time** (daily trend line): https://us.posthog.com/project/319723/insights/7RcVnRDn
- 🔽 **Event Discovery Funnel** (explore → event card conversion): https://us.posthog.com/project/319723/insights/sYb65F6Z
- 🏆 **Most Clicked Events** (breakdown by event title): https://us.posthog.com/project/319723/insights/K2s9PvL4
- 🧭 **Navigation Link Popularity** (breakdown by nav label): https://us.posthog.com/project/319723/insights/m991Gtur
- 👥 **Weekly Active Users by Action** (week-over-week unique users): https://us.posthog.com/project/319723/insights/pIx9fhAs

### Agent skill

We've left an agent skill folder in your project at `.claude/skills/posthog-integration-nextjs-app-router/`. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
