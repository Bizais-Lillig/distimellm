# Notes from Shueh-Ying Liao, Paris team

Background, references and reasoning for ideas I brought to the Paris discussions, on the whiteboard or aloud (21–24 September 2026; below, day 1 = Tuesday 22 September, day 2 = Wednesday 23 September). The shared decisions themselves are already recorded in `Notes_output_and_prompt.md` and in the structure `extracted_eventime_structure.json`.

---

## 1. Relation types: Allen's interval algebra

Relations between events should follow Allen's interval algebra rather than a single ordering index. I brought it to the Paris discussion on day 1; the shared structure now uses its seven directed types: before, equals, overlaps, during, starts, finishes, meets. (Ref. James F. Allen, "Maintaining Knowledge about Temporal Intervals", Communications of the ACM 26(11), 1983, pp. 832–843.)

The author defines 13 mutually exclusive relations: six pairs of inverses, plus equals. Because our relations are directed (A→B), the seven types cover all 13: "A after B" is written "B before A". This is why it matters which event is A and which is B. For recurring events, during covers the case raised on day 2 in [Marie&#39;s comment on #1](https://github.com/Bizais-Lillig/distimellm/issues/1#issuecomment-5788258102) ("he went to the swimming pool everyday during these three years"): each visit is during the three-year interval, so the relation layer can express it without a separate `event_type` field.

## 2. Forward and backward verification

A single score cannot tell a model that reasons from a model that guesses. I proposed on day 1 to ask the same fact in both directions: forward as a question ("which came first, A or B?"), backward as a fact verification ("A came before B: true or false?"), and to report how often the two answers agree. A model that is right one way and wrong the other is not reasoning: it is guessing from word order or co-occurrence, or recalling a sentence it has seen in one direction only. A model that has memorised the whole text may pass both ways. A second test, which I also proposed on day 1, answers what the first cannot: remove every time expression from the text and ask the same questions again. A model that still orders the events correctly is not reading the dates: it is depending on its memory of the text, or on the logic of the narrative (a death comes before a burial). The gap between the dated and the undated scores shows how much of the result the text itself supports.

## 3. Reference time as a second layer

Relations between events are one layer; a reference time is the second. I suggested it on day 2. Some texts mix narrated events with moral judgment (and quotation). Older Chinese records are often interwoven with both. A reference time (tied to a type of event) gives each event the point of view from which it is narrated, and only then do the relations become usable. For example, `ENC/rotary/cmn/SPSP192506121501.txt` (申報, 12 June 1925) reports a telegram exchange between the Tianjin and Shanghai Rotary clubs. 日前 is anchored to the date of the newspaper, 當即 to the receipt of the telegram. Without a reference-time layer, the relations between these events, and between them and the unrest it mentions (目今風潮), cannot be stated. This is distinct from the utterance time already kept in the structure (`sources`, the date of each document): the utterance time is when the text speaks, the reference time is the moment the narration takes as its "now" for a given event. So we need at least three kinds of time: utterance time, reference time and event time, with the temporal or logical relations between events defined within the scope of a reference time.

## 4. Factuality: events that did not (or not yet) happen

The original structure has no way to tell us if an event is planned, reported, expected, negated or hypothetical. I proposed on day 1 to add one field for this with a standard vocabulary rather than inventing one during our annotation. For example, `ENC/exp/cmn/SPSP192606271118.txt` (申報, 27 June 1926): 不日學成歸國, "will return home shortly, having completed his studies". The return is expected, not realised.

## 5. Chinese calendar: do not convert every Chinese time expression

Prompt V3 keeps dates as written in the text (dynasty, era, reign, sexagenary, month, season, double hour) instead of converting them. I raised these points on days 1 and 2:

- Lunar months are not Western months. Each month begins on a new moon (朔) and has 29 or 30 days, and a year may have a thirteenth, intercalary month (閏月). In the Song and Yuan, 三月一日 falls, for example, on 17 March in 1181 and on 15 April in 1211 (Julian dates). 三月 is an interval, not "March".
- Double hours (時辰). 子時, 丑時… are two-hour intervals, so they belong in the (min, max) tuples, not in a single time point.
- Sexagenary dates (干支). A 干支 year recurs every 60 years and a 干支 day every 60 days, so neither can be placed without the reign era and the month.

So normalisation should be a separate step, after extraction. It should also record which calendar table it used. We can use Academia Sinica's converter (兩千年中西曆轉換, https://sinocal.sinica.edu.tw/), which converts Chinese dates from 1 CE to 2100 into Western dates, including intercalary months and sexagenary years and days. I suggest adding such a converter to our pipeline as its normalisation step, so that dates are converted from a calendar table rather than by the model itself.

The project's lexicon, `external_data/sample_tenure_lexicon.json`, lists expressions of time relative to an official's tenure. Calendar expressions and time expressions that are not dates (like phenology, animal behaviour, celestial movement, human activities) could be added alongside it.

## 6. Questions of method from the opening meeting (21 September)

Three questions I raised at the opening, which stay open:

- Genre classification before schema. What counts as an event, and which time expressions matter, depends on the kind of document: a biography, a newspaper notice, a commemorative inscription. The schema should fit the genre, not the reverse: classify the document first, or instruct the model to, then apply the schema suited to it. Giving a date the text does not provide turns reconstructing a record into building a study object.
- Reasoning or memory: on texts a model has probably read during training, a correct date or order may come from memory rather than from the text. How do we tell temporal reasoning from recall?
- What kind of error: when a result is wrong, the cause may be the model, the tokenisation of the text, or the way the text is represented. These need separating before anything is called a finding.
