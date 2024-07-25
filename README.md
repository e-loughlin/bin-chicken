# Bin Chicken DB Library

<p align="center">
<img src="bin_chicken_logo.png" style="display: block; margin: 0 auto; width: 200px; height: 200px;">
</p>

## Overview
Bin Chicken is a simple Python library wrapping the [Ibis Library](https://ibis-project.org/) designed to help data scientists and engineers streamline their SQL-related tasks and enhance their workflow efficiency. This library aims to provide a foundational toolset for analyzing experiments, fetching data, building insights, and standardizing repeatable data science tasks.

### Naming

"Bin Chicken" is an Australian colloquial term to refer to the Australian White Ibis, due to its habit of eating from rubbish bins.

### Features

[- GPT Query Tool](#gpt-query-tool)
  - Run SQL commands on your Ibis Database Connection with a user prompt query.

Setting Up a Virtual Environment
To create a virtual environment and install the required packages from requirements.txt, follow these steps:

## Create a Virtual Environment

```bash
python -m venv venv
```

## Activate the Virtual Environment

### On Windows

```bash
venv\Scripts\activate
```

### On macOS and Linux

```bash
source venv/bin/activate
```

## Install Dependencies

1. Create a `requirements.txt` file with the following content:

```plaintext
pandas
sqlalchemy
numpy
scipy
matplotlib
ibis-framework
openai
python-dotenv
```

2. Install the dependencies using pip:

```bash
pip install -r requirements.txt
```

## Usage

### GPT Query Tool

Here is an example of using Bin Chicken GPT Query Tool:

```python
import sys
import os
import ibis
from IPython.display import display, Markdown

# Add the library path
sys.path.append(os.path.abspath('../binchicken'))

# Import the GPT query tool
from gpt import GPTQueryTool

# Load the .env file
from dotenv import load_dotenv
load_dotenv()

# Get the environment variable
openai_api_key = os.getenv('OPENAI_API_KEY')

# Connect to a SQLite database
conn = ibis.connect("sqlite://sakila.db")

# Initialize the GPT query tool
gpt_tool = GPTQueryTool(
    openai_api_key,
    safe_mode=True
)

# Run a query
result = gpt_tool.query(
    conn, 
    "Find all actors whose last names contain the letters LI. Order the rows by last name and first name, in that order",
    execute=True
)

# Display the results
display(result)

```

Generated SQL: 

```sql

SELECT * FROM actor
WHERE last_name LIKE '%LI%'
ORDER BY last_name, first_name;
```

Resulting in the following Pandas Dataframe:

actor_id | first_name | last_name | last_update
--- | --- | --- | ---
86 | GREG | CHAPLIN | 2020-12-23 07:12:30
82 | WOODY | JOLIE | 2020-12-23 07:12:30
34 | AUDREY | OLIVIER | 2020-12-23 07:12:29
15 | CUBA | OLIVIER | 2020-12-23 07:12:29
172 | GROUCHO | WILLIAMS | 2020-12-23 07:12:31
137 | MORGAN | WILLIAMS | 2020-12-23 07:12:30
72 | SEAN | WILLIAMS | 2020-12-23 07:12:29
83 | BEN | WILLIS | 2020-12-23 07:12:30
96 | GENE | WILLIS | 2020-12-23 07:12:30
164 | HUMPHREY | WILLIS | 2020-12-23 07:12:31

