# Nothing Design Skill

A design system skill for [Claude Code](https://claude.ai/code) inspired by Nothing's visual language. Monochrome, typographic, industrial.

I kept describing the same design rules to Claude over and over — Swiss typography, OLED blacks, segmented progress bars, dot-matrix motifs. So I packaged it into a reusable skill.

![Preview](preview.gif)

## What you get

Tell Claude `/nothing-design` or say "Nothing style" and it generates UI following these principles:

- Three-layer visual hierarchy (display, body, metadata — that's it)
- Space Grotesk + Space Mono + Doto font stack
- Full dark and light mode token system
- Segmented progress bars, mechanical toggles, instrument-style widgets
- Output as HTML/CSS, SwiftUI, or React/Tailwind

## Install

The easiest way to install this skill is via the `skills` CLI:

```sh
npx skills add dominikmartn/nothing-design-skill
```

### Manual Install

If you prefer manual installation, clone the repository and copy the `skills` folder into your agent's skills directory (renaming it to `nothing-design` for clarity):

```sh
git clone https://github.com/dominikmartn/nothing-design-skill.git
cp -r nothing-design-skill/skills ~/.claude/skills/nothing-design
```

That's it. Next time you start your AI agent (like Claude Code or Gemini CLI), the skill is available.

## What's inside

The skill is located in `skills/`:

| File | |
|------|---|
| `SKILL.md` | Design philosophy, craft rules, workflow |
| `references/tokens.md` | Colors, fonts, spacing, motion tokens |
| `references/components.md` | Buttons, cards, lists, tables, overlays |
| `references/platform-mapping.md` | CSS, SwiftUI, React output mappings |

## License

MIT
