# Data Catalogs and Governance

The common data-catalog vocabulary -- the data assets a catalog holds, the glossary terms and domains that describe them, their owners and their lineage -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Data Governance, Data Catalog, Data Management, Metadata Management, Data Lineage, Data Quality, Data Observability in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| data_asset | 23 | 23 | id 70%, name 70% | tables 12, entity 7, assets 5, entities 4 |
| glossary_term | 7 | 7 | id 86%, name 86%, definition 71%, tags 71%, updated_at 57% | terms 4, glossaryterms 3, glossaries 2, glossary 2 |
| data_domain | 10 | 9 | name 100%, id 89%, description 67%, updated_at 67%, created_at 56% | domains 8, dataproducts 3, domain 1 |

Cohort: 94 providers with harvested OpenAPI, 27 crosswalks. Of the providers exposing a data_asset: 48% create, 74% list, 70% fetch, 44% update, 44% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Data assets -- tables, entities, datasets -- agree on id and name; created_at reaches 48% and asset_type 44%. A catalog's asset is a typed node whose type decides the rest of its shape.
- The business layer agrees better than the technical one: glossary terms agree on id, name, definition, tags and updated_at. Data domains agree on name, id, description, updated_at and created_at.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The fully qualified name, URN or GUID that each catalog uses as the asset key maps to id.
- Lineage was dropped; it is published as OpenLineage run events, a standard to take in its own pass.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
