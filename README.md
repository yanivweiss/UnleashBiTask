# IMDb Database Query Tool

This repository contains a Python script for interacting with the IMDb dataset using natural language queries. The script utilizes the OpenAI API and SQLite database to provide information from the dataset in response to user queries.

### 1)
### High-Level Architecture Description

**Frameworks:**  
You are already using **LangChain**, an open source orchestration framework for the development of applications using large language models (LLMs). LangChain provides a standard interface for chains, lots of integrations with other tools, and end-to-end chains for common applications. It can facilitate most use cases for LLMs and natural language processing (NLP), like chatbots, intelligent search, question-answering, summarization services, or even virtual agents capable of robotic process automation. LangChain is a good choice for building a BI assistant, as it allows you to leverage the power of LLMs without having to deal with the complexity of their implementation and integration.

**Models & Algorithms:**  
You are using **OpenAI**, a platform that provides access to various LLMs, such as GPT-3, Codex, DALL-E, and others. OpenAI offers a range of capabilities, such as natural language understanding, natural language generation, computer vision, and code generation. OpenAI is a good choice for building a BI assistant, as it can handle complex and diverse queries, generate SQL queries from natural language, and produce high-quality responses. However, OpenAI also has some limitations, such as the need for an API key, the cost of using the platform, and the potential for generating inaccurate or biased results.

**Databases:**  
You are using **SQLite**, a self-contained, serverless, zero-configuration, transactional SQL database engine. SQLite is a good choice for building a BI assistant, as it is lightweight, portable, reliable, and fast. However, SQLite also has some limitations, such as the lack of concurrency, scalability, and security features. Depending on the size and complexity of your data, you might consider using other database systems, such as PostgreSQL, MySQL, MongoDB, or others.

---

### Preprocessing Stage

Before you can use your BI assistant, you need to perform some preprocessing steps, such as: 

1. **Data Preparation:** Load your data from TSV files into a SQLite database, using the `load_imdb_csv` function. This function reads the TSV files, converts them into pandas dataframes, and stores them into SQLite tables.

2. **Fine Tuning:** Optionally fine-tune your LLM to better suit your domain and task using OpenAI’s Playground.

---

### Question Answering Flow

The question answering flow of your BI assistant is as follows: 

1. **Input:** User enters a natural language question.
2. **Processing:**
   - **Connection:** Connect to the SQLite database.
   - **Chain Creation:** Create a database chain for querying.
   - **Query Generation:** Generate a SQL query from the natural language question.
   - **Query Execution:** Execute the SQL query on the SQLite database.
3. **Output:** Return the query result to the user in various formats.

---

### Alternative Choices: Pros and Cons

**Frameworks:**  
Alternative - **Streamlit**  
Pros: Create interactive web apps with Python.  
Cons: Not specifically designed for LLM applications, might require more coding.

**Models & Algorithms:**  
Alternative - **Hugging Face**  
Pros: Open source, free, and easy to integrate.  
Cons: Might require more fine-tuning and customization.

**Databases:**  
Alternative - **PostgreSQL**  
Pros: Advanced features like concurrency, scalability, full-text search.  
Cons: More complex and resource-intensive.

---
### 2)

## Functions

### `load_imdb_csv(folder_path)`

This function does the following:

1. Connects to a SQLite database (creating it if it doesn't exist).
2. Reads all TSV (Tab-Separated Values) files from a given folder.
3. Converts the contents of each file into a DataFrame using Pandas.
4. Writes each DataFrame to a table in the SQLite database, with the table name derived from the file name.
5. Closes the database connection after processing all files.

### `connect_database()`

This function establishes a connection to the SQLite database named 'my_database.db' and returns the database connection object.

### `DatabaseChain(openai_api_key, db)`

This function initializes an OpenAI object with specified parameters and creates an SQLDatabaseChain object using the OpenAI object and the database connection. This chain is used to process natural language queries against the database.

### `process_question(question, db_chain)`

This function uses the `db_chain` object to process a given question and returns the result.

### `main()`

The `main()` function orchestrates the entire process:

1. Asks the user for their OpenAI API key and the path to the IMDb dataset.
2. Calls `load_imdb_csv` to load data into the SQLite database.
3. Enters a loop where it:
   - Prompts the user for a query related to the movie database.
   - Initializes `db_chain` and processes the query through `process_question`.
   - Prints the response.
   - Asks the user if they want to exit the loop.

## Execution Flow

The script runs the `main()` function, which drives the entire process. It allows users to interact with the IMDb dataset using natural language queries and provides results based on the data stored in the SQLite database.

Please make sure you have the required dependencies installed before running the script. You can find the IMDb dataset and additional instructions on how to set up and use this tool in the repository's documentation.
