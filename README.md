rmq-publish
===========

This is a simple RabbitMQ publisher tool written in Erlang.

Build
-----
You need Erlang and [rebar](https://github.com/basho/rebar).

    $ cd rmq-publish
    $ rebar get-deps compile escriptize
    [...]

This should fetch dependencies, compile everything, and create executable escripts.

You can also use `make` to drive the build:

    $ make

Usage
-----
Simple publishing:

    $ ./rmq_publish -e myexchange -r routingkey -d ~/docs_to_publish/ --dps=500

This will publish all files in `~/docs_to_publish` to the broker running on `localhost:5672`, using the exchange `myexchange` with the routing key `routingkey`.

To specify broker access:

    $ ./rmq_publish -u amqp://guest:guest@192.168.1.1:5672/%2f -e myexchange -r key -d ~/docs_to_publish/

To use individual files as input, not a directory:

    $ ./rmq_publish -e myexchange -r routingkey -f ~/file1.txt -f ~/file2.txt

The `-f`/`--file` option can be specified multiple times as seen above, just like the `-d`/`--directory` option.

You can also supply tarballs as input to `rmq_publish`. They will be extracted in memory and the files inside the tarball published. This parameter can be used multiple times as well:

    $ ./rmq_publish -e myexchange -r routingkey -b ~/first_archive.tar.gz -b ~/second_archive.tar.gz

Input parameters (i.e. `-f`, `-d` and `-b`) can be mixed in any combination.
