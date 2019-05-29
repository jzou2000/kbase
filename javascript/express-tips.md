---
title: Some Tips of Express.js
date: 2019-05-24
tags: express express.js tips
---

## Parsing POST data
Start from Express 4.16
````
app.use(express.json())
app.use(express.urlencode({extended: true}))
// app.use(express.multipart()) // security concerns?

// URL encoding
//    POST: name=foo&color=red
// or JSON encoding
//    POST: {"name": "foo", "color": "red"}
app.post('/url', (req, res) => {
    // your POST data is req.body
    var name = req.body.name
})
````

Express 4.0 to 4.15
````sh
npm install --save body-parser
````
and
````js
var body_parser = require('body-parser')
app.use(body_parser.json())
app.use(body_parser.urlencode({extended: true}))

````