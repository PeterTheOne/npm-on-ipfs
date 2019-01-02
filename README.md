<p align="center">
  <img src="https://github.com/ipfs-shipyard/npm-on-ipfs/raw/master/img/npm-on-ipfs.jpg" alt="npm distributed on top of lots of connected IPFS nodes worldwide" />
</p>

# npm on IPFS

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](https://protocol.ai)
[![](https://img.shields.io/badge/project-IPFS-blue.svg?style=flat-square)](http://ipfs.io/)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)
[![Build Status](https://ci.ipfs.team/buildStatus/icon?job=IPFS%20Shipyard/npm-on-ipfs/master)](https://ci.ipfs.team/job/IPFS%20Shipyard/job/npm-on-ipfs/job/master/)
[![Code Coverage](https://codecov.io/gh/ipfs-shipyard/npm-on-ipfs/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs-shipyard/npm-on-ipfs)
[![Dependency Status](https://david-dm.org/ipfs-shipyard/npm-on-ipfs.svg?style=flat-square)](https://david-dm.org/ipfs-shipyard/npm-on-ipfs)

> Install your favourite modules from the Distributed Web using IPFS. Have a cache always ready and share them in all your local networks.

## PRE-RELEASE WARNING

This module depends on features in the upcoming [v0.34.0](https://github.com/ipfs/js-ipfs/issues/1721) release of [js-ipfs](https://github.com/ipfs/js-ipfs) (due by the end of December 2018).

If you use this module, please also upgrade your IPFS install with

```console
npm install -g ipfs@0.34.0-pre.0
```

## Resources

- [The original demo video](https://vimeo.com/147968322)
- [Lengthy introduction in a blog post](http://daviddias.me/blog/stellar-module-management/)
- [Node.js Interactive Talk - Stellar Module Management](https://www.youtube.com/watch?v=-S-Tc7Gl8FM)

## Lead Maintainer

[Alex Potsides](https://github.com/achingbrain)

## Install this module

```console
> npm i ipfs-npm -g
```

# Usage

`ipfs-npm` wraps your chosen package manager (e.g. npm or yarn) with configuration to use IPFS to retrieve your dependences instead of over HTTP from the central npm registry.

In the directory with your `package.json` file, run:

```console
$ ipfs-npm install
👿 Spawning an in-process IPFS node
Swarm listening on /ip4/127.0.0.1/tcp/57029/ipfs/QmVDtTRCoYyYu5JFdtrtBMS4ekPn8f9NndymoHdWuuJ7N2
🗂️ Loading registry index from https://registry.js.ipfs.io
☎️ Dialling registry mirror /ip4/35.178.192.119/tcp/10015/ipfs/QmWBaYSnmgZi6F6D69JuZGhyL8rm6pt8GX5r7Atc6Gd7vR,/dns4/registry.js.ipfs.io/tcp/10015/ipfs/QmWBaYSnmgZi6F6D69JuZGhyL8rm6pt8GX5r7Atc6Gd7vR
🗑️ Replacing old registry index if it exists
📠 Copying registry index /ipfs/QmQmVsNFw3stJky7agrETeB9kZqkcvLSLRnFFMrhiR8zG1 to /npm-registry
👩‍🚀 Starting local proxy
🚀 Server running on port 57314
🎁 Installing dependencies with /Users/alex/.nvm/versions/node/v10.8.0/bin/npm
...
```

You can use any command you'd use with npm/yarn with ipfs-npm in exactly the same way:

```console
$ ipfs-npm install
$ ipfs-npm version minor
$ ipfs-npm publish

$ ipfs-npm --package-manager=yarn
// etc
```

## CLI

```console
$ ipfs-npm --help
ipfs-npm

Installs your js dependencies using IPFS

Options:
  --help                        Show help                              [boolean]
  --version                     Show version number                    [boolean]
  --package-manager             Which package manager to use - eg. npm or yarn
                                                                [default: "npm"]
  --ipfs-registry               Where to download any packages that haven't made
                                it into the registry index yet from
                                        [default: "https://registry.js.ipfs.io"]
  --registry-upload-size-limit  How large a file upload to allow when proxying
                                for the registry             [default: "1024MB"]
  --registry-update-interval    Only request the manifest for a given module
                                every so many ms                [default: 60000]
  --registry-connect-timeout    How long to wait while dialling the mirror
                                before timing out                [default: 5000]
  --registry-read-timeout       How long to wait for individual packages before
                                timing out                       [default: 5000]
  --ipfs-mfs-prefix             Which mfs prefix to use
                                                      [default: "/npm-registry"]
  --ipfs-node                   "proc" to start an in-process IPFS node,
                                "disposable" to start an in-process disposable
                                node, "go" or "js" to spawn an IPFS node as a
                                separate process or a multiaddr that resolves to
                                a running node                 [default: "proc"]
  --ipfs-repo                   If --ipfs-node is set to "proc", this is the
                                path that contains the IPFS repo to use
                                                [default: "/Users/alex/.jsipfs"]
  --ipfs-flush                  Whether to flush the MFS cache   [default: true]
  --clone-pin                   Whether to pin cloned modules   [default: false]
  --request-max-sockets         How many concurrent http requests to make while
                                cloning the repo                   [default: 10]
  --request-retries             How many times to retry when downloading
                                manifests and tarballs from the registry
                                                                    [default: 5]
  --request-retry-delay         How long in ms to wait between retries
                                                                 [default: 1000]
  --request-timeout             How long in ms we should wait when requesting
                                files                           [default: 30000]
  --npm-registry                A fallback to use if the IPFS npm registry is
                                unavailable
                                         [default: "https://registry.npmjs.com"]
```

## Update your registry index

By default we keep a local copy of the npm registry index in your [`mfs`](https://github.com/ipfs/js-ipfs-mfs) at `/npm-registry` and update it when you install new packages. This means for the first request for a given module it will be fetched from npm over http.  There is a continously updated copy of the npm registry index with CIDs for all modules being generated by the [`ipfs-npm-registry-mirror`](https://github.com/ipfs-shipyard/ipfs-npm-registry-mirror) - if you'd like to clone this registry index, use the `update-registry-index` subcommand:

```console
$ ipfs-npm update-registry-index
```
