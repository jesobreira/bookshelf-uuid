# bookshelf-uuid-column
[![Build Status](https://circleci.com/gh/estate/bookshelf-uuid.svg?style=shield)](https://circleci.com/gh/estate/bookshelf-uuid)
[![Code Climate](https://codeclimate.com/github/estate/bookshelf-uuid/badges/gpa.svg)](https://codeclimate.com/github/estate/bookshelf-uuid)
[![Test Coverage](https://codeclimate.com/github/estate/bookshelf-uuid/badges/coverage.svg)](https://codeclimate.com/github/estate/bookshelf-uuid/coverage)
[![Version](https://badge.fury.io/js/bookshelf-uuid.svg)](http://badge.fury.io/js/bookshelf-uuid)
[![Downloads](http://img.shields.io/npm/dm/bookshelf-uuid.svg)](https://www.npmjs.com/package/bookshelf-uuid)

Automatically generate UUIDs for your models and let you choose the column name.

Useful if you are using standard integer primary keys but prefer not to expose these to the public, rather identifying your resources based on an unique ID.

### Installation

After installing `bookshelf-uuid-column` with `npm i --save bookshelf-uuid-column`,
all you need to do is add it as a bookshelf plugin and enable it on your models.

```javascript
let knex = require('knex')(require('./knexfile.js').development)
let bookshelf = require('bookshelf')(knex)

// Add the plugin
bookshelf.plugin(require('bookshelf-uuid-column'))

// Enable it on your models
let User = bookshelf.Model.extend({ tableName: 'users', uuid: true, uuidAttribute: 'uuid' }) // default uuidAttribute is 'uuid'
```

### Usage

Nothing fancy here, just keep using bookshelf as usual.

```javascript
// This user is indestructible
let user = yield User.forge({ email: 'foo@bar' }).save()
console.log(user.id) // 6b7a192f-6e1c-4dcb-8e57-14ab16d5fdf4
```

### Settings

`bookshelf-uuid-column` generates UUIDs v4 by default, but you can easily switch to
v1 UUIDs or a custom generator.

```javascript
bookshelf.plugin(require('bookshelf-uuid-column'), {
  type: 'v1' // Or your own function
})
```

### Testing

```bash
git clone git@github.com:jesobreira/bookshelf-uuid-column.git
cd bookshelf-uuid-column && npm install && npm test
```
