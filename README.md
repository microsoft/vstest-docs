# vstest-docs
Documentation for vstest runner &amp; engine
Developer guide to integrate with vstest runner

# Contributing
We use [docfx](https://github.com/dotnet/docfx/releases) for building this
documentation. A short primer on editing this repo is below.

First, [download](https://github.com/dotnet/docfx/releases) latest release of
docfx and extract it locally. We will use `d:\tmp\docfx` as destination for
these steps.

Open a command prompt, `git clone` this repo. You may use following commands to
build and run a local server.

```
> cd d:\src\vstest-docs
> d:\tmp\docfx\docfx.exe build
> d:\tmp\docfx\docfx.exe serve
```

Open [http://localhost:8080/_site][] in a browser to see the rendering of the
documentation.
