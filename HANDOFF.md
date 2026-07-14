# Safora — Landing page · Developer handoff

A single-page marketing site for **Safora**, the autonomous design-system governance
instrument. Static, dependency-free, ready to implement and deploy as-is.

---

## 1. Files in this package

| File | Role |
|------|------|
| `index.html` | The full page — markup + inline vanilla JS for the animated hero "rosace". |
| `landing.css` | All styling. Design tokens live in `:root` at the top. |
| `safora/logomark.svg` | Brand mark (also inlined in the HTML — kept here for reference). |
| `safora/logo-landscape.svg` | Wordmark lockup (reference asset). |
| `HANDOFF.md` | This file. |

> The HTML only loads **one** external stylesheet (`landing.css`) and the Google Fonts.
> All logos and illustrations are inline SVG/CSS — **there are no image assets to ship.**

---

## 2. Stack & constraints

- **100% static.** No framework, no build step required. Plain HTML + CSS + one inline `<script>`.
- The only JavaScript is the hero rosace animation (bottom of `index.html`). It is vanilla,
  self-contained, and uses `requestAnimationFrame`. **Do not refactor or "optimise" it.**
- Fully **responsive** (breakpoints at 1080px and 720px) and honours
  `prefers-reduced-motion` (animations degrade to a static state).
- Single brand accent (orange `#F4641D`); warm-black shell `#161614`; greige paper `#EBE9E2`.
- Fonts: **Geist** (sans) and **Spline Sans Mono** (mono), with `Helvetica Neue / Arial` fallbacks.

---

## 3. Implementation prompt (paste into Codex)

```
Implémente et déploie cette landing page statique telle quelle.

Fichiers source (à respecter au pixel, ne pas redesigner) :
- index.html     (markup + script vanilla de la rosace animée du hero)
- landing.css    (tout le style ; design tokens en :root)
- safora/        (logos SVG de référence ; le logomark est déjà inline dans le HTML)

Contraintes :
- Site 100 % statique, aucun framework. Le seul JS est inline en bas de index.html
  (animation de la rosace) — ne pas le toucher ni le "refactorer".
- Garder le responsive existant et le support prefers-reduced-motion.
- Conserver la charte : un seul accent orange, fond shell sombre, papier greige.

Modification fonctionnelle — exposition self-serve :
- Garder `SAFORA_LANDING_CONFIG.showPublicAuthAndGitHubCtas` à `true` par défaut.
- Exposer Sign in / Sign up et faire pointer les CTA principaux vers :
    https://app.safora.run/sign-up
- Garder l'ancien lien beta Tally dans `SAFORA_LANDING_CONFIG.betaSignupUrl` uniquement
  comme fallback si le flag est remis à `false`.
- Remplacer la surface publique "Join the beta" par "Start free" sans introduire
  de CTA GitHub séparé sur la landing.

Polices — auto-héberger au lieu de Google Fonts (supprime la dernière dépendance externe) :
- Supprimer les <link> vers fonts.googleapis.com / fonts.gstatic.com et les preconnect.
- Héberger en .woff2 dans /fonts/ :
    • Geist — 400, 500, 600
    • Spline Sans Mono — 400, 500
  (les deux sont en licence OFL, auto-hébergement autorisé)
- Ajouter les @font-face correspondants en haut de landing.css, avec font-display: swap.
- Ne PAS changer les piles font-family dans :root (--font-sans / --font-mono) ni les fallbacks.

Déploiement :
- Hébergement statique (Vercel / Netlify / GitHub Pages).
- Vérifier : aucune erreur console, la rosace s'anime au chargement, le rendu est
  identique sur desktop et mobile.
```

---

## 4. Page structure (top → bottom)

1. **Nav** — sticky, on the dark shell.
2. **Hero** — headline + animated rosace whose orange centre doubles as the "LIVE" dot,
   over a faithful in-frame mock of the product's Command center.
3. **Governance loop** — ingest → audit → fix → confirm → learn (the orange ring marks the
   one human checkpoint).
4. **Honest score** — animated trajectory ruler; "a score never moves on a promise".
5. **Proofs** — spec-sheet hairline cells.
6. **Safety** — contre-jour block, "every change is a pull request".
7. **Knowledge Pack** — the moat.
8. **Pricing** — Free / Solo / Starter (recommended) / Team, Enterprise row, add-ons note.
   Plan limits are expressed in product terms (repos, PR reviews, governance) — raw token
   budgets and overage rates are intentionally kept off the public page (dashboard/billing only).
9. **Final CTA** + **Footer**.

---

## 5. Public CTA exposure

Public auth and platform-start CTAs are gated by `SAFORA_LANDING_CONFIG.showPublicAuthAndGitHubCtas`
near the bottom of `index.html`.

Default public behaviour keeps that flag `true`: Sign in and Sign up are exposed, and
the primary CTA is "Start free" linking to:

```txt
https://app.safora.run/sign-up
```

When the flag is set to `false`, the landing page falls back to the private-beta copy and
uses `SAFORA_LANDING_CONFIG.betaSignupUrl` for "Join the beta".
