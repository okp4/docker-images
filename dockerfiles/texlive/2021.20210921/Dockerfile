FROM debian:bullseye-20211115

ENV \
    DEBIAN_FRONTEND noninteractive \
    LANG=C.UTF-8

# basic installation
RUN \
    echo "deb http://deb.debian.org/debian sid main"        \
      > /etc/apt/sources.list.d/debian-unstable.list        \
 && apt-get update                                          \
 && apt-get install -y --no-install-recommends              \
      perl-tk=1:804.035-0.1+b1                              \
      wget=1.21-1+b1                                        \
      xz-utils=5.2.5-2                                      \
      latexmk=1:4.70b-0.2                                   \
 && apt-get install -y --no-install-recommends -t unstable  \
      texlive=2021.20210921-1                               \
 && apt-get -y remove git                                   \
 && rm -rf /var/lib/apt/lists/*                             \
 && rm /etc/apt/sources.list.d/debian-unstable.list

RUN useradd -ms /bin/bash latex             \
 && chown -R latex /usr/local/share/texmf   \
 && chown -R latex /var/lib/texmf

USER latex

# extra packages
RUN \
    tlmgr --usermode init-usertree  \
 && tlmgr --usermode install        \
      adjustbox         \
      arsclassica       \
      bera              \
      booktabs          \
      classicthesis     \
      doclicense        \
      draftwatermark    \
      enumitem          \
      eulervm           \
      lipsum            \
      listings          \
      microtype         \
      mparhack          \
      siunitx           \
      titlesec          \
      tocloft           \
      todonotes         \
      xcolor            \
      xpatch

WORKDIR /home/latex/source

CMD ["/bin/bash"]