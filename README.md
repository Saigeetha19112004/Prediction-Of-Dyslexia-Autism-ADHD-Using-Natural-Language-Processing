# Prediction-Of-Dyslexia-Autism-ADHD-Using-Natural-Language-Processing
```markdown

## Table of Contents
1. [Features](#features)
2. [Setup](#setup)
3. [Usage](#usage)
4. [Dyslexia Test Details](#dyslexia-test-details)
5. [Questionnaire Details](#questionnaire-details)
6. [PDF Report](#pdf-report)
7. [Dependencies](#dependencies)
8. [Limitations](#limitations)

## Features
- **Dyslexia Screening**: Analyzes user-typed sentences against randomly generated ones to identify potential dyslexic patterns like misspellings, transpositions, and word confusions.
- **Autism Screening**: Uses a short questionnaire to assess behavioral traits associated with ASD.
- **ADHD Screening**: Uses a short questionnaire to assess behavioral traits associated with ADHD.
- **PDF Report Generation**: Consolidates all screening results into a printable PDF document.
- **Configurable Thresholds**: Allows adjustment of similarity thresholds and diagnostic scores.

## Setup

To run this notebook, you need to install several Python libraries. These are typically handled by the `!pip install` commands at the beginning of the notebook.

```python
!pip install reportlab
!pip install fuzz
!pip install nltk
!pip install fuzzywuzzy
```

Additionally, you will need to download NLTK resources:

```python
import nltk
nltk.download('punkt')
nltk.download('words')
nltk.download('punkt_tab') # Although this is not explicitly used for the project, it is in the notebook.
```

**Create `sentences.txt`**: Before running the `main()` function, ensure you have a file named `sentences.txt` in the same directory as your notebook (or accessible path). This file should contain sentences, one per line, that will be used for the dyslexia copying test.

Example `sentences.txt`:
```
The quick brown fox jumps over the lazy dog.
Never underestimate the power of a good book.
Technology has revolutionized the way we live and work.
Learning a new language opens up new worlds.
```

## Usage

1.  **Run all cells in the notebook.** This will install dependencies, define functions, and prepare the environment.
2.  **Call the `main()` function.** This initiates the screening process.

    ```python
    if __name__ == '__main__':
        main()
    ```

3.  **Follow the prompts**: The program will ask for the patient's name and ID, then guide you through the dyslexia copying test (3 attempts) and the behavioral questionnaires.
4.  **Review the PDF report**: Upon completion, a PDF report named `[patient_name]_[patient_id]_neurodev_report.pdf` will be generated in the current directory.

## Dyslexia Test Details

- The test presents three randomly chosen sentences from `sentences.txt`.
- The user is asked to copy each sentence.
- The input is compared to the original sentence using fuzzy string matching (`fuzzywuzzy`) and a custom `dyslexia_analysis` function.
- The `dyslexia_analysis` function calculates a score based on:
    - Non-dictionary words.
    - Dyslexic letter confusions (e.g., 'b'/'d', 'p'/'q').
    - Dyslexic word confusions (e.g., 'was'/'saw').
    - Transpositions and reversals.
- A `SIMILARITY_THRESHOLD` (default 50) is used to determine if the user's input is sufficiently similar to the target sentence to be considered for scoring, preventing irrelevant inputs.
- An `DYSLEXIA_SCORE_THRESHOLD` (default 3.5) determines the verdict for dyslexia likelihood.

## Questionnaire Details

- Two sets of questions are asked: one for Autism-related traits and one for ADHD-related traits.
- Users respond with `never`, `lessOften`, `sometimes`, or `moreOften`.
- Answers are mapped to numeric scores (0-3).
- Each question has a weight, and scores are aggregated to produce a total score for Autism and ADHD.
- **Autism Threshold**: `AUTISM_THRESHOLD` (default 18.0) determines the likelihood verdict.
- **ADHD Threshold**: `ADHD_THRESHOLD` (default 12.0) determines the likelihood verdict.

## PDF Report

The generated PDF report includes:
- Patient's Name and ID.
- Average Dyslexia Score and Verdict.
- List of user-entered sentences and their individual dyslexia scores.
- Autism Score and Verdict.
- ADHD Score and Verdict.
- (Future expansion) Dyscalculia Score and Verdict.

## Dependencies
- `reportlab`: For generating PDF documents.
- `nltk`: Natural Language Toolkit for tokenization and word corpus.
- `fuzzywuzzy`: For fuzzy string matching (similarity comparison).
- `tqdm`: (Included in `DdipzWoHR8uB` cell but not used in the `main` function) For progress bars.
- `Pillow` (dependency of reportlab)
- `charset-normalizer` (dependency of reportlab)
- `click` (dependency of nltk)
- `joblib` (dependency of nltk)
- `regex` (dependency of nltk)

## Limitations
- This is a **screening tool only** and should not be used as a diagnostic instrument. A formal diagnosis requires assessment by qualified professionals.
- The questionnaires are simplified and based on general behavioral indicators.
- The dyslexia scoring is heuristic and may not capture all nuances of reading difficulties.
- The `sentences.txt` file needs to be manually created by the user.
- The current version only considers a specific set of dyslexic confusions.
