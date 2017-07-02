#Nexus TipBot For Slack
Easily transfer money between team members on your Slack channel.

## Basic features
 - With a single message, send and receive Nexus
 - A tip has no transaction fee. There are no extra cost added to your tip.
 - Get the fiat prices.

## How to Run a TipBot
### Setup Slack Bot
 - Add a bot integration to Slack [here](https://my.slack.com/services/new/bot)
    - Make sure you copy the Slack API token


### Install TipBot
 - `git clone https://github.com/narubyriverlione/slack-tipbot`
 - `cd slack-tipbot`
 - `npm install`


### Optional depending on enabled advanced features
- Install MongoDB (depending on your OS follow: https://docs.mongodb.com/manual/administration/install-community/ )


### Run
Change the `YOUR_SLACK_TOKEN`, `YOUR_RPC_USER` and `YOUR_RPC_PASSWORD` in the below snippet to the API key.
```sh
 node bot.js --slack-token="YOUR_SLACK_TOKEN" --rpc-user="YOUR_RPC_USER" --rpc-password="YOUR_RPC_PASSWORD" 
```

You can also use ENV variable instead of argument:
 - `TIPBOT_SLACK_TOKEN`
 - `TIPBOT_RPC_USER`
 - `TIPBOT_RPC_PASSWORD`
 
You can also set the *RPC port* if you need to, it defaults to 9336

If your wallet is locked (and it should !) provided the *passphrase* via the `--wallet-password`argument or the `TIPBOT_WALLET_PASSWORD` enviroment variable.

Optional you can set `DEBUG = "tipbot:*"` to see debug messages.


You should use [forever](https://www.npmjs.com/package/forever) to run the bot persistend.
Create a json file with all the needed arguments.


## Usage
You can control / communicate with the tipbot by sending the bot a **direct message** or **mentioning** its name in a channel.
The tipbot responds to certain 'trigger words' in a sentence, so you can wrap the trigger word in a nice looking sentence and it will work.

For example, to trigger the `help` command you can could say `hey @tipbot can you help me figure out how tipping works`
and the `help` in that sentence will trigger displaying the help information.

## Commands / Trigger words
##### `help`        - *ask the bot for help*
eg; `hey @mr.robot can you show me the help info!`

##### `balance`     - *ask the bot for your current balance*
eg; `hey @mr.robot can you please tell me my balance`

##### `send <value + unit> @someone` - *tell the bot to send coins to someone*
eg; `@mr.robot please send .001 NXS to @bob` will send 0.001 NXS to @bob.

This command has a few aliases which you can use; `give` and `sent`. 
You can also use fiat currencies, they will be converted to the Dash value.
eg; `@tipbot can you give @bob 1 euro` or `@tipbot I'd like you to send @bob 0.5 usd`

##### `deposit`     - *ask the bot for a deposit address*
eg; `@tipbot I'd like to deposit to my tip jar`

##### `withdraw`    -  *tell the bot you want to withdraw to an address*
after you've requested the withdraw the bot will confirm with you if it's OK, replying with `yes`, `ok` or `sure` will make the transaction happen.
eg; `@mr.robot I want to withdraw 0.5 NXS to 2XXxxXXxxXXxxXXxxXXxxXXxxXXxxXXxxXXxxXXxxXXxxXX`

##### `currencies` - ask the bot for a list of supported currencies. 
eg; `_@mr.robot what currencies do you know?`

##### `price`      - ask the bot for the Dash price in a particular currency. 
eg; `_@mr.robot price in USD!` 

##### `convert`    - ask the bot to convert between a particular currency and Dash (or visa versa)
eg; `@mr.robot 1 USD to EUR!_​  or; ​_@mr.robot 0.03 Nexus to GBP`

### ADMIN ONLY COMMANDS
##### `emergency restart` Restart the Slack connection of tipbot. 

##### `balance all`      show all the tip jars (must be enabled in code)

##### `balance check`    show the balance of a specific user (must be enabled in code) 
eg;        `mr.robot balance check @user` 


##### `whisper`         Send a message in a private channel to a user as dashbot.
Use case :moderator warning.
