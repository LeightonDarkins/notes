# PSS Standalone ElasticSearch

## For Reference

The bulk of what's written here has bee shamelessly lifted from [here](https://www.elastic.co/guide/en/elasticsearch/reference/6.5/index.html).

## Install ElasticSearch

- [Download the archive (tar/zip)](https://www.elastic.co/downloads/past-releases/elasticsearch-6-5-0)
- Extract it
  - Tar: `tar -xvf *archivename*`
- Put the extracted folder wherever you like on your system

## Run ElasticSearch

- Get yourself into the ElasticSearch directory

```
cd place/where/you/put/elasticsearch
```

- Run it
  - this will start ElasticSearch with its default settings

```
./bin/elasticsearch
```

- Test it by executing this as a GET HTTP request
  - Need a client to interact with HTTP endpoints? [Postman is a good option](https://www.getpostman.com/).
  - curl is good too ;)

```
http://localhost:9200/?pretty
```

- You should see a response like this:

```
{
    "name": "1fNQ8X2",
    "cluster_name": "elasticsearch",
    "cluster_uuid": "tFz-m1IZQC6pnjdcTd7q2w",
    "version": {
        "number": "6.5.0",
        "build_flavor": "default",
        "build_type": "tar",
        "build_hash": "816e6f6",
        "build_date": "2018-11-09T18:58:36.352602Z",
        "build_snapshot": false,
        "lucene_version": "7.5.0",
        "minimum_wire_compatibility_version": "5.6.0",
        "minimum_index_compatibility_version": "5.0.0"
    },
    "tagline": "You Know, for Search"
}
```

## Configure Elastic Search

### The Basics

- Find and open the ElasticSearch config file

```
place/where/you/put/elasticsearch/config/elasticsearch.yml
```

- Copy the following text and paste it above the comments in the config file

```
# don't allow queries via HTTP (great for PROD)
http.enabled: false
```

- Restart ElasticSearch (if it's running)

  - kill the process in the Terminal: `ctrl + c`
  - start it back up the same way as before: `./bin/elasticsearch`

- Test to see if the config applied properly

```
http://localhost:9200/?pretty
```

- Yup, no response. HTTP is disabled

### Data And Logs

It'd be great if ElasticSearch's data could live in the same place it used to.

- Open the ElasticSearch config file again
- Copy the following settings, replacing any existing entries in the file
  - notice that we're turning HTTP back on
  - `${HOME}` references the `$HOME` environment variable

```
# this is where ElasticSearch will put it's data
path.data: ${HOME}/.pss/elasticsearch/data

# this is where ElasticSearch puts it's logs
path.logs: ${HOME}/.pss/logs/elasticsearch

# don't allow queries via HTTP (great for PROD)
http.enabled: true
```

- Restart ElasticSearch (if it's running)

  - kill the process in the Terminal: `ctrl + c`
  - start it back up the same way as before: `./bin/elasticsearch`

- Test to see if the config applied properly

```
http://localhost:9200/?pretty
```

- Same response as the first test? Awesome!

```
{
    "name": "1fNQ8X2",
    "cluster_name": "elasticsearch",
    "cluster_uuid": "tFz-m1IZQC6pnjdcTd7q2w",
    "version": {
        "number": "6.5.0",
        "build_flavor": "default",
        "build_type": "tar",
        "build_hash": "816e6f6",
        "build_date": "2018-11-09T18:58:36.352602Z",
        "build_snapshot": false,
        "lucene_version": "7.5.0",
        "minimum_wire_compatibility_version": "5.6.0",
        "minimum_index_compatibility_version": "5.0.0"
    },
    "tagline": "You Know, for Search"
}
```

- Look at the node itself to see if the directory changes have applied correctly

```
http://localhost:9200/_nodes
```

- This is quite a large response, look out for the following JSON
  - these values are correct for my \$HOME environment variable

```
"path": {
  "data": [
      "/Users/leightondarkins/.pss/elasticsearch/data"
  ],
  "logs": "/Users/leightondarkins/.pss/logs/elasticsearch",
  "home": "/Users/leightondarkins/Code/elasticsearch/elasticsearch-6.5.0"
},
```

- You can also verify that the paths were created/populated by navigating to their configured location in Finder/Explorer

## Create The PSS Index

Running PSServer will automatically (re)create the PSS index on startup.

If you have HTTP enabled you can verify that it exists with the following request:

```
localhost:9200/_cat/indices?v
```

and response:

```
health status index uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   pss   s5mvF-ktTMSLXW69TxWFGg   1   0          0            0       230b           230b
```
