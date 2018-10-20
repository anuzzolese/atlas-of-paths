FROM tenforce/virtuoso:1.3.1-virtuoso7.2.2

# Add Virtuoso bin to the PATH
ENV PATH /usr/local/virtuoso-opensource/bin/:$PATH

# Add Virtuoso config
COPY virtuoso.ini /virtuoso.ini

# Add dump_nquads_procedure
COPY dump_nquads_procedure.sql /dump_nquads_procedure.sql

# Add Virtuoso log cleaning script
COPY clean-logs.sh /clean-logs.sh

# Add startup script
COPY virtuoso.sh /virtuoso.sh

# Download ontologies
WORKDIR /usr/local/virtuoso-opensource/share/virtuoso/vad/ontologies/

RUN apt-get update\
  && apt-get install -y curl \
  && curl -L -H "Accept: text/turtle" https://w3id.org/italia/onto/Route > route.ttl \
  && curl -L -H "Accept: text/turtle" https://w3id.org/italia/onto/AtlasOfPaths > atlas.ttl \
  && curl -L -H "Accept: text/turtle" https://w3id.org/italia/onto/l0 > l0.ttl 

VOLUME /data
WORKDIR /data
EXPOSE 8890
EXPOSE 1111

CMD ["/bin/bash", "/virtuoso.sh"]
