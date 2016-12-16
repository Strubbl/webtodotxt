# Web Todo.txt

A web-based GUI to manage a [Todo.txt](http://todotxt.com/) file.

<p align="center">
  <img src="https://github.com/EpocDotFr/webtodotxt/raw/master/screenshot.png">
</p>

## Features

  - Add / edit / remove tasks
  - Tasks due date (WIP)
  - Filters on all possible task data
  - Projects and contexts are cached locally for future use (WIP)
  - Automatic sorting
  - Save and reload the task list
  - Clear displaying of the task priority and completion
  - Automatic task creation date and completion date setting
  - Basic Markdown support for inline formatting (strong, emphasis, code, deleted, link) (WIP)
  - Automatic saving (WIP)
  - Internationalized & localized in 3 languages:
    - English (`en`)
    - French (`fr`)
    - Portuguese (WIP) (`pt`)

## Prerequisites

  - Should work on any Python 3.x version. Feel free to test with another Python version and give me feedback
  - A [uWSGI](https://uwsgi-docs.readthedocs.io/en/latest/)-capable web server (optional, but recommended)

## Installation

Clone this repo, and then the usual `pip install -r requirements.txt`.

## Configuration

Copy the `config.example.py` file to `config.py` and fill in the configuration parameters.

Available configuration parameters are:

  - `SECRET_KEY` Set this to a complex random value
  - `DEBUG` Enable/disable debug mode
  - `LOGGER_HANDLER_POLICY` Policy of the default logging handler

More informations on the three above can be found [here](http://flask.pocoo.org/docs/0.11/config/#builtin-configuration-values).

  - `USER` The credentials required to access the app. **It is highly recommended to serve this web app through HTTPS** because it uses [HTTP basic auth](https://en.wikipedia.org/wiki/Basic_access_authentication)
  - `TODOTXT_LOCATION` Path to a Todo.txt file (may be relative or absolute)
  - `FORCE_LANGUAGE` Force the lang of the web app to be one of the supported ones (defaults to `None`: auto-detection from the `Accept-Language` HTTP header). See in the features section above for a list of available lang keys

I'll let you search yourself about how to configure a web server along uWSGI.

## Usage

  - Standalone

Run the internal web server, which will be accessible at `http://localhost:8080`:

```
python local.py
```

Edit this file and change the interface/port as needed.

  - uWSGI

The uWSGI file you'll have to set in your uWSGI configuration is `uwsgi.py`. The callable is `app`.

  - Others

You'll probably have to hack with this application to make it work with one of the solutions described [here](http://flask.pocoo.org/docs/0.11/deploying/). Send me a pull request if you make it work.

## How it works

This project is built on [Vue.js](http://vuejs.org/) 2 for the frontend and [Flask](http://flask.pocoo.org/) (Python) for
the backend. The [todotxtio](https://github.com/EpocDotFr/todotxtio) PyPI package is used to parse/write the Todo.txt file,
giving/receiving data through [Ajax](https://en.wikipedia.org/wiki/Ajax_(programming)).

## Gotchas

  - Be aware that this web application isn't intended to be used on mobile devices

Instead, use native mobile apps to edit and sync the Todo.txt file:

**On Android**, [Simpletask Cloudless](https://play.google.com/store/apps/details?id=nl.mpcjanssen.simpletask) along [FolderSync Lite](https://play.google.com/store/apps/details?id=dk.tacit.android.foldersync.lite)

**On iOS**, I don't know. Feel free to share your finds.

  - This web application wasn't designed to be multi-process compliant

If you sync your Todo.txt file via SFTP or something from the mobile apps and at the same time you're modifiying it via
this web app, you'll probably end with a loss of data because both sides can't be aware of the latest version of the file
in realtime: they both erase the file with their data.

So make sure you're modifying it from one location at a time with the latest up-to-date Todo.txt file.

## Contributors

Thanks to:

  - [@Pepsit36](https://github.com/Pepsit36) (Portuguese translations)

## End words

If you have questions or problems, you can [submit an issue](https://github.com/EpocDotFr/webtodotxt/issues).

You can also submit pull requests. It's open-source man!