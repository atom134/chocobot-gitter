# chocobot

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/chocolatey/chocobot-gitter?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

chocobot is a chat bot built on the [Hubot][hubot] framework. It was initially generated by [generator-hubot][generator-hubot], and configured to be deployed on [Heroku][heroku] to get you up and running as quick as possible.

This README is intended to help get you started. Definitely update and improve to talk about your own instance, how to use and deploy, what functionality he has, etc!

[heroku]: http://www.heroku.com
[hubot]: http://hubot.github.com
[generator-hubot]: https://github.com/github/generator-hubot

### Gitter Setup

To get hubot, or in our case chocobot running, these are the steps that had to be followed.  I have captured them here so that we don't forget what was done :smile_cat:

**NOTE:** Although there are two hubot adapter's for Gitter, we found that only one of them works.  Namely, this [one](https://github.com/huafu/hubot-gitter2).  The other [one](https://github.com/kcjpop/hubot-gitter) seems older, and has been replaced by the one that we ended up using.

* Login into [Gitter](http://gitter.im) with the Github account that you want to run as your bot
* Join the room that you want the bot to be activated on (i.e. chocolatey/choco)
* Install node.js (which includes npm)
* Install Heroku Toolkit
* `mkdir C:\heroku\chocobot`
* `cd .\chocobot`
* `heroku login`
* `npm install --global coffee-script hubot`
* `npm install --global yo generator-hubot`
* `yo hubot` (when prompted, enter `gitter2` as adapter name, and `chocobot` as name
* `npm install --save hubot-gitter2`
* `git init`
* `git add .`
* `git commit -m "Initial commit"`
* `heroku create`
* `heroku config:set HUBOT_GITTER2_TOKEN=****` (here the token is the Personal Access Token for Github Account that will be running as the bot, in our case, the choco-bot user on Github.  The Personal Access Token can be retrieved from [here](https://developer.gitter.im/)
* `heroku config:set HEROKU_URL=https://whispering-peak-2284.herokuapp.com/` (this is to keep the heroku application alive.  The URL is generated from the `heroku create` command above
* `heroku config:set HUBOT_GITTER2_TESTING_ROOMS=chocolatey/choco` (this was used initially to verify that it was working on one room in particular, but it was later removed so that any room that choco-bot user is signed into will respond to commands)
* `heroku config:set HUBOT_ADAPTER="gitter2"` (this ensures we use the gitter2 adapter)
* `git push heroku master`
* `heroku logs` (if all goes well here, you should see something simalar to the following)

![image](https://cloud.githubusercontent.com/assets/1271146/5890975/1b0b13d4-a471-11e4-97db-9be2b5fbae77.png)

If all of the above has worked, go to your Gitter Chat Room, and try issuing a hubot command like `hubot ping` and hopefully you will see the following:

![image](https://cloud.githubusercontent.com/assets/1271146/5890979/96fa7066-a471-11e4-9042-b1db63b4e984.png)

### IRC Setup

Starting with the existing codebase set up with Gitter Setup instructions.

* `heroku create`
* `heroku config:set HEROKU_URL="https://dry-cliffs-7209.herokuapp.com"` - this is to keep the heroku application alive.  The URL is generated from the `heroku create` command above
* `heroku config:set HUBOT_ADAPTER="irc"` - this ensures we use the gitter2 adapter
* `heroku config:set HUBOT_IRC_DEBUG="true"`
* `heroku config:set HUBOT_IRC_NICK="choco-bot"`
* `heroku config:set HUBOT_IRC_NICKSERV_USERNAME="choco-bot"`
* `heroku config:set HUBOT_IRC_NICKSERV_PASSWORD="****"`
* `heroku config:set HUBOT_IRC_PORT=6697`
* `heroku config:set HUBOT_IRC_ROOMS="#chocolatey"`
* `heroku config:set HUBOT_IRC_SERVER="chat.freenode.net"`
* `heroku config:set HUBOT_IRC_SERVER_FAKE_SSL="true"`
* `heroku config:set HUBOT_IRC_UNFLOOD=800`
* `heroku config:set HUBOT_IRC_USESSL="true"`
* `heroku config:set FITBIT_CLIENT_ID="****"`
* `heroku config:set FITBIT_CLIENT_SECRET="****"`
* `heroku config:set FITBIT_OAUTH_TOKEN="****"`
* `heroku config:set FITBIT_OAUTH_TOKEN_SECRET="****"`
* `git push heroku master`
* `heroku logs` - this may show you issues but see if the bot joined the room.

**NOTE**: This heroku is in a different directory than the other adapter (with the same github code).

### Fitbit Configuration

In order to generate the `FITBIT_OAUTH_TOKEN` and `FITBIT_TOKEN_SECRET` you need to walk through the OAuth registration process.  In our case, we created a new Fitbit user specifically for chocobot.  Once this account was set up, we then created a new Fitbit application over at http://dev.fitbit.com/apps.  Once this app was created you are given the following:

* Client (Consumer) Key
* Client (Consumer) Secret
* Temporary Credentials (Request Token) URL
* Token Credentials (Acccess Token) URL
* Authorize URL
 
With these pieces of information, head over to https://www.runscope.com/oauth1_tool and paste all the values in.  From there, you will be given the permanent OAuth Token and OAuth Token Secret that the Fitbit script can then make use of.

*NOTE* You will need to create a runscope account in order to use the above tool

### Running chocobot Locally

You can test your hubot by running the following.

You can start chocobot locally by running:

    % bin/hubot

You'll see some start up output about where your scripts come from and a
prompt:

    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading adapter shell
    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading scripts from /home/tomb/Development/hubot/scripts
    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading scripts from /home/tomb/Development/hubot/src/scripts
    Hubot>

Then you can interact with chocobot by typing `chocobot help`.

    chocobot> chocobot help

    chocobot> animate me <query> - The same thing as `image me`, except adds a few
    convert me <expression> to <units> - Convert expression to given units.
    help - Displays all of the help commands that Hubot knows about.
    ...


### Scripting

An example script is included at `scripts/example.coffee`, so check it out to
get started, along with the [Scripting Guide](https://github.com/github/hubot/blob/master/docs/scripting.md).

For many common tasks, there's a good chance someone has already one to do just
the thing.

### hubot-scripts

There will inevitably be functionality that everyone will want. Instead
of writing it yourself, you can check
[hubot-scripts][hubot-scripts] for existing scripts.

To enable scripts from the hubot-scripts package, add the script name with
extension as a double quoted string to the `hubot-scripts.json` file in this
repo.

[hubot-scripts]: https://github.com/github/hubot-scripts

### external-scripts

Hubot is able to load scripts from third-party `npm` package. Check the package's documentation, but in general it is:

1. Add the packages as dependencies into your `package.json`
2. `npm install` to make sure those packages are installed
3. Add the package name to `external-scripts.json` as a double quoted string

You can review `external-scripts.json` to see what is included by default.

##  Persistence

If you are going to use the `hubot-redis-brain` package
(strongly suggested), you will need to add the Redis to Go addon on Heroku which requires a verified
account or you can create an account at [Redis to Go][redistogo] and manually
set the `REDISTOGO_URL` variable.

    % heroku config:add REDISTOGO_URL="..."

If you don't require any persistence feel free to remove the
`hubot-redis-brain` from `external-scripts.json` and you don't need to worry
about redis at all.

[redistogo]: https://redistogo.com/

## Adapters

Adapters are the interface to the service you want your hubot to run on. This
can be something like Campfire or IRC. There are a number of third party
adapters that the community have contributed. Check
[Hubot Adapters][hubot-adapters] for the available ones.

If you would like to run a non-Campfire or shell adapter you will need to add
the adapter package as a dependency to the `package.json` file in the
`dependencies` section.

Once you've added the dependency and run `npm install` to install it you can
then run hubot with the adapter.

    % bin/hubot -a <adapter>

Where `<adapter>` is the name of your adapter without the `hubot-` prefix.

[hubot-adapters]: https://github.com/github/hubot/blob/master/docs/adapters.md

## Deployment

    % heroku create --stack cedar
    % git push heroku master

If your Heroku account has been verified you can run the following to enable
and add the Redis to Go addon to your app.

    % heroku addons:add redistogo:nano

If you run into any problems, checkout Heroku's [docs][heroku-node-docs].

You'll need to edit the `Procfile` to set the name of your hubot.

More detailed documentation can be found on the
[deploying hubot onto Heroku][deploy-heroku] wiki page.

### Deploying to UNIX or Windows

If you would like to deploy to either a UNIX operating system or Windows.
Please check out the [deploying hubot onto UNIX][deploy-unix] and
[deploying hubot onto Windows][deploy-windows] wiki pages.

[heroku-node-docs]: http://devcenter.heroku.com/articles/node-js
[deploy-heroku]: https://github.com/github/hubot/blob/master/docs/deploying/heroku.md
[deploy-unix]: https://github.com/github/hubot/blob/master/docs/deploying/unix.md
[deploy-windows]: https://github.com/github/hubot/blob/master/docs/deploying/unix.md

## Campfire Variables

If you are using the Campfire adapter you will need to set some environment
variables. Refer to the documentation for other adapters and the configuraiton
of those, links to the adapters can be found on [Hubot Adapters][hubot-adapters].

Create a separate Campfire user for your bot and get their token from the web
UI.

    % heroku config:add HUBOT_CAMPFIRE_TOKEN="..."

Get the numeric IDs of the rooms you want the bot to join, comma delimited. If
you want the bot to connect to `https://mysubdomain.campfirenow.com/room/42`
and `https://mysubdomain.campfirenow.com/room/1024` then you'd add it like this:

    % heroku config:add HUBOT_CAMPFIRE_ROOMS="42,1024"

Add the subdomain hubot should connect to. If you web URL looks like
`http://mysubdomain.campfirenow.com` then you'd add it like this:

    % heroku config:add HUBOT_CAMPFIRE_ACCOUNT="mysubdomain"

[hubot-adapters]: https://github.com/github/hubot/blob/master/docs/adapters.md

## Restart the bot

You may want to get comfortable with `heroku logs` and `heroku restart`
if you're having issues.
