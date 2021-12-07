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
      texlive=2021.20211127-1                               \
 && apt-get -y remove git                                   \
 && rm -rf /var/lib/apt/lists/*                             \
 && rm /etc/apt/sources.list.d/debian-unstable.list

# add user
RUN useradd -ms /bin/bash latex             \
 && chown -R latex /usr/local/share/texmf   \
 && chown -R latex /var/lib/texmf

USER latex

# extra packages
RUN \
    tlmgr --usermode init-usertree  \
 && tlmgr --usermode install        \
      adjustbox         \
      aeguill           \
      arsclassica       \
      babel-dutch       \
      babel-english     \
      babel-french      \
      babel-german      \
      background        \
      bera              \
      booktabs          \
      ccicons           \
      csquotes          \
      classicthesis     \
      doclicense        \
      draftwatermark    \
      fontawesome5      \
      enumitem          \
      eulervm           \
      ifmtarg           \
      lipsum            \
      listings          \
      minted            \
      microtype         \
      mparhack          \
      needspace         \
      pgf               \
      siunitx           \
      titlesec          \
      tocloft           \
      todonotes         \
      xcolor            \
      xifthen           \
      xpatch            \
      xstring           \
      xurl              \
      zref

WORKDIR /home/latex/source

CMD ["/bin/bash"]