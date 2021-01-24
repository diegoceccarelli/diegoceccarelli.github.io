+++
title = "SSSS"
+++

## Semantic Search Shortcuts Dataset 

This dataset has been used to perform the experiments for the paper [When Entities Meet Query Recommender Systems: Semantic Search Shortcuts](https://www.researchgate.net/publication/241687007_When_entities_meet_query_recommender_systems_semantic_search_shortcuts).

We build a dataset consisting in 130 queries extracted 
from the [http://www.europeana.eu](Europeana)
query logs, containing a sample of users' interactions covering two 
years (from August 27, 2010 to January, 17, 2012).

We split the dataset in three disjoint sets: 
  * The 50 queries in the first set are short (composed by only **one** term);
  * The second set contains 50 queries having an average length of 4.2 terms;
  * The 30 queries in the third set have an average length of 9.93 terms. 

For each query in the three sets, we compute the top-10 recommendations 
produced by the SS query recommender system (see the [paper](https://www.researchgate.net/publication/241687007_When_entities_meet_query_recommender_systems_semantic_search_shortcuts)) for more details 
on the recommender) and we map them to entities by using a simple 
interface providing an user-friendly way to associate entities to queries. 
Three annotators participated to the manual annotation. 
They manually annotated queries and their related recommendations 
with one or more Wikipedia entities. An entity is represented by 
its title and its numerical id, available in a recent English Wikipedia dump, e.g.

```
  wikiName:Krater
  id:1502187
```
represents the entity described here [http://en.wikipedia.org/wiki/Krater](http://en.wikipedia.org/wiki/Krater). 

Queries are available [here](/sac/queries.txt): the 
file contains the flat list of the queries in the format:

```
	<id> <tab> <query> 
```

of course, queries with `id in [1,50]` belong to the first set, queries with `id  \in
[51, 100]` belong to the second set while the others belong to the third set.

The annotated recommendations for the each query are 
available [here](/sac/dataset.json).
Each line of this file represents the annotated recommendations for a query encoded 
using *json*. 

Each record contains a field `query`, which has a field `query` containing 
the raw query extracted from the logs and a field entities contains the 
list of entities associated by the annotators (each entity is represented by 
its `wikiname` and its `wiki-id`). The other field in the record is called 
`suggestions` and is made by a list of recommended queries, each one modelled
as a map containing a field `query` with the raw query recommended, and 
a field `entities` with the entities associated by the annotators.

### Example
```json

{
  "query": {
    "query": "amphore",
    "entities": [
      {
        "wikiName": "Amphora",
        "id": 51812
      }
    ],
    "suggestions": [
      {
        "query": "amphore   hermes",
        "entities": [
          {
            "wikiName": "Amphora",
            "id": 51812
          },
          {
            "wikiName": "Hermes",
            "id": 14410
          }
        ]
      },
      {
        "query": "amphore antigone",
        "entities": [
          {
            "wikiName": "Amphora",
            "id": 51812
          },
          {
            "wikiName": "Antigone",
            "id": 67196
          }
        ]
      }
    ]
  }
}

```
contains two recommendations for the query `amphore` (associated to the
entity [Amphora](http://en.wikipedia.org/wiki/Amphora). One is the query 
`amphore hermes` (associated to the entities [Amphora](http://en.wikipedia.org/wiki/Amphora)
and [Hermes](http://en.wikipedia.org/wiki/Hermes). The other is the 
query `amphore antigone` ( associated to the entities [Amphora](http://en.wikipedia.org/wiki/Amphora) and [Antigone](http://en.wikipedia.org/wiki/Antigone) ).


Please if you use it in your paper cite: 

```
@inproceedings{ceccarelli2013entities,
    title={When Entities Meet Query Recommender Systems: Semantic Search Shortcuts},
    author={Ceccarelli, D. and Gordea, S. and Lucchese, C. and Nardini, F.M. and Perego, R.},        
    booktitle={SAC '13: 28th Symposium On Applied Computing, Coimbra, Portugal, March 2013},
    year={2013}
}
```

Feel free to contact me via [email](mailto:diego.ceccarelli@gmail.com) for more details.

-------------------------------------

Licensed under the Apache License, Version 2.0 (the 'License');
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an 'AS IS' BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


