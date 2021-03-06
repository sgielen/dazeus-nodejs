# DaZeus Node.js Bindings
This package provides bindings for the DaZeus IRC Bot

## Getting started
Here's an example echobot, that just repeats every message back to the channel

    var dazeus = require("dazeus");
    var client = dazeus.connect({path: '/tmp/dazeus.sock'}, function () {
        client.on('PRIVMSG', function (network, user, channel, message) {
            client.message(network, channel, message);
        });
    });

## Quick Reference
We start by setting up a new instance of the client:

    var dazeus = require("dazeus");
    var client = dazeus.connect({path: '/tmp/dazeus.sock'}, function () {

    });

The connect function will return a client object that can be used to query the server
and which will respond to anything DaZeus throws at it. Instead of providing a `path`
variable you may also provide a `host` and `port` to connect using TCP.

The provided callback function will be executed as soon as a connection is established.
By creating your own listeners and triggering your own actions you can interact with DaZeus

### Events
Events may be captured by using the `on` method on a client object. Please take a look at
the DaZeus documentation to see what events are available. The event interface used is that from
Node.js's events.EventEmitter. Take a look at their documentation to see how listening to events
works in Node.js

Callback arguments depend on the parameters returned by DaZeus. Events you can listen for are:

- `CONNECT`
- `DISCONNECT`
- `JOIN`
- `PART`
- `QUIT`
- `NICK`
- `MODE`
- `TOPIC`
- `INVITE`
- `KICK`
- `PRIVMSG`
- `NOTICE`
- `CTCP`
- `CTCP_REP`
- `ACTION`
- `UNKNOWN`
- `WHOIS`
- `NAMES`
- `PRIVMSG_ME`
- `CTCP_ME`
- `ACTION_ME`

Some examples to get you going:

    client.on('PRIVMSG', function (network, user, channel, message) {
        // every event has a different set of parameters
    });

    client.on('WHOIS', function (network, server, user) {
        // you don't need to specify all parameters if you don't need them
    });

### Methods
All these methods provide callbacks that are executed when the information requested is provided
by the bot. Sometimes this information might be limited to a confirmation of the action performed.


    DaZeus.getProperty(property[, scope], callback)

Retrieve a property from the database DaZeus provides.


    DaZeus.setProperty(property, value[, scope][, callback])

Store a property in the DaZeus database.


    DaZeus.unsetProperty(property[, scope][, callback])

Remove a property from the DaZeus database.


    DaZeus.message(network, channel, message[, callback])

Send a message to a specific channel on a specific network.


    DaZeus.action(network, channel, message[, callback])

Send a '/me' message to a specific channel on a specific network.


    DaZeus.join(network, channel[, callback])

Join a channel.


    DaZeus.part(network, channel[, callback])

Leave a channel.


    DaZeus.networks(callback)

Retrieve the list of networks the bot is connected to.


    DaZeus.channels(network, callback)

Retrieve the list of channels the bot has joined for a network.


    DaZeus.nick(network, callback)

Retrieve the nickname of the bot.


    DaZeus.whois(network, nick, callback)

Send a '/whois' request for a specific nick on a network.

    DaZeus.onCommand(command[, network], callback)

Receive a notification when a command is executed, for example to catch `}help` you would write:
`DaZeus.onCommand('help', function () { /* ... */ });`

    DaZeus.reply(network, channel, user, message[, highlight][, callback])

Reply to a message sent by a user in a channel. By default the bot will also add a highlight for
the user if the channel is public. This function will also automatically resolve replies in private
conversations.


## Helper functions
Some helper functions are provided, please take a look at the source for detailed documentation of these:

    dazeus.optionsFromArgv(argv)

    dazeus.optimist()

    dazeus.help(argv)

    dazeus.readFile(file)

    dazeus.writeFile(file, data)

    dazeus.existsIn(file, str)

    dazeus.randomFrom(file)

    dazeus.removeFrom(file, str)

    dazeus.appendTo(file, str)

    dazeus.firstArgument(args)

    dazeus.isCommand(command, args, yes[, no])

