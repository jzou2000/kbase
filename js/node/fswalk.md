---
title: fswalk
description: walk fs directory with optional filter
---


```js
//
//  fswalk
//      a promise that walks a tree asynchrously with optional filter (RE pattern),
//      resolved with a list of {name, stat}
//
const fs = require('fs')
const path = require('path')

// to disable warnings like
// (node:6988) ExperimentalWarning: The fs.promises API is experimental
// export NODE_NO_WARNINGS=1
// or node --no-warnings

var _fswalk = function(wpath, pattern) {
    var result = []
    const _walk = function(pwd, pattern) {
        return new Promise((resolve, reject) => {
            fs.readdir(pwd, (err, files) => {
                if (err) reject(err)
                if (!files) return
                Promise.all(files.map((f) => {
                    var fpath = path.join(pwd, f)
                    return new Promise((resolve, reject) => {
                        fs.stat(fpath, (err, stats) => {
                            if (err) reject(err)
                            return resolve(stats)
                        }); })
                        .then((stats) => {
                            if (stats.isDirectory()) {
                                return _walk(fpath, pattern)
                            } else {
                                if (!pattern || fpath.match(pattern))
                                    result.push({name: fpath, stat: stats})
                            }
                        })
                })).then(() => { return resolve(result); })
            })
        })
    }

    return _walk(wpath, pattern)
}


exports.fswalk = _fswalk


```

The sample script that uses this module

```js
// test app for:
//      fswalk
//
const tk = require('./jtk')
const path = require('path')

const root = process.argv[2] || '.'

// walk the path root and find xml files of the pattern
tk.fswalk(root, /suite.*\.xml$/i)
.then((flist) => {
    for (var n of flist) {
        console.log(path.relative(root, n.name))
    }
})
.catch ((err) => {
    console.log(`catch: ${err}`)
})

```
