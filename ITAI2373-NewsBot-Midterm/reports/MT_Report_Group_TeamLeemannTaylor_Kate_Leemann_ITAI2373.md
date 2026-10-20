# NewsBot Technical Report

Kate Leemann and Roderick Taylor | ITAI 2373<br/>Post-submission correction | Reproducible prototype


## Purpose and revision history

NewsBot is an integrated prototype for editorial routing and media monitoring. It processes English news text, predicts one of five topics, extracts entities, and summarizes sentiment and grammatical patterns. The target user is an analyst who reviews the outputs; automated decisions and business time savings have not been validated.


This report documents corrections made after the original submission. The submitted notebook, README, and outputs remain in archive/submitted/. Revised results below are generated from the corrected notebook using the supplied BBC CSV. Preserving both states makes changes and claims traceable.



## Dataset and scope

The BBC News Classification file contains 1,490 labeled articles. Removing 50 exact duplicate texts leaves 1,440 articles across Business, Entertainment, Politics, Sports, and Technology. The assignment permits the recommended BBC dataset and requires at least four categories; Health is therefore not claimed as a supported category.


A fixed, stratified 80/20 split provides 1,152 training records and 288 test records. Missing and empty text/labels are removed; conflicting exact-duplicate labels and dataset-size violations trigger checks. Near-duplicate stories are not yet grouped. The supplied source text is lowercase, reducing cues for grammar and named entities.



## Course alignment and access

The assignment numbers TF-IDF, POS, syntax, sentiment, classification, and NER as components 3-8. The corresponding course modules are 4, 5, 6, 7, and 8, with classification and NER sharing Module 8. Audio topics are outside the explicit NewsBot requirements. The system uses scikit-learn, spaCy, NLTK, pandas, and plotting libraries on CPU.


Repository: https://github.com/SCheeses/Kate-Leemann-AI-Portfolio



## Processing and integration

The revised cleaner decodes HTML entities, separates element and punctuation boundaries, removes script/style content, expands English contractions, and normalizes whitespace. A contextual spaCy lemmatizer replaces noun-default WordNet processing. Stop-word filtering retains no, not, and nor. Original article text is separately preserved for sentiment, NER, POS, and dependencies.


TF-IDF pipelines compare unigrams with bigrams, standard with sublinear term frequency, and vocabulary limits of 2,000 with 5,000 features. Vocabulary and IDF are learned inside each training fold. The model comparison uses three-fold stratified cross-validation and macro F1; the selected pipeline is then evaluated on the existing holdout.



## Linguistic and sentiment components

Cached spaCy documents support article-level POS proportions, dependency features, noun-phrase rates, and NER for PERSON, ORG, GPE, DATE, and MONEY. Category averages give each article equal weight where appropriate. Entity co-occurrence counts shared articles and does not establish factual relationships or resolve aliases.


VADER processes original text using standard positive/negative thresholds. Emotion cues count normalized dictionary lemmas per 1,000 alphabetic tokens. This exploratory baseline ignores contextual emotion, sarcasm, and negation. The dictionary is AI-assisted and is not a validated emotion dataset or classifier.



## Semantic roles and new inputs

Dependency rules provide candidate agents, patients, recipients, and locations with active/passive voice and direct negation. These are approximations, not trained semantic-role predictions. The course example of an instrument acting as a grammatical subject exposes a known failure; the courtroom location is also missed when attached to a noun rather than directly to the verb.


The integrated interface adds terminal punctuation to a headline before combining it with the body, validates nonempty inputs, rejects text with no known TF-IDF features, and returns structured JSON-compatible results. Other unsupported topics may still receive one of the five known labels.



## Measured classification results

The corrected run selected SVM. Existing-holdout performance was 97.57% accuracy and 0.9740 macro F1; Technology recall was 91.49%. The submitted version achieved 96.18% accuracy, 0.9598 macro F1, and 87.23% Technology recall. Differences should not be interpreted as statistically established superiority.


Corrected best CV macro F1 by model: SVM: 0.9791; Logistic Regression: 0.9726; Naive Bayes: 0.9674.


The old holdout already informed error analysis, so this rerun measures behavior on a known split. A new publisher/time-period dataset is needed to assess generalization independently. CV variability, category-specific precision/recall, and individual mistakes should be considered alongside accuracy.



## Verification and observed errors

The full corrected notebook is executed sequentially. Eighteen targeted regression checks exercise the actual notebook definitions: text boundaries, contractions, lemmas, negation, passive roles, recipients, missing inputs, entity types, headline separation, integrated output fields, JSON serialization, and unknown-vocabulary rejection. Synthetic fixtures test behavior and are not real-news accuracy benchmarks.


The original fictional demonstration misidentified Riverside United as a person and merged headline words into a subject. Boundary handling is corrected; entity typing still requires review. Additional role examples deliberately expose the instrument-versus-agent ambiguity. The archive documents the original failures rather than concealing them.



## Implications for analysts

Topic predictions can suggest queues for human review. Entity mentions can help locate coverage; category-level sentiment and grammatical summaries can guide investigation. News sentiment does not measure public opinion, author intent, or media bias. Confidence values are model probabilities, not guarantees; calibration has not been evaluated on independent news.



## Reproduction and deliverables

Download BBC News Train.csv under the applicable Kaggle terms and place it beside the notebook, in data/, or in /content/ on Colab. Alternatively set NEWSBOT_DATASET to its path. Run the setup cell and then all cells in order. The setup uses the current kernel, pinned core dependencies, the small English spaCy model, and NLTK resources.


The project includes the corrected executed notebook, fresh charts and tables, regression checks, setup instructions, this report, and a two-page team reflection draft. Full source articles and extracted source-sentence tables are excluded from public export. The optional video has not been recorded; no video bonus is claimed.



## Limitations and next work

Exact deduplication does not eliminate near-duplicate leakage. The corpus is historical, English-only, single-publisher, and lowercased. NER, emotion, sentiment, and relationship extraction lack representative human-labeled accuracy evaluations. Aliases, pronouns, quotations, passive constructions outside the rules, and prepositional attachments remain limitations.


Next steps are independent current-news testing, explicit annotation guidelines, small manual extraction evaluations, entity alias resolution, and an evaluated human-review workflow. Any additional feature experiments should use training-only model selection and an untouched final evaluation set.



## Contributions, sources, and assistance

Kate Leemann and Roderick Taylor report equal shared work. The reflection requires their confirmation of individual experiences. OpenAI ChatGPT/Codex provided substantial implementation, debugging, analysis support, and documentation drafting, including this post-submission correction.


Sources: instructor NewsBot assignment and starter notebook; ITAI 2373 Modules 2, 4, 5, 6, 7, and 8; BBC News Classification (kaggle.com/competitions/learn-ai-bbc/data); scikit-learn.org/stable; spacy.io/usage; nltk.org; github.com/cjhutto/vaderSentiment; github.com/kootenpv/contractions. The private course files and raw BBC dataset are not redistributed.


Repository: https://github.com/SCheeses/Kate-Leemann-AI-Portfolio
