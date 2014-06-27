hubot-hall
==========

# A [Hubot](https://github.com/github/hubot) adapter for [Hall](https://hall.com)

Please view the quick start instructions below, or the subsequent detailed instructions.

### Compatibility with Hubot

 * Hubot >= 2.4.2

## Quick start for installing hubot-hall on Heroku

1. Complete the [instructions in the Hubot README for your particular platform](https://github.com/github/hubot/blob/master/docs/deploying) and return to these steps to configure your app for Hall.

1. Create a new Hall account for your bot to use.
 * You can set the first name and last name on the account to whatever you wish.
 * Once setup is complete, you can invoke your bot with either the full name of the user account or with the name you give the bot when you start it up.
 * Record the email address and password so you can configure your Hubot-Hall adapter later.


1. The `hubot/` directory that you created in the Hubot on Heroku instructions above is all that is relevant to us now. Let's switch to it:

        % cd hubot/

1. Edit `package.json` and add `hubot-hall` to the `dependencies` section. It should look something like this:

        "dependencies": {
          "hubot-hall": "latest",
          ...
        }

1. Edit `package.json` and add a `node` limitation to the `engines` section. It should look something like this (the Hall adapter only works with a limited range of node versions):

        "engines": {
          "node": ">= 0.8.x <= 0.9.0",
          ...
        }

1. If you won't be using the `redis-brain.coffee` script, you need to remove it from the array in `hubot-scripts.json` file.

1. Edit `Procfile` and change it to use the `hall` adapter and give it a name (optional) where `bot_name` is the name you'll use to invoke the bot (it will default to hubot):

        web: bin/hubot -a hall -n bot_name

1. Configure it:

      You will need to set a configuration variable if you are hosting on the free Heroku plan (if you haven't already done so).

        % heroku config:add HEROKU_URL=http://soothing-mists-4567.herokuapp.com

      Where the URL is your Heroku app's URL (shown after running `heroku create`, or `heroku rename`).

      Set the email to the email you used to register the bot with Hall:

        % heroku config:add HUBOT_HALL_EMAIL="..."

      Set the password to the password chosen when you created the bot's account.

        % heroku config:add HUBOT_HALL_PASSWORD="..."

1. Add and commit your package.json changes:

        % git add .
		% git commit -m "added the hubot-hall dependency"

1. Deploy and start the bot:

        % git push heroku master
        % heroku ps:scale web=1

      This will tell Heroku to run 1 of the `web` process type which is described in the `Procfile`.

1. You should see the bot join all rooms it has been added to. If not, check the output of `heroku logs`. You can also use `heroku config` to check the config vars and `heroku restart` to restart the bot. `heroku ps` will show you its current process state.

1. Assuming your bot's name is "Hubot", the bot will respond to commands like "@hubot help".  The '@' symbol is optional.

1. To configure the commands the bot responds to, you'll need to edit the `hubot-scripts.json` file ([valid script names here](https://github.com/github/hubot-scripts/tree/master/src/scripts)) or add scripts to the `scripts/` directory.

1. To deploy an updated version of the bot, simply commit your changes and run `git push heroku master` again.

## Running locally on Mac OS X or Linux

1. Complete the [instructions in the Hubot wiki](https://github.com/github/hubot/wiki/Deploying-Hubot-onto-Unix) and return to these steps to configure your app for Hall.

1. Create a new Hall account for your bot to use.
 * You can set the first name and last name on the account to whatever you wish.
 * Once setup is complete, you can invoke your bot with either the full name of the user account or with the name you give the bot when you start it up.
 * Record the email address and password so you can configure your Hubot-Hall adapter later.

1. The `hubot/` directory that you created in the Hubot on Unix instructions above is all that is relevant to us now. Let's switch to it:

        % cd hubot/

1. Edit `package.json` and add `hubot-hall` to the `dependencies` section. It should look something like this:

        "dependencies": {
          "hubot-hall": "latest",
          ...
        }

1. Edit `package.json` and add a `node` limitation to the `engines` section. It should look something like this (the Hall adapter only works with a limited range of node versions):

        "engines": {
          "node": ">= 0.8.x <= 0.9.0",
          ...
        }

1. Install the dependencies

        % npm install

1. Configure it:

      Set the email to the email you used to register the bot with Hall:

        % export HUBOT_HALL_EMAIL="..."

      Set the password to the password chosen when you created the bot's account.

        % export HUBOT_HALL_PASSWORD="..."

1. Run the hubot with the Hall adapter

        % bin/hubot -a hall

1. Or run hubot from a script like so:

    #!/bin/bash

    export HUBOT_HALL_EMAIL="..."
    export HUBOT_HALL_PASSWORD="..."

    bin/hubot --a hall

## Detailed setup instructions

Follow these instructions if you would like to setup a Hubot on Hall, but you don't necessarily have developer tools, etc. installed!

### Setting up Heroku

Heroku is a place for you to serve web applications from, and for small apps, it is free! We will serve our bot from Heroku. We'll need to make an account and then install the "Heroku toolbelt", which allows you to manage your Heroku account.

* Visit <a href="http://heroku.com" target="_blank">http://heroku.com</a> and sign up for an account.
* Visit <a href="https://toolbelt.heroku.com/" target="_blank">https://toolbelt.heroku.com/</a> and install the Heroku toolbelt.
* Click on the "Spotlight" icon in your system's menu bar and search for "Terminal". Open it.
* Type in `heroku login` then hit enter. Follow the instructions.

### Installing Apple Developer Tools

You will need to setup the Apple Developer tools, which will be used to build
the tools you need for your bot. Don't worry, it's easy!

* From the Terminal, type in `xcode-select --install` and follow the prompt.

### Setting up Homebrew

Homebrew is the simplest way to install any developer tools you might need. We
will install it to set up the pre-requisites we need for our bot.

* Visit <a href="http://brew.sh/" target="_blank">http://brew.sh</a> to install Homebrew. There is a section on the homepage with the heading "Install Homebrew" at the bottom of the page. Underneath the heading is a command. Copy and paste that into your Terminal and hit enter. Follow the instructions.
* Type in `brew update` and hit enter.
* Check to make sure Homebrew is installed correctly. Type in `brew doctor` and hit enter to verify that Homebrew is installed correctly.
* Install Node by typing in `brew install node npm` and hitting enter.

### Installing Hubot

* First, install the needed "hubot" library we will use to create our bot. Type in `npm install -g hubot coffee-script` and hit enter.
* Create a new directory called "Projects". You can do
this by typing in `mkdir Projects` and hitting enter. This will create a "Projects" directory on your hard drive at `/Users/<your user name>/Projects`.
* Switch into this directory by typing `cd Projects` and then hitting enter.
* Create a new bot by typing in `hubot --create wilma` where "wilma" is what you want your bot to be named.
* Change into your bot's directory. Type in `cd wilma` and hit enter.
* Test out your bot by typing in `bin/hubot` and hitting enter. Some warnings may appear but they should not affect the bot.
* Try typing in `hubot help` and hitting enter to see if the bot is working. Try typing in other commands as well. This is useful to test your bot.
* Exit by hitting `Ctrl-C`.

### Installing Sublime Text

* Now you need a text editor. Visit <a href="http://www.sublimetext.com/">http://www.sublimetext.com/</a> and download Sublime Text. Open up the disk image you downloaded, and copy Sublime Text to your Applications folder.
* Open Sublime Text from your Applications folder to make sure it works.
* In the Terminal, type in `ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl /usr/local/bin/sublime` and hit enter. This will allow you to open Sublime Text from the Terminal.

### Setting up your bot

* First, we need to keep track of our changes. We will use a "version tracker"
called git. We will create a new "repository". Type in `git init` and hit enter.
* Add all the files into the repo. Type in `git add .` and hit enter.
* Commit all the files you just added. Type in `git commit -m 'Initial commit'` and hit enter.
* Next, we will set aside some resources on Heroku for hosting our bot. Type in `heroku create` and hit enter. It will give you a URL starting with `http://`. Make note of it. For later.
* Next, we will add the "hubot-hall" adapter to your bot for use with Hall. Edit the "package.json" file by typing in `sublime package.json` and hitting enter. Under the "dependencies" section, add "hubot-hall", like so:

<pre>
  "dependencies": {
    "hubot": ">= 2.6.0 < 3.0.0",
    "hubot-scripts": ">= 2.5.0 < 3.0.0",
    "hubot-hall": "latest"
  }
</pre>

* Under "engines", make sure we use a version of Node that works with
"hubot-hall".

<pre>
  "engines": {
    "node": ">= 0.8.x <= 0.9.0",
    "npm": ">= 1.1.x"
  }
</pre>

* After you edit "package.json", make sure you save it by going to the "File" menu and selecting "Save", and then close it by clicking the red "close" button.

* Edit "hubot-scripts.json" file by typing `sublime hubot-scripts.json` and remove "redis-brain.coffee" for the moment. The contents of the file should look like:

<pre>
  ["shipit.cofee"]
</pre>

It allows your bot to have memories, but we will wait to explain how to set it up in a later tutorial.

* Make sure to save and close "hubot-scripts.json" like you did with "package.json".
* Edit "Procfile" by typing `sublime Procfile` and edit it to look like this:

<pre>
  web: bin/hubot -a hall -n wilma
</pre>

Where "wilma" is the name you want your bot to respond to.

* Make sure to save and close "Procfile" like you did with the previous files.

### Creating a Hall account for your bot

* Visit <a href="http://hall.com" target="_blank">http://hall.com</a> and set up an account. I like to give my bot my email but with a suffix so its email goes to my account. If my email account is "bieber@hall-inc.com", then my bot's email address would be "bieber+wilma@hall-inc.com".
* Next, we will need to set some settings on the bot. Remember the link I told you to remember from the previous section? In the Terminal, type in `heroku config:add HEROKU_URL='...'` where `...` is that link. Then hit enter.
* Next, type in `heroku config:add HUBOT_HALL_EMAIL='...'` where `...` is the email you used for your bot. Then hit enter.
* Finally, type in `heroku config:add HUBOT_HALL_PASSWORD='...'` where `...` is your password. Then hit enter. You can clear your Terminal so prying eyes don't see your password by hitting Command-K.

### Deploying your bot

* Add the files you changed by typing in `git add .` and hitting enter.
* Commit the files by typing in `git commit -m "added the hubot-hall dependency"` and hitting enter.
* Push your code to Heroku by typing in `git push heroku master` and hitting enter.
* Provision resources to be used by your bot by typing in `heroku ps:scale web=1` and hitting enter.
* You're done! Visit Hall and invite your bot to a group!

### Extra credit

* In the `scripts/` directory is some scripts. Try modifying one, then adding and committing your code, then running `git push heroku master` to deploy it. You should see your changes almost immediately!
* Try adding an existing script from one of the thousands of pre-made scripts at <a href="https://github.com/github/hubot-scripts" target="_blank">https://github.com/github/hubot-scripts</a> to your `scripts/` directory, adding the file, commiting, and deploying it.
* Try adding the `redis-brain.coffee` back. You will need to provision "RedisToGo" for your Heroku instance and you will need to `brew install redis-server` and follow the instructions locally.

### More Links

* Hubot Hall library—<a href="https://github.com/Hall/hubot-hall" target="_blank">https://github.com/Hall/hubot-hall</a>
* Hubot Readme—<a href="https://github.com/github/hubot/blob/master/docs/README.md" target="_blank">https://github.com/github/hubot/blob/master/docs/README.md</a>
* Guide to deploying Hubot to Heroku—<a href="https://github.com/github/hubot/blob/master/docs/deploying/heroku.md" target="_blank">https://github.com/github/hubot/blob/master/docs/deploying/heroku.md</a>
* Scripting Hubot—<a href="https://github.com/github/hubot/blob/master/docs/scripting.md">https://github.com/github/hubot/blob/master/docs/scripting.md</a>
* Hubot Scripts Repository—<a href="https://github.com/github/hubot-scripts" target="_blank">https://github.com/github/hubot-scripts</a>

