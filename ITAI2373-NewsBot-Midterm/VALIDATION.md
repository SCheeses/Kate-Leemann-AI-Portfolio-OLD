# Correction validation

The original submission is preserved at base commit `c9f6f724f09b05188c6cd3d6bac0693f357eae7d` and in `archive/submitted/`.

## Verified

The regression script exercises actual notebook definitions using the small English spaCy model and a tiny synthetic classifier fixture. It checks HTML entities and block boundaries, hyphens, script exclusion, contractions, missing input, contextual verb lemmas, negation preservation, passive roles, negated relationships, recipient roles, empty sentiment, NER type restrictions, headline boundaries, integrated output fields, JSON serialization, empty article rejection, and unknown-vocabulary rejection.

All 18 checks passed. The synthetic classifier exists solely to exercise the interface; its predictions are not an evaluation of BBC accuracy.

## Remaining limitations

All 27 code cells completed sequentially with no error outputs, including setup, model selection, linguistic analyses, integration, and portable export. SVM achieved 97.57% accuracy and 0.9740 macro F1 on the existing holdout. The original CSV checksum is recorded in data_manifest.json. The historical executed notebook and tables remain available in the archive. Independent current-news evaluation is not complete.

The reflection is a draft based on the existing local reflection and documented shared contributions. Teammate-specific personal experiences require team confirmation. The optional video is not produced.

## Interpretation

Changes made after inspecting test errors cannot be treated as a blind test improvement. Use a genuinely independent dataset for final generalization evaluation. Dependency rules and synthetic checks do not measure semantic-role accuracy in real news. Human annotation is still needed for sentiment, emotion, NER, and relation extraction.
