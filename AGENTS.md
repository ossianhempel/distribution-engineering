# AGENTS.md

- This is a plugin for distribution engineering including marketing, branding, copywriting, and positioning.
- It takes inspiration from Every's Compound Engineering (CE) plugin when it comes to structure - both plugin-wise and the "loop-like" workflow with skills that tie into each other and with specialized subagents used by specific skills. 
- This plugin is also "CE-aware" ie it understands terms from CE and can integrate/hook into them when relevant (e.g. CONCEPTS.md, STRATEGY.md, etc). 

The kit we ship within existing repo:

```
brand_atomic_system/
├── readme.md
├── magic_trick.md
├── human/                      ← drop PDF brand guidelines here
└── agent/
    ├── verbal/
    │   ├── positioning.md
    │   ├── audience.yaml
    │   ├── messaging.md
    │   ├── differentiation.md
    │   ├── concepts.md
    │   └── voice.md
    └── visual/
        ├── colors_and_type.css
        ├── fonts/              ← 5 OTFs
        ├── assets/             ← logo + brand assets
        ├── components/         ← 11 UI primitives
        ├── tokens/             ← 25 token specimens
        ├── motion/             ← full motion system (JSON, CSS)
        └── artifacts/
            ├── web/
            └── product/
```