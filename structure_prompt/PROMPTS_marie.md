# PROMPTS

## INSTRUCTION PROMPT
CONTEXT: You are a **[historian / philologist / specialist of literature / political scientist / journalist]**. You have assembled a dataset in which you are looking for information regarding your topic of interest: **[a character / the career or the training of a person / the occurrences of an event / the evolution of a rite or phenomenon / the creation and transformations of a building]**.

ADDITIONAL CONTEXT:

Purpose: Compile all the events and the related temporal information (when, how long) that characterize your topic of interest

Style: Structured

Tone: Neutral

Audience: Experts in your field worldwide

Response Format: A JSON structured text. It necessarily contains "sources" --> the files where the events related to your topic are mentioned, "events" --> the events related to your topic and the afferent temporal information, "event_relations" --> the relations between events stated in the text. 
Expected JSON structure:
{
    "topic_record":
    {
    "sources":"liste de tuples [(filename,date of utterance)]",
    "events":
    [
        {"event_id": "prefix+integer",
        "event_name": "string inspired by one or more texts", 
        "event_sources": "list of tuples: [(filename,[time related expressions])]",
        "relative_order": "an integer, two events can share the same relative order if the happen at the same moment, Null if not even implicit in the text",
        "time_start": "tuple(min_start_timestamp, max_start_timestamp) OR Null)",
        "time_end": "tuple(min_end_timestamp, max_end_timestamp) OR Null)",
        "range": "tuple of tuples: (min(unit,value), max(unit,value)) OR Null"
    }
    ],
    "event_relations":
    [
        {"relation_id": "event_idA_event_idB",
        "event_idA":"",
        "event_idB":"",
        "span_between": "(min(unit,value), max(unit,value)), 0, Null",
        "relation_sources": "list of tuples: [(filename,[time related expressions])]"
    }
    ]
    }
}


INSTRUCTIONS:

Step 1: You read through the dataset in order to identify all the events related to your topic of interest (the events). Keep track of the file in wich you identify these events (the sources). Beware of the order in wich these events appear in each file, as this order might help you order the events in a chronological order. **Here it is possible to add a definition of the kind of events that we are looking for: types of events that should be included.**

Step 2: Look for all the temporal information on each event provided by the text: the temporal expressions as well as the implicit temporal indications.

Step 3: Order the events chronologically by means of integer (an event numbered 1 happened before an event numbered 4). If two events start at the same moment, associate them with the same integer.

Step 4: Identify all the events that are linked with one another (event relations) and look for temporal expressions that can help understand the timespan that separates the two events.

Step 5: Compile the information that you gathered and output a JSON file. Compile in a TXT file all the remarks and doubts that you may have regarding some of the events that you included in or excluded from the JSON file (with indications on the files where these events are mentioned).

Step 6: The JSON filename should be composed of the following elements: topic (no spaces) + "\_timeline\_" + timestamp + ".json". Example : taiwaneseministersofforeignaffairs_timeline_202623021856.json

NOTE:
- All the events in the JSON file NEED TO BE MENTIONED in the files your study, you ARE NOT ALLOWED to add events that are not mentioned in these files.
- It might be useful to think of different types of time: Absolute time, Relative time, Event-anchored time, No indication.
- DO NOT ADD temporal information unless it is deduced from the text.
- The range (the time during which the event happens) will be expressed using measures. Pick among the following ones: centuries, decades, years, months, days, hours, minutes, seconds.
- The span between events is set to 0 if immediate succesion or overlap between events ; Null if no information.
- You might need to convert dates in the Gregorian calendar, tell me in the TXT file if you are not confident in the result (event_id, expression and how you would convert it in the gregorian calendar should you dare to do so). If you are not confident do not add your conversion in the JSON file.
- You shall **include/not include** events that occur in dreams or are fantasized.
- Preserve UTF8 encoding and original text as event name and temporal expressions.


## IN-CONTEXT PROMPT


## SPECIFIC PROMPT