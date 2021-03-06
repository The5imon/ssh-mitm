# ssh-mitm - intercept ssh traffic [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=ssh%20mitm%20server%20for%20security%20audits%20supporting%20public%20key%20authentication%2C%20session%20hijacking%20and%20file%20manipulation%20&url=https://github.com/ssh-mitm/ssh-mitms&via=SshMitm&hashtags=ssh,mitm,security,audit)

[![CodeFactor](https://www.codefactor.io/repository/github/ssh-mitm/ssh-mitm/badge)](https://www.codefactor.io/repository/github/ssh-mitm/ssh-mitm)
[![Documentation Status](https://readthedocs.org/projects/ssh-mitm/badge/?version=latest)](https://docs.ssh-mitm.at/?badge=latest)
[![PyPI downloads](https://pepy.tech/badge/ssh-mitm/month)](https://pepy.tech/project/ssh-mitm)
[![GitHub](https://img.shields.io/github/license/ssh-mitm/ssh-mitm?color=%23434ee6)](https://github.com/ssh-mitm/ssh-mitm/blob/master/LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)


**man in the middle (mitm) server for security audits supporting public key authentication, session hijacking and file manipulation**

![SSH-MITM example](https://ssh-mitm.at/img/mitm-example.png)


## Give a Star! :star:
This keeps me motivated in developing this tool. Thanks!


## NEW in 0.4.3 - 2021-03-09

- compatibility with dropbear ssh clients

[Full Changelog](https://github.com/ssh-mitm/ssh-mitm/blob/master/CHANGELOG.md)


## Features

* Hijacking and logging of terminal sessions
* SCP and SFTP
    * store files
    * replace files
    * inject additional files
* Agent Forwarding
* Port Forwarding
* Check and test clients against known vulnerabilities
* Plugin support

## Installation of SSH-MITM

<img src="https://ssh-mitm.at/assets/images/streamline-free/monitor-loading-progress.svg" align="left" width="128">

The first step to using any software package is getting it properly installed.

To install SSH-MITM, simply run this simple command in your terminal of choice:

    $ pip install ssh-mitm

If you want to install all supported plugins for ssh-mitm you can install them with:

    $ pip install ssh-mitm[plugins]

## Quickstart

<img src="https://ssh-mitm.at/assets/images/streamline-free/programmer-male.svg" align="left" width="128">

Starting an intercepting mitm-ssh server with password authentication and session hijacking is very simple.

All you have to do is run this command in your terminal of choice.

    $ ssh-mitm --remote-host 192.168.0.x

Now let's try to connect to the ssh-mitm server.
The ssh-mitm server is listening on port 10022.

    $ ssh -p 10022 user@proxyserver

You will see the credentials in the log output.

    2021-01-01 11:38:26,098 [INFO]  Client connection established with parameters:
        Remote Address: 192.168.0.x
        Port: 22
        Username: user
        Password: supersecret
        Key: None
        Agent: None


## Session hijacking

<img src="https://ssh-mitm.at/assets/images/streamline-free/customer-service-woman.svg" align="left" width="128">

Getting the plain text credentials is only half the fun.
When a client connects, the ssh-mitm starts a new server, which is used for session hijacking.

    2021-01-01 11:42:43,699 [INFO]  created injector shell on port 34463.
                                    connect with: ssh -p 34463 127.0.0.1

To hijack the session, you can use your favorite ssh client. This connection does not require authentication.

    $ ssh -p 34463 127.0.0.1

After you are connected, your session will only be updated with new responses, but you are able to execute commands.

Try to execute somme commands in the hijacked session or in the original session.

The output will be shown in both sessions.


## Important note

**SSH-MITM should not be used as a jump host!**

It's intended to be used during security audits and not for separating networks.

If you need a jump host with audit capabilities (for security compliences), you can find a
[comparison of jump hosts](https://docs.ssh-mitm.at/jumphosts.html) in SSH-MITM's documentation.


## Contributing

<img src="https://ssh-mitm.at/assets/images/streamline-free/write-paper-ink.svg" align="left" width="128">

**Pull requests are welcome.**

For major changes, please open an issue first to discuss what you would like to change.

See also the list of [contributors](https://github.com/ssh-mitm/ssh-mitm/graphs/contributors) who participated in this project.
