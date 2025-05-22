Sharing my full setup here (with `ubuntu:22.04` ) for anyone who wants to have a try — it works on my machine (Mac with M4 chip), and I can rebuild and reopen the container without issues. Just note that rebuilding takes a bit more time because Bochs gets installed during the setup.

## 1. `Dockerfile`

I also removed the COPY instruction and just used mount to map local files.

```Dockerfile
FROM ubuntu:22.04

RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
		bash \
		build-essential \
		gdb \
		gcc \
		emacs \
		vim \
		nano \
		qemu \
		qemu-system-i386 \
		wget \
		xorg-dev \
		libncursesw5 \
		libncurses5-dev \
		dos2unix \
		expect \
		rsync \
		git\
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* 

RUN mkdir -p /pintos/src

ENV PINTOS_HOME=/pintos

ENV PATH=/pintos/src/utils:$PATH

WORKDIR /pintos
```

## 2. `init.sh`

```sh
#!/bin/bash
set -e

cd /pintos/src/misc
wget --no-check-certificate https://sourceforge.net/projects/bochs/files/bochs/2.6.11/bochs-2.6.11.tar.gz
sh ./bochs-2.6.11-build.sh /usr/local
rm -f bochs-2.6.11.tar.gz

cd /pintos/src/utils
make

cd /pintos/src/threads
make

echo "finish initialization!"
```

While running this script and compiling utils, I ran into a version issue — `<stropts.h>` isn’t available anymore in newer Ubuntu versions like 22.04.
Since this header and the related code didn’t seem important for our assignment, I just:
- Commented out the `#include <stropts.h>` line and a bit of unused related code
- Added -Wno-format-security to the Makefile to silence some warnings
After that, utils compiled just fine!
## 3.  Build image (for Mac M-chip)

Since I’m using a Mac with an M-series chip (M4), I used `buildx` to build the image first. On other environments, It might be able to just use docker run directly. 

```
docker buildx build --platform linux/amd64 -t pintos-amd64 . --load
```

## 4. `.devcontainer/devcontainer.json`

I believe we can just use docker run directly here and then run `init.sh` for the first time — I just chose to use a dev container as a small practice by myself.
```json
{
	"name": "C69-Pintos",
	"image": "pintos-amd64",
	"workspaceFolder": "/pintos",
	"mounts": [
		"source=${localWorkspaceFolder},target=/pintos,type=bind"
	],
	"runArgs": ["--platform=linux/amd64"],
	"customizations": {
		"vscode": {
			"settings": {
				"terminal.integrated.defaultProfile.linux": "bash"
			},
			"extensions": ["ms-vscode.cpptools"]
		}
	},
	"postCreateCommand": "./init.sh"
}
```

