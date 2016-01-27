# RethinkDBFS
A file storage system for RethinkDB inspired by GridFS

[![npm version](https://img.shields.io/npm/v/rethinkdbfs.svg)](https://www.npmjs.com/package/rethinkdbfs)
[![license](https://img.shields.io/npm/l/rethinkdbfs.svg)](https://github.com/internalfx/rethinkdbfs/blob/master/LICENSE)

---

Special thanks to [Arthur Andrew Medical](http://www.arthurandrew.com/) for sponsoring this project.

Arthur Andrew Medical manufactures products with ingredients that have extensive clinical research for safety and efficacy. We specialize in Enzymes, Probiotics and Antioxidants.

---

## Installation

```
npm install rethinkdbfs
```

## Getting Started

```javascript
var RethinkDBFS = require('rethinkdbfs')

var dbfs = RethinkDBFS({db: 'example'})

// prepDB creates tables and indexes if they don't exist, returns a promise.
dbfs.prepDB().then(function () {
  // We are now ready to read and write files

  // create read stream from file
  var fileStream = fs.createReadStream('./bigvid.mp4')

  // Pipe it to a dbfs write stream
  fileStream.pipe(dbfs.writeFile({filename: '/videos/bigvid.mp4'}))

  // Listen for 'end' to know when the file is written to the database
  fileStream.on('end', function () {
    // File is now written to the database

    //Read the file and pipe it to a write stream to save the file back out to the file system.
    dbfs.readFile({filename: '/videos/bigvid.mp4'}).pipe(fs.createWriteStream('./test-bigvid.mp4'))
  })

})

```
