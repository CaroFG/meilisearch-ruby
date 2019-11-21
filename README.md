# Meilisearch Ruby Client

[![Gem Version](https://badge.fury.io/rb/meilisearch.svg)](https://badge.fury.io/rb/meilisearch)
[![Licence](https://img.shields.io/badge/licence-MIT-blue.svg)](https://img.shields.io/badge/licence-MIT-blue.svg)

The ruby client for MeiliSearch API.

MeiliSearch provides an ultra relevant and instant full-text search. Our solution is open-source and you can check out [our repository here](https://github.com/meilisearch/MeiliDB).</br>
You can also use MeiliSearch as a service by registering on [meilisearch.com](https://www.meilisearch.com/) and use our hosted solution.


## 🔧 Installation

With `gem` in command line:
```bash
$> gem install meilisearch
```

In your `Gemfile` with [bundler](https://bundler.io/):
```ruby
source 'https://rubygems.org'

gem 'meilisearch'
```

## 🚀 Getting started

Here is a quickstart to create an index and add documents.

```ruby
require 'meilisearch'

index_uid = 'yourIndexUid'
documents = [
  { id: 123,  title: 'Pride and Prejudice' },
  { id: 456,  title: 'Le Petit Prince' },
  { id: 1,    title: 'Alice In Wonderland' },
  { id: 1344, title: 'The Hobbit' },
  { id: 4,    title: 'Harry Potter and the Half-Blood Prince' },
  { id: 42,   title: 'The Hitchhiker\'s Guide to the Galaxy' }
]

client = MeiliSearch::Client.new('yourUrl', 'yourApiKey')
client.create_index(index_uid)
client.add_documents(index_uid, documents)
```

## 🎬 Examples

You can check out [the API documentation](https://docs.meilisearch.com/references/).

### Search

#### Basic search

```ruby
response = client.search(index_uid, 'prince')
puts response
```

```json
{
    "hits": [
        {
            "id": 456,
            "title": "Le Petit Prince",
            "_formatted": {
                "id": 456,
                "title": "Le Petit Prince"
            }
        },
        {
            "id": 4,
            "title": "Harry Potter and the Half-Blood Prince",
            "_formatted": {
                "id": 4,
                "title": "Harry Potter and the Half-Blood Prince"
            }
        }
    ],
    "offset": 0,
    "limit": 20,
    "processingTimeMs": 13,
    "query": "prince"
}
```

#### Custom search

All the supported options are described in [this documentation section](https://docs.meilisearch.com/references/search.html#search-in-an-index).

```ruby
response = client.search(index_uid, 'prince', { limit: 1 })
puts response
```

```json
{
    "hits": [
        {
            "id": 456,
            "title": "Le Petit Prince",
            "_formatted": {
                "id": 456,
                "title": "Le Petit Prince"
            }
        }
    ],
    "offset": 0,
    "limit": 1,
    "processingTimeMs": 10,
    "query": "prince"
}
```
