
# Database Sharding using MySQL

This project demonstrates a database sharding implementation using MySQL. The project creates and manages two shards, distributing data based on the first letter of names for efficient and scalable data storage and retrieval.

## Features

- Automated creation of shard databases and tables.
- CRUD operations via a Node.js Express API server.
- Data sharding based on the first letter of names (A-M to Shard1, N-Z to Shard2).
- Randomized data generation with a Java application for populating the shards.
- Command-line interface for CRUD operations using Node.js.

## Prerequisites

- Java Development Kit (JDK) 8 or later.
- MySQL 5.7 or later.
- Node.js 14 or later.
- JDBC Driver for MySQL.

## Project Structure

- `src/DatabaseSetup.java`: Sets up the shard databases and tables.
- `src/PhoneBookSharder.java`: Populates shards with random data.
- `apiServer/server.js`: Node.js Express API for CRUD operations.
- `apiServer/crud-cli.js`: CLI for interacting with the API server.

## Usage

### Setting up the Databases and Tables

1. Compile and run the `DatabaseSetup.java` file to create the shard databases and tables:
2. 
### Populating the Shards

1. Compile and run the `PhoneBookSharder.java` file to populate the shards with random data:

### Running the API Server

1. Navigate to the `apiServer` directory and install dependencies:
   ```bash
   cd apiServer
   npm install
   ```

2. Start the server:
   ```bash
   node server.js
   ```

3. The server will run at `http://localhost:3000`.

### Using the CLI

1. Run the CLI script to interact with the phonebook API:
   ```bash
   node crud-cli.js
   ```

### Example CLI Operations

#### Create an Entry
```
Enter Name: G Varun Tyagarayan
Enter Phone Number: +91-1234567890
Phonebook Entry Created: { id: 1, name: 'G Varun Tyagarayan', phone_number: '+91-1234567890' }
```

#### Get All Entries
```
All Phonebook Entries:
{
  data: [
    { id: 1, name: 'G Varun Tyagarayan', phone_number: '+91-1234567890' }
  ],
  shard: 'Both shards'
}
```

#### Update an Entry
```
Enter ID of the entry to update: 1
Enter New Name: G Varun Tyagarayan
Enter New Phone Number: +91-0987654321
Phonebook Entry Updated: { id: 1, name: 'G Varun Tyagarayan', phone_number: '+91-0987654321' }
```

#### Delete an Entry
```
Enter ID of the entry to delete: 1
Enter Name: G Varun Tyagarayan
Phonebook Entry Deleted: { message: 'Phonebook entry deleted', id: 1 }
```

## Contributing

Contributions are welcome! Please fork this repository and submit a pull request for review.

## Authors

- [G Varun Tyagarayan](https://varuntyagarayanme.netlify.app/)
