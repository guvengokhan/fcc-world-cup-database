# World Cup Database

This project is a core component of the freeCodeCamp Relational Database Certification. It demonstrates advanced SQL querying, data normalization, and automated data insertion using Bash scripting. The system processes historical World Cup tournament data from a CSV file and structures it into a relational PostgreSQL database.

## Project Overview

The objective of this project is twofold:
1. Design and populate a PostgreSQL database using a dataset of World Cup matches (`games.csv`).
2. Write a comprehensive suite of SQL queries (`queries.sh`) to extract specific tournament statistics, leveraging advanced aggregate functions, multi-table joins, and data filtering.

## Tech Stack & Skills Demonstrated

*   **Database Management:** PostgreSQL
*   **Querying Language:** SQL (Data Definition Language, Data Manipulation Language, Joins, Aggregate Functions)
*   **Automation & Data Ingestion:** Bash Scripting (Shell Scripting, file reading loops)
*   **Concepts Applied:** Data Normalization, Primary and Foreign Key Constraints, Unique Constraints, String Manipulation.

## Database Schema & Architecture

The database `worldcup` is designed around two normalized tables to eliminate data redundancy:

1.  **`teams`**: Stores unique names of participating countries.
    *   `team_id` (SERIAL, Primary Key)
    *   `name` (VARCHAR, Unique)
2.  **`games`**: Stores the details of every tournament match.
    *   `game_id` (SERIAL, Primary Key)
    *   `year` (INT)
    *   `round` (VARCHAR)
    *   `winner_id` (INT, Foreign Key referencing `teams`)
    *   `opponent_id` (INT, Foreign Key referencing `teams`)
    *   `winner_goals` (INT)
    *   `opponent_goals` (INT)

## How the Scripts Work

### 1. Data Insertion (`insert_data.sh`)
This script automates the process of reading `games.csv`. It parses each row, checks if the winner and opponent teams already exist in the `teams` table, inserts them if they are missing to obtain their IDs, and then inserts the complete match statistics into the `games` table. It utilizes conditional logic to prevent duplicate entries.

### 2. Data Querying (`queries.sh`)
This script contains complex SQL queries designed to compute specific statistics from the populated database. Examples of analytical queries executed include:
*   Total and average goals scored by winning and losing teams.
*   The team names and years of all tournament champions.
*   Filtering teams based on specific patterns (e.g., names starting with 'Co').

## How to Run & Test Locally

To test this project on your local machine, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/guvengokhan
    cd fcc-world-cup-database
    ```

2.  **Recreate the database:**
    Ensure PostgreSQL is running locally, then rebuild the database structure using your SQL dump file:
    ```bash
    psql -U postgres < worldcup.sql
    ```

3.  **Run the data insertion script:**
    ```bash
    chmod +x insert_data.sh
    ./insert_data.sh
    ```

4.  **Execute the statistics queries:**
    ```bash
    chmod +x queries.sh
    ./queries.sh
    ```

---
*Completed as part of the Relational Database Curriculum on freeCodeCamp.*

