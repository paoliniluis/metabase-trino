FROM eclipse-temurin:11-jre-focal as runner

ENV FC_LANG en-US LC_CTYPE en_US.UTF-8

WORKDIR /app/

ADD run_metabase.sh .
ADD https://github.com/starburstdata/metabase-driver/releases/download/2.0.0/starburst-2.0.0.metabase-driver.jar plugins/starburst.metabase-driver.jar

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends ttf-dejavu && \
    # cleaning everything to reduce container size
    apt-get autoremove -y && apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* && \
    # providing permissions to the nobody user
    curl https://downloads.metabase.com/enterprise/latest/metabase.jar -o metabase.jar && \
    chmod +x run_metabase.sh && \
    chmod -R a+rwX /app/

# expose our default runtime port
EXPOSE 3000

# run it
ENTRYPOINT ["/app/run_metabase.sh"]