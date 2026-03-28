# keisetsu Developer Guide

This document provides technical information, operational rules, repository structure, standard workflow, distribution model, and documentation notes for keisetsu developers and contributors.

## Repository Relationships

```text
[keisetsu-publisher]
  Generates kdb + deck manifest
            |
            v
[keisetsu-database]
  Publishes schema + catalog + kdb + deck manifest
            |
            v
[keisetsu-mobile]
  Fetch catalog -> fetch kdb -> study/test

[keisetsu-docs]
  Cross-manages concepts, operations, and procedures
```

## Repositories

- [keisetsu-publisher](https://github.com/kumo01GitHub/keisetsu-publisher)
    - Deck editor UI based on Next.js
    - Create new decks, import CSV or kdb, and re-export kdb
    - Download ZIP containing deck manifest (JSON) and .kdb

- [keisetsu-database](https://github.com/kumo01GitHub/keisetsu-database)
    - Stores distributable `databases/*.kdb`
    - Schema contracts `schema/*.sql`
    - Distribution index `catalog/catalog.json`
    - Scripts for catalog update, format validation, and consistency checks

- [keisetsu-mobile](https://github.com/kumo01GitHub/keisetsu-mobile)
    - Learning app using Expo + React Native
    - Fetches deck list from GitHub catalog
    - Downloads kdb / imports local kdb files
    - Study mode / test mode
    - Saves test history, allows deck switching/deletion

## Standard Workflow

1. Create or edit cards in `keisetsu-publisher` and generate a ZIP containing the deck manifest (JSON) and .kdb
2. Place the downloaded ZIP file anywhere, then in the `keisetsu-database` directory, run `npm run unpack -- <ZIP file path>` to automatically extract `.kdb` to `databases/` and the manifest (`{deck-id}.json`) to `catalog/decks/`
3. In `keisetsu-database`, run `npm run build` to regenerate `catalog/catalog.json`
4. In `keisetsu-database`, run `npm run validate:kdb` and `npm run validate:catalog` to validate format and consistency
5. In `keisetsu-database`, push or create a tag to distribute
6. In `keisetsu-mobile`, verify deck acquisition and learning via the catalog

## Distribution Model

- Public URLs use GitHub Raw format
- Deck list starts from `catalog/catalog.json` and references each deck manifest
- Clients follow from catalog to deck manifest, then from deck manifest to `.kdb`
- Actual data is in `databases/*.kdb`

```text
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/catalog.json
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/decks/{deck-id}.json

deck manifest path is used to fetch .kdb
Example: https://raw.githubusercontent.com/{owner}/{repo}/{ref}/databases/starter-basic.kdb
```

## Documentation Notes

- Until the first release, expect repeated breaking changes due to design revisions
- Before the first release, specifications, data formats, and UI are not stable and compatibility is not guaranteed
- When the schema changes, update the README for mobile/publisher/database simultaneously
- After the first release, clearly state distribution tags and update history for changes affecting compatibility
- **Note: Distribution via Expo Go is not officially recommended.** Expo Go is intended for learning and testing purposes; for production, use a development build as recommended in the [official FAQ](https://docs.expo.dev/faq/#what-can-i-do-or-cannot-do-with-expo-go).
