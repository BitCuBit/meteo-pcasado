FROM openjdk:11.0.13-slim-buster as build

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
USER root

COPY . /source

RUN cd /source && ./mvnw -DfinalName="app" -P api-docs,prod clean package

FROM openjdk:11.0.13-jre-slim-buster

ENV APPLICATION_SLEEP 0

COPY --from=build /source/api/target/app.jar /app/app.jar
COPY docker-entrypoint.sh /app/docker-entrypoint.sh

EXPOSE 8080

ENTRYPOINT [ "/app/docker-entrypoint.sh"]

# Define labels at end to avoid rebuilding image when they change.
ARG LABEL_BUILD_CREATED="n/a"
ARG LABEL_IMAGE_VERSION="n/a"
ARG LABEL_REVISION="n/a"

LABEL org.opencontainers.image.authors='Pablo Casado Varela <pcasado@bitcubit.com>'
LABEL org.opencontainers.image.url='https://github.com/BitCuBit/meteo-pcasado'
LABEL org.opencontainers.image.documentation='https://github.com/BitCuBit/meteo-pcasado'
LABEL org.opencontainers.image.source='https://github.com/BitCuBit/meteo-pcasado'
LABEL org.opencontainers.image.vendor='Pablo Casado Varela'
LABEL org.opencontainers.image.licenses='MIT'
LABEL org.opencontainers.image.title='Meteo'
LABEL org.opencontainers.image.description='This image contains all required executables to deploy the Meteo api'
