# Remove a docker container once its exited
For work, I needed to create a docker executable that would clone a database when given the src and target DB instance info via environment variables. I learned you can add the `--rm` flag to delete the container after its has exited.

```
docker run \
  --rm \
  --env SRC_DB_HOST='1.2.3.4' \
  --env SRC_DB_PASSWORD='abc' \
  --env SRC_DB_NAME='main' \
  --env TARGET_DB_HOST='5.4.3.4' \
  --env TARGET_DB_PASSWORD='efg' \
  --env TARGET_DB_NAME='core' \
  pgdup:v1
```