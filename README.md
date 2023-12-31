# ConvoContext

ConvoContext is a Python application that leverages the power of the Hugging Face Transformers library to provide you with instant answers to your questions based on context. It's a versatile tool that can work with various file types like PDFs, DOCX, PPTX, CSV and plain text files.

## Table of Contents

- [About](#about)
- [Getting Started](#getting-started)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [Example Usage](#reference)
- [Contributing](#contributing)

## About

This project is a work in progress, created by [Manav Israni](https://github.com/manavtech07). It may take some time to process larger contexts, but it will improve over time.

## Getting Started

These instructions will help you get started with ConvoConnect and set up the environment.

### Prerequisites

To use ConvoContext, you'll need to have the following installed:

- Python 3
- Dependencies listed in `requirements.txt`

### Installation

1. Clone the ConvoContext repository and change the directory:

   ```bash
   git clone https://github.com/manavtech07/ConvoConnect.git
   cd ConvoConnect
   ```

2. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## How It Works

ConvoContext combines the power of language models and file parsing to answer questions based on provided context. It currently supports PDF, DOCX, PPTX, CSV, and plain text file formats.

**ConvoContext is still a work in progress**, and further developments are planned to expand its capabilities and enhance its performance. This project represents a minor step in the journey of mine and aims to provide a foundation for future improvements.

In the case of CSV format, ConvoContext can also provide small insights regarding data, such as identifying the highest salary.

## Usage

1. To upload the necessary libraries
   ```bash
   import requests
   from transformers import BertTokenizer, BertForQuestionAnswering
   from PyPDF2 import PdfReader
   from docx import Document
   from pptx import Presentation
   import os
   from transformers import pipeline
   ```
   
2. To upload the content
   ```bash
   from get_content import FileContentReader
   file_reader = FileContentReader()
   # Set the file paths for processing
   from google.colab import files
   uploaded_files = files.upload()
   file_paths = list(uploaded_files.keys())

   file_reader.set_file_paths(file_paths)
   # Get the combined content and model name
   result = file_reader.process_files()
   combined_content, file_extension = result[0], result[1]
   print(combined_content)
   ```
3. When prompted, enter your question.
4. ConvoContext will provide you with answers based on the provided context.
5. If not this way, you can type the content
   ```bash
   combined_content= input("Content: ")
   file_extension=".txt"
   ```
6. Now load models, tokenizers and create pipeline
   ```bash
   from modelling import ModelSelector

   model_selector = ModelSelector(file_extension)
   tqa_model = model_selector.get_tqa_model()
   model_name = model_selector.get_model_name()
   tokenizer = model_selector.get_tokenizer()
   model = model_selector.get_model()
   ```
7. Now main.py
   ```bash
   from main import QAModel

   question = input("Question: \n")
   qa_model = QAModel(tqa, file_extension, question, combined_content)
   answer, extracted_reference = qa_model.run()

   if answer is not None:
     print(f'\n------------------------------------------------------------------------------------------------\n\nAnswer: 
   {answer["answer"]}\n\n------------------------------------------------------------------------------------------------ \n\nContext:\n{extracted_reference}')

   else:
   print(f'\n------------------------------------------------------------------------------------------------\n\nAnswer: \n{extracted_reference}')

   ```

## Reference

For reference, you can refer to this Colab notebook: [ConvoContext](https://colab.research.google.com/drive/1RXes7JYkGgsmLbS3mj2o61nOzdI6E29C?usp=sharing)

## Contributing

Contributions to make ConvoContext even better are welcomed. If you'd like to contribute, please open an issue or a pull request on our GitHub repository:)




   
   


   
   


