# Easy SparQL

At this document, you can learn about SparQL in easiest mode of study! 

Join and contribute if you want have incredible examples of yours and complete
this document repo.

## SparQL

SparQL is one of the most important query language that introduced by wikidata
at wikimedia. That is one of wiki media products inside of wikimedia and
wikipedia.

At first i would say, you can learn a lot of things by
[reading](https://www.wikidata.org/wiki/Wikidata:SPARQL_tutorial) the Wikidata
documentation about it query language.

Before any technical info, I should mention that, SparQL created for crawling
and getting a lot of data from Wikidata (server) as datasets for data
scientist, AI research and another staff.

- Wikidata: is a knowledge base database. It contains millions of data.
  Anythings that want. Even Wikipedia use this data. This data is freedom!
- SparQL: for simple manner, SparQL is a query language to getting data from
  Wikidata server! It is looks like SQL|GraphQL, made for crawling huge amount 
  of data
- WDQS: the Wikidata Query Service. We learn SparQL to crawling WDQS dataset


## SparQL Variables

We define our variable with `?varName`.

Before we define our variables we should select data for this variables.

```sparql
select ?varName
```

## Define some conditions

Like SQL or GraphQL you can write your conditions to getting and crawling even
ordering your dataset.

```sparql
select ?x
where {
    x y is over on ?x
}
```

## Where we can run our example

[OpenMe](https://query.wikidata.org/)

### EXAMPLE

```sparql
select ?student
where {
    ?student eyeColor blue.
    ?student educatedAt shamsipour.
}
```

Level of conditions is at first your var, next is property about that student
next is value.

_Note:_ that you can't define your value of properties and entities look like,
mamad or jeff or blue or green!


For first our real word example, You need one use-case and open
[Wikidata](https://wikidata.org/) web site to find your use-case.

Search in Wikidata is special:

- You can search use-case name, like mamad, or anythings at default term:
  <search term>
- You can search use-case property by this term: P:<search term>

Meaning of `P` in first of <search term> is, I want all properties of my search
term!

For example to having name of Steve Jobs children we can use this name for
searching, use `child` as properties, and put it at SparQL syntax like following
example:

```sparql
select ?child
where {
    ?child wdt:P40 wd:Q19837
}
```

- **wdt**: is property and started by P => Properties
- **wd**: is main query id and started by Q => Query

It's look like json format, instead of key we use wdt and instead of value we
use wd. `wdt: wd`

That will return list of Steve Jobs children. But without name! use **label** at
the end of your variable name to have label to be human readable. And use
wikibase label service.

```sparql
select ?child ?childLabel
where {
    ?child wdt:P40 wd:Q19837

    # Add this service to have label at variable
    SERVICE wikibase:label { 
        bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". 
    }
}
```

## Search in Stanford university

```sparql
select ?person ?personLabel ?personImage ?birthPlaceLabel ?birthDate
where {
  ?person wdt:P69 wd:Q41506.
  # Filter students by female sex property
  # ?person wdt:P21 wd:Q6581072.
  ?person wdt:P18 ?personImage.
  ?person wdt:P19 ?birthPlaceLabel .
  ?person wdt:P569 ?birthDate .
  
  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". 
  }
}
```