# Notes related to expected output (structure) and prompt preparation

for the prompt:
- "relative order": if events start at the same time, use the same number
- "type_of_time":"choose between: Absolute time, Relative time, Event-anchored time, No indication
- "duration": unit list to be given (centuries, decades, years, months, days, hours, minutes, seconds)
- "span": is set to 0 if immediate succesion or overlap between events ; Null if no information

questions :
- do we leave aside "who", "location"
- at this stage we do not specify the type of link between events (causal, overlap, included in, main/secondary event) but we accept connected events even without temporal information


# Notes on the expected output after applying to corpora

**Attempts on using initial schema in the following corpora :**
- ENC : 
    - newspapers
    - no parallel corpora zh/en
    - en : time markers are mostly relative + missing event years
    - zh : "before" "before", differences between utterance time and event time

- TW :
    - reported political speeches
    - pb of correspondance between filenames + not exact translation (ex : po_en_1669.txt is summary and po_zh_8342.txt is the whole speech)
    - zh time expression is "today" vs english time expression is the date
    - hypotheticals and conditionals, are they events or not ?
    - sometimes very precise (day of week "Wednesday"), keep it and not just in text
    - very fine-grained events (minute-long events, such as "X talked to Y", "X met Y") : do we keep them ? Or do we stop at a higher granularity ?

- INSCR :
    - commemorative discourse
    - fixed kind of events (construction :construction, repairs, destruction, failure ; officials coming and going; commemoration itself)
    - time expressions : dynasty, era, sexagenary year => granularity of year/month/day
    - qualifiers of time expressions

**Raised questions :**
1. Level of granularity + information retained depends on end task + genre of corpora (what do we want to do with this corpora ?)
2. Do we care about the corpora or is it a support for LLM experimentations ?
3. How to name the events ? We chose the name of events in gold standard by hand. We should not let the LLM chose it when extracting to avoid semantic drift. The "event_name" would be the extracted text (the mention).  


**What was missing from the original schema :**
- schema on the possible type of relations between events (James F Allen's interval-based temporal logic)
- punctual events + recurring events 
- utterance time vs event time => impacts the "before" and relative times of events, especially in commemorative discourse, political discourse and newspapers
- probable events that did not happen or should happen => out of scope for the task but still interesting to keep

**Issues with current schema**:
- span_between is vague for most events, cannot have such a precise tuple 
- topic_record : why a person's name ? entity-centric vs event centric views => proposition to change to corpus' name
- we disagree with storing a relation between events within an event ("relative_order")

**Solutions :**
- keep reference of span in text (start_char, end_char)
- add a field "event_type : recurrent, punctual, durative
- in case of punctual events, time_end is Null and is not useful. In case of range events, end_date might also be null if unknown ("she will be working as a teacher starting Monday")
- new field "utterance time" => to be filled from metadata
- new field "event time" => as given in the text
- for time fields, addition of a XXXX scheme if information is unknown + use of dynasties, era, era year, era month, era day format for TPGJ. Example : XXXX-07-03

**Working hypotheses**:
1. An event is a happenstance mentioned in the text alongside a time marker (date, "last week", "during a meeting", etc.)
2. We put aside future events expressed with conditionality ("should", "is expected to", etc.)
3. Time markers can be relative to other events ("after the meeting", "before he accepted the engineering job")


**Summary of changes made to schema**:
- events :
    - removed event_name to replace with event_text
    - refined event_location
    - added event_type
    - added precision to time_start and time_end formats
- event_relations :
    - replaced span_between by relation_type (folows a more defined logic)
    - removed source_files because they are dedicuble from events using event_id

Now, who is event A and who is event B is important because relation_types are directed. 