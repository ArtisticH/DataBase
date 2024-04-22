
```node.js
// connetcion.js

const mysql = require('mysql');

async function main(callback) {
  
  const mysqlConnection = mysql.createConnection({
    host: process.env.MYSQL_HOST,
    user: process.env.MYSQL_USER,
    password : process.env.MYSQL_PASSWORD,
    database : process.env.MYSQL_DATABASE
  });

  try {
    mysqlConnection.connect();
    callback(mysqlConnection);
  } catch (e) {
    console.log('connection.js error', e);
    throw new Error('Unable to Connect to Database');
  }
}

module.exports = main;
```


```node.js
// server.js

const myDB = require('./connection.js');
const routes = require('./routes.js');
...
myDB(mysqlConnection => {
  routes(app, mysqlConnection);
});
```

```node.js
// routes.js

function queryFunc(sql, values, mysqlConnection) {
  return new Promise((resolve, reject) => {
    mysqlConnection.query(sql, values, (err, results) => {
      if (err) reject(err);
      else resolve(results);
    });
  });
}

module.exports = function (app, mysqlConnection) {
  app.route('/').get((req, res) => {
    res.sendFile(__dirname + '/index.html');
  });

  app.route('/category').get(async (req, res) => {
    const query = 'SELECT * FROM category';
    const results = await queryFunc(query, [], mysqlConnection);
    const resultsArr = [];
...
```
