# test-repo
testing-creation

docker ps -a --format "{{.Names}}: {{.Mounts}}" | grep "model-cache"

# For the nextcloud volume
docker run --rm -v nextcloud_aio_mastercontainer:/volume alpine sh -c \
  "apk add --no-cache jq && \
   echo '{\"Labels\": {\"com.docker.compose.project\": \"meridian-docker-suite\"}}' > /tmp/labels.json && \
   cat /tmp/labels.json"

docker volume create --name temp_volume
docker run --rm -v nextcloud_aio_mastercontainer:/from -v temp_volume:/to alpine cp -av /from/. /to/.
docker volume rm nextcloud_aio_mastercontainer
docker volume create --name nextcloud_aio_mastercontainer --label com.docker.compose.project=meridian-docker-suite
docker run --rm -v temp_volume:/from -v nextcloud_aio_mastercontainer:/to alpine cp -av /from/. /to/.
docker volume rm temp_volume
