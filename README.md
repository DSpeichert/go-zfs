# Go Wrapper for ZFS

Simple wrappers for ZFS command line tools.

To use:
```
go get github.com/DSpeichert/go-zfs/v3
```

[![Go Reference](https://pkg.go.dev/badge/github.com/DSpeichert/go-zfs/v3.svg)](https://pkg.go.dev/github.com/DSpeichert/go-zfs/v3)

This is a hard fork of [mistifyio/go-zfs](https://github.com/mistifyio/go-zfs), which unfortunately has not seen a new release since 2015 despite merging some PRs.

One may prefer to use the more maintained [zrepl/zrepl/zfs](https://github.com/zrepl/zrepl/tree/master/zfs) package.

## Requirements

You need a working ZFS setup. [Ubuntu](https://ubuntu.com/tutorials/setup-zfs-storage-pool) is arguably the easiest to use with ZFS natively.

Generally you need root privileges to use anything zfs related.

## Changelog

* `go mod` support
* `v3` is an API-breaking change, hence it's a major release.
* Github Actions run tests on latest Ubuntu corresponding ZFS version bundled
* `context.Context` added everywhere to support timeouts, the context is passed to `exec.Exec`
* tests moved to same package name to avoid self-dependency

# Hacking

The tests have decent examples for most functions.

```go
//assuming a zpool named test
//error handling omitted


f, err := zfs.CreateFilesystem(context.TODO(), "test/snapshot-test", nil)
ok(t, err)

s, err := f.Snapshot(context.TODO(), "test", nil)
ok(t, err)

// snapshot is named "test/snapshot-test@test"

c, err := s.Clone(context.TODO(), "test/clone-test", nil)

err := c.Destroy(context.TODO())
err := s.Destroy(context.TODO())
err := f.Destroy(context.TODO())

```

# Contributing #

See the [contributing guidelines](./CONTRIBUTING.md)
