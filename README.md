# Sevenhugs Smart Remote SDK for prototype

## How to install

First clone the SDK from github:

    $ git clone git@github.com:sevenhugs/smart-remote-sdk.git
    $ cd smart-remote-sdk

You also need to clone all submodules:

    $ git submodule init
    $ git submodule update

Then, install a local copy of lua and its libraries:

    $ make -C lib/lua install
    $ make -C lib/lualib install

> You can use your own lua installation if you like, the SDK uses Lua
version 5.3.  However using the procedure in this file is a great way to make
sure your environment is set up exactly the same way as ours.

> If you're running Linux and get compilation errors, make sure you have
installed the readline development package (which is probably named
`libreadline-dev` or `readline-devel`).

This will install lua in `$HOME/local/lua`, you should make sure that
`$HOME/local/lua/bin` is in your PATH or use the full path to lua each time
you run it.

You can test that lua is installed correctly (this will get the page at
http://remote.sevenhugs.com/):

    $ cd lua
    $ lua install_test.lua

If this prints "Success!" you are ready to go!

## Running a control test

You will find examples control scripts in `lua/control` with their associated
test script in `lua/control/test`.  Every control script accepts the `--help`
argument to print a short usage guide.

You can also use the `--debug` option to see a dump of HTTP exchanges done by
the script.

### Philips Hue

    $ cd lua/control/test
    $ lua test_hue.lua --address 192.168.0.50 --light 1 --user myuser
    $ lua test_hue.lua --address 192.168.0.50 --light 1 --user myuser --set true 0.5

* `--address`: this is the address of the Philips Hue bridge.  It can be found
  using UPnP or by visiting http://www.meethue.com/api/nupnp.
* `--light`: this is the light identifier (this is a number, not the light
  name).
* `--user`: this is the user name created by pressing the pairing button on
  the bridge (see [Philips Hue API - Getting started][1]).
* `--set`: set state (on or off) and brightness (between 0 and 1).

[1]: http://www.developers.meethue.com/documentation/getting-started

### Sonos

    $ cd lua/control/test
    $ lua test_sonos.lua --address 192.168.0.51
    $ lua test_sonos.lua --address 192.168.0.51 --set_state true
    $ lua test_sonos.lua --address 192.168.0.51 --set_volume 0.5
    $ lua test_sonos.lua --address 192.168.0.51 --command '"next"'

* `--address`: this is the address of the Sonos player.  It can be found using
  SSDP or in the Sonos application.
* `--set_state`: set state (playing or paused).
* `--set_volume`: set volume (between 0 and 1).
* `--command`: `"next"` or `"previous"` song (this must be parsed as a lua
  string, so quotes should not be protected from the shell).
