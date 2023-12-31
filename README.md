# IFTTT Webhook SSL server
[IFTTT](https://ifttt.com/) [Webhook](https://ifttt.com/maker_webhooks) SSL server to suspend/wake on lan/poweroff/reboot a Windows-PC and/or a Raspberry Pi.

## Prerequisites

1. Win7: Windows ssh server with key authentication to logon, e.g. [Bitvise SSH Server](https://www.bitvise.com/winsshd). Win10 has a built-in OpenSSH Server as an optional feature.
2. [Sysinternals PsShutdown](https://docs.microsoft.com/en-us/sysinternals/downloads/psshutdown) configured to run as administrator.
3. Windows and NIC configured for Wake On Lan (WOL) with a magic packet.
4. Linux server with systemd and Python 3.5+, e.g. a [Raspberry Pi](https://www.raspberrypi.org/learning/hardware-guide/components/raspberry-pi/).
5. Public IP address and name with a valid SSL certificate, a [Let’s Encrypt](https://letsencrypt.org/)  certificate for a DDNS name will do.


## Configuration/Installation

1. Copy the example configuration to `webhook.ini` and fill in your credentials.
2. Test the the respective `suspend`,  `wake`, `poweroff`, `poweroff_linux` or `reboot_linux` commands without IFTTT connectivity with `sudo webhook.py -v [command]`.
3. Create IFTTT applets with an `if this`-Button Widget and a `then that`-Webhook with method `POST`, Content Type `application/json` and a command in the `example.json` format.
4. Run the server in verbose mock mode (no communication with the Windows-PC) with `sudo webhook.py -m -v` and check the IFTTT applets.
5. To double check run the server in production mode with just `sudo webhook.py`.
6. Run `sudo make install` to install the `webhook.service` as a system service.


## Changes

2022-04-21: Added an optional `argument` for `wake` and `poweroff` to override the `mac` resp. `host` configured in `webhook.ini`.