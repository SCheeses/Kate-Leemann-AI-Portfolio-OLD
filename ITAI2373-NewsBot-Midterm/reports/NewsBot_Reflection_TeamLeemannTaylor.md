# Group Reflective Journal

Kate Leemann and Roderick Taylor | ITAI 2373 | Exactly two pages<br/>Team-review draft - personal statements require confirmation


## Team collaboration and individual contributions

Kate Leemann and Roderick Taylor previously reported equal, side-by-side collaboration with shared responsibility for the project. This draft records that joint contribution model; it does not assign individual ownership of algorithms or invent separate experiences. Both teammates should verify their participation and add their own specific example before treating this as their final personal reflection.


The existing project provides evidence of integration work: adapting the starter to the BBC schema, correcting setup resources, deduplicating articles, comparing classifiers, and documenting results. The post-submission corrections described here were prepared with substantial AI assistance and should be distinguished from work completed before the original submission.



## Technical integration challenges

The starter expected a small sample with title, date, and source fields. The BBC file instead provides ArticleId, Text, and Category. A consistent content column allows the analyses to share article IDs and labels. The submitted pipeline already removed 50 exact duplicates, retained 1,440 articles, and reserved 288 for testing. It also fitted TF-IDF inside cross-validation and cached spaCy documents; these were existing strengths, not newly repaired defects.


The correction pass addressed concrete text errors. Deleting punctuation merged hyphenated words; removing adjacent HTML tags merged paragraphs; contractions and HTML entities were incompletely normalized. Contextual lemmatization now handles verbs, and original text is retained for sentiment and grammar. Separating headlines from article bodies prevents merged grammatical subjects. These changes show why an end-to-end run and targeted examples are both necessary.



## Learning from language structure

Course Module 6 distinguishes grammatical structure from semantic meaning. The revised examples include active and passive roles, recipients, and negation. A key opening a door is still labeled a candidate agent by the simple syntax rule, even though the key is an instrument. Reporting this failure is more informative than presenting all extracted relationships as facts.



## Business value assessment

The intended users are editors and media-monitoring analysts who need help sorting articles and finding mentions. The corrected run selected SVM and produced 97.57% accuracy and 0.9740 macro F1 on the existing 288-article test split. Technology recall was 91.49%. These are post-submission measurements; the original version recorded 96.18% accuracy and 0.9598 macro F1.


The old holdout had already been inspected before these corrections. Its revised score is useful for regression comparison, but it is not an independent estimate of improvement. No time savings or production benefits have been measured. Ambiguous topics and automated entity or sentiment estimates require human review.



## Future enhancements

Priorities are an independent current-news evaluation, near-duplicate detection, and a manually labeled sample for sentiment, entities, and relationships. Entity aliases such as Tony Blair and Blair need reconciliation. The emotion dictionary is a small exploratory baseline; normalizing its entries fixes matching consistency but does not make it a validated emotion classifier.


Future experiments could compare TF-IDF with linguistic features within training-only cross-validation. Improving evidence quality should come before adding an interface or more complex models. Unsupported categories, quoted claims, pronouns, and prepositional attachment remain open limitations.



## Professional development and disclosure

The project illustrates reproducibility, error analysis, and communicating uncertainty alongside scores. An archive preserves the submitted state, dependency versions are recorded, and regression checks exercise the corrected functions. These practices make a portfolio project easier to inspect and maintain.


This reflection was drafted with OpenAI ChatGPT/Codex assistance using the existing reflection and repository evidence. Both teammates must confirm the personal contribution account and supply their own collaboration lesson. It is deliberately labeled a review draft rather than claiming that generated prose is an independently written student reflection.


Repository: https://github.com/SCheeses/Kate-Leemann-AI-Portfolio
