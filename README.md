tor-mirror-bootstrap
====================

Quickly set up a mirror of the Tor website on OSX.

## Requirements

Read [Tor's official documentation on running a mirror](https://www.torproject.org/docs/running-a-mirror.html.en) to learn more about the technical requirements. The system requirements for running a mirror are as follows:

* Have at least 8 GB of disk space on location where you wish to host mirror
* `cron`, `launchd`, or other system task scheduler
* A web server - Apache, nginx, etc.

This bootstrap script currently only checks the first requirement - the other two are up to you to deal with. This script's job is to download and update the files within your mirror, synchronizing them to those provided by the Tor project via `rsync`.

## Installation

1. Download the setup script (*note: `curl` may fail, it doesn't seem to play nice with GitHub's servers*):
```
wget https://raw.githubusercontent.com/alebcay/tor-mirror-bootstrap/master/setup
```

(the setup script will fetch the update script if you don't have it). Or, just get the whole repo:
```
git clone https://github.com/alebcay/tor-mirror-bootstrap
```

2. Run the setup script. **`cd` to the location where you want the mirror to be, your mirror will be at `$(pwd)/tor-mirror`:
```
./setup
```
This could take a while. Your computer is fetching about 4.4 GB of data from Tor's servers at this step.

3. The docroot of the mirror is at `$(pwd)/tor-mirror`. Place this in an Apache `VirtualHost` block or an nginx `server` block.

## Updating

Tor requires all servers to remain updated with it's source. There should be `update` in the same directory as `setup`. Run it to update your sources (and make sure to schedule it with `cron`, `launchd`, etc.). **`update` runs in the same directory it's launched in, so make sure the working directory is set correctly when executing with `cron` or `launchd`.**
