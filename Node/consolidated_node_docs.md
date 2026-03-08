# A Comprehensive Guide to Node.js and Sequelize

This document provides a consolidated overview of the Node.js runtime, its ecosystem, and a detailed guide to using the Sequelize ORM for database integration.

## 1. Introduction to Node.js

### 1.1. What is Node.js?

-   **Runtime Environment**: Node.js is a server-side JavaScript runtime environment. It allows you to run JavaScript code on the server, outside of a web browser.
-   **V8 Engine**: Node.js is built on Chrome's V8 JavaScript engine, which it embeds within a C++ application. V8 compiles JavaScript directly into native machine code, making it highly performant.
-   **Use Cases**: Node.js is excellent for building fast, scalable network applications, such as web servers, API backends, shell scripts, and more.

### 1.2. Node.js vs. The Browser

| Feature          | Browser Environment                               | Node.js Environment                                            |
| ---------------- | ------------------------------------------------- | -------------------------------------------------------------- |
| **Global Object**| `window`                                          | `global`                                                       |
| **DOM Access**   | Yes (e.g., `document`, `window.onload`)           | No. No `document` or `window` objects.                         |
| **Modules**      | ES Modules (`import`/`export`). Historically, no module system. | CommonJS (`require`/`module.exports`) is built-in.           |
| **Environment**  | Runs on user's machine in various browsers (Chrome, Firefox, etc.). | Runs on a server or a developer's machine in a single environment. |
| **APIs**         | Provides browser-specific APIs (DOM, Fetch, etc.). | Provides server-specific APIs (File System, HTTP, Process, etc.). |

### 1.3. The Event Loop and Non-Blocking I/O

Node.js uses a single-threaded, event-driven architecture that allows it to handle many concurrent connections efficiently.

-   **Single-Threaded**: Node.js runs your JavaScript code on a single thread.
-   **Event Loop**: An internal loop that continuously checks for and processes events (like an incoming API request or a completed database query) from a queue.
-   **Non-Blocking I/O**: When an application needs to perform an I/O (Input/Output) operation (like reading a file or making a network request), it doesn't wait for the operation to complete. Instead, it registers a callback function and continues executing other code. When the I/O operation finishes, the event loop picks up the result and executes the corresponding callback. This prevents the single thread from being blocked by slow operations.

### 1.4. The REPL

REPL stands for **R**ead-**E**val-**P**rint-**L**oop. It's an interactive console for running JavaScript code. You can start it by typing `node` in your terminal without a filename.

## 2. Core Concepts

### 2.1. Modules (CommonJS)

Node.js uses the CommonJS module system to organize code into separate files.

-   **`require()`**: A built-in function to import a module. To import a local file, use a relative path (e.g., `./myModule.js`). To import a package from `node_modules`, just use its name (e.g., `express`).
-   **`module.exports`**: A special object. Any properties or functions attached to `module.exports` will be exposed and can be imported by other files.

**Example:**
```javascript
// ./my-module.js
const sayHello = () => "Hello!";
module.exports.sayHello = sayHello;

// ./index.js
const myModule = require('./my-module.js');
console.log(myModule.sayHello()); // Prints "Hello!"
```

### 2.2. The `process` Object

The `process` object is a global object that provides information about, and control over, the current Node.js process.

-   **`process.argv`**: An array containing the command-line arguments passed when the Node.js process was launched.
    -   `process.argv[0]`: Path to the Node.js executable.
    -   `process.argv[1]`: Path to the script being executed.
    -   `process.argv[2]...`: Additional command-line arguments.
-   **`process.env`**: An object containing the user's environment variables. This is crucial for configuring applications for different environments (development, staging, production) without hardcoding values. You can set environment variables in your shell before running the script:
    ```bash
    NODE_ENV=production node index.js
    ```
    Inside `index.js`, `process.env.NODE_ENV` would be `"production"`.

### 2.3. File System (`fs` module)

The `fs` module provides an API for interacting with the file system. Most methods have both synchronous (`...Sync`) and asynchronous (callback-based or Promise-based) forms.

```javascript
const fs = require('fs');

// Asynchronous read
fs.readFile('my-file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Synchronous read
try {
  const data = fs.readFileSync('my-file.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error(err);
}
```

### 2.4. Buffers and Streams

-   **Buffer**: A temporary holding spot for a chunk of data, typically in RAM. Node.js uses buffers to handle binary data.
-   **Stream**: The flow of data from one point to another. Streams are a powerful way to handle large amounts of data efficiently without keeping it all in memory. For example, you can read a large file and pipe its contents directly to an HTTP response.

## 3. Project Management with npm

`npm` (Node Package Manager) is the default package manager for Node.js.

### 3.1. `package.json`

This file is the heart of a Node.js project. It contains metadata and manages dependencies.
-   **`npm init`**: Command to create a `package.json` file.
-   **`dependencies`**: Packages required for the application to run in production. Install with `npm install <package-name>`.
-   **`devDependencies`**: Packages only needed for development and testing (e.g., linters, test frameworks). Install with `npm install <package-name> --save-dev`.
-   **`scripts`**: Defines command-line scripts to automate tasks (e.g., `"start": "node index.js"`). Run with `npm run <script-name>`.

### 3.2. Semantic Versioning (SemVer)

Versions are formatted as `MAJOR.MINOR.PATCH`.
-   **`PATCH`**: For backward-compatible bug fixes.
-   **`MINOR`**: For backward-compatible new features.
-   **`MAJOR`**: For changes that break backward compatibility.

In `package.json`:
-   **`~` (Tilde)**: Allows patch-level changes. `~1.2.3` will accept `1.2.4`, but not `1.3.0`.
-   **`^` (Caret)**: Allows minor-level changes. `^1.2.3` will accept `1.3.0`, but not `2.0.0`.

### 3.3. Common `npm` Commands

-   **`npm install` (or `npm i`)**: Installs all dependencies from `package.json`.
-   **`npm install <package>`**: Installs a specific package and adds it to `dependencies`.
-   **`npm uninstall <package>`**: Removes a package.
-   **`npm outdated`**: Checks for outdated packages.
-   **`npm audit`**: Scans your project for security vulnerabilities.
-   **`npm ls`**: Lists installed packages.

## 4. Building a Web Server

### 4.1. The `http` Module

Node.js has a built-in `http` module for creating web servers.

```javascript
const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
  // Parse the request URL
  const parsedUrl = url.parse(req.url, true);
  const path = parsedUrl.pathname; // e.g., /users
  const method = req.method.toUpperCase(); // e.g., GET

  // Simple routing
  if (path === '/hello') {
    res.writeHead(200, {'Content-Type': 'application/json'});
    res.end(JSON.stringify({ message: 'Hello World' }));
  } else {
    res.writeHead(404, {'Content-Type': 'application/json'});
    res.end(JSON.stringify({ message: 'Not Found' }));
  }
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

### 4.2. Introduction to Express.js

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It simplifies the process of creating a server and handling routes.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

## 5. Database Integration with Sequelize

Sequelize is a modern TypeScript and Node.js ORM (Object-Relational Mapper) for Postgres, MySQL, MariaDB, SQLite, and Microsoft SQL Server. It simplifies database interactions by mapping database tables to JavaScript objects.

### 5.1. Part 1: Setup and Configuration

1.  **Install Sequelize and a Driver**:
    ```bash
    npm install sequelize
    # Install the driver for your database
    npm install mysql2 # For MySQL
    npm install pg pg-hstore # For Postgres
    ```
2.  **Establish a Connection**: Create a Sequelize instance to connect to your database.
    ```javascript
    const { Sequelize } = require('sequelize');

    const sequelize = new Sequelize('database_name', 'username', 'password', {
      host: 'localhost',
      dialect: 'mysql' /* one of 'mysql' | 'postgres' | 'sqlite' | 'mariadb' | 'mssql' */
    });

    // Test the connection
    try {
      await sequelize.authenticate();
      console.log('Connection has been established successfully.');
    } catch (error) {
      console.error('Unable to connect to the database:', error);
    }
    ```

### 5.2. Part 2: Models

Models represent tables in your database.
1.  **Define a Model**: Use `sequelize.define()`.
    ```javascript
    const { DataTypes } = require('sequelize');

    const User = sequelize.define('User', {
      // Model attributes are defined here
      firstName: {
        type: DataTypes.STRING,
        allowNull: false
      },
      lastName: {
        type: DataTypes.STRING
      }
    }, {
      // Other model options go here
    });
    ```
2.  **Sync the Model**: `sync()` creates the table if it doesn't exist.
    ```javascript
    // This will create the table, dropping it first if it already existed
    await User.sync({ force: true });
    console.log("The table for the User model was just (re)created!");
    ```

### 5.3. Part 3: Basic Queries (CRUD)

-   **Create (Insert)**:
    ```javascript
    const jane = await User.create({ firstName: "Jane", lastName: "Doe" });
    ```
-   **Read (Select)**:
    ```javascript
    // Find all users
    const users = await User.findAll();

    // Find one user with a WHERE clause
    const user = await User.findOne({
      where: {
        firstName: "Jane"
      }
    });
    ```
-   **Update**:
    ```javascript
    await User.update({ lastName: "Smith" }, {
      where: {
        firstName: "Jane"
      }
    });
    ```
-   **Delete**:
    ```javascript
    await User.destroy({
      where: {
        firstName: "Jane"
      }
    });
    ```

### 5.4. Part 4: Associations

Sequelize can define relationships between models.
-   **One-to-One (`hasOne`, `belongsTo`)**: A `User` has one `Profile`.
    ```javascript
    Profile.belongsTo(User);
    User.hasOne(Profile);
    ```
-   **One-to-Many (`hasMany`, `belongsTo`)**: A `Project` has many `Tasks`.
    ```javascript
    Project.hasMany(Task);
    Task.belongsTo(Project);
    ```
-   **Many-to-Many (`belongsToMany`)**: A `Student` belongs to many `Courses`. This requires a "through" table.
    ```javascript
    Student.belongsToMany(Course, { through: 'StudentCourse' });
    Course.belongsToMany(Student, { through: 'StudentCourse' });
    ```
To fetch associated data, use the `include` option in your query:
```javascript
const users = await User.findAll({ include: Profile });
```

### 5.5. Part 5: Raw SQL Queries

You can execute raw SQL for complex queries.
```javascript
const [results, metadata] = await sequelize.query("SELECT * FROM Users");

// With replacements to prevent SQL injection
const users = await sequelize.query(
  'SELECT * FROM Users WHERE status = :status',
  {
    replacements: { status: 'active' },
    type: QueryTypes.SELECT
  }
);
```