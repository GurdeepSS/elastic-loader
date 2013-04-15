# elastic-loader

A utility for bulk loading data into elasticsearch. It can also execute multiple commands in a simplified format. It's a single java jar with no external dependencies so it's easy to run.

## Download

Current Version: [elastic-loader-0.2.0.jar](http://elastic-loader.s3.amazonaws.com/elastic-loader-0.2.0.jar)

## Usage

The basic usage is `java -jar elastic-loader.jar FILENAME SERVER_URL`

For example, you could run `java -jar elastic-loader.jar test_import http://localhost:9200` to load the data from the file `test_import` into the server at `http://localhost:9200`. Where `test_import` looks like:

```
# Issue an HTTP Request, without stopping due to failure
TRY DELETE /foo
# Issue an HTTP request that will stop the import if it fails
POST /foo {"_mapping": {}}
# Bulk index items of time foo and bar
BULK INDEX foo/bar
{"user": "foo", "_id": 1}
{"user": "baz", "_id": 3}
# A comment, followed by an index request
BULK INDEX foo/bar
{"user": "bort"}
{"ohai": "there", "_id": 4}
DELETE /foo/bar/4
```

The format allows you to issue arbitrary HTTP requests and to use the bulk API to add new documents as well with a more concise format. You specify the index and document type once, and subsequent documents will be imported. Each document should probably specify the `_id` field unless you truly want random IDs from elasticsearch.

This project was created to aid the process of running examples for the book [Exploring Elasticsearch](http://exploring-elasticsearch.com).

## License

Copyright © 2013 Andrew Cholakian

Distributed under the Eclipse Public License, the same as Clojure.
