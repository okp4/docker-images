FROM alpine:3.16
EXPOSE 9300

RUN wget -q https://github.com/solarlabsteam/cosmos-exporter/releases/download/v0.3.0/cosmos-exporter_0.3.0_Linux_x86_64.tar.gz -O - |\
    tar -zxvf - -C /usr/bin

ENTRYPOINT [ "cosmos-exporter" ]
CMD [ "--denom", "uknow" ]
