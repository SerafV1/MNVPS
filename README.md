# Nodemaster - MNVPS

The **Nodemaster** scripts is a collection of utilities to manage, setup and update masternode instances.

I am quite confident this is the single best and almost effortless way to setup different crypto masternodes, without bothering too much about the setup part.

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
NODEMASTER BTC DONATIONS  33ENWZ9RCYBG7nv6ac8KxBUSuQX64Hx3x3
Seraf BTC DONATIONS 3QeyxTvNbk3k6JnFLbuFgRSUQ7L7Ypb7JT
```


Feel free to use my reflink to signup and receive a bonus w/ vultr:
<a href="https://www.vultr.com/?ref=7564562"><img src="https://www.vultr.com/media/banner_2.png" width="468" height="60"></a>

## Supported masternode projects

The ever growing list of supported projects is now maintained at [https://nodemaster-vps.com/supported-masternode-projects/](https://nodemaster-vps.com/supported-masternode-projects/).

However in addition to the officially listed projects, this version also supports:

BitMoney (V2 / Phoenix Project)
Galilel
---

**NOTE on the VPS choice for starters**

**Vultr** is highly recommended for this kind of setup. I created an [easy step-by-step guide for the VPS provider vultr](/docs/masternode_vps.md) that will guide you through the hardest parts.

---

## About / Background

Many masternode crypto currencies only have incomplete or even non-existing instructions available how to setup a masternode from source.

This project started as handy bash script to setup my $PIVX masternodes in 2016 when there was almost zero documentation and anything that existed was either $DASH specific, sucked and in most cases both. For that reason, i started to work on a not-so-sucking way to install a lot of different masternodes with next to none manual intervention.

Many people use binaries, end of with an insecure configuration or fail completely. This is obviously bad for the stability of the individual network.

After doing hundreds of masternode installations in the past two years, I decided to share some of my existing auto-install and management scripts with the community to work on a generalised & reliable setup for all masternode coins.

Comparing with building from source manually, you will benefit from using this script in the following way(s):

* 100% auto-compilation and 99% of configuration on the masternode side of things. It is currently only tested on a vultr VPS but should work almost anywhere where IPv6 addresses are available
* Developed with recent Ubuntu versions in mind, currently only 16.04 is supported
* Installs 1-100 (or more!) masternodes in parallel on one machine, with individual config and data
* Compilation is currently from source for the desired git repo tag (configurable via config files)
  Some security hardening is done, including firewalling and a separate user
* Automatic startup for all masternode daemons
* This script needs to run as root, the masternodes will and should not!
* It's ipv6 enabled, tor/onion will follow

## Installation

SSH to your VPS and clone the Github repository:

```bash
git clone https://github.com/SerafV1/MNVPS/ && cd MNVPS
```

Install & configure your desired master node with options:

```bash
./install.sh -p bitmoney
./install.sh -p galilel
```

## Examples for typical script invocation

These are only a couple of examples for typical setups. Check my [easy step-by-step guide for [vultr](/docs/masternode_vps.md) that will guide you through the hardest parts.

**Install & configure 4 BITMONEY masternodes:**

```bash
./install.sh -p bitmoney -c 4
./install.sh -p galilel -c 4 -n 6

```

**Update daemon of previously installed BITMONEY masternodes:**

```bash
./install.sh -p bitmoney -u
```

**Install 6 BITMONEY masternodes with the git release tag "tags/v2.1.1.0"**

```bash
./install.sh -p bitmoney -c 6 -r "tags/v2.1.1.0"
```

**Wipe all BITMONEY masternode data:**

```bash
./install.sh -p bitmoney -w
```

## Options

The _install.sh_ script support the following parameters:

| Long Option  | Short Option | Values              | description                                                         |
| :----------- | :----------- | ------------------- | ------------------------------------------------------------------- |
| --project    | -p           | project, e.g. "pix" | shortname for the project                                           |
| --net        | -n           | "4" / "6"           | ip type for masternode. (ipv)6 is default                           |
| --release    | -r           | e.g. "tags/v2.1.1"  | a specific git tag/branch, defaults to latest tested                |
| --count      | -c           | number              | amount of masternodes to be configured                              |
| --update     | -u           | --                  | update specified masternode daemon, combine with -p flag            |
| --sentinel   | -s           | --                  | install and configure sentinel for node monitoring                  |
| --wipe       | -w           | --                  | uninstall & wipe all related master node data, combine with -p flag |
| --help       | -h           | --                  | print help info                                                     |
| --startnodes | -x           | --                  | starts masternode(s) after installation                             |

## Troubleshooting the masternode on the VPS

If you want to check the status of your masternode, the best way is currently running the cli e.g. for $MUE via

```
/usr/local/bin/BitMoney-cli -conf=/etc/masternodes/bitmoney_n1.conf getinfo

{
    "version" : 2010100,
    "protocolversion" : 70006,
    "walletversion" : 61000,
    "balance" : 0.00000000,
    "zerocoinbalance" : 0.00000000,
    "blocks" : 10589,
    "timeoffset" : 0,
    "connections" : 26,
    "proxy" : "",
    "difficulty" : 5997.44423436,
    "testnet" : false,
    "moneysupply" : 5339887.65015577,
    "zsndsupply" : {
        "1" : 0.00000000,
        "5" : 5.00000000,
        "10" : 0.00000000,
        "50" : 0.00000000,
        "100" : 0.00000000,
        "500" : 0.00000000,
        "1000" : 0.00000000,
        "5000" : 0.00000000,
        "total" : 5.00000000
    },
    "keypoololdest" : 1539737893,
    "keypoolsize" : 1001,
    "paytxfee" : 0.00000000,
    "relayfee" : 0.00010000,
    "staking status" : "Staking Not Active",
    "errors" : ""
}

```

# Help, Issues and Questions

I activated the "[issues](https://github.com/masternodes/vps/issues)" option on github to give you a way to document defects and feature wishes. Feel free top [open issues](https://github.com/masternodes/vps/issues) for problems / features you are missing here: [https://github.com/masternodes/vps/issues](https://github.com/masternodes/vps/issues).

I might not be able to reply immediately, but i do usually within a couple of days at worst. I will also happily take any pull requests that make masternode installations easier for everyone ;-)

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
NODEMASTER BTC DONATIONS  33ENWZ9RCYBG7nv6ac8KxBUSuQX64Hx3x3
CRYPTVENTURE BTC DONATIONS 3FQSjittAYZj9im7dCywUZDjqMXHF6Xr2j
```


