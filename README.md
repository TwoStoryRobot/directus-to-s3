# docker-directus-to-s3

Container that daily backs up a Directus instance to S3

## How to Use

Basic usage is as follows:

```
docker run \
  -e "MYSQL_HOST=mysql" \
  -e "MYSQL_USER=directus" \
  -e "MYSQL_PASSWORD=password" \
  -e "AWS_BUCKET=my-aws-bucket" \
  -e "AWS_DEFAULT_REGION=us-west-1" \
  -e "AWS_ACCESS_KEY_ID=my-aws-access-key-id" \
  -e "AWS_SECRET_ACCESS_KEY=my-aws-secret-access-key" \
  --link mysql:mysql \
  -v /path/to/directus/uploads:/media/uploads \
  twostoryrobot/directus-to-s3
```

This will start a cron in the background which will run an upload script daily. All of the databases will be export from the provided mysql database and packaged with the current stage of the `/uploads` folder from Directus. This package will be uploaded to the provided S3 bucket as `directus_dump_<date>T<time>.tar.gz`.
