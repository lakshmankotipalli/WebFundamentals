project_path: /web/tools/workbox/_project.yaml
book_path: /web/tools/workbox/_book.yaml
description: A guide on how to precache files with Workbox CLI.

{# wf_blink_components: N/A #}
{# wf_updated_on: 2018-01-19 #}
{# wf_published_on: 2017-11-15 #}

# Precache Files with Workbox CLI {: .page-title }

This page explains how to use the Workbox Command Line Interface (a.k.a the
Workbox CLI) to generate the list of files to precache and add it to your
service worker.

<aside class="note"><b>Note:</b> You'll need to have
<a href="https://nodejs.org/en/download/">Node installed</a> to use the
Workbox CLI.</aside>

## Install the CLI

To start, install the CLI from NPM.

<pre class="devsite-terminal devsite-click-to-copy">
npm install workbox-cli --global
</pre>

You should be able to run the command `workbox --help` after it's installed.

<pre class="devsite-terminal">
workbox --help

    workbox-cli is the command line interface for Workbox.

    Usage:
    $ workbox <command> [options]

    ...
</pre>

## Run the Wizard

The next step is to run the wizard. This will setup the CLi to work for your
project. The wizard will ask a set of questions about your projects file
structure which'll be used to determine the files that should be precached.

Start the wizard like so:

<pre class="devsite-terminal">
workbox wizard --injectManifest
</pre>

## Add an Injection Point

Before the files can be "injected" into your service worker, you need to add
this line of code to your service worker file:

```javascript
workbox.precaching.precacheAndRoute([]);
```

This piece of code will be replaced by the CLI with the list of files (See
the next section).

## Inject a Manifest with the CLI

The final step is to run the inject manifest command:

<pre class="devsite-terminal">
workbox injectManifest
</pre>

This command will create the list of files to precache, read your service
worker file, inject the manifest and output a new service worker file
with the manifest. The end result with look like this:

<pre class="prettyprint lang-javascript"><code>workbox.precaching.precacheAndRoute([
  {
    "url": "basic.html",
    "revision": "7ca37fd5b27f91cd07a2fc68f20787c3"
  },
  {
    "url": "favicon.ico",
    "revision": "1378625ad714e74eebcfa67bb2f61d81"
  },
  {
    "url": "images/hamburger.svg",
    "revision": "d2cb0dda3e8313b990e8dcf5e25d2d0f"
  },

  ...

]);</code></pre>

When you make a change to your project, run the inject manifest command
and you'll have an up to date service worker with precache support.

{% include "web/tools/workbox/guides/_shared/precache-config.md" %}
