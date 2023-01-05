# OKP4 Docker Images

> 🐳 Repository for [Docker](https://www.docker.com/what-docker) configurations and images we use at [@okp4][okp4].

![lint](https://img.shields.io/github/actions/workflow/status/okp4/docker-images/lint.yml?branch=main&label=lint&style=for-the-badge&logo=github)
![build](https://img.shields.io/github/actions/workflow/status/okp4/docker-images/build.yml?branch=main&label=build&style=for-the-badge&logo=github)
![publish](https://img.shields.io/github/actions/workflow/status/okp4/docker-images/publish.yml?branch=main&label=publish&style=for-the-badge&logo=github)
[![conventional commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?logo=conventionalcommits&style=for-the-badge)](https://conventionalcommits.org)
[![contributor covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg?style=for-the-badge)](https://github.com/okp4/.github/blob/main/CODE_OF_CONDUCT.md)
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

## You want to submit a Dockerfile? 😍

Any contribution is very welcome. Make sure you commit your Dockerfile in the path that matches `./dockerfiles/$PROJECT/$VERSION` alongside with a `README.md` that will be used as dockerhub description. Also, please, check out OKP4 health files :

- [Contributing](https://github.com/okp4/.github/blob/main/CONTRIBUTING.md)
- [Code of conduct](https://github.com/okp4/.github/blob/main/CODE_OF_CONDUCT.md)

## License

The project is licensed under the `BSD-3-Clause License` which you can find in file [LICENSE.md](LICENSE).

Software components inside the image built by this project are under the respective licenses chosen by their respective copyright holders.

[dockerfiles]: https://docs.docker.com/engine/reference/builder/
[docker]: https://www.docker.com/what-docker
[okp4]: http://okp4.com
