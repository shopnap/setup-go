# Go module cache with GitHub Action.

Composite GitHub Action which combines the perfect pairing of `actions/setup-go` with `actions/cache` for the caching of both the Golang module and build caches.

Reducing all these workflow steps:

```yml
steps:
  - name: Setup Golang
    uses: actions/setup-go@v2
    with:
      go-version: 1.17
  - name: Setup Golang caches
    uses: actions/cache@v2
    with:
      path: |
        ~/.cache/go-build
        ~/go/pkg/mod
      key: ${{ runner.os }}-golang-${{ hashFiles('**/go.sum') }}
      restore-keys: |
        ${{ runner.os }}-golang-
```

to:

```yml
steps:
  - name: Setup Golang with cache
    uses: shopnap/setup-go@main
    with:
      go-version: 1.17
```

## Credit:

The core idea was taken from `magnetikonline/action-golang-cache@v1`. This repo is a fork of that repo for our use case.
