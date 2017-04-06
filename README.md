# api documentation for  [dat (v12.0.3)](https://datproject.org)  [![npm package](https://img.shields.io/npm/v/npmdoc-dat.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-dat) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-dat.svg)](https://travis-ci.org/npmdoc/node-npmdoc-dat)
#### Dat is the package manager for data. Easily share and version control data.

[![NPM](https://nodei.co/npm/dat.png?downloads=true)](https://www.npmjs.com/package/dat)

[![apidoc](https://npmdoc.github.io/node-npmdoc-dat/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-dat_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-dat/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-dat/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-dat/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "max ogden"
    },
    "bin": {
        "dat": "bin/cli.js"
    },
    "bugs": {
        "url": "https://github.com/datproject/dat/issues"
    },
    "dependencies": {
        "dat-doctor": "^1.2.3",
        "dat-encoding": "^4.0.2",
        "dat-node": "^1.4.0",
        "dat-registry": "^2.1.2",
        "debug": "^2.6.2",
        "memdb": "^1.3.1",
        "mkdirp": "^0.5.1",
        "nets": "^3.2.0",
        "pretty-bytes": "^4.0.2",
        "progress-string": "^1.2.1",
        "prompt": "^1.0.0",
        "rimraf": "^2.5.4",
        "status-logger": "^3.0.0",
        "subcommand": "^2.1.0",
        "xtend": "^4.0.1"
    },
    "description": "Dat is the package manager for data. Easily share and version control data.",
    "devDependencies": {
        "dat-land": "github:datproject/datfolder",
        "hypercore": "^4.15.1",
        "hyperdiscovery": "^1.0.1",
        "recursive-readdir-sync": "^1.0.6",
        "standard": "^9.0.1",
        "tap-spec": "^4.1.1",
        "tape": "^4.6.3",
        "tape-spawn": "^1.4.2"
    },
    "directories": {
        "test": "tests"
    },
    "dist": {
        "shasum": "41bafebe40a7d4f9f347ae3a96afc64bd4fcd951",
        "tarball": "https://registry.npmjs.org/dat/-/dat-12.0.3.tgz"
    },
    "gitHead": "29246df27dff180092508292b087ba8529338f2e",
    "homepage": "https://datproject.org",
    "keywords": [
        "data package",
        "dataset",
        "replication",
        "distributed"
    ],
    "license": "BSD-3-Clause",
    "maintainers": [
        {
            "name": "jhand",
            "email": "joe@joeahand.com"
        },
        {
            "name": "karissa",
            "email": "krmckelv@gmail.com"
        },
        {
            "name": "mafintosh",
            "email": "mathiasbuus@gmail.com"
        },
        {
            "name": "maxogden",
            "email": "max@maxogden.com"
        }
    ],
    "name": "dat",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/datproject/dat.git"
    },
    "scripts": {
        "auth-server": "DEBUG=* node scripts/auth-server.js",
        "install-precommit": "echo ./node_modules/.bin/standard > .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit",
        "standard": "standard",
        "test": "standard && tape 'tests/*[!auth].js' | tap-spec"
    },
    "version": "12.0.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module dat](#apidoc.module.dat)
1.  object <span class="apidocSignatureSpan">dat.</span>dat_json

#### [module dat.dat_json](#apidoc.module.dat.dat_json)
1.  [function <span class="apidocSignatureSpan">dat.dat_json.</span>read (dat, cb)](#apidoc.element.dat.dat_json.read)
1.  [function <span class="apidocSignatureSpan">dat.dat_json.</span>write (dat, defaults, cb)](#apidoc.element.dat.dat_json.write)



# <a name="apidoc.module.dat"></a>[module dat](#apidoc.module.dat)



# <a name="apidoc.module.dat.dat_json"></a>[module dat.dat_json](#apidoc.module.dat.dat_json)

#### <a name="apidoc.element.dat.dat_json.read"></a>[function <span class="apidocSignatureSpan">dat.dat_json.</span>read (dat, cb)](#apidoc.element.dat.dat_json.read)
- description and source-code
```javascript
read = function (dat, cb) {
  // dat.json
  // reads to dat.meta if exists
  // (TODO: move to module & validate dat.json)
  fs.readFile(datJsonFile(dat), 'utf8', function (err, body) {
    if (err) return cb(err)
    if (!body) return cb(null, {})
    var meta
    try {
      meta = JSON.parse(body)
    } catch (e) {
      return cb(new Error('Error reading the dat.json file.'))
    }
    cb(null, meta)
  })
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.dat.dat_json.write"></a>[function <span class="apidocSignatureSpan">dat.dat_json.</span>write (dat, defaults, cb)](#apidoc.element.dat.dat_json.write)
- description and source-code
```javascript
write = function (dat, defaults, cb) {
  if (typeof defaults === 'function') {
    cb = defaults
    defaults = {}
  }
  dat.meta = {
    title: defaults.title || path.basename(dat.path),
    url: defaults.url,
    name: defaults.name,
    description: defaults.description || ''
  }
  if (dat.key) dat.meta.url = 'dat://' + stringKey(dat.key)
  fs.writeFile(datJsonFile(dat), JSON.stringify(dat.meta), cb)
}
```
- example usage
```shell
...
// TODO: could be optimized for frequent metadata updates
archive.metadata.on('update', updateDownload)

// General Archive Info
var niceType = (type === 'clone') ? 'Cloning' : type.charAt(0).toUpperCase() + type.slice(1) + 'ing'
progressOutput[0] = '${niceType} Dat Archive: ${dat.path}'
progressOutput[1] = ui.link(dat.key) + '\n'
if (opts.quiet && type !== 'clone') process.stdout.write(ui.link(dat.key))

// Stats
stats = dat.trackStats()
stats.on('update:blocksProgress', checkDone)

// Network
if (!opts.upload && type !== 'sync') opts.upload = false // Do not upload on pull/clone
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
