## Ghost Dockerfile
This repository contains a **Dockerfile** to build a [Ghost](https://www.ghost.org/) blogging platform container image for [Docker](https://www.docker.io). It's really similar to the [trusted build](https://github.com/dockerfile/ghost) but the override script can deal with your uploaded images too, so you can migrate your Ghost installation to a Docker container without losing anything.

### Installation
1. Install [Docker](https://www.docker.io/).
2. Pull the [image build](https://index.docker.io/u/javivelasco/ghost/) from public [Docker Registry](https://index.docker.io/): `$ docker pull javivelasco/ghost` or build your own image from this repository Dockerfile: `$ docker build -t="javivelasco/ghost" github.com/javivelasco/dockerfile-ghost`.

### Usage
Just run the image:

    $ docker run -d -p 80:2368 javivelasco/ghost

You can customize your Ghost installation overriding data (images, database, themes) and configuration. This is useful to run an instance of Ghost with previous installation data. Create a folder in your host, let's call it `<override-dir>` containing:
* `config.js`: contains your blog configuration. It's important to replace default host address (`127.0.0.1`) inside server production configuration with `0.0.0.0`.
* `content/data`: persistent data such as the SQLite database.
* `content/themes`: installed themes.
* `content/images`: images uploaded from previous installation.

You can run your image with all this data:

    $ docker run -d -p 80:2368 -v <override-dir>:/ghost-override javivelasco/ghost

Where `<override-dir>` should be an absolute path to the mentioned folder.

### Dependencies
* Since Ghost runs on Node, the image is built from [dockerfile/nodejs](http://dockerfile.github.io/#/nodejs) trusted build image.
