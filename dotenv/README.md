# dotenv

```
npm install dotenv@16.0.1
```

## .env

```
MYSQL_HOST=localhost
MYSQL_PORT=33060
MYSQL_USER=root
MYSQL_PASSWORD=root
MYSQL_DATABASE_NAME=trybecashdb
MYSQL_WAIT_FOR_CONNECTIONS=true
MYSQL_CONNECTION_LIMIT=10
MYSQL_QUEUE_LIMIT=0
```

## connection.js

```
//const mysql = require('mysql2/promise');

// const connection = mysql.createPool({
  host: process.env.MYSQL_HOST,
  port: process.env.MYSQL_PORT,
  user: process.env.MYSQL_USER,
  password: process.env.MYSQL_PASSWORD,
  database: process.env.MYSQL_DATABASE_NAME,
  waitForConnections: process.env.MYSQL_WAIT_FOR_CONNECTIONS,
  connectionLimit: process.env.MYSQL_CONNECTION_LIMIT,
  queueLimit: process.env.MYSQL_QUEUE_LIMIT,
// });

// module.exports = connection;
```

## server.js

```
require('dotenv').config();
// const app = require('./app');

// const port = 3001;

// app.listen(port, async () => {
//   console.log(`API TrybeCash está sendo executada na porta ${port}`);
// });
```

## .gitignore

```
node_modules
.env
```

## .env-example 

```
MYSQL_HOST=<ENDEREÇO DO BANCO>
MYSQL_USER=<NOME DE USUÁRIO DO BANCO>
MYSQL_USER=<PORTA DE CONEXÃO DO BANCO>
MYSQL_PASSWORD=<SENHA DE ACESSO DO BANCO>
MYSQL_DATABASE_NAME=<NOME DO BANCO DE DADOS>
MYSQL_WAIT_FOR_CONNECTIONS=true
MYSQL_CONNECTION_LIMIT=10
MYSQL_QUEUE_LIMIT=0
```