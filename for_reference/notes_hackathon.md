## 1. How do we identify events?
- manually?
- extract event along with the timeline
- what is the impact of the length of the texts
- clear instructions, steps
- the issue of replicability
- events/ consensus
- RAG ? Pipeline that narrows down the sections of the text that are useful?
- Is CKIP useful? https://github.com/ckiplab/ckiptagger

Different methods:
- rule based extraction
- supervised machine learning approach (annotate + train)
- deep learning

While sleeping, he dreamed of ... who, two years before, had ...

## Bibliographical notes

### Lande Dmytro and Strashnoy Leonard. LLM Reconstructions of the Text Narrative With and Without the Time Markers (October 26, 2024). Available: http://dx.doi.org/10.2139/ssrn.5000687
- notion d'hypergraph
- liens entre événements caractérisés : association, cause-consequence
- sequence / ordre des événements

Mais pas de proposition de structure très pertinente pour notre projet.

### Narrative-of-Thought: Improving Temporal Reasoning of Large Language Models via Recounted Narratives (Xinliang Frederick Zhang, Nick Beauchamp, Lu Wang)

"We propose a new prompting technique tailored for temporal reasoning, NARRATIVE-OF-THOUGHT (NOT), that first converts the events set to a Python class, then prompts a small model to generate a temporally grounded narrative, guiding the final generation of a temporal graph."

Très intéressant

Difficulté pour LLMs : la séquence des événements, qui ne correspond pas forcément à la séquence de la narration (en cela, les biographies pourraient être plus faciles à exploiter)

**Prompts pourraient être très utiles :**

"Instruction Type Detailed Instruction

News Report
You are provided with a set of unordered event descriptions.
You are also provided with a set of event relations which instructs you how to temporally link a pair of events.
They are displayed as functions defined within a python class. \n
Your goal is to write a *news report* based on the provided event descriptions and event relations set.
The generated *news report* should adhere to the non-fiction genre.
Meanwhile, the generated *news report* should honor the provided temporal information. \n

Simple English
You are provided with a set of unordered event descriptions.
You are also provided with a set of event relations which instructs you how to temporally link a pair of events.
They are displayed as functions defined within a python class. \n
Your goal is to write a *simple and concise story* based on the provided event descriptions and event relations set.
The generated *story* should be simple such that it can be understood by a 10-year-old child,
and it should be concise such that it can be written within a short paragraph.
Meanwhile, the generated *story* should honor the provided temporal information. \n

Role Play
You are provided with a set of unordered event descriptions.
You are also provided with a set of event relations which instructs you how to temporally link a pair of events.
They are displayed as functions defined within a python class. \n
Your goal is to write a *simple and concise story* based on the provided event descriptions and event relations set.
The generated *story* should honor the provided temporal information. \n
Now, imagine you are a character in the *story*.
Let’s write a *story* that clearly depicts how you, as a character, experience the events, and how you react to them.

Simple Report
You are provided with a set of unordered event descriptions.
You are also provided with a set of event relations which instructs you how to temporally link a pair of events.
They are displayed as functions defined within a python class. \n
Your goal is to write a *simple and concise report* based on the provided event descriptions and event relations set.
The generated *report* should be simple such that it can be understood by a 10-year-old child,
and it should be concise such that it can be written within a short paragraph.
Meanwhile, the generated *report* should honor the provided temporal information. \n"

Evoque un graphe, mais pas d'informations temporelles réellement --> step by step ? Event/chronology/date/duration ?

### Do Large Language Models (LLMs) Understand Chronology? (Pattaraphon Kenny Wongchamcharoen, Paul Glasserman)

Pour séquence chronologique

A tester :  https://github.com/kennywong524/chronollm

Etapes de réflexion et de vérification : "Why does Extended Thinking help? A working hypothesis We do not know the mechanism
within the model that allows for such flawless performance. However, we hypothesize that because
ET grants the model a large, private scratchpad to deliberate before emitting any visible text, this may
enable a reliable internal routine: (1) enumerate all presidents; (2) verify membership against the
criterion implicit in the task; (3) perform pairwise chronology checks; (4) remove any duplicates; and
(5) emit the final ordered list.
Separating thinking from outputting may reduce early-commitment and exposure-bias errors, and it
allows multiple self-checks without incurring user-visible tokens"

Aussi, pour limiter l'anachronisme : " Instead of asking the LLM to order events or
historical figures chronologically, we ask it to reliably judge whether it would be chronologically
possible for an event to occur. "

Enfin, toutes sortes de distances et mesures présentées en fin d'article.

Mais pas de structure proposée

### Benchmarking Temporal Reasoning: Can Large Language Models Navigate Time When Stories Refuse to Follow a Straight Line? (Feifei Sun1 Ziyi Tong1 Houjing Wei1 Cheng Peng1 Teeradaj Racharak2 Minh Le Nguyen)

Pour le ranking, mesure : Kendall

Aborde la question de la manière d'extraire les événéments : en chercher dans chaque phrase ?

**Retient 3 types de temps :**
- Absolute time
- Relative time
- Event-anchored time

Intéressant mais pas de structure proposée

### TIME-LLM: TIME SERIES FORECASTING BY REPROGRAMMING LARGE LANGUAGE MODELS (Ming Jin1∗, Shiyu Wang2∗, Lintao Ma2, Zhixuan Chu2, James Y. Zhang2, Xiaoming Shi2,Pin-Yu Chen3, Yuxuan Liang6, Yuan-Fang Li1, Shirui Pan4†, Qingsong Wen)

Le repo : https://github.com/KimMeen/Time-LLM

Il faudrait prendre le temps d'examiner cette méthode : pas du fine-tuning, une autre stratégie. A tester ?

Pas de format proposé.