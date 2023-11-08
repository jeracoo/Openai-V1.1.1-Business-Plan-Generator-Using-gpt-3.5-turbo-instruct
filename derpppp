import tkinter as tk
from tkinter import simpledialog
from docx import Document
from datetime import datetime
import openai
print(dir(openai))  # This will print all the top-level attributes for the openai module
# print(openai.Completion)  # This should not raise an AttributeError if the installation is correct
import os  # To access environment variable for API key

# Function to set up the OpenAI client
# (API Key should be set as an environment variable for security reasons)
def setup_openai_client():
    openai.api_key = 'XXXXXXXX'  # Replace 'your-api-key-here' with your actual OpenAI API key
    return openai



# Function to generate text for each section using OpenAI's API
def generate_text_for_section(openai_client, section_name, user_input):
    response = openai.completions.create(
        model="gpt-3.5-turbo-instruct",
        prompt=f"Write a detailed description for a business plan section titled '{section_name}'. Project idea: {user_input}.",
        max_tokens=500
    )
    return response.choices[0].text.strip()

# Create the main document structure
def create_document_structure(openai_client, document, structure, user_input):
    for section, subsections in structure.items():
        document.add_heading(section, level=1)
        if subsections:  # If there are subsections
            for subsection in subsections:
                document.add_heading(subsection, level=2)
                content = generate_text_for_section(openai_client, subsection, user_input)
                document.add_paragraph(content)
        else:  # If no subsections, generate content for the main section
            content = generate_text_for_section(openai_client, section, user_input)
            document.add_paragraph(content)

# Check if the API key environment variable is set
if 'OPENAI_API_KEY' not in os.environ:
    raise EnvironmentError("The environment variable 'OPENAI_API_KEY' must be set with your OpenAI API key.")

# Proceed with the script only if it's the main module
if __name__ == "__main__":
    # Initialize OpenAI API client
    client = setup_openai_client()
    
    # (rest of the code related to the GUI and document generation)
    
# Document structure based on the provided template
document_structure = {
    "1. Project and document details": [
        "1.1. Project details",
        "1.2. Document control",
        "1.3. Revision history"
    ],
    "2. Introduction": [
        "2.1. Epic",
        "2.2. Feature(s)",
        "2.3. Feature(s) description",
        "2.4. Benefit hypothesis",
        "2.5. Feature(s) scope",
        "2.5.1 In-scope",
        "2.5.2 Out-of-scope",
        "2.6. Dependencies",
        "2.7. Assumptions",
        "2.8 Constraints",
        "2.9 Stakeholders"
    ],
    "3. Business process": [
        "3.1. Current business process",
        "3.2. Future business process"
    ],
    "4. System Overview": [
        "4.1. High level concept diagram",
        "4.2. System context",
        "4.3. System functions"
    ],
    "5. User stories": [
        "5.1. User characteristics",
        "5.2. User pathway",
        "5.3. User journey"
    ],
    "6. Requirements": [
        "6.1. Business requirements/User stories",
        "6.2. Solution/Technical user stories"
    ],
    "7. Core requirements": [],
    "8. Project specific requirements": [],
    "9. Terms, acronyms, and related artefacts": [
        "9.1. Terms and acronyms",
        "9.2. Related artefacts",
        "9.3. Other reference documents",
        "9.4. Document reviewers",
        "9.5. Document approvers"
    ],
    "10. Document governance": [
        "10.1. Legal sign-off determination",
        "10.2. Senior Responsible Officer (SRO) sign-off"
    ],
    "11. Project change requests": [],
    "12. Appendix 1. PSR A: Letters or Forms": [],
    "13. Appendix 2. PSR B: BI and Benefits Management Data Requirements": [],
    "14. Appendix 3. PSR C: Change Management": [],
    "15. Appendix 4. PSR D: Digital Analytics": []
}

# Start GUI for input
root = tk.Tk()
root.withdraw()  # Hide the main window

# Ask the user what they would like to build
user_input = simpledialog.askstring("Input", "What would you like me to build in the business plan?")
donkey = user_input

# Proceed only if user input is provided
if user_input:
    # Create a new Word document
    doc = Document()
    doc.add_heading('Business Plan', 0)

    # Add the user input as the introduction or overview
    doc.add_heading('Overview', level=1)
    doc.add_paragraph(user_input)

    # Generate and add other sections based on the structure
    create_document_structure(client, doc, document_structure, user_input)


# Before saving, print all paragraphs to the console for debugging
for paragraph in doc.paragraphs:
    timestamp = datetime.now().strftime("%Y%m%d%H%M%S")
    filename = f'Business_Plan_{timestamp}.docx'
    doc.save(filename)
    print(f"The business plan has been saved to '{filename}'.")
    root.destroy()

# Run the application
root.mainloop()
