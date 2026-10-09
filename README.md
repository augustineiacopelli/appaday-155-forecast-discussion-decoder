# AppADay 155: Forecast Discussion Decoder

Fetches the latest National Weather Service Area Forecast Discussion (AFD) for any forecast office and decodes it into plain English with Claude. Defaults to Wichita (ICT).

**Live:** https://augustineiacopelli.github.io/appaday-155-forecast-discussion-decoder/
**Portfolio:** https://augustineiacopelli.github.io/appaday/

## What it does

The app pulls the newest AFD from the public NWS API (`api.weather.gov/products/types/AFD/locations/{OFFICE}`, then `/products/{id}`), splits it into its sections (Key Messages, Update, Discussion, Short Term, Long Term, Aviation, Fire Weather, and so on), and shows each one as a collapsible card. The office picker lists 121 forecast offices with the four Kansas offices (ICT, TOP, DDC, GLD) pinned first, plus a filter box. An age badge turns green, amber, or red as the discussion gets older, and a notice appears when a newer discussion is issued.

A five segment gravity gauge rates the discussion as Quiet, Routine, Active, Elevated, or High Impact. The level is the higher of a keyword scan of the text and Claude's own severity score, and it tints the hero panel, the hazard chips, and the card accents.

## Claude decoding

Open Settings with the gear button and paste a Claude API key. The key and an optional session name are stored only in this browser's localStorage. The model is read from the portfolio `config.json` (Sonnet tier) with a built in fallback, and requests send `thinking: {type: "disabled"}` with a 4000 token budget.

Pick a voice: News Reporter (default), Plain Talk, Snarky, or Comical. Each decode returns a headline, a summary, hazard chips, and a plain language version of every section with the forecaster's confidence. Decodes are cached per discussion and voice, so switching back to a voice you already used costs nothing.

**Safety rule:** in every voice, hazard facts, timing, location, and uncertainty are stated straight. At Elevated or High Impact a banner reminds readers to follow official NWS watches and warnings. The Preliminary Point Temps table is always shown raw and never decoded.

## Glossary

About 90 meteorology and aviation terms (CAPE, SRH, dryline, QLCS, FROPA, VFR, Zulu times, SPC risk levels, and more) are underlined in both the Original and Decoded views. Tap any one for a definition in a bottom sheet. The glossary and the original text work without an API key.

## Details

Single `index.html`, inline CSS and JS, Google Fonts only. Works offline from the last saved discussion if the NWS cannot be reached.

Category: E (Educational)
AI powered: Yes (Claude API)
