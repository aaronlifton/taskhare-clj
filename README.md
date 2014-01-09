# TaskHare

![TaskHare](http://i.imgur.com/IKexLmb.jpg)

###### History

* Development began on 9 January 2014.
* Minimum viable product will be released on 1 February 2014.

## GET /api/1/task/list

    {
        limit: optional(integer)
        start: optional(integer)
    }

###### What the result looks like:

    { 
        title: string
        description: string
        author: uniqid
        creation: integer // UNIX Timestamp
        reward: integer // USD 1/100
    }

## POST /api/1/task/create

    {
        title: string
        description: string
    }
    
*Requires authentication.*

## GET /api/1/task/read

    $task: uniqid

## PUT /api/1/task/update/title

    $task: uniqid
    $title: string

*Requires authentication. You must be the author of that task.*

## PUT /api/1/task/update/description

    $task: uniqid
    $title: string

*Requires authentication. You must be the author of that task.*

## DELETE /api/1/task/delete

    $task: uniqid

*****

This generated project has a few basics set up beyond the bare Compojure defaults:

* Cookie-backed session store
* Stack traces when in development
* Environment-based config via [enviorn](https://github.com/weavejester/environ)
* [HTTP-based REPL debugging](https://devcenter.heroku.com/articles/debugging-clojure) via [drawbridge](https://github.com/cemerick/drawbridge)

## Usage

To start a local web server for development you can either eval the
commented out forms at the bottom of `web.clj` from your editor or
launch from the command line:

    $ lein run -m taskhare.web

Initialize a git repository for your project.

    $ git init
    $ git add .
    $ git commit -m "Initial commit."

You'll need the [heroku toolbelt](https://toolbelt.herokuapp.com)
installed to manage the heroku side of your app. Once it's installed,
get the app created:

    $ heroku apps:create taskhare
    Creating taskhare... done, stack is cedar
    http://taskhare.herokuapp.com/ | git@heroku.com:taskhare.git
    Git remote heroku added

You can deploy the skeleton project immediately:

    $ git push heroku master
    Writing objects: 100% (13/13), 2.87 KiB, done.
    Total 13 (delta 0), reused 0 (delta 0)

    -----> Heroku receiving push
    -----> Clojure app detected
    -----> Installing Leiningen
           Downloading: leiningen-2.0.0-preview7-standalone.jar
    [...]
    -----> Launching... done, v3
           http://taskhare.herokuapp.com deployed to Heroku

    To git@heroku.com:taskhare.git
     * [new branch]      master -> master

It's live! Hit it with `curl`:

    $ curl http://taskhare.herokuap.com
    ["Hello" :from Heroku]

The cookie-backed session store needs a session secret configured for encryption:

    $ heroku config:add SESSION_SECRET=$RANDOM_16_CHARS

## Remote REPL

The [devcenter article](https://devcenter.heroku.com/articles/debugging-clojure)
has a detailed explanation, but using the `repl` task from Leiningen
2.x lets you connect a REPL to a remote process over HTTP. The first
step is setting up credentials:

    $ heroku config:add REPL_USER=[...] REPL_PASSWORD=[...]

Then you can launch the REPL:

    $ lein repl :connect http://$REPL_USER:$REPL_PASSWORD@myapp.herokuapp.com/repl

Everything you enter will be evaluated remotely in the running dyno,
which can be very useful for debugging or inspecting live data.

## License

Copyright © 2014 FIXME

Distributed under the Eclipse Public License, the same as Clojure.
