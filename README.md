# ElasticMQ on Docker

ElasticMQ on Docker, ElasticMQ docker container.

This container is used for local-pc development.
You can use this container, when you develop an application
used AWS SQS for messaging without aws services.

see.
https://github.com/adamw/elasticmq

# Getting started

Start docker container.

```
$ docker pull takemikami/elasticmq
$ docker run -d -v /var/log/elasticmq:/var/log -p 9324:9324 -t takemikami/elasticmq
```

Execute sample program.

sample.rb

```
require 'aws-sdk'

sqscli = Aws::SQS::Client.new(
  region:             'dummy-sqs',
  endpoint:           "http://192.168.59.103:9324",
  access_key_id:      'dummy',
  secret_access_key:  'dummy',
)

sqscli.create_queue(queue_name: 'test')

options = {
  queue_url: 'http://192.168.59.103:9324/queue/test',
}
resp = sqscli.receive_message(options)

p resp
```

```
$ gem install aws-sdk
$ ruby sample.rb
```

# Build Container

```
$ docker build -t elasticmq .
```
