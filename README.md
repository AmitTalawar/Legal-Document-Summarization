# Legal Document Summarization

## Overview

This project implements an extractive summarization system tailored for legal documents. It focuses on summarizing lengthy legal judgments—specifically those from the Indian legal system—using state-of-the-art transformer models. The goal is to reduce complex legal texts into concise, informative summaries that capture the essential details of a case.

## Table of Contents

- [Overview](#overview)
- [Project Details](#project-details)
- [Data and Methods](#data-and-methods)
- [Models Used](#models-used)
- [Challenges and Solutions](#challenges-and-solutions)
- [Results](#results)

## Project Details

This mini project explores legal document summarization using both abstractive and extractive techniques. The system processes legal judgments sourced from the Legal Information Institute (LII) of India. The project evaluates multiple transformer models—such as BART, PEGASUS, BERTSum, and Longformer—against ROUGE metrics to assess summarization quality.

## Data and Methods

### Data
- **Source:** Legal documents from the Legal Information Institute (LII) of India.
- **Scope:** Approximately 40,000 documents spanning from 1950 to 2022.
- **Format:** Documents include a 'Headnote' (summary) and a 'Decision'. Note that only documents from 1950 to 1998 contain headnotes.

### Methods
- **Data Extraction:** Utilized Selenium with OCR to scrape and extract text from legal websites.
- **Pre-processing:** Splitting documents into ‘Headnote’ and ‘Decision’, handling legal abbreviations, and preparing the dataset for training.
- **Summarization Approaches:**
  - **Abstractive Summarization:** Using models like BART-Large-CNN and PEGASUS.
  - **Extractive Summarization:** Using models like BERTSum, with Longformer deployed to manage long input sequences.
- **Evaluation:** Summaries are evaluated using ROUGE-1, ROUGE-2, and ROUGE-L metrics.

## Models Used

- **BART-Large-CNN:** Fine-tuned on the CNN/Daily Mail dataset for summarization tasks.
- **PEGASUS:** Pre-trained by masking important sentences to enhance abstractive summarization.
- **BERTSum:** An extractive summarization model that leverages BERT for sentence ranking.
- **Longformer:** Adapted to handle the long sequences typical in legal documents, thanks to its efficient attention mechanism.

## Challenges and Solutions

- **Sequence Length:**  
  *Challenge:* Legal decisions often far exceed the typical transformer token limits.  
  *Solution:* Text is segmented into chunks and processed using cosine similarity to merge summaries; alternatively, Longformer is used to natively handle long inputs.

- **Computational Limits:**  
  *Challenge:* Fine-tuning on long documents is computationally intensive.  
  *Solution:* Reduced the number of training epochs and leveraged external resources such as HuggingFace AutoTrain.

- **Abbreviations:**  
  *Challenge:* Legal texts contain many domain-specific abbreviations.  
  *Solution:* Implemented regex-based extraction and manual mapping to expand abbreviations during pre-processing.

- **Conversion from Abstractive to Extractive:**  
  *Challenge:* Gold-standard summaries (headnotes) are abstractive, complicating direct training of extractive models.  
  *Solution:* Explored cosine similarity techniques to align abstractive summaries with corresponding extractive content.

## Results

- **Evaluation Metrics:** ROUGE-1, ROUGE-2, and ROUGE-L scores were used to assess summary quality.
- **Key Findings:**  
  - Pre-trained models (BART-Large-CNN without fine-tuning) achieved high ROUGE scores.
  - Fine-tuning via AutoTrain showed promising results, especially with the BART-Longformer configuration.
- Detailed metrics and model comparisons are provided in the project report.
