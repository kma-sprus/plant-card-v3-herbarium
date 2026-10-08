# Wave One Herbarium

A static explorer for the first Plant Card v3 content wave: 50 plant species
generated with gpt-5.4 and localized into English, Spanish, German, French and
Portuguese. First generated on staging on 2026-09-20, then regenerated on
2026-10-08 with prompt version v3.1: pot sizes are now a single category,
the humidity care action is tied to the humidity band, and the light guidance
is one short sentence.

Open the site, or read `data/` directly.

## What is here

| Path | Contents |
|---|---|
| `index.html` | The explorer. No build step, no dependencies beyond Google Fonts. |
| `data/index.json` | One summary record per species: rank, names, taxonomy, badges, cost. |
| `data/sp-<id>.json` | One species in full: identity, linked cards, and the generated card and care-details content in all five languages. |

## Reading the content

Each species carries, per language, the card shown in the app (description,
plant needs, care plan, care tips, common issues, symbolism) and the extended
care details (13 plant-needs blocks, 11 care-guide blocks, advice, pests and
diseases, FAQs, interesting facts).

Two things surprise people on first read:

- **The closed-set values stay in English in every language.** Fields like
  `wateringNeeds` or `careDifficulty` are vocabulary keys, translated at request
  time from dictionaries rather than by the translation model. A German record
  reading `Keep Soil Moist` is correct. The free prose around them is genuinely
  translated.
- **Eleven species carry a `validation` entry.** Those are fields where the
  model's answer disagreed with a deterministic check and was overruled: seven
  pot-size labels re-derived from the stated diameter, four watering levels in
  the care details re-aligned with the card. The explorer marks the pot-size
  ones in place; the watering ones sit in the care-details grid.

## Provenance

`sourceHash` on a non-English record is the hash of the English content it was
translated from; a mismatch means the translation is stale. `usage` records the
token counts for every model call and is cumulative: a regenerated row keeps
the earlier generation's entries, so the explorer prices only the latest
generation.

Data is a point-in-time export from staging and is not kept in sync.
