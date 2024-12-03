
# TrustGraph UK Legislation demo dataset

## What's here

Some UK legislation data - some of the UK legislation passed by Parliament
in 2022, 2023 and 2024.  This has been taken from https://legislation.gov.uk
by automated means.  This does not include any legislation which was
recorded as scanned copies or PDF files.

This also includes a loader script which can load the data into TrustGraph
processing for knowledge extraction.

## Dataset

There are 3 years' of legislation here: 2022, 2023, 2024.  If you've seen
me do a demo, it was with the 2024 dataset only, you don't need to load
everything to get some interesting answers.  The example notebooks were
created with 2024 loaded.

This was taken from legislation.gov.uk, and released under the following
licence:

> All content is available under the Open Government Licence v3.0 except
> where otherwise stated.

Each year's dataset consists of an index file in JSON format.  Each entry in
the index describes a piece of legislation, including date, title, a
description if known.  There is also a filename to the text from the
legislation.  The text files in the dataset are mostly there, but the text
extraction from the legislation database doesn't handle all formatting
types.

## Setup to use the loader

You need a running trustgraph system e.g. run a 0.17 docker compose file,
and give the system at least a minute to settle in.  The configuration I
used for the demo is given below:

- [`TrustGraph + Pinecone + Cassandra`](docker-compose.yaml) - a Docker
  Compose YAML file I used to launch TrustGraph with adapters to connect
  to Pinecone and Google AI studio included.  To use this you need to
  set up a Pinecone account and also a Google AI studio.
  
  ```
  GOOGLE_AI_STUDIO_KEY=google-ai-studio=api-key-goes-here
  export PINECONE_API_KEY=api-key-goes-here
  ```

## To run the loader

This uses Python.  It relies on a Pulsar dependency which is known not
to work with Python 3.13, so we use 3.12:

```
python3.12 -m venv env

. env/bin/activate

pip3 install requests
pip3 install trustgraph-base
```

And then load the 2024 dataset:

```
./load 2024
```

## Notebooks to run queries

- [`GraphRAG queries`](simple-queries.ipynb) - a Jupyter notebook containing
  a few simple GraphRAG queries using the TrustGraph REST API.
  
- [`Agent queries`](agent-queries.ipynb) - a Jupyter notebook containing
  an agent query using the AgentClient API this exposes the thought /
  observation responses from the agent API because they are not available
  in the REST API yet.  This is a work in progress.
  
## Further information

- [TrustGraph repo](https://github.com/trustgraph-ai/trustgraph)
- [TrustGraph discord](https://discord.gg/sQMwkRz5GX)
- [TrustGraph docs](https://trustgraph.ai)

## Purpose

With the exception of the Legislation data licenced from UK gov...

The information provided in this repo is shared freely for educational
purposes for the intention that is to be useful. No claims are made as to
the accuracy of the information, or its suitability for any specific
purpose.