# test-repo
testing-creation


# Stop relevant containers
docker-compose stop nextcloud_aio_mastercontainer immich-machine-learning

# Create new volumes with correct project name
docker volume create meridian-docker-suite_nextcloud_aio_mastercontainer
docker volume create meridian-docker-suite_model-cache

# Copy data from old volumes to new ones
echo "Copying Nextcloud data (this may take a while)..."
docker run --rm \
  -v nextcloud_aio_mastercontainer:/source \
  -v meridian-docker-suite_nextcloud_aio_mastercontainer:/destination \
  alpine sh -c "cp -av /source/. /destination/"

echo "Copying model-cache data (this may take a while)..."
docker run --rm \
  -v plex-docker-suite_model-cache:/source \
  -v meridian-docker-suite_model-cache:/destination \
  alpine sh -c "cp -av /source/. /destination/"

echo "Volume data migration complete!"
