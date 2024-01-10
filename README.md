# IMDb Database Query Tool

This repository contains a Python script for interacting with the IMDb dataset using natural language queries. The script utilizes the OpenAI API and SQLite database to provide information from the dataset in response to user queries.

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
