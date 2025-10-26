# Resume Analyzer with Deep Learning

## Architecture Overview

- **Frontend**: Streamlit web UI for file upload and results display
- **NLP Engine**: spaCy (en_core_web_sm) for entity extraction + fine-tuned BERT/RoBERTa for classification
- **Analysis Modes**: General resume quality assessment + job description matching
- **File Support**: PDF and DOCX resume formats

## Project Structure

```py
resume-analyzer/
├── app.py                    # Main Streamlit application
├── models/
│   ├── resume_classifier.py # Fine-tuned model wrapper
│   ├── entity_extractor.py  # spaCy NER implementation
│   └── scorer.py            # Scoring algorithms
├── utils/
│   ├── text_extractor.py    # PDF/DOCX text extraction
│   └── preprocessor.py      # Text cleaning utilities
├── data/
│   └── training/            # Dataset for fine-tuning
├── requirements.txt         # Dependencies
└── README.md
```

## Phase 1: Jupyter Notebook Prototyping (7-Step Framework)

Create notebooks to prototype and experiment with each component:

### Notebook 1: `01_data_collection.ipynb`

- Download resume dataset from Hugging Face
- Explore dataset structure and statistics
- Download sample resumes for testing
- Prepare data directory structure

### Notebook 2: `02_text_extraction.ipynb`

- Install and test PyMuPDF for PDF extraction
- Install and test python-docx for DOCX extraction
- Test extraction on sample resumes
- Handle edge cases (corrupted files, images, tables)

### Notebook 3: `03_text_preprocessing.ipynb`

- Clean extracted text (remove special chars, extra whitespace)
- Normalize text (lowercase, tokenization)
- Identify and preserve important sections (Education, Experience, Skills)
- Create reusable preprocessing functions

### Notebook 4: `04_entity_extraction_spacy.ipynb`

- Load spaCy `en_core_web_sm` model
- Extract entities: names, emails, phones, URLs
- Create custom patterns for skills, certifications
- Test on sample resumes and visualize results

### Notebook 5: `05_model_training.ipynb`

- Load Hugging Face dataset
- Prepare training/validation splits
- Fine-tune BERT/RoBERTa for resume classification
- Evaluate model performance (accuracy, F1)
- Save trained model weights

### Notebook 6: `06_scoring_system.ipynb`

- Implement completeness scoring (sections present)
- Implement skills matching (with/without job description)
- Calculate experience relevance score
- Assess formatting quality
- Combine into overall score (0-100)

### Notebook 7: `07_feedback_generation.ipynb`

- Generate feedback based on scores
- Identify missing sections
- Suggest skill improvements
- Compare with job description (keyword gaps)
- Create structured feedback output

## Phase 2: Production Application Development

After validating the approach in notebooks, convert to production code:

### 1. Environment Setup

Create `requirements.txt` with all dependencies

### 2. Modular Code Structure

Extract notebook code into:

- `utils/text_extractor.py` - From notebook 2
- `utils/preprocessor.py` - From notebook 3
- `models/entity_extractor.py` - From notebook 4
- `models/resume_classifier.py` - From notebook 5
- `models/scorer.py` - From notebook 6 & 7

### 3. Streamlit UI (`app.py`)

Build interface with:

- **Sidebar**: File uploader (PDF/DOCX), optional job description input
- **Main Panel**:

  - Overall score display (gauge/progress bar)
  - Category breakdown (bar chart)
  - Extracted entities table
  - Detailed feedback list
  - Skills comparison (word cloud or table)

- **Footer**: Model info and credits

### 4. Integration & Testing

- Connect all modules into complete pipeline
- Test with various resume formats
- Validate scoring consistency
- Handle edge cases

## Key Features

- ✓ Upload resume (PDF/DOCX)
- ✓ Optional job description matching
- ✓ Entity extraction (name, skills, education, etc.)
- ✓ Overall score (0-100)
- ✓ Category-wise breakdown
- ✓ Actionable feedback
- ✓ Skills gap analysis
- ✓ ATS-friendly format checking

## Testing Strategy

- Test with various resume formats
- Validate scoring consistency
- Test with/without job descriptions
- Handle edge cases (corrupted files, non-resumes)
