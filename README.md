# OKP4 Docker Images

> 🐳 Repository for [Docker](https://www.docker.com/what-docker) configurations and images we use at [@okp4][okp4].

[![build](https://github.com/okp4/docker-images/actions/workflows/build.yml/badge.svg)](https://github.com/okp4/docker-images/actions/workflows/build.yml)
[![lint](https://github.com/okp4/docker-images/actions/workflows/lint.yml/badge.svg)](https://github.com/okp4/docker-images/actions/workflows/lint.yml)
[![publish](https://github.com/okp4/docker-images/actions/workflows/publish.yml/badge.svg)](https://github.com/okp4/docker-images/actions/workflows/publish.yml)
[![conventional commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

## Purpose

This repository contains various [Dockerfiles][dockerfiles] to build [Docker][docker] images we use [@okp4][okp4] and published to the [Github
Container Registry](https://github.com/orgs/okp4/packages) of our organization.

## Repository organization

The different dockerfiles are under the `dockerfiles` folder.

```text
.
├── <name-of-image>     # name of the docker image published under ghcr.io/okp4/<name-of-image>
│   ├── <tag-of-image>  # the tag of image - version, variant, etc.
│   │   └── Dockerfile  # the dockerfile
│   │
│   └── README.md       # a short description of the purpose of the docker image 
│
└── <etc.>
```

[dockerfiles]: https://docs.docker.com/engine/reference/builder/
[docker]: https://www.docker.com/what-docker
[okp4]: http://okp4.com
