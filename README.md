# CSV / JSON Auto-Reader Experiment

**Name:** Deepak B V  
**Register No.:** 212223060036  

---

## Aim
To implement a single Python function that automatically detects whether a given file is in **.csv** or **.json** format and reads its contents into a list of dictionaries.

---

## Explanation
This experiment demonstrates how to create a **flexible and reusable** Python function that can process two popular data formats—CSV and JSON—without requiring separate code paths from the user.

* The function determines the file type by checking its **extension**.
* For `.csv` files, Python’s built-in **csv.DictReader** is used to convert each row into a dictionary, keyed by the header columns.
* For `.json` files, the **json.load()** method directly converts the file contents into a Python list of dictionaries.

By unifying these approaches into one function, we simplify data ingestion and make the code more maintainable.

---

## AI Tools Used
To explore AI-assisted coding, two different AI systems were consulted and their outputs compared:

* **AI Tool 1:** Google Gemini  
* **AI Tool 2:** ChatGPT  

Both were given the same prompt:

> “Write a single Python function `read_data_from_file(filepath)` that can read both .csv and .json files.  
>  The function should return a list of dictionaries, where each dictionary represents a row (for .csv) or an object (for .json).  
>  The function must automatically detect the file type based on its extension.”

---

## Analysis of Google Gemini’s Output
* Used **os.path.splitext** to robustly identify the file extension.  
* Employed effective `try…except` blocks for handling `FileNotFoundError` and invalid formats.  
* Produced clean, production-ready Python style.

---

## Analysis of ChatGPT’s Output
* Strong error handling with detailed messages.  
* Consistent use of `csv.DictReader` and `json.load`.  
* Straightforward, readable structure.

Both tools arrived at almost identical, well-structured functions—demonstrating a strong grasp of Python’s standard libraries and good programming practices.

---

## Final Combined Code

```python
import csv
import json
import os

def read_data_from_file(filepath):
    """
    Reads data from a .csv or .json file and returns a list of dictionaries.

    Args:
        filepath (str): Path to the input file.

    Returns:
        list: A list of dictionaries containing the file data,
              or an empty list if an error occurs.
    """
    extension = os.path.splitext(filepath)[1].lower()

    if extension == '.csv':
        try:
            with open(filepath, 'r', newline='', encoding='utf-8') as f:
                reader = csv.DictReader(f)
                return list(reader)
        except FileNotFoundError:
            print(f"Error: File not found at {filepath}")
            return []
        except Exception as e:
            print(f"CSV read error: {e}")
            return []

    elif extension == '.json':
        try:
            with open(filepath, 'r', encoding='utf-8') as f:
                return json.load(f)
        except FileNotFoundError:
            print(f"Error: File not found at {filepath}")
            return []
        except (json.JSONDecodeError, ValueError) as e:
            print(f"Invalid JSON file: {e}")
            return []
        except Exception as e:
            print(f"JSON read error: {e}")
            return []

    else:
        print("Error: Only .csv and .json files are supported.")
        return []
```
## Conclusion
A single Python function, **`read_data_from_file()`**, was successfully implemented to automatically detect and read both CSV and JSON files into a list of dictionaries.

Both AI tools—**Google Gemini** and **ChatGPT**—provided near-identical, high-quality solutions.

The final version integrates the best practices from both, featuring strong error handling, clean code, and full compatibility with common data formats.

This experiment highlights how AI coding assistants can accelerate development while still allowing the programmer to merge, refine, and validate the final product.

---

## Result
The prompt executed successfully. The function performed as expected for **CSV**, **JSON**, and **invalid file** inputs.
