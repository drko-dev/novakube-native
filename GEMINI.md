# NovaKube — Gemini / Google Antigravity project instructions

Read [AGENTS.md](AGENTS.md) before any repository work. Its existing branding, architectural boundaries, security rules, milestone gates, QA and i18n requirements are authoritative.

## Mandatory skill for frontend

Before designing, implementing, auditing, or changing HTML/CSS, web UI, Electron renderer UI, or browser/client-side JavaScript, **load and follow** [Modern Web Guidance](.agents/skills/modern-web-guidance/SKILL.md), vendored from https://github.com/GoogleChrome/modern-web-guidance.

Search relevant, focused web-platform topics through `npx -y modern-web-guidance@latest search "focused UI query" --skill-version 2026_11_10-47b4c80e`; retrieve matching guide IDs with `npx -y modern-web-guidance@latest retrieve "<guide-id>"` **before writing frontend code**. Check compatibility, fallbacks, a11y, security, performance, and tests. Do not use this skill for backend-only or infrastructure-only tasks. Preserve existing designs and project scope.

For Google Antigravity, the official additional plugin installation is `agy plugin install https://github.com/GoogleChrome/modern-web-guidance`, when it is not already installed. Do not install it automatically as part of production builds.

- **Canonical governance standard:** `NovaKube-Workspace/docs/standards/FRONTEND_ENGINEERING_STANDARD.md`.
- **Scope in `novakube-native`:** Applies only to web/HTML/CSS/JS companion or documentation frontends (**Baseline Widely available** default). `novakube-native` remains a pure Rust native desktop app (no Electron, Tauri, or WebView).
- **Gemini CLI extension:** `gemini extensions install https://github.com/GoogleChrome/modern-web-guidance --auto-update`. Group queries by feature rather than per file.
