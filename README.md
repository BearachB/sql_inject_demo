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
13. Run `CREATE DATABASE sql_injection_demo` to create a new database for this project
14. `QUIT` exits the MySQL monitor
15. Note: `mysql.server stop` stops the MySQL server. Do not run this if you are using the server.

Add your MySQL credentials to an environment variable.
```bash
$ cd server
$ echo 'MYSQL_CREDS="mysql_password"' > .env
```

The following will start up the actual webapp.
```bash
$ cd client && yarn install     # Installs client dependencies
$ cd ../server && yarn install  # Installs server dependencies
$ yarn dev                      # Starts Express server
```
In a new terminal, run:
```bash
$ cd client
$ yarn serve                    # Starts Vue.js server
```

If you get errors connecting to MySQL, run the following:
`$ mysql -u root -p`
```SQL
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mysql_password';
flush privileges;
QUIT;
```


## XKCD
![Bobby Tables XKCD Comic](https://imgs.xkcd.com/comics/exploits_of_a_mom.png)

(In case you haven't seen this yet)
