# This is a temporary fork of @slonik/migrator.

- This is a patch that works for now until @slonik/migrator is compatible with slonik v33.
- Focuses only on migration by .sql files.

# slonik-tools

[![Node CI](https://github.com/mmkal/slonik-tools/workflows/CI/badge.svg)](https://github.com/mmkal/slonik-tools/actions?query=workflow%3ACI)
[![codecov](https://codecov.io/gh/mmkal/slonik-tools/branch/master/graph/badge.svg)](https://codecov.io/gh/mmkal/slonik-tools)

Various utilities for [slonik](https://npmjs.com/package/slonik)

## Packages

<!-- codegen:start {preset: monorepoTOC, sort: package.name} -->
- [@slonik/migrator](https://github.com/mmkal/slonik-tools/tree/master/packages/migrator#readme) - A cli migration tool for postgres, using [slonik](https://npmjs.com/package/slonik).
- [@slonik/typegen](https://github.com/mmkal/slonik-tools/tree/master/packages/typegen#readme) - A library that uses [slonik](https://npmjs.com/package/slonik) to generate typescript interfaces based on your sql queries.
- [slonik-tools-demo](https://github.com/mmkal/slonik-tools/tree/master/packages/demo#readme) - A demo project which uses [@slonik/typegen](https://npmjs.com/package/@slonik/typegen) and [@slonik/migrator](https://npmjs.com/package/@slonik/migrator), intended to show a working example for each package.
<!-- codegen:end -->

## Development

Requirements:

* node + yarn
* docker + docker-compose

[lerna](https://npmjs.com/packages/lerna) is used to manage the packages.

To get started:

```bash
yarn
yarn dependencies
```

This starts a local postgres database that the tests will connect to (depends on `docker-compose`). After running that in its own window: 

```bash
yarn ci
```

will build, migrate and test all packages.

While developing, it can be useful to run `yarn build -w` to compile continuously in the background and `yarn test` to just run tests. The tests use jest, so all the usual jest features can be used. For example, `yarn test packages/migrator` will run the tests only for the migrator package. `yarn test $(npx lerna changed --parseable)` runs tests for all changed packages.

### Publishing

Run [this workflow](https://github.com/mmkal/slonik-tools/actions/workflows/publish.yml). To make sure the correct packages are actually published, it requires a hash of the publish command's dry-run output. You can get this by running the workflow with no parameters, and copying the expected value from the failure logs, or run `yarn changes:hash` locally.
