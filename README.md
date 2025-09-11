# Creativity Experiment: AI Chatbot Interaction Analysis

This repository contains the code, data, and analysis for an experimental study investigating how different types of AI chatbot interactions affect creative idea generation, idea diversity, and perceived ownership.

## Repository Structure

- `analysis/` - Contains all analysis scripts, data, and outputs
  - `Code/` - Analysis scripts and code
    - `Analysis_Study.Rmd` - Main R Markdown analysis file  
    - `refined_idea_similarity_analysis.py` - Python script for OpenAI embedding-based diversity calculations
  - `Data/` - Raw and processed data files
    - `data_clean.csv` - Cleaned experimental data
    - `data_merged.csv` - Raw merged data from all participants
    - `Elaboration_analysis.csv` - Coded elaboration depth data
    - `ideas_with_diversity_scores_embeddings.npz` - Embeddings for diversity calculations
  - `Figures/` - Generated visualizations and plots
- `backend/` - Backend configuration files
  - `.env.example` - Example environment file (template for API keys)
  - `.env` - Environment variables (API keys, configuration) - *create from example*
- `requirements.txt` - Python dependencies for diversity analysis
- `Rater Documents/` - Documentation for human raters
  - Coding schemes and rater instructions

## Study Design

The experiment examines five experimental conditions:
- **Question-Mode** (`feedback`) - AI asks questions
- **Suggestion-Mode** (`suggestion`) - AI provides suggestions  
- **Model-Led** (`improvement`) - AI leads the creative process
- **Vanilla** - Basic AI interaction without specific prompting
- **Control** - No AI assistance

### Key Measures

**Primary Outcomes:**
- Idea Quality (rated by multiple trained raters)
- Idea Diversity (computed using semantic embeddings)
- Perceived Idea Ownership

**Secondary Measures:**
- Creative Self-Efficacy
- UX measures (Performance Expectancy, Effort Expectancy, Hedonic Motivation)
- Cognitive workload (NASA-TLX)
- Elaboration depth (H-IDEA coding scheme)

## Getting Started

### Prerequisites

- R (version 4.0.0 or higher)
- RStudio (recommended IDE for running the analysis)
- Python 3.8+ (for embedding analysis)
- Required R packages (automatically installed when running the code):
  - `psych` - For reliability analyses and psychometrics
  - `tidyverse` - For data manipulation and visualization
  - `lme4`, `lmerTest` - For mixed-effects models
  - `emmeans` - For estimated marginal means and contrasts
  - `ggplot2`, `gridExtra` - For visualization
  - `fmsb` - For spider/radar charts
  - `stargazer` - For LaTeX table generation
  - `here` - For robust file paths
  - `papaja`, `knitr` - For reproducible reporting

### Running the Analysis

#### Python Setup (Required for Diversity Analysis)

Before running the R analysis, you need to set up the Python environment for semantic similarity calculations:

1. **Install Python dependencies:**
   
   **Recommended:** Use a virtual environment:
   ```bash
   python -m venv creativity_env
   source creativity_env/bin/activate  # On Windows: creativity_env\Scripts\activate
   pip install -r requirements.txt
   ```
   
   Or install directly:
   ```bash
   pip install -r requirements.txt
   ```

2. **Set up OpenAI API access:**
   - Copy the example environment file:
     ```bash
     cp backend/.env.example backend/.env
     ```
   - Edit `backend/.env` and replace `your_openai_api_key_here` with your actual API key
   - Get an API key from [OpenAI's platform](https://platform.openai.com/api-keys)
   - **Important:** Never commit your actual `.env` file to version control

3. **Run the Python diversity analysis:**
   ```bash
   cd analysis/Code/
   python refined_idea_similarity_analysis.py
   ```
   
   This script will:
   - Calculate semantic embeddings for ideas using OpenAI's text-embedding-3-large model
   - Compute diversity scores within conditions and across all ideas
   - Generate `ideas_with_diversity_scores.csv` and `ideas_with_diversity_scores_embeddings.npz`
   
   **Note:** This step requires an active internet connection and OpenAI API credits. The script processes text through OpenAI's embedding API to calculate semantic similarity between ideas.

#### R Analysis in RStudio

After completing the Python setup, run the main R analysis:

1. **Open RStudio**
2. **Open the main analysis file** (`analysis/Code/Analysis_Study.Rmd`)
3. **Run the entire analysis using RStudio's interface:**
   - **Method 1 (Recommended):** Click the "Run" dropdown menu in the toolbar → Select "Run All"
   - **Method 2:** In the R Markdown document, click the "Run" dropdown → Select "Run All Chunks Below"
   - **Method 3:** Use keyboard shortcuts:
     - macOS: Select all code (⌘ + A) and run (⌘ + Enter)  
     - Windows: Select all code (Ctrl + A) and run (Ctrl + Enter)
   - **Method 4:** Run chunk by chunk by clicking the green "play" button in each code chunk or using (Ctrl/⌘ + Shift + Enter)

The R analysis will:
- Load and clean the data (including Python-generated diversity scores)
- Generate descriptive statistics and demographic summaries
- Conduct reliability analyses (Cronbach's α, ICC)
- Test hypotheses using planned contrasts
- Create publication-ready visualizations
- Export LaTeX tables for manuscript preparation

**Important:** The Python diversity analysis must be completed first, as the R analysis depends on the diversity scores generated by the Python script.

## Analysis Components

### Hypothesis Testing
- **H1:** Idea quality improvement across AI conditions vs. control
- **H2-H3:** Idea diversity effects for Question-Mode and Suggestion-Mode vs. Model-Led and Vanilla
- **H4-H5:** Perceived ownership effects for Question-Mode and Suggestion-Mode vs. Model-Led and Vanilla

### Statistical Methods
- Linear models with planned contrasts
- Mixed-effects models for within-subject changes
- Effect size calculations (Cohen's d)
- Multiple comparison corrections (Holm adjustment)
- Reliability analysis (Cronbach's α, ICC for rater agreement)

### Visualizations
- Violin plots for main dependent variables
- Spider/radar charts for UX measures
- Before-after plots for within-subject changes
- Marginal effects plots for interaction analyses

### Exploratory Analyses
- Elaboration depth analysis using H-IDEA coding scheme
- Cognitive workload (NASA-TLX) comparisons
- Regression analysis of effort-ownership relationships
- Disproportionate effects analysis across initial creativity levels

## Results

Key findings and visualizations are automatically generated in the `analysis/Figures/` directory:
- `violin_refinedSim_ideaQuality_ownership_by_condition.png` - Main outcome measures
- `ux_measures_spider_chart.png` - User experience radar chart
- `within_subject_change_publication.png` - Before-after analysis
- `marginal_effects_regression.png` - Interaction effects


## Data Privacy & Ethics

This research follows ethical guidelines for human subjects research. All participant data has been anonymized, and the study was conducted with appropriate institutional approval.

## Citation

If you use this code or data in your research, please cite:

```
[publication details as soon as available]
```

---

*This analysis was conducted using reproducible research practices with R Markdown and follows APA reporting guidelines.*
