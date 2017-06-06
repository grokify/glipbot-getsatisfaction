# GetSat Glipbot

GetSat Glipbot is a chatbot built on the [Hubot][hubot] framework. It was
initially generated by [generator-hubot][generator-hubot], and configured to be
deployed on [Heroku][heroku] to get you up and running as quick as possible.

It uses the following:

* [hubot-glip](https://github.com/tylerlong/hubot-glip) adatper - [NPM](https://www.npmjs.com/package/hubot-glip)
* [hubot-getsatisfaction](https://github.com/grokify/hubot-getsatisfaction) handler - [NPM](https://www.npmjs.com/package/hubot-getsatisfaction)

### Running GetSat Glipbot on Heroku

If you already have your Glip email address and password, you can use [Heroku One-Button Deployment](https://devcenter.heroku.com/articles/heroku-button).

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

### Running GetSat Glipbot Locally

You can test your hubot by running the following, however some plugins will not
behave as expected unless the [environment variables](#configuration) they rely
upon have been set.

You can start GetSat Glipbot locally by running `bin/hubot` with the `--name` parameter. The Glip and GetSat environment variables should be set.

    $ HUBOT_GLIP_SERVER=https://platform.ringcentral.com \
      HUBOT_GLIP_APP_KEY=MyGlipAppKey \
      HUBOT_GLIP_APP_SECRET=MyGlipAppSecret \
      HUBOT_GLIP_USERNAME=16505550123
      HUBOT_GLIP_EXTENSION=102
      HUBOT_GLIP_PASSWORD=MyUserPassword
      HUBOT_GETSATISFACTION_COMPANY=ringcentral \
      HUBOT_GETSATISFACTION_VIEW=markdown \
      ./bin/hubot -n hubot -a glip

You'll see some start up output and a prompt:

    [Sat Feb 28 2015 12:38:27 GMT+0000 (GMT)] INFO Using default redis on localhost:6379
    gsbot>

Then you can interact with GetSatGlipbot by typing `GetSatGlipbot help`.

    gsbot gs help
    gsbot gs search topics sort:votes glip
    ...

### Configuration

### external-scripts

There will inevitably be functionality that everyone will want. Instead of
writing it yourself, you can use existing plugins.

Hubot is able to load plugins from third-party `npm` packages. This is the
recommended way to add functionality to your hubot. You can get a list of
available hubot plugins on [npmjs.com][npmjs] or by using `npm search`:

    % npm search hubot-scripts panda
    NAME             DESCRIPTION                        AUTHOR DATE       VERSION KEYWORDS
    hubot-pandapanda a hubot script for panda responses =missu 2014-11-30 0.9.2   hubot hubot-scripts panda
    ...

To use a package, check the package's documentation, but in general it is:

1. Use `npm install --save` to add the package to `package.json` and install it
2. Add the package name to `external-scripts.json` as a double quoted string

You can review `external-scripts.json` to see what is included by default.

##  Persistence

If you are going to use the `hubot-redis-brain` package (strongly suggested),
you will need to add the Redis to Go addon on Heroku which requires a verified
account or you can create an account at [Redis to Go][redistogo] and manually
set the `REDISTOGO_URL` variable.

    % heroku config:add REDISTOGO_URL="..."

If you don't need any persistence feel free to remove the `hubot-redis-brain`
from `external-scripts.json` and you don't need to worry about redis at all.

[redistogo]: https://redistogo.com/

## Adapters

## Deployment

    % heroku create --stack cedar
    % git push heroku master

If your Heroku account has been verified you can run the following to enable
and add the Redis to Go addon to your app.

    % heroku addons:add redistogo:nano

If you run into any problems, checkout Heroku's [docs][heroku-node-docs].

You'll need to edit the `Procfile` to set the name of your hubot.

More detailed documentation can be found on the [deploying hubot onto
Heroku][deploy-heroku] wiki page.

### Deploying to UNIX or Windows

If you would like to deploy to either a UNIX operating system or Windows.
Please check out the [deploying hubot onto UNIX][deploy-unix] and [deploying
hubot onto Windows][deploy-windows] wiki pages.

[heroku-node-docs]: http://devcenter.heroku.com/articles/node-js
[deploy-heroku]: https://github.com/github/hubot/blob/master/docs/deploying/heroku.md
[deploy-unix]: https://github.com/github/hubot/blob/master/docs/deploying/unix.md
[deploy-windows]: https://github.com/github/hubot/blob/master/docs/deploying/windows.md

## Restart the bot

You may want to get comfortable with `heroku logs` and `heroku restart` if
you're having issues.
