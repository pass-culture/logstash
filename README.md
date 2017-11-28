# Logstash boilerplate

This repository contains a boilerplate for deploying logstash on Scalingo.

You have three different configuration available:

* `logstash.conf`: this configuration will listen for http request
  authenticated by the authentication information passed in the `USER` and
  `PASSWORD` environment variables and send it to and elasticsearch database.
  This will also parse url defined variables.
* `logstash-json.conf` this configuration is based on the previous one but if
  the content is a valid json it will parse it
* `logstash-kv.conf` this configuration is based on `logstash.conf` but it will
  also parse the content to search and parse patterns like `key=value`

By default we are using the `logstash.conf` configuration, but you can use
another one by changing the `web` process of the `Procfile` from: ``` web:
bin/logstash -f logstash.conf ```

To:
```
web: bin/logstash -f logstash-json.conf
```

To:
```
web: bin/logstash -f logstash-kv.conf
```

## Configuration

You will need to configure the following environment variables:

* `USER` the username that you will use to authenticate against your logstash
  instance
* `PASSWORD` the password that you will use to authenticate against your
  logstash instance
* `ELASTICSEARCH_URL` the URL of your elasticsearch instance. (If you use our
  Elasticsearch addon, this will be automatically added)

You will also change the `change-me` index name in the output section of your
logstash configuration.
# logstash-test-runner

![image](http://i.imgur.com/hQm9yAb.gif)

Example tests are in the `__tests__` directory.
To add a tests, simply add a new directory with the given input `input.log`, the ETL configuration `logstash.conf`, and the expected output `output.log`.

## Prerequisites

* Install nodejs
* Run `npm install`
* Install Docker

# Setup

* Clone repository
* Setup your test directory as follows

```sh
__tests__
  crawlers
    input.log
    logstash.conf
    output.log
  mongo
    input.log
    logstash.conf
    output.log
  # ...
```

* Run your tests

```sh
# ./test.sh <test-parent-directory>
./test.sh __tests__
```

NOTE: Multiline logs in logstash need translate in reverse to filebeat in terms of `multiline.match` from `previous` => `after` and `next` => `before`.
