# Go Vanity URLs

Go Vanity URLs is a simple Go server that allows you
to set custom import paths for your Go packages.

## Quickstart

Install and run the binary:

```
$ go install github.com/martyanov/govanityurls@latest
$ # update vanity.yaml
$ govanityurls
$ # open http://localhost:8080
```

## Configuration File

```
host: example.com
cache_max_age: 3600
paths:
  /foo:
    repo: https://github.com/example/foo
    display: "https://github.com/example/foo https://github.com/example/foo/tree/master{/dir} https://github.com/example/foo/blob/master{/dir}/{file}#L{line}"
    vcs: git
```

<table>
  <thead>
    <tr>
      <th scope="col">Key</th>
      <th scope="col">Required</th>
      <th scope="col">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row"><code>cache_max_age</code></th>
      <td>optional</td>
      <td>The amount of time to cache package pages in seconds.  Controls the <code>max-age</code> directive sent in the <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control"><code>Cache-Control</code></a> HTTP header.</td>
    </tr>
    <tr>
      <th scope="row"><code>host</code></th>
      <td>optional</td>
      <td>Host name to use in meta tags.   You can use this option to fix the host when using this service behind a reverse proxy.</td>
    </tr>
    <tr>
      <th scope="row"><code>paths</code></th>
      <td>required</td>
      <td>Map of paths to path configurations.  Each key is a path that will point to the root of a repository hosted elsewhere.  The fields are documented in the Path Configuration section below.</td>
    </tr>
  </tbody>
</table>

### Path Configuration

<table>
  <thead>
    <tr>
      <th scope="col">Key</th>
      <th scope="col">Required</th>
      <th scope="col">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row"><code>display</code></th>
      <td>optional</td>
      <td>The last three fields of the <a href="https://github.com/golang/gddo/wiki/Source-Code-Links"><code>go-source</code> meta tag</a>.  If omitted, it is inferred from the code hosting service if possible.</td>
    </tr>
    <tr>
      <th scope="row"><code>repo</code></th>
      <td>required</td>
      <td>Root URL of the repository as it would appear in <a href="https://golang.org/cmd/go/#hdr-Remote_import_paths"><code>go-import</code> meta tag</a>.</td>
    </tr>
    <tr>
      <th scope="row"><code>vcs</code></th>
      <td>required if ambiguous</td>
      <td>If the version control system cannot be inferred, then this specifies the version control system as it would appear in <a href="https://golang.org/cmd/go/#hdr-Remote_import_paths"><code>go-import</code> meta tag</a>.  This can be one of <code>git</code>, <code>hg</code>, <code>svn</code>, or <code>bzr</code>.</td>
    </tr>
  </tbody>
</table>
