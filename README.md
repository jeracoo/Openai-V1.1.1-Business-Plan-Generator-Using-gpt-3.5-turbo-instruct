# OpenAI Business Plan Generator

The OpenAI Business Plan Generator is a Python script that assists users in creating a detailed business plan document using OpenAI's GPT-3.5 Turbo model. It automates the process of generating business plan content, streamlining the creation of well-structured and insightful documents tailored to the user's input.

## Features

- **Automated Business Plan Writing**: Generate text for various business plan sections using GPT-3.5 Turbo.
- **Document Structure Template**: A predefined structure that can be customized according to the business needs.
- **Interactive User Interface**: Collect user input through a simple dialogue box to guide the content generation process.
- **Output in Word Format**: The resulting business plan is saved as a Microsoft Word document, making it easy to share and edit further.
- **Environment Variable Integration for API Keys**: Secure handling of OpenAI API keys using environment variables.

## How It Works

1. The script initializes by setting up the OpenAI client with your API key.
2. The user is prompted to enter their business idea.
3. A Word document is created with headings and subheadings based on a preset document structure.
4. For each section, content is generated using GPT-3.5 Turbo model calls, and the content is inserted into the document.
5. The business plan is saved with a unique timestamp, ensuring that each document is distinct.

## Prerequisites

Before running the script, make sure you have:

- Python installed on your machine
- `tkinter` for the GUI part
- `python-docx` for creating Word documents
- An OpenAI API key set as an environment variable

## Setup

To run the script, you will need to:

1. Clone the repository.
2. Install the required dependencies.
3. Set up your OpenAI API key as an environment variable.
4. Run the script to start building your business plan.

## Usage

```bash
python business_plan_generator.py
