# Telex
A Telegram Bot based on plugins. 

This bot uses twx.botapi and twx python libraries for its bindings.

Everything is being written for Python 3.4/3.5 currently. Everything works in a virtualenv installed and sourced in the launch script.

Some plugins require admin permissions. You can set an admin in permissions.conf using the following format

```
[groups]
  admins = <userid#>,<userid#>,<userid#>
```

You can get your user id number by sending the following query to the bot

```
/tginfo id
```

### Installation
Steps:
1: Clone git repository.
2: Edit configuration files.
3. Create and activate virtualenv.
2: Install dependencies
5: Run telex

#### Cloning the repository

    git clone --recursive https://github.com/datamachine/telex.git && cd telex

#### Setting up configuration
Put in bot token in `telex.conf.example` and rename it to `telex.conf`
    
Put in your user id in `permissions.conf.example` and rename to `permissions.conf`

#### Creating and activating virtualenv
    virtualenv -p python3 .virtualenv
    source .virtualenv/bin/activate

#### Installing dependencies
    pip install -r requirements.txt

#### Running telex

To start the bot, run the following in telex directory. Be sure to be inside your virtualenv.

    python runner.py

### Running telex as a service

#### For systems with systemd

If you have [systemd](http://www.freedesktop.org/wiki/Software/systemd/), you can run the bot as a service by following the below procedure.

To check if you have systemd, run 

    if test -d /usr/lib/systemd; then echo "exist"; else echo "doesn't exist"; fi

If output is ```exist``` then you have systemd and you can continue with below steps.

Edit the config file:

    sed -i "s/<username>/$(whoami)/g" etc/telex.service
    sed -i "s/<telexpath>/$(pwd)/g" etc/telex.service
    sudo cp etc/telex.service /etc/systemd/system/

Enabling service:

    sudo systemctl enable telex.service

Starting/Stopping telex:

    sudo systemctl start telex.service # To start it
    sudo systemctl status telex.service # To check status
    sudo systemctl stop telex.service # To stop it

Make sure that the status is Active: active (running)

#### For systems with upstart

If you have [upstart](http://upstart.ubuntu.com/), you can run the bot as a service by following the below procedure.

To check if you have upstart, run 

    if test -d /usr/lib/upstart; then echo "exist"; else echo "doesn't exist"; fi

If output is ```exist``` then you have upstart and you can continue with below steps.

Edit the config file:

    sed -i "s/<username>/$(whoami)/g" etc/telex.conf
    sed -i "s/<telexpath>/$(pwd)/g" etc/telex.conf
    sudo cp etc/telex.conf /etc/init/

Starting/Stopping telex:

    sudo start telex # To start it
    sudo stop telex # To stop it

#### For Mac
 Follow insrucions here: http://superuser.com/questions/264954/can-i-use-a-bash-script-as-a-service-in-os-x-without-having-to-set-it-up-trough

# Notes
While already very capable, this bot is still in relatively early development. Some plugin names, or plugin API calls may be modified. However, we are starting to settle on our stable APIs.

With that said, we do strive to have the bot continue to function seamlessly when pulling the latest HEAD

# Contact

The primary developers are Vince (@Surye) and Phillip (@xlopo) and can be contacted directly through telegram.

You can also join our telegram group using the link: https://telegram.me/twxapi

Bug reports and issues can be reported at: https://github.com/datamachine/telex/issues
