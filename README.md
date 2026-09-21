# Wave One Herbarium

A static explorer for the first Plant Card v3 content wave: 50 plant species
generated with gpt-5.4 and localized into English, Spanish, German, French and
Portuguese, as generated on staging on 2026-09-20.

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
- **Eight species carry a `validation` entry.** Those are fields where the
  generated care text disagreed with the card and deterministic checks overruled
  it: five on watering, three on pot size. The explorer marks them in place.

## Provenance

`sourceHash` on a non-English record is the hash of the English content it was
translated from; a mismatch means the translation is stale. `usage` records the
token counts for every model call, which is where the cost figures come from.

Data is a point-in-time export from staging and is not kept in sync.
