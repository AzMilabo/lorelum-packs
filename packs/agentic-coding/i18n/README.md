# Localization

This directory contains localized companion content for the `agentic-coding` Pack. Localizations help people read and discuss Practices; they are not separate runtime Packs or retrieval sources.

The canonical English files in [`../practices`](../practices/) remain the only source of truth for Practice IDs, metadata, anti-pattern IDs, installation, validation of runtime content, and retrieval behavior. When a localization conflicts with its canonical file, the canonical file governs.

## Layout and maintenance

- Put each locale under `<locale>/practices/` and preserve the canonical Practice's relative path.
- Localized Practice files contain a translated title and the six translated body sections only. They do not duplicate runtime frontmatter or IDs.
- Translate the complete meaning of the trigger, guidance, anti-pattern, rationale, exceptions, and example. Do not add rules or change their strength.
- Keep commands, code identifiers, canonical IDs that appear in prose, and technical names unchanged where translation would make them ambiguous.
- Let Lorelum generate localization synchronization metadata from formatted canonical Markdown. Do not calculate or edit source digests by hand.

Locale coverage may be partial unless a Pack policy requires completeness. A localization is current only when its recorded source digest matches the formatted canonical file it was translated from.
