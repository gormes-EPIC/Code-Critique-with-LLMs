# Lab 1: Code Critique Program with LLMs

## Objective

- Create a program in Python that queries an LLM for bug identification and general code suggestions about local files.
- Leverage local LLMs with command line tools.
## Getting Started

1. First, install `ollama` on your machine with 
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
2. Then start the model with `ollama run model`. For example:
```
ollama run llama3
# Or
ollama run codellama
```
3. Some models you can use are:
	1. `mistral`
	2. `gemma`
	3. `codellama`
	4. `llava` (for vision)
	5. `phi`
	6. `orca-mini`
	7. `qwen`
	8. `vicuna`
	9. `openchat`
	10. `wizardcoder`
4. Here is a quick sample of using POST requests to query an LLM:
```python
import requests

# URL of the Ollama API (default is localhost)
url = "http://localhost:11434/api/generate"

# JSON payload with model and prompt
payload = {
    "model": "llama3",
    "prompt": "Explain how photosynthesis works.",
    "stream": False  # Set to True if you want to stream the response
}

# Make the POST request
response = requests.post(url, json=payload)

# Parse and print the response
if response.status_code == 200:
    data = response.json()
    print(data['response'])
else:
    print("Error:", response.text)
```
4. If you want to stream tokens as they are generated, use this instead:
```python
import requests

# URL of the Ollama API (default is localhost)
url = "http://localhost:11434/api/generate"

# JSON payload with model and prompt
payload = {
    "model": "llama3",
    "prompt": "Write a poem about space.",
    "stream": True
}

# Make the POST request, print the response as it is streamed
with requests.post(url, json=payload, stream=True) as r:
    for line in r.iter_lines():
        if line:
            print(line.decode('utf-8'))
```

## Your Task

1. Your task is to write a Python program to query an LLM and get feedback about a provided code file.
2. Your program should take the file to analyze as a command line argument when running the program.
3. Note, this program will not run unless your model has been started in another terminal. You can add code to start a new model, if one is not running. 

**Sample Use:**
```
$ python code_critique.py example_file.py

No problem! I can take a look at example_file.py and analyze it for bugs and offer suggestions.
Bugs
* On line 14, ...
```
## docstrings

1. Once your program is complete, add [docstrings](https://www.geeksforgeeks.org/python-docstrings/) comments to your program. For each class and method, add a docstring comment to explain the method or class surrounded by triple quotes. Use Google's style of docstrings that list the arguments and return type.  
```
def multiply_numbers(a, b):
    """
    Multiplies two numbers and returns the result.

    Args:
        a (int): The first number.
        b (int): The second number.

    Returns:
        int: The product of a and b.
    """
    return a * b
print(multiply_numbers(3,5))
```

## Deliverables

1. A working program as described above with appropriate docstring comments
2. Upload to GitHub using terminal
## Extensions

1. Allow uploading multiple files that it will analyze as a whole. Creating this tool now will help you later in this course.
## Rubric
- 3 pts - Contains all required components and comments
- 2 pts - Contains all required components but is missing appropriate docstring comments
-  1.5 pts - Did not submit
