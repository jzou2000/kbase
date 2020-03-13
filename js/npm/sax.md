---
title: sax
weight: 100
tags: [npm]
catagories: [javascript]
---

[sax](https://www.npmjs.com/package/sax) - an evented streaming XML parser in JavaScript.

Alternative: node-expat (4.8M) is libexpat node.js bind.

```js
#! /usr/bin/env node
// test app for
//  sax-js          js stream of xml-sax
//
const fs = require('fs')
const readline = require('readline')

const sax = require('sax')
const parser = sax.createStream(true, {position: true, lowercase: true})
const log = console.log

var ctx = {
    inText: false,
    text: '',
    append (t) {
        this.inText = true
        this.text += t
    },
    flush () {
        if (this.inText) {
            log(`    text=[${this.text}]`)
            this.text = ''
            this.inText = false
        }
    }
}

parser.on('opentag', (node) => {
    ctx.flush()
    var attr = node.attributes
    var sattr = Object.keys(attr).length > 0 ? ` ${JSON.stringify(attr)}` : ''
    log(`name=${node.name}${sattr}`)
    rs.skip = true
    rs.close()
})
.on('closetag', (name) => {
    ctx.flush()
    log(`----${name}`)
})
.on('text', (text) => {
    // no process at all (e.g. trim etc)
    ctx.append(text)
})
.on('comment', (s) => {
    ctx.flush()
    log(`    comment=[${s}]`)
})
.on('processinginstruction', (obj) => {
    // sax-js doesn't parse processing-instruction
    //      e.g. <?xml version="1.0" encoding="utf-8"?>
    // the object has (in above example)
    //      name    "xml"
    //      body    {version: "1.0", encoding: "utf-8"}
    ctx.flush()
    log(`    pi=` + JSON.stringify(obj, null, 2))
})
.on('error', (err) => {
    if (!rs.skip) {
        log(`parser error: ${err} at line=${parser._parser.line} col=${parser._parser.column}`)
        //log(`parser: ${JSON.stringify(parser, null, 2)}`)
        rs.skip = 1
        rs.close()
    }
})
.on('end', () => {
    log(`    ====end===`)
})

var rs = fs.createReadStream(process.argv.slice(2)[0], 'utf-8')
// var rl = readline.createInterface({
//     input: rs,
//     crlfDelay: Infinity
// })
rs.pipe(parser)

/*
rl.on('end', () => {
    log(`EOF`)
})
.on('close', () => {
    log(`close`)
})
.on('line', (data) => {
    if (rl.skip) return
    //log(typeof data)
    //log(`${JSON.stringify(data)}`)
    //log(`====line [${data}]`)
    parser.write(data)   
})
*/
log(`app end`)

```

This is another example that detects the root tag without reading the whole XML file.

```js

// find root tag using sax without parsing the whole xml file

const log = console.log

const get_xml_root = function (fname) {
    const sax = require('sax')
    const fs = require('fs')
    var saxp = sax.parser(true)
    var xfs = fs.createReadStream(fname, {encoding: 'utf-8', highWaterMark: 1024})
        .on('data', (data) => {
            //log(`    on data=${data}`)
            saxp.write(data)
        })
    return new Promise((resolve, reject) => {
        saxp.onopentag = (tag) => {
            xfs.close()
            resolve(tag.name)
        }
        saxp.onerror = (err) => {
            reject(err)
        }
    })
}

get_xml_root(process.argv[2])
    .then((tag_name) => {
        log(`root: ${tag_name}`)
    })
    .catch((e) => {
        log(`catch: ${e}`)
    })


```
