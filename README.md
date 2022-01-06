# docker-tern

![Build Docker images](https://github.com/philips-software/docker-tern/workflows/Build%20Docker%20images/badge.svg)
![repolinter](https://github.com/philips-software/docker-tern/workflows/repolinter/badge.svg)
[![Slack](https://philips-software-slackin.now.sh/badge.svg)](https://philips-software-slackin.now.sh)

# Docker images

This repo will contain docker images with _tern_

Current versions available:
```
.
├── 2
│   ├── scancode
│   └── vanilla
├─── latest
│   └── tern
└─── local
    └── tern
```
## Usage

Images can be found on [https://hub.docker.com/r/philipssoftware/tern/](https://hub.docker.com/r/philipssoftware/tern/).

Since `tern` internally relies on Docker, we need to run this container in `--privileged` mode so it can mount on the host's disk as well as bind `docker.sock` from the host.

```
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock philipssoftware/tern --version 
```

## Extracting Bill of Material from Docker Images

Tern makes it very easy to extract Docker images BOMs. All the available export formats are available on the [official docs](https://github.com/vmware/tern)

Example:

```bash
mkdir my_dir

docker run --rm -v /var/run/docker.sock:/var/run/docker.sock philipssoftware/tern report -f json -i debian:buster > debian_buster.json
```

This command will create a file called `debian_buster.json` with Debian's Buster [official image](https://hub.docker.com/layers/debian/library/debian) BOM

## Content

The images obviously contains Tern, but also two other files:
- `REPO`
- `TAGS`

### REPO

This file has a url to the REPO with specific commit-sha of the build.
Example: 

```
$ docker run philipssoftware/tern:latest cat REPO
https://github.com/philips-software/docker-tern/tree/14ab374e0812ba03e32e5f2c81c7c9dfb8ef7958
```

### TAGS

This contains all the similar tags at the point of creation. 

```
$ docker run philipssoftware/tern cat TAGS
tern:2 tern:latest
```

You can use this to pin down a version of the container from an existing development build for production. When using `tern` for development. This ensures that you've got all security updates in your build. If you want to pin the version of your image down for production, you can use this file inside of the container to look for the most specific tag, the last one.

## Why

> Why do we have our own docker image definitions?

We often need some tools in a container for checking some things. F.e. [jq](https://stedolan.github.io/jq/), [aws-cli](https://aws.amazon.com/cli/) and [curl](https://curl.haxx.se/).
We can install this every time we need a container, but having this baked into a container seems a better approach.

That's why we want our own docker file definitions.

## Issues

- If you have an issue: report it on the [issue tracker](https://github.com/philips-software/docker-tern/issues)

## Author

- Thales Sousa  <thales.sousa@philips.com>
- Jeroen Knoops <jeroen.knoops@philips.com>

## License

License is MIT. See [LICENSE file](LICENSE.md)

## Philips Forest

This module is part of the Philips Forest.

```
                                                     ___                   _
                                                    / __\__  _ __ ___  ___| |_
                                                   / _\/ _ \| '__/ _ \/ __| __|
                                                  / / | (_) | | |  __/\__ \ |_
                                                  \/   \___/|_|  \___||___/\__|  

                                                                 Infrastructure
```

Talk to the forestkeepers in the `docker-images`-channel on Slack.

[![Slack](https://philips-software-slackin.now.sh/badge.svg)](https://philips-software-slackin.now.sh)
