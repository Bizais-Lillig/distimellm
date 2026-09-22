# enc-cmn-schema-fitcheck — original-schema fit-check on ENC/cmn

Four documents annotations filled against the original schema (`d8ac056`, before this branch's changes). Texts in `texts/`, JSON + notes per case in `annotations/`. Redone against the current schema at repo root in `/annotations/` (`annotations_enc_exp_cmn_SPSP192606271118.json`, `..._SPSP192708311019.json`, `annotations_enc_rotary_cmn_SPSP193109022001.json`, `..._SPSP192506121501.json`).

Finding from redoing them: the top-level key moved from a person's name to a corpus path (`"ENC/exp/cmn"`, like CMallart's `"ENC/rotary/eng"`), that fixes B, C, and D below, without anyone forcing it.

| Case | Document                                          | Fills?     | Held                                                | Broken                                                                                                                  |
| ---- | ------------------------------------------------- | ---------- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| A    | 沈鴻來 scholarship profile (`SPSP192606271118`) | Mostly     | event naming, in-text dates, the one clear relation | undated intermediate event; no field for an unrealized future event ("不日學成歸國"); silent 民國→Gregorian conversion |
| B    | 黃倩儀 + sister 黃倩鴻 (`SPSP192708311019`)     | Undefined  | each subject's own per-event fields, in isolation   | no rule for >1 subject; the shared founding event has no single home                                                    |
| C    | Rotary meeting notice (`SPSP193109022001`)      | Degenerate | the single action's own fields                      | named person has zero biography; the real subject (the club) isn't a person and can't be a key at all                   |
| D    | Inter-club telegram (`SPSP192506121501`)        | No         | nothing                                             | no individual named anywhere, no valid`topic_record` key exists without inventing one                                |
