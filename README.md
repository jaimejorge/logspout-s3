# Logspout-S3

Logspout-S3 is a container app that listens on the Docker bus and streams
application logs to Amazon S3 at some FLUSH_INTERVAL. It's built as an adapter
to github.com/gliderlabs/logspout.

## Usage

```shell
docker run -d --name=logspout-s3 \
	-e 'BACKLOG=false' \
	-e 'AWS_ACCESS_KEY=YOUR_KEY' \
	-e 'AWS_SECRET_KEY=YOUR_SECRET_KEY' \
	-e 'AWS_REGION=us-east-1' \
	-e 'FLUSH_INTERVAL=120' \
	--volume=/var/run/docker.sock:/var/run/docker.sock \
	pressly/logspout-s3 \
	s3://pressly-logs-test
```

See the `example/` folder and Makefile to get started. It demonstrates a REST API
service with JSON structured logging output, and also the start command
for logspout-s3 which will stream those logs.

If you'd like to query the logs, check out https://aws.amazon.com/athena/ which
uses S3 as a backend for any kind of log data to query/visualize.

# LICENSE

MIT