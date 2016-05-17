FROM debian:jessie

RUN apt-get update && apt-get install -y git make gcc g++ libbz2-dev libz-dev bzip2
RUN git clone https://github.com/yinqiwen/ardb.git

ENV storage_engine rocksdb

RUN cd ardb && \
  make && \
  cp src/ardb-server /usr/bin && \
  cp ardb.conf /etc && \
  cd .. && \
  yes | rm -r ardb

RUN sed -e 's@home.*@home /var/lib/ardb@' \
  -e 's/loglevel.*/loglevel info/' -i /etc/ardb.conf

RUN echo 'trusted-ip *.*.*.*' >> /etc/ardb.conf

WORKDIR /var/lib/ardb

EXPOSE 36380
ENTRYPOINT /usr/bin/ardb-server /etc/ardb.conf
