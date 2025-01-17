A fork of [bryanpkc/corkscrew](https://github.com/bryanpkc/corkscrew) to add GitHub actions
to build/release Linux versions for internal use.


Welcome to Corkscrew
====================

## Introduction

Corkscrew is a tool for tunneling SSH through HTTP proxies, but... you might
find another use for it.

Corkscrew has been compiled on:

- HPUX
- Solaris
- FreeBSD
- OpenBSD
- Linux
- Win32 (with Cygwin)

Corkscrew has been tested with the following HTTP proxies:

- Gauntlet
- CacheFlow
- JunkBuster
- Apache mod_proxy

Please open a pull request if you get it working on other proxies or compile
it elsewhere.


## Where Do I Get It?

Corkscrew's primary distribution site was
[agroman.net/corkscrew](https://web.archive.org/web/20170510154150/http://agroman.net/corkscrew/),
however it seems that the site went down and this repository is here to keep
the code available. The new location is then
[github.com/bryanpkc/corkscrew](https://github.com/bryanpkc/corkscrew).


## How Do I Install It?

First you need to install development tools:

```bash
# For Debian-based distributions (Ubuntu, ElementaryOS, ...)
sudo apt install build-essential

# For Red-Hat-based distributions (CentOS, Fedora, ...)
sudo yum groupinstall 'Development tools'
```

You need to clone the repo and then you need to go into the `corkscrew` source
directory and run

```bash
autoreconf --install
./configure
make
sudo make install
```

This will compile `corkscrew` and copy it into `/usr/local/bin/corkscrew`.

If you want to go more in depth about the configuration, please have a look at
the [INSTALL](./INSTALL) file which gives general information about the build
system.


## How Is It Used?

Setting up Corkscrew with SSH/OpenSSH is very simple. Adding
the following line to your `~/.ssh/config` file will usually do
the trick (replace `proxy.example.com` and `8080` with correct values):

```text
ProxyCommand /usr/local/bin/corkscrew proxy.example.com 8080 %h %p
```

**NOTE**: Command line syntax has changed since version 1.5. Please
notice that the proxy port is NOT optional anymore and is required
in the command line.


## How Do I Use The HTTP Authentication Feature?

You will need to create a file that contains your usename and password
in the form of:

```text
username:password
```

I suggest you place this file in your `~/.ssh` directory.

After creating this file you will need to ensure that the proper perms
are set so nobody else can get your username and password by reading
this file. So do this:

```text
chmod 600 myauth
```

Now you will have to change the `ProxyCommand` line in your `~/.ssh/config`
file. Here's an example:

```text
ProxyCommand /usr/local/bin/corkscrew proxy.work.com 80 %h %p ~/.ssh/myauth
```

The proxy authentication feature is very new and has not been tested
extensively so your mileage may vary. If you encounter any problems
when trying to use this feature please email me. It would be helpful
if you could include the following information:

- Proxy version (ie. Gauntlet Proxy, Microsoft Proxy Server, etc)
- Operating system you are trying to run corkscrew on
- Command line syntax you are using
- Any error messages that are visible to you

**NOTE**: I have had problems using the auth features with Mircosoft Proxy
server. The problems are sporadic, and I believe that they are related
to the round-robin setup that I was testing it again. Your mileage may
vary.


## Who Contributed?

The main author is Pat Padgett. But none of the contact info left work anymore,
so a name is all we have.

Bryan Chan created this repository and tweaked the code a little bit. Then
Rémy Sanchez improved the documentation.
