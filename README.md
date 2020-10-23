# Starter Code

* Includes: Express server + routing
* Angular app with mock data

## Instructions

### check your dependencies `ng update`

### type `yarn` or `npm i`

### run `npm start`

* starts server and loads app in browser

## or run `node server.js` in one terminal and `ng s -o` in another

* server on localhost:3000, app on localhost:4200

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.1.2.

## Task: Database setup

1. Run: ```npm install sequelize sqlite -save```
2. Add file: models/db.js
3. Add code: <https://github.com/sequelize/express-example/blob/master/express-main-example/sequelize/index.js>
4. NOTE this is updated file compaired to the video example. Needs investigation and update in the code

```JavaScript
const { Sequelize } = require('sequelize');
const { applyExtraSetup } = require('./extra-setup');

// In a real app, you should keep the database connection URL as an environment variable.
// But for this example, we will just use a local SQLite database.
// const sequelize = new Sequelize(process.env.DB_CONNECTION_URL);
const sequelize = new Sequelize({
 dialect: 'sqlite',
 storage: 'sqlite-example-database/example-db.sqlite',
 logQueryParameters: true,
 benchmark: true
});

const modelDefiners = [
 require('./models/user.model'),
 require('./models/instrument.model'),
 require('./models/orchestra.model'),
 // Add more models here...
 // require('./models/item'),
];

// We define all models according to their files.
for (const modelDefiner of modelDefiners) {
 modelDefiner(sequelize);
}

// We execute any extra setup after the models are defined, such as adding associations.
applyExtraSetup(sequelize);

// We export the sequelize connection instance to be used around our app.
module.exports = sequelize;
```

1. Video File version (requires updating)

```JavaScript
"use strict";

var fs = require("fs");
var path = require("path");
const { Sequelize } = require("sequelize");
var Squelize = require("sequelize");
var basename = path.basename(__filename);
var env = process.env.NODE_ENV || "development";
var config = require(__dirname + "/../config/config.js")[env];
var db = {};

if (config.use_env_variable) {
  var sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
  var sequelize = new Sequelize(
    config.database,
    config.username,
    config.password,
    config
  );
}

fs.readdirSync(__dirname)
  .filter((file) => {
    return (
      file.indexOf(".") !== 0 && file !== basename && file.slice(-3) === ".js"
    );
  })
  .forEach((file) => {
    var model = sequelize["import"](path.join(__dirname, file));
    db[model.name] = model;
  });

Object.keys(db).forEach(() => {
  if (db[modelName].associate) {
    db[modelName].associate(db);
  }
});

db.sequelize = sequelize;
db.Sequelize = Squelize;

module.exports = db;
```
