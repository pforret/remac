![bash_unit CI](https://github.com/pforret/remac/workflows/bash_unit%20CI/badge.svg)
![Shellcheck CI](https://github.com/pforret/remac/workflows/Shellcheck%20CI/badge.svg)
![GH Language](https://img.shields.io/github/languages/top/pforret/remac)
![GH stars](https://img.shields.io/github/stars/pforret/remac)
![GH tag](https://img.shields.io/github/v/tag/pforret/remac)
![GH License](https://img.shields.io/github/license/pforret/remac)
[![basher install](https://img.shields.io/badge/basher-install-white?logo=gnu-bash&style=flat)](https://basher.gitparade.com/package/)

# remac

change the MAC address of your computer to avoid traceability

## Installation

with [basher](https://github.com/basherpm/basher)

	$ basher install pforret/remac

or with `git`

	$ git clone https://github.com/pforret/remac.git
	$ cd remac

## Usage

```bash
Program: remac 1.0.0 by peter@forret.com
Updated: Feb 10 12:55:04 2021
Description: change the MAC address of your computer to avoid trackability
Usage: remac [-h] [-q] [-v] [-f] [-l <log_dir>] [-t <tmp_dir>] [-p <prefix>] [-i <interface>] <action> <input?>
Flags, options and parameters:
-h|--help        : [flag] show usage [default: off]
-q|--quiet       : [flag] no output [default: off]
-v|--verbose     : [flag] output more [default: off]
-f|--force       : [flag] do not ask for confirmation (always yes) [default: off]
-l|--log_dir <?> : [option] folder for log files   [default: /Users/pforret/log/remac]
-t|--tmp_dir <?> : [option] folder for temp files  [default: .tmp]
-p|--prefix <?>  : [option] MAC company prefix: <company>/<XX:XX:XX>/copy  [default: copy]
-i|--interface <?>: [option] name of interface: <eth0>  [default: first]
<action>         : [parameter] action to perform: get/set/prefix
<input>          : [parameter] search text for prefix (optional)

```
### remac get

get MAC addresses for all active interfaces
```bash
> ./remac get
Interface: en0 | IP address: 192.168.1.47 | MAC: 3c:15:c2:d8:xx:xx (Apple, Inc.)
```

### remac prefix {search term}

get existing MAC prefixes for different vendors

```bash
> ./remac prefix cray
00:00:6D        CrayComm        Cray Communications, Ltd.
00:00:80        CrayComm        Cray Communications (formerly Dowty Network Services)   # [Also shows as "Harris (3M) (new)" and/or "Imagen(?)" elsewhere]
00:0E:AB        Cray    Cray Inc
00:40:A6        CrayRese        Cray Research Inc. 
```

### remac set

set new MAC address (will require sudo password)

```bash
> ./remac set 
…  Interface to set: en0
…  Old MAC address : 3c:15:c2:d8:xx:xx
…  Using company ID: 3c:15:c2 (Apple, Inc.)
…  New MAC address : 3c:15:c2:ea:76:34
…  Changing the network address requires the root password
Password:

# explicitly specify manufacturer prefix to use
> ./remac -p "cray" set
…  Interface to set: en0
…  Old MAC address : 3c:15:c2:d8:19:ce
…  Using company ID: 00:00:6D (Cray Communications, Ltd.)
…  New MAC address : 00:00:6D:1a:49:17
…  Changing the network address requires the root password
Password:

> ./remac -p "00:00:6B" set
…  Interface to set: en0
…  Old MAC address : 3c:15:c2:d8:xx:xx
…  Using company ID: 00:00:6B (Silicon Graphics)
…  New MAC address : 00:00:6B:13:30:f8
…  Changing the network address requires the root password
Password:

# explicitly specify interface to set
> ./remac -i "eth1" set
…  Interface to set: eth1
…  Old MAC address : 00:03:FF:00:19:ce
…  Using company ID: 00:03:FF (Microsoft Corporation)
…  New MAC address : 00:03:FF:ea:76:34
…  Changing the network address requires the root password
Password:


```

## Acknowledgements

* idea by [josh.works](https://josh.works/shell-script-basics-change-mac-address#figure-out-which-adapter-your-machine-is-using-to-connect-to-the-wifi) via [HN](https://news.ycombinator.com/item?id=26060152)
* script created with [bashew](https://github.com/pforret/bashew)

&copy; 2021 Peter Forret
