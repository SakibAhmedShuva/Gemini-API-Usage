# Gemini API Usage

This repository demonstrates how to use Google's Gemini API for generative AI applications. The project provides a simple implementation that shows how to authenticate with the API, list available models, and generate content.

## Features

- Connect to the Gemini API using your API key
- List all available Gemini models that support content generation
- Generate text content using different Gemini models
- Examples using both the legacy and current client approaches

## Prerequisites

- Python 3.7+
- A Google AI Studio account with API access
- Gemini API key (get one from [Google AI Studio](https://ai.google.dev/))

## Installation

1. Clone this repository:
```bash
git clone https://github.com/SakibAhmedShuva/gemini-api-usage.git
cd gemini-api-usage
```

2. Install the required packages:
```bash
pip install google-generativeai==2.1.4
```

## Setup

### Option 1: Environment Variables (Recommended)

For security, it's best to use environment variables for your API key:

```bash
export GEMINI_API_KEY="your_api_key_here"
```

Then in your code:
```python
import os
api_key = os.environ.get("GEMINI_API_KEY")
```

### Option 2: Direct Assignment (Not recommended for production)

Only for quick testing, you can directly assign your API key:

```python
api_key = "your_api_key_here"  # Replace with your actual API key
```

> **⚠️ Security Warning:** Never commit your real API key to a public repository.

## Usage

### Running the Notebook

The repository includes a Jupyter notebook `gemini.ipynb` that you can run directly in Google Colab or any Jupyter environment.

### Listing Available Models

```python
import google.generativeai as genai

# Configure the client with your API key
genai.configure(api_key=api_key)

# List and filter available models
for m in genai.list_models():
    if 'generateContent' in m.supported_generation_methods:
        print(f"Model Name: {m.name}")
```

### Generating Content with Legacy API

```python
import google.generativeai as genai

# Configure with your API key
genai.configure(api_key=api_key)

# Create a model instance
model = genai.GenerativeModel("gemini-1.5-flash-latest")

# Generate content
response = model.generate_content("Explain how AI works in a few words")
print(response.text)
```

### Generating Content with Current Client API

```python
from google import genai

# Initialize client
client = genai.Client(api_key=api_key)

# Generate content
response = client.models.generate_content(
    model="gemini-2.5-pro-exp-03-25", 
    contents="Explain how AI works in a few words"
)
print(response.text)
```

## Available Models

The Gemini API offers several models with different capabilities and performance characteristics:

- `gemini-1.5-flash-latest` - Fast, efficient model for most general use cases
- `gemini-1.5-pro-latest` - More powerful model for complex reasoning
- `gemini-2.5-pro-exp-03-25` - Experimental model with enhanced capabilities

The actual list of available models may change. Use the `list_models()` function to get the most up-to-date list.

## Error Handling

The example includes basic error handling to catch authentication and API request issues:

```python
try:
    # Your Gemini API code here
except Exception as e:
    print(f"An error occurred: {e}")
    print("Please ensure your API key is correct and valid.")
```

## Resources

- [Google Generative AI Python SDK Documentation](https://ai.google.dev/tutorials/python_quickstart)
- [Gemini API Documentation](https://ai.google.dev/docs)
- [Google AI Studio](https://ai.google.dev/)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

- [SakibAhmedShuva](https://github.com/SakibAhmedShuva)
