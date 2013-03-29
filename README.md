hubot-hall
==========

# A [Hubot](https://github.com/github/hubot) adapter for [Hall](https://hall.com)

### Compatibility with Hubot

 * Hubot >= 2.4.2

### Compatibility with NodeJS

 * Preferably use NodeJS 0.8.x or later

## Installing Hubot-Hall on Heroku

1. Follow the [instructions in the Hubot wiki](https://github.com/github/hubot/wiki/Deploying-Hubot-onto-Heroku).

1. Create a new Hall account for your bot to use.
 * Make sure the first name of the account is the name of your hubot
 * You can leave the last name blank
 * Record the email address and password so you can configure your Hubot-Hall adapter later


1. The `hubot/` directory that you created in the Hubot on Heroku instructions above is all that is relevant to us now. Let's switch to it:

        % cd hubot/

1. Edit `package.json` and add `hubot-hall` to the `dependencies` section. It should look something like this:

        "dependencies": {
          "hubot-hall": "latest",
          ...
        }

1. Edit `Procfile` and change it to use the `hall` adapter:

        web: bin/hubot --adapter hall

1. Configure it:

      You will need to set a configuration variable if you are hosting on the free Heroku plan.

        % heroku config:add HEROKU_URL=http://soothing-mists-4567.herokuapp.com

      Where the URL is your Heroku app's URL (shown after running `heroku create`, or `heroku rename`).

      Set the email to the email you used to register the bot with Hall:

        % heroku config:add HUBOT_HALL_EMAIL="..."

      Set the password to the password chosen when you created the bot's account.

        % heroku config:add HUBOT_HALL_PASSWORD="..."

1. Deploy and start the bot:

        % git push heroku master
        % heroku ps:scale web=1

      This will tell Heroku to run 1 of the `web` process type which is described in the `Procfile`.

1. You should see the bot join all rooms it has been added to. If not, check the output of `heroku logs`. You can also use `heroku config` to check the config vars and `heroku restart` to restart the bot. `heroku ps` will show you its current process state.

1. Assuming your bot's name is "Hubot", the bot will respond to commands like "@hubot help".  The '@' symbol is optional.

1. To configure the commands the bot responds to, you'll need to edit the `hubot-scripts.json` file ([valid script names here](https://github.com/github/hubot-scripts/tree/master/src/scripts)) or add scripts to the `scripts/` directory.

1. To deploy an updated version of the bot, simply commit your changes and run `git push heroku master` again.

## Running on Unix

1. Follow the [instructions in the Hubot wiki](https://github.com/github/hubot/wiki/Deploying-Hubot-onto-Unix).

1. Create a new Hall account for your bot to use.
 * Make sure the first name of the account is the name of your hubot
 * You can leave the last name blank
 * Record the email address and password so you can configure your Hubot-Hall adapter later

1. The `hubot/` directory that you created in the Hubot on Unix instructions above is all that is relevant to us now. Let's switch to it:

        % cd hubot/

1. Edit `package.json` and add `hubot-hall` to the `dependencies` section. It should look something like this:

        "dependencies": {
          "hubot-hall": "latest",
          ...
        }

1. Install the dependencies

        % npm install

1. Configure it:

      Set the email to the email you used to register the bot with Hall:

        % heroku config:add HUBOT_HALL_EMAIL="..."

      Set the password to the password chosen when you created the bot's account.

        % heroku config:add HUBOT_HALL_PASSWORD="..."

1. Run the hubot with the Hall adapter

        % bin/hubot -a hall

1. Or run hubot from a script like so:

    #!/bin/bash

    export HUBOT_HALL_EMAIL="..."
    export HUBOT_HALL_PASSWORD="..."

    bin/hubot --a hall