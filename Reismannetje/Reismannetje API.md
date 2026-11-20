---
tags: [reismannetje, code, api]
---
# Reismannetje API

Alles onder `/api` vereist een sessiecookie en (behalve auth) header `X-Team`.

**Auth**: `POST /auth/register|login|logout|forgot|reset`, `GET /auth/me`, `PUT /auth/email|password`, `DELETE /auth/account`
**Groep**: `POST /teams`, `GET|POST /invite/:code`, `GET /join/:code`, `GET /team/qr`, `GET /unread` → [[Groepen en chat]]
**Inhoud**: `GET /content` (alles van de groep in één keer), `PUT /settings`
**Secties/items (pinnen, vluchten, verblijven…)**: `POST /sections`, `PUT /sections/:id`, `PUT /sections/reorder`, `POST /sections/:id/items`, `PUT /items/:id`, `PUT /items/:id/best`, `POST /items/:id/like`, `DELETE /items/:id`
**Reizen**: `POST /trips`, `PUT|DELETE /trips/:id`, `POST /trips/:id/like`, `PUT /trips/:id/rsvp`, `PUT /trips/:id/stops` ([[Rondreis]]), `POST /trips/:id/todos|plan|expenses|docs`, `PUT|DELETE /todos/:id`, `DELETE /plan/:id`, `PUT|DELETE /expenses/:id`, `PUT|DELETE /docs/:id`, `POST /trip-bundles`
**Datumprikker/stemmen**: `PUT /availability`, `DELETE /availability/:name`, `POST /polls`, `PUT /polls/:id`, `PUT /polls/:id/vote`, `GET /polls/slug/:slug`, `POST /roulette` → [[Datumprikker en stemronde]]
**Hulp**: `GET /nearby/:kind`, `POST /drive`, `POST /link-info`, `POST /upload`, `GET /prices/flight|stay|status`
**Swipen**: `PUT /reactions` (geeft `{match}`) → [[Ideeën en swipen]]
**Prijsalarm**: `POST /watches`, `DELETE /watches/:id` → [[Tickets en prijsalarm]]
**Push**: `GET /push/key`, `POST /push/subscribe|unsubscribe` → [[PWA en push]]
**Live**: `GET /api/live?team=ID[&tv=1]` (SSE) → [[Planavond]]

**Publiek (geen login)**: `/healthz`, `/go?u=`, `/reis/:slug`, `/reizen/:slug`, `/stem/:slug`, `/og/*.jpg`, `/bestemmingen[/:cat]`, `/bestemming/:slug`, `/sitemap.xml`, `/robots.txt`, `/privacy`, `/reset/:token`, `/tickets/:id` (cookie + lidmaatschap).

Zie [[Reismannetje backend]].
