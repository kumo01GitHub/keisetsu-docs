# keisetsu Docs

**Available languages:**
- [English](./README.md) (default)
- [日本語](./README.ja.md)
- [Español](./README.es.md)
- [Português](./README.pt.md)
- [中文](./README.zh.md)
- [한국어](./README.ko.md)

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/kumo01GitHub/keisetsu-docs/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

This is the documentation hub for the overall design intent and operational policy of keisetsu.

`keisetsu-docs` is a central place to manage cross-repository specifications, operational rules, and update procedures for all keisetsu implementations (publisher / database / mobile).

- Clarifies the responsibilities of each repository
- Documents distribution and validation flows independently from implementation
- Maintains common decision criteria for specification changes

## Concept

keisetsu is an open-source flashcard app that makes learning data storage and distribution routes public, allowing users to own and use their own learning materials.

- Goal
  - Create an environment where anyone can learn with just a smartphone
- Motivation
  - Solve existing issues such as data being private, online dependency, and unclear update routes
- Advantages
  - All specifications, data, and distribution flows are public and transparent
  - OSS: anyone can update and use the data for free
- Approach
  - Separate creation (publisher), distribution (database), and usage (mobile) for easy updates and reuse
  - Use a public schema for data structure, a public catalog for distribution routes, and an offline-capable app for learning

## User Guide

### How to use the keisetsu mobile app

1. Install the Expo Go app on your smartphone.
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. Scan the QR code to launch the keisetsu app.

![Expo QR](assets/eas-update.svg)

You can start using the keisetsu app immediately.

### How to use the keisetsu web deck editor

1. Access the [keisetsu-publisher public page](https://keisetsu-publisher.vercel.app)
2. Create a new deck, or import CSV / existing kdb
3. Edit cards and deck info (ID, title, language, etc.)
4. Download the ZIP file
5. Extract the downloaded ZIP and place the generated files in keisetsu-database, then [submit an addition/edit request](https://github.com/kumo01GitHub/keisetsu-database/issues)

### Supported Languages

- English (`en`)
- Japanese (`ja`)

## Developer Guide

For detailed repository structure, operational rules, and technical information, see [DEVELOPER.md](./DEVELOPER.md.en).
