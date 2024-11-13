# News Letter Registration Web App with MySQL and Express

## Project Overview

This project is a user registration web application developed using Node.js, Express, and MySQL. It allows users to register by providing their email addresses, and the app stores this information in a MySQL database. The application uses SQL for managing the data interactions, including querying and updating the user data in the database.

## Key Technologies

- **Node.js**: The runtime environment for executing JavaScript on the server side.
- **Express**: A web application framework for Node.js, used to set up the server and define routes.
- **MySQL**: The relational database management system used to store user data.
- **EJS**: Embedded JavaScript templating for rendering dynamic HTML content.
- **dotenv**: Environment variable management for securely handling sensitive data.
- **body-parser**: Middleware for parsing request bodies, specifically `application/x-www-form-urlencoded` for form data in this project.

## Project Structure

The main structure includes:
1. **Environment Configuration**: Using `.env` to securely store database credentials.
2. **Express Server Setup**: Configured to listen on port 8080.
3. **Static Files**: Serving static files from the `public` directory.
4. **MySQL Connection**: Configuring a connection to the MySQL database.

## SQL Usage

### Database Setup

The MySQL database consists of a single table named `users`. Each record represents a user and includes fields for a unique user ID and an email address.

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE
);
```
## SQL Queries
1. Counting Users
The home route (/) displays the total number of registered users. To achieve this, a SELECT COUNT(*) query is used:
```
let q = "SELECT COUNT(*) AS count FROM users";
connection.query(q, function(err, results){
    if(err) throw err;
    let count = results[0].count;
    res.render("home", {count: count});
});
```
2. Registering a New User
The /register route handles new user registrations. When a form is submitted, it executes an INSERT INTO query to add the user’s email to the users table:
```
let person = { email: req.body.email };
connection.query('INSERT INTO users SET ?', person, function(err, result) {
    if (err) throw err;
    res.redirect("/");
});
```
The SQL INSERT INTO statement is dynamically populated using the user-provided email, which is securely passed to prevent SQL injection.

## Key Features
#### Environment Variables: Sensitive information like database credentials are stored in a .env file to ensure security.
#### Data Handling with SQL: This app uses SQL queries to retrieve and modify data, showcasing SQL’s integration with Node.js for effective data management.
#### Error Handling: Basic error handling is implemented to ensure the application fails gracefully in the event of a database error.

## Running the Project
1. Clone the repository.
2. Install dependencies:
  ```
npm install
```
3. Set up a MySQL database and create the users table.
4. Configure environment variables in a .env file:
   ```
   DB_HOST=your_host
   DB_USER=your_user
   DB_PASSWORD=your_password
   DB_NAME=your_database
   ```
5. Start the server:
   ```node app.js```
6. Open http://localhost:8080 in a browser to view the app.

## Conclusion
### This project demonstrates a straightforward use of SQL within a Node.js environment, allowing for data querying, insertion, and error handling with SQL and MySQL. It serves as a template for building similar applications that require user registration and database interaction with SQL.

