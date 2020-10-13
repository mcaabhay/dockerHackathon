# Start docker file
FROM cirrusci/flutter as build

WORKDIR /app
# copy only required files 
COPY ./web ./web
COPY ./lib ./lib
COPY ./assets ./assets
COPY ./pubspec.yaml ./pubspec.yaml

# copy only required files
COPY ./build ./build

RUN flutter channel beta \
    && flutter upgrade \
    && flutter config --enable-web \
    && flutter build web
ARG LABEL_URL
ARG LABEL_TITLE
ARG LABEL_SOURCE
ARG LABEL_REVISION
ARG LABEL_VERSION
ARG LABEL_CREATED

LABEL org.opencontainers.image.url=${LABEL_URL} \
    org.opencontainers.image.title=${LABEL_TITLE} \
    org.opencontainers.image.source=${LABEL_SOURCE} \
    org.opencontainers.image.revision=${LABEL_REVISION} \
    org.opencontainers.image.version=${LABEL_VERSION} \
    org.opencontainers.image.created=${LABEL_CREATED}

#nginx for serve web app
FROM nginx
COPY --from=build /app/build/web /usr/share/nginx/html