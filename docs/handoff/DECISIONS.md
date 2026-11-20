# Decisions

| Date | Decision | Who | What it means |
| --- | --- | --- | --- |
| 2026-11-20 | Move Bonus Track onto wf-template: repo `brandvm/wf-bonustrack` (public, from the template) | Team (Kajal) | The site gets a repo, workspace, audit baseline and rollback point. The live site is unchanged until each batch's go-ahead. |
| 2026-11-20 | Staging slug `wf-bonus-track` (the real webflow.io subdomain); MCP server named `webflow-bonustrack` | Team | The check scripts use https://wf-bonus-track.webflow.io. The MCP server name follows the client name, not the subdomain, so it differs from the template's `webflow-<slug>` default. |
| 2026-11-20 | Fixes BT-01…BT-12 wait; each batch needs the person's go-ahead, and a live publish needs the word "publish" | Team | Nothing is written to Webflow during setup. |
