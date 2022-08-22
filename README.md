# OKP4 Docker Images

> 🐳 Repository for [Docker](https://www.docker.com/what-docker) configurations and images we use at [@okp4][okp4].

![lint](https://img.shields.io/github/workflow/status/okp4/docker-images/Lint?label=lint&style=for-the-badge&logo=github)
![build](https://img.shields.io/github/workflow/status/okp4/docker-images/Build?label=build&style=for-the-badge&logo=github)
![publish](https://img.shields.io/github/workflow/status/okp4/docker-images/Publish?label=publish&style=for-the-badge&logo=github)
[![conventional commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?logo=conventionalcommits&style=for-the-badge)](https://conventionalcommits.org)
[![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg?style=for-the-badge)](https://opensource.org/licenses/BSD-3-Clause)

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

## License

The project is licensed under the `BSD-3-Clause License` which you can find in file [LICENSE.md](LICENSE).

Software components inside the image built by this project are under the respective licenses chosen by their respective copyright holders.

[dockerfiles]: https://docs.docker.com/engine/reference/builder/
[docker]: https://www.docker.com/what-docker
[okp4]: http://okp4.com
