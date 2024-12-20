
# Phonebook Application with Database Sharding

This project demonstrates a phonebook system using MySQL databases with sharding. It provides a simple API to manage phonebook entries, including CRUD operations, and a CLI to interact with the API.

## Project Structure

```
/project-root
    /src
        /DatabaseSetup.java
        /PhoneBookShared.java
    /apiServer
        /apiServer.js
    /crud-cli.js
    /package.json
    /README.md
```

## Prerequisites

Before running the application, ensure you have the following installed:

- **Node.js** (version 14 or higher)
- **MySQL** (version 5.7 or higher)
- **Java** (for running Java setup files)
- **Axios** (for making HTTP requests)
- **Body-parser** (for parsing JSON data in requests)

## Setup Guide

### Step 1: Create MySQL Databases

You will need two MySQL databases to simulate the sharding setup. The first database (`shard1`) will store phonebook entries for names starting with `A-M`, and the second database (`shard2`) will store entries for names starting with `N-Z`.

1. **Log in to MySQL** using the following command:

    ```bash
    mysql -u root -p
    ```

2. **Create the databases**:

    ```sql
    CREATE DATABASE shard1;
    CREATE DATABASE shard2;
    ```

3. **Create a `phone_book` table in both databases**:

    For `shard1`:

    ```sql
    USE shard1;
    CREATE TABLE phone_book (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        phone_number VARCHAR(15) NOT NULL
    );
    ```

    For `shard2`:

    ```sql
    USE shard2;
    CREATE TABLE phone_book (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        phone_number VARCHAR(15) NOT NULL
    );
    ```

### Step 2: Setting Up the Project

1. **Clone the repository**:

    ```bash
    git clone <repository_url>
    cd <project_directory>
    ```

    Or, **download** the project files as a ZIP and extract them.

2. **Install the required Node.js packages**:

    ```bash
    npm install
    ```

### Step 3: Run Database Setup and Populate Data

First, we need to configure and set up the database tables.

#### Running `DatabaseSetup.java`:

1. **Navigate to the `src` folder**:

    ```bash
    cd src
    ```

2. **Run `DatabaseSetup.java`** to set up and populate the database with phonebook entries. This will ensure that the database is populated with some initial data.

    ```bash
    javac DatabaseSetup.java
    java DatabaseSetup
    ```

    This script sets up the database connections, creates the necessary tables, and populates the phonebook tables with sample data.

#### Running `PhoneBookShared.java`:

1. **Run `PhoneBookShared.java`** to simulate the logic of sharding based on the user's name.

    ```bash
    javac PhoneBookShared.java
    java PhoneBookShared
    ```

    This file ensures that entries with names starting with `A-M` are stored in `shard1`, and entries with names starting with `N-Z` are stored in `shard2`.

### Step 4: Start the API Server

1. **Navigate to the `apiServer` folder**:

    ```bash
    cd ../apiServer
    ```

2. **Start the API server** by running:

    ```bash
    node apiServer.js
    ```

    This will start the server on `http://localhost:3000`. The API server will handle CRUD operations for the phonebook system. You'll be able to create, read, update, and delete phonebook entries via API requests.

### Step 5: Interact with the API Using the CLI

1. **Open another terminal window** and navigate to the project directory.

2. **Run the CLI script** to interact with the phonebook API:

    ```bash
    node crud-cli.js
    ```

3. **Follow the on-screen prompts** in the CLI to:

    - Create a new phonebook entry
    - Retrieve all phonebook entries
    - Retrieve a specific phonebook entry by name
    - Update a phonebook entry
    - Delete a phonebook entry

    The CLI will interact with the shared MySQL databases (`shard1` and `shard2`) to perform the CRUD operations.

### Step 6: API Routes

Here are the available routes for the phonebook API:

- **POST `/phonebook`**: Create a new phonebook entry.

    **Request body**:

    ```json
    {
        "name": "John Doe",
        "phone_number": "123-456-7890"
    }
    ```

    **Response**:

    ```json
    {
        "id": 1,
        "name": "John Doe",
        "phone_number": "123-456-7890"
    }
    ```

- **GET `/phonebook`**: Get all phonebook entries.

    **Response**:

    ```json
    [
        {
            "id": 1,
            "name": "John Doe",
            "phone_number": "123-456-7890"
        }
    ]
    ```

- **GET `/phonebook?name=<name>`**: Get a phonebook entry by name.

    **Response**:

    ```json
    {
        "data": {
            "id": 1,
            "name": "John Doe",
            "phone_number": "123-456-7890"
        },
        "shard": "Shard 1"
    }
    ```

- **PUT `/phonebook/:id`**: Update a phonebook entry by ID.

    **Request body**:

    ```json
    {
        "name": "John Smith",
        "phone_number": "987-654-3210"
    }
    ```

- **DELETE `/phonebook/:id`**: Delete a phonebook entry by ID.

    **Response**:

    ```json
    {
        "message": "Phonebook entry deleted",
        "id": 1
    }
    ```

### Step 7: Exit the CLI

To exit the CLI, simply select `0` when prompted.

---

## Explanation of the Files

### 1. **`DatabaseSetup.java`**

- **Purpose**: This file sets up the initial database schema and populates it with sample data.
- **How it works**: It connects to MySQL, creates the databases (`shard1`, `shard2`), and inserts random phonebook entries into them.

### 2. **`PhoneBookShared.java`**

- **Purpose**: This file ensures the data is sharded across the two databases based on the first letter of the name. Names starting with `A-M` are added to `shard1`, and names starting with `N-Z` are added to `shard2`.
- **How it works**: It divides the data by querying the names and assigning them to the correct shard.

### 3. **`apiServer.js`**

- **Purpose**: This file sets up an Express.js server to handle API requests.
- **How it works**: It defines CRUD routes for managing phonebook entries and interacts with the MySQL databases (`shard1` and `shard2`) to perform the requested operations.

### 4. **`crud-cli.js`**

- **Purpose**: This is the Command-Line Interface (CLI) that allows users to interact with the phonebook API.
- **How it works**: It presents a menu for the user to choose an action (e.g., create, update, delete phonebook entries), and sends HTTP requests to the API server based on the user's input.

---

## Troubleshooting

- **Error: "ECONNREFUSED"**: This error indicates that your MySQL server is not running. Make sure MySQL is started.
- **Error: "Invalid option"**: Ensure that you select a valid option (1-5) in the CLI menu.
- **Database connection issues**: Verify the MySQL connection credentials in `apiServer.js` and `PhoneBookShared.java`.

---

## Conclusion

This project demonstrates how to build a basic phonebook system using Node.js, Java, and MySQL, with database sharding for scalability. You can extend this project by adding more features like user authentication, search functionalities, or integrating it with a frontend application.
