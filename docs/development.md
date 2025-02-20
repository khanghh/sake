# Development

## Build instructions

### Prerequisites

- [go 1.18 or above](https://golang.org/doc/install)
- [goreleaser](https://goreleaser.com/install/) (optional)
- [golangci-lint](https://github.com/golangci/golangci-lint) (optional)

### Building

```bash
# Build sake for your platform target
make build

# Build sake binaries and archives for all platforms using goreleaser
make build-all

# Generate Manpage
make gen-man
```

## Developing

```bash
# Format code
make gofmt

# Manage dependencies (download/remove unused)
make tidy

# Lint code
make lint

# Standing in examples directory you can run the following to debug faster
go run ../main.go run ping -a
```

## Releasing

The following workflow is used for releasing a new `sake` version:

1. Create pull request with changes
2. Generate manpage `make gen-man`
3. Pass all tests
4. Run `make build-all` to verify windows build
5. Update `Makefile` and `CHANGELOG.md` with correct version, and add all changes to `CHANGELOG.md`
6. Squash-merge to main with `Release vx.y.z` and description of changes
7. Run `make release`, which will:
  1. Create a git tag with release notes
  2. Trigger a build in Github that builds cross-platform binaries and generates release notes of changes between current and previous tag

## Dependency Graph

Create SVG dependency graphs using graphviz and [goda](https://github.com/loov/goda).

```bash
goda graph "github.com/alajmo/sake/..." | dot -Tsvg -o res/graph.svg
goda graph "github.com/alajmo/sake:all" | dot -Tsvg -o res/graph-full.svg
```
