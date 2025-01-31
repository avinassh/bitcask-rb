# bitcask-rb: A Log-Structured Hash Table for Fast Key/Value Data

[![Ruby](https://img.shields.io/badge/ruby-3.1.1-brightgreen)](https://www.ruby-lang.org/en/)
[![BDD](https://img.shields.io/badge/rspec-3.1-green)](https://rspec.info/)
[![Ruby Style Guide](https://img.shields.io/badge/code%20style-rubocop-red)](https://github.com/rubocop/rubocop)
[![CircleCI](https://dl.circleci.com/status-badge/img/gh/dineshgowda24/bitcask-rb/tree/main.svg?style=shield)](https://dl.circleci.com/status-badge/redirect/gh/dineshgowda24/bitcask-rb/tree/main)
[![codecov](https://codecov.io/gh/dineshgowda24/bitcask-rb/branch/main/graph/badge.svg?token=HY8IQSEKCA)](https://codecov.io/gh/dineshgowda24/bitcask-rb)
[![DeepSource](https://deepsource.io/gh/dineshgowda24/bitcask-rb.svg/?label=active+issues&token=aISrLFG-Rwka_9MMiZixX_NT)](https://deepsource.io/gh/dineshgowda24/bitcask-rb/?ref=repository-badge)

<img src="image.png"/>

Fast, Persistent key/value store based on [bitcask paper](https://riak.com/assets/bitcask-intro.pdf) written in Ruby.
An attempt to understand and build our persistent key/value store capable of storing data enormous than the RAM. This, in any way, is not intended for production. For simplicity, implementation has ignored a few specifications from the paper.

## Prerequisites

- Ruby
- bundler

## Setup

```shell
bundle install
```

## Usage

```ruby
db_store = Bitcask::DiskStore.new('bitcask.db')

# Setting values in store using put or hash style
db_store.put("Anime", "One Piece")
db_store["Luffy"] = "Straw Hat"
db_store[2020] = "Leap Year"
db_store.put("pie", 3.1415)

# Getting values from store using get or hash style
db_store["Anime"]
db_store.get("Luffy")
db_store["pie"]
db_store.get(2020)

# Listing keys
db_store.keys

# Size of the store
db_store.store
```

## Tests

```shell
bundle exec rspec
```

## Advantages

- Simple yet powerful
- Easy to use
- Store data enormous than RAM
- Data file is OS agnostic
- Portable
- Faster read/writes
- Minimal dependecies

## Features

| Feature                               | Support            |
|---------------------------------------|--------------------|
| Persisted in disk                     | :white_check_mark: |
| Get API                               | :white_check_mark: |
| Put API                               | :white_check_mark: |
| Int, Float and String for k/v         | :white_check_mark: |
| CRC                                   | :white_check_mark: |
| Directory Support                     | :x:                |
| Delete API                            | :x:                |
| Files Merge and LSM Trees             | :x:                |

## Benchmarks

### CPU Cycles

```ruby
Benchmarked with value_size of 78 bytes
                                                         user     system      total        real
DiskStore.put : 10k records                          0.026963   0.018983   0.045946 (  0.046078)
DiskStore.get : 10k records                          0.031211   0.009727   0.040938 (  0.041154)
DiskStore.put : 100k records                         0.367399   0.196536   0.563935 (  0.566659)
DiskStore.get : 100k records                         0.313556   0.102338   0.415894 (  0.416280)
DiskStore.put : 1M records                           4.649307   2.209731   6.859038 (  6.887667)
DiskStore.get : 1M records                           3.357120   1.047637   4.404757 (  4.409732)
avg_put:                                             0.000005   0.000002   0.000007 (  0.000007)
avg_get:                                             0.000003   0.000001   0.000004 (  0.000004)
```

### Iterations Per Second

```ruby
Warming up --------------------------------------
DiskStore.put : 100 records with data size: 702 Bytes
                       149.000  i/100ms
DiskStore.get : 100 records, value size: 702 Bytes
                         2.389k i/100ms
DiskStore.put : 100 records, value size: 6 Kb
                        22.000  i/100ms
DiskStore.get : 100 records, value size: 6 Kb
                         2.098k i/100ms
DiskStore.put : 100 records, value size: 660 Kb
                         1.000  i/100ms
DiskStore.get : 100 records, value size: 660 Kb
                       148.000  i/100ms
Calculating -------------------------------------
DiskStore.put : 100 records with data size: 702 Bytes
                          1.552k (±15.7%) i/s -      7.450k in   5.008519s
DiskStore.get : 100 records, value size: 702 Bytes
                         24.100k (± 3.7%) i/s -    121.839k in   5.062195s
DiskStore.put : 100 records, value size: 6 Kb
                        655.280  (±53.4%) i/s -      1.716k in   5.272456s
DiskStore.get : 100 records, value size: 6 Kb
                         19.883k (± 7.1%) i/s -    100.704k in   5.090910s
DiskStore.put : 100 records, value size: 660 Kb
                          4.479  (± 0.0%) i/s -     23.000  in   5.166651s
DiskStore.get : 100 records, value size: 660 Kb
                          3.286k (±39.4%) i/s -      8.140k in   5.272424s
```

## Contributing

If you wish to contribute in any way, please fork the repo and raise a PR.

[![CircleCI](https://dl.circleci.com/insights-snapshot/gh/dineshgowda24/bitcask-rb/main/workflow/badge.svg?window=30d)](https://app.circleci.com/insights/github/dineshgowda24/bitcask-rb/workflows/workflow/overview?branch=main&reporting-window=last-30-days&insights-snapshot=true)