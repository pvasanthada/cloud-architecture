# Diagrams

Editable Draw.io XML sources for the six headline architectures in this repository. Open
any `.drawio` file at [app.diagrams.net](https://app.diagrams.net) (File → Open From →
Device) or in the VS Code Draw.io Integration extension.

| File | Corresponds to |
|---|---|
| `hub-spoke.drawio` | `cloud-patterns/hub-spoke.md` |
| `landing-zone.drawio` | `cloud-patterns/landing-zone.md` |
| `zero-trust.drawio` | `cloud-patterns/zero-trust.md` |
| `hybrid-cloud.drawio` | `reference-architectures/hybrid-cloud.md` |
| `ai-platform.drawio` | `reference-architectures/ai-platform.md` |
| `kubernetes.drawio` | `reference-architectures/kubernetes-platform.md` |

Equivalent Mermaid renderings of these diagrams are embedded directly in their corresponding
Markdown documents and render natively on GitHub without any export step. PNGs are not
committed to this repository so diagrams never go stale relative to their editable source —
export one with `drawio --export --format png --output <name>.png diagrams/<name>.drawio`
if you need a static image.
