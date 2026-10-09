When interacting with Cloudflare, use the cf CLI unless the project has a Wrangler configuration file.

<!-- prototype-kit:rules v5 -->
## Prototype kit rules (installed by the prototype-kit skill; edit the skill, not this block)

The `prototype-kit` skill (`~/.claude/skills/prototype-kit/`) provides the prototype environment tools: the chrome panel
(flow starting points, Desktop/Tablet/Mobile switcher, default sizes, resizable device frame, liquid-glass capsule,
⌘\ / Ctrl+\ to hide, system toasts, demo hints), the inspector panel (Figma-style, key `I`) and the local dev server.

- **Reuse the kit — never re-implement it.** Whenever a prototype needs any of these tools — new prototype, React/Vue/Vite
  project, or an old prototype carrying its own copy — load the skill and plug in the kit's files
  (`kit.py new` / `update-chrome` / `vite`); never write or hand-port your own version.
- The chrome ships with the prototype (it is deployed); the inspector never does (local dev only).
- System messages about the prototype's limits ("isn't designed yet", "only page 1 is designed", "isn't part of the
  prototype") always use the kit's toast: `data-action="soon"` / `data-soon="…"` or `ProtoChrome.toast(msg)` —
  never a hand-made toast.
- Demo hints beside the device (prototype rules the viewer can't guess: registered vs new email, right vs wrong code)
  always use the kit's hint card: `hints` in `ProtoChrome.init` / `ProtoChrome.hint(def)` — never a hand-made card.
- Never edit the kit folder itself; project tweaks stay in the project. A change for everyone = a merge request to the
  kit's git repository (see the kit's README), merged by its owner. Update the kit with `git pull`.
<!-- /prototype-kit:rules -->

## Frontend skills: when to use them

**Load automatically when writing code** (no need to ask):
- `modern-javascript-patterns` — any JS/TS: ES6+, async/await, modules, no legacy patterns.
- `vercel-react-best-practices` — any React code (write, refactor, review). For Vite/SPA prototypes apply the
  client-side rules (re-renders, bundle, rendering, JS perf); skip the Next.js/server-only rules.
- `vercel-composition-patterns` — when designing or refactoring React components and their props API
  (compound components, context, no boolean-prop sprawl, React 19 APIs).
- Web Interface Guidelines (rules behind `web-design-guidelines`) — follow them while writing HTML/CSS/JSX:
  semantic elements, labels/aria, `:focus-visible`, form attributes, no `transition: all`, transform/opacity
  animations, `prefers-reduced-motion`, img width/height. Don't run the full review unprompted.

**Only when the user asks:**
- `web-design-guidelines` — full UI audit ("проверь UI", review, accessibility check) with `file:line` findings.
- `frontend-design` — aesthetic direction / visual concept for a new UI.
- `ui-ux-pro-max` — styles, palettes, font pairings, design-system generation.
- `review-animations` — animation/motion code review ("проверь анимации"). Has `disable-model-invocation: true`.

**Priority:** a project design system (e.g. `ds/CONTRACT.md`) and the prototype-kit rules always win over any skill.
Visual skills never override the project's tokens or components.

## WordPress skills: when to use them

Official skills from `WordPress/agent-skills`. In a WordPress project (theme, plugin, `wp-content`, WP site repo) start
with `wordpress-router` — it classifies the repo (`wp-project-triage`) and routes to the skill below:
- `wp-plugin-development` — hooks, data storage, settings, security (nonces, capabilities, sanitize early / escape
  late, prepared queries). Also for a classic theme's `functions.php` / `inc/*` and mu-plugins.
- `wp-rest-api` — custom endpoints: `register_rest_route`, argument schema, `permission_callback`, response shape.
- `wp-wpcli-and-ops` — WP-CLI: content seeding, db export/import, safe search-replace between environments.
- `wp-env` — local WordPress in Docker (`@wordpress/env`).
- `wp-performance` — backend profiling: WP-CLI profile/doctor, Query Monitor, autoloaded options, object cache.
- `wp-phpstan` — PHPStan setup and fixes for themes / plugins.
- Block route only: `wp-block-development` (block.json, dynamic render), `wp-block-themes` (theme.json, templates),
  `wp-interactivity-api` (`data-wp-*` directives), `wp-patterns`.

No skill covers classic PHP themes + ACF or Polylang — those conventions live in the project's `CLAUDE.md`.

## Personal additions

Personal, not shared rules live in `CLAUDE.personal.md` next to this file (gitignored):

@CLAUDE.personal.md
