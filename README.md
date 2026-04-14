# keywordreference
App4KeywordReference
# App4KeywordReference

An R/Shiny application for **manuscript pre-submission screening**.  
The app is designed to help authors and reviewers quickly inspect five practical aspects of a manuscript before journal submission:

1. **Keyword representation**
2. **Reference extraction and checking**
3. **Language quality / wording review**
4. **AMA-style in-text citation order**
5. **Technical readiness for submission**

In addition to summary checks, the app produces **co-word networks**, **SS plots**, **Kano plots**, **Sankey views**, and **AAC summaries** for both the main document and the reference section.

---

## Features

- Upload **PDF**, **DOCX**, **TXT**, or **CSV** files
- Analyze a **web article / PubMed page** by URL
- Extract and summarize manuscript text from:
  - main body
  - reference section
- Generate:
  - keyword tables
  - MeSH-supported keyword candidates
  - extracted reference tables
  - reference author/journal networks
  - submission-readiness summary report
- Check **sequential AMA-style citations** against the extracted reference list
- Export:
  - CSV data tables
  - PNG figures

---

## Intended use

This app is not a replacement for editorial review, reporting guidelines, or peer review.  
It is a **decision-support tool** for screening common manuscript problems before submission.

It is especially useful for detecting:

- weak keyword coverage
- incomplete or problematic reference extraction
- poor wording or language-quality issues
- incorrectly ordered in-text citations in AMA style
- technical issues that may delay submission or complicate review

---

## Project structure

A typical repository structure is:

```text
.
├─ app.R
├─ R/
│  └─ *.R
├─ data/
│  └─ SOFTX-S-26-00528.pdf   # optional bundled demo PDF
├─ mesh_keyword_validation.R # optional
├─ renderSSplot.R            # optional
├─ appAAC.R                  # optional
├─ reference_extraction.py   # optional Python bridge
└─ python/
   └─ reference_extraction.py # optional alternative location
```

Notes:

- `app.R` is the main Shiny entry point.
- Files inside `R/` are auto-sourced on startup.
- If `reference_extraction.py` is available and Python is configured, the app uses it for reference extraction; otherwise it falls back to an R-based extractor.

---

## Requirements

### R
- R 4.2+ recommended
- RStudio optional but convenient

### Required R packages
The app auto-loads / auto-installs packages when needed, but for reproducible setup you can install them manually:

```r
install.packages(c(
  "shiny", "pdftools", "readr", "dplyr", "stringr", "tibble",
  "udpipe", "stopwords", "igraph", "visNetwork", "DT", "scales",
  "ggplot2", "htmltools", "ggrepel", "networkD3", "plotly", "xml2",
  "httr", "stringi", "reticulate"
), repos = "https://cloud.r-project.org")
```

### Optional Python support
Python is optional, but recommended if you want the external reference extraction bridge.

- Python 3.x
- `reticulate` in R
- `reference_extraction.py` placed either:
  - in the repository root, or
  - in `python/reference_extraction.py`

You can also specify Python explicitly:

```r
Sys.setenv(RETICULATE_PYTHON = "C:/path/to/python.exe")
```

---

## Run locally

### Option 1: RStudio
Open the project folder and run:

```r
shiny::runApp()
```

### Option 2: From terminal / R console
Set the working directory to the repository root, then run:

```r
setwd("path/to/App4KeywordReference")
shiny::runApp()
```

If your app file is not in the current directory, run:

```r
shiny::runApp("path/to/App4KeywordReference")
```

---

## How to use

1. Launch the app.
2. Choose one of the following input modes:
   - upload a **PDF / DOCX / TXT / CSV** file
   - check **Extract keywords from website instead of uploaded file** and paste a URL
3. Select the **language / UDPipe model**.
4. Adjust optional analysis settings:
   - parts of speech to keep
   - candidate pool size
   - minimum frequency
   - minimum co-occurrence
5. Click:
   - **Analyze** for the main workflow
   - **Run submission report** for the summary screening output

---

## Main tabs / outputs

### Overview
General diagnostics and uploaded-document information.

### Submission Readiness Report
Summarizes manuscript status, language quality, and technical compliance.

### Keyword Leader-Member Trace
Shows:
1. original document keywords (leaders)
2. additional aligned terms / members
3. final top-20 keywords after FLCA-based processing

### Keywords
Displays RAKE and TF-IDF outputs for the main document.

### MeSH Keywords
Provides MeSH-oriented validation tables and reference-backed support.

### Main Document
Generates network-based views for the main manuscript text, including:
- Network
- SSplot
- Kano plot
- Sankey
- AAC summary

### References
Includes:
- extracted references
- reference co-word rows
- AMA sequential citation check
- reference nodes / relations
- reference network visualizations
- downloadable coword data

---

## Supported inputs

- **PDF**: works best for digital-text PDFs
- **DOCX**: useful for structured manuscript sections
- **TXT**: plain-text manuscript input
- **CSV**: flexible input for text columns
- **URL**: web-linked article input

---

## Important limitations

- The app is designed primarily for **AMA-style numbered references**.
- Non-AMA reference sections, HTML-heavy pages, and irregular web formatting are handled on a **best-effort** basis.
- Scanned image PDFs may need OCR before analysis.
- Chinese (Simplified) and Chinese (Traditional) currently map to the same UDPipe label in this app.
- Actual UDPipe model availability depends on your runtime environment.

---

## Example use cases

- Screen a manuscript before journal submission
- Check whether extracted keywords reflect the abstract / discussion / conclusion
- Verify whether numbered references are detected correctly
- Inspect whether in-text citations appear in proper AMA sequence
- Generate keyword and reference co-word visualizations for review

---

## Suggested GitHub workflow

### 1. Create a new repository
On GitHub, create a repository such as:

```text
App4KeywordReference
```

### 2. Add your project files
Put your Shiny app files into the repository root.

### 3. Add this README
Save this file as:

```text
README.md
```

### 4. Commit and push
Example Git commands:

```bash
git init
git add .
git commit -m "Initial commit for App4KeywordReference"
git branch -M main
git remote add origin https://github.com/yourname/App4KeywordReference.git
git push -u origin main
```

---

## Citation
If you use this tool in a manuscript, cite the corresponding article or software paper for **App4KeywordReference** if available.

You may also cite the broader methodological background for manuscript screening, reference verification, and AMA citation compliance as appropriate.

---

## License
Add your preferred license here, for example:

- MIT License
- GPL-3.0
- CC BY 4.0 (for documentation only)

Example:

```text
MIT License
```

---

## Acknowledgments
This app extends a manuscript-screening workflow built in **R/Shiny**, with support for multilingual text handling, reference extraction, network visualization, and submission-readiness reporting.

