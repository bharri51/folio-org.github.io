---
layout: page
title: Using Nightmare for UI testing
permalink: /guides/using-nightmare/
menuInclude: no
menuTopTitle: Guides
---

Nightmare is a high-level browser automation library from Segment.

The goal is to expose a few simple methods that mimic user actions (like goto, type and click), with an API that feels synchronous for each block of scripting, rather than deeply nested callbacks. It was originally designed for automating tasks across sites that don't have APIs, but is most often used for UI testing and crawling.

Under the covers it uses Electron, which is similar to PhantomJS but roughly twice as fast and more modern.

## Run an existing scenario

Follow the [platform-core](https://github.com/folio-org/platform-core) README which explains how to run integration tests.
 
So clone that repository, install dependencies and run tests.

As explained there, this needs a running Okapi.
That can be achieved by downloading a [Prebuilt Vagrant box](https://github.com/folio-org/folio-ansible/blob/master/doc/index.md#prebuilt-vagrant-boxes).
Alternatively use the `--url` option.

```code
git clone https://github.com/folio-org/platform-core
cd platform-core
git checkout snapshot
yarn
yarn test-int --run WD:loan_renewal
```

## Test local changes

I want to demonstrate you flow of running test for new branch:

1. Let's create a new directory and go there.

1. create a **package.json** file with such content:
```code
{
   "private": true,
   "workspaces": [
     "*"
   ],
   "devDependencies": {
     "@folio/stripes-cli": "^1.2.0"
   },
   "dependencies": {}
}
```

1. clone platform core (and checkout **snapshot** branch)

1. clone module (or modules) where we have added changes (and checkout branch with new feature)

1. After that, we should install dependencies for our modules. So we should run yarn in the folder where we have modules and **package.json** file.
So you should install dependencies in a folder similar to what we have in the screenshot (In this case I have made changes in the **ui-circulation** module, so I have cloned this module) :
![Image](/images/nightmare/nightmare-folder-example.png "folder-example")
1. After that we can go to the platform-core directory and run tests:
```code
yarn test-int
```

## Some hints

In tests, you should use **CSS** selectors instead of **[data-test...]** attributes, because these attributes will be stripped from the production build and therefore are unavailable when the integration tests run against folio-testing or folio-snapshot.

Always check the current state of the back-end, because some dependencies may cause unexpected behavior. (the possible way is to destroy and restart vagrant before running tests)

Follow the operation by:
* providing the **--show** option:
 ```code
yarn test-int --show
```
* adding **show: true** property in nightmare config or particular scenario (as shown in the screenshot):
![Image](/images/nightmare/nightmare-code-example.png "code-example")


## Useful links
* https://github.com/folio-org/platform-core
* https://github.com/segmentio/nightmare


