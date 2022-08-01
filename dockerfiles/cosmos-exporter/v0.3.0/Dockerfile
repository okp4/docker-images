FROM alpine:3.16
EXPOSE 9300
USER root
RUN wget https://github.com/solarlabsteam/cosmos-exporter/releases/download/v0.3.0/cosmos-exporter_0.3.0_Linux_x86_64.tar.gz
RUN tar xvfz cosmos-exporter* -C /usr/bin

ENTRYPOINT [ "cosmos-exporter" ]
CMD [ "--denom", "uknow" ]
