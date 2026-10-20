# Japanese Learning Application

## Motivation & Core Issues

This Japanese learning application was made to address the following issues with current learning apps:

1. Lack of active recall modes (too much focus on passive recognition)
2. Review of isolated words rather than in functional lexical units or collocations (leading to unnatural phrasing habits)

This app is made to guide learners through a staged scaffolding pipeline, from passive comprehension to cloze retrieval to full sentence construction using authentic collocations.

## Resources

### Base Lexicon

This application uses the base open-source lexicon, JPDict, which contains the following information on its words:

1. JLPT level classification (N5-N1)
2. Part of speech (e.g., noun, verb, adverb, adjective, conjunctions)
3. Semantic vocabulary (e.g., jukugo, domain-specific vocab)

### Collocation Extraction & Corpus Linking

Moreover, for common collocations, pairwise mappings are extractedfrom the following empirical Japnaese corpora:

1. NINJAL-LWP for BCCWJ - dependency-parsed (Noun-Particle-Predicate)
2. NINJAL VVLEX - compound verbs (Verb-Verb)

### Offline LLM Augmentation

However, due to this list not being exhaustive, a cheap offline local LLM (such as the Qwen 2.5 via Ollama) or a batched lightweight model will be tasked with discovering missing word pairing mappings in addition to the above-extracted collocations. Queries will anchor on specific nouns/verbs/jukugo in order to prevent combinatorial explosion.

### EXPRESSION Taxonomy

All will be consolidated into a dictionary of EXPRESSIONS.

The following EXPRESSION types comprise the abovementioned dictionary:

1. Connectors & discourse markers (e.g., tokorode, ~monono, ~nisuginai)
    1. Conjunctions
    2. Transitional adverbs
    3. Sentence-ending particles
    4. Formality markers
2. Collocations
    1. Case frames [Noun-Particle-Verb/Adjective] (e.g., shinsei wo dasu)
    2. Paired adverbials [adverbs requiring specific syntactic endings] (e.g., kesshite...nai, marude...noyouda)
    3. Fixed idioms (e.g., atama wo kakaeru)
    4. Compound verbs/grammar stems [lexicalized chains] (e.g., ~kanenai, ukeireru, omoitsuku)
3. Core jukugo/content nouns [high-frequency content words acting as semantic anchors] 

## Game Mechanics

The ultimate goal of this entire game is for the enrichment of the user's vocabulary, hence to be able to study, review, and master every EXPRESSION in the DICTIONARY. Hence, daily reviews rely on random drawing of EXPRESSIONS for learning/review in every session, similar to the mechanics of popular memory and SRS apps, such as Anki.

### Progress Tracking

Due to the fundamental difference in the skills of active recall and passive recognition, a scoring system reflecting the drawability (frequency of draw) of an EXPRESSION is established with three scores.

1. Passive score
    - Frequency accumulation is slow (since it is easier to recall meanings once read)
2. Active cloze score
    - Frequency accumulation is moderate (since it needs more frequent repetition for a user to remember a word based on its surrounding words/context clues)
3. Active build score
    - Frequency accumulation is fast (since it needs constant drilling for a user to use a word in building a phrase/sentence from scratch)

These scores hold a base score reflective of JLPT level and the type of EXPRESSION. Higher-JLPT level words hold less frequency than lower-JLPT level words. As for type of EXPRESSION, the order of high-to-low frequency goes top-down in the above list.

These scores are modified based on progression in the game modes introduced. Higher mastery brings down the drawability score.

### Game Modes

From these, we introduce the following three game modes:

1. Reading challenge (passive recognition)
    1. Agent chooses 4 EXPRESSIONS at random and builds a short passage in Japanese using all of them (furigana included) + an English translation
    2. User reads passage for set amount of time
    3. User answers matching game (word-furigana-English)
    4. Correctness alters passive score for each word
2. Cloze challenge (active recall)
    1. Agent chooses 4 EXPRESSIONS at random and builds a cloze challenge and the corresponding English translation
    2. User figures out what the right EXPRESSION is to put in the blanks
    3. Correctness alters active cloze score based on the following bool criteria accumulating partial points:
        1. Correct collocation used?
        2. Correct tense? (if applicable)
3. Build challenge (active recall)
    1. Agent chooses 4 EXPRESSIONS at random and provides an English translation of the target passage
    2. User tasked with translating the English passage into Japanese
    3. Correctness alters active build score based on the following bool criteria accumulating partial points:
        1. Target collocation used? If not, is the used similar?
        2. Correct particles used?
        3. Core conjugations and clause endings and grammar sound?
        4. Phrasing natural?
    4. Provide the ideal answer using all target collocations in the intended way

The cloze challenge is unlocked once enough EXPRESSIONS have been learned in the reading challenge; the build challenge is unlocked once enough EXPRESSIONS have been learned in the cloze challenge.

### NOTE:
1. Should we save all the created passages?
