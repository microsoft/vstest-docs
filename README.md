### Visual Studio Test Platform Documentation
You've found the GitHub repository which contains the content for the Visual Studio Test Platform documentation.
If you are looking for the Visual Studio Test Platform product GitHub repository, you can find it [here](https://github.com/Microsoft/vstest).

### Documentation
- [Test Platform Architecture](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0001-Test-Platform-Architecture.md)
- [Test Discovery Protocol](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0002-Test-Discovery-Protocol.md)
- [Test Execution Protocol](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0003-Test-Execution-Protocol.md)
- [Adapter Extensibility](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0004-Adapter-Extensibility.md)
- [Test Platform SDK](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0005-Test-Platform-SDK.md)
- [Editors API Specification](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0007-Editors-API-Specification.md)
- [Roadmap](https://github.com/Microsoft/vstest-docs/blob/master/roadmap.md)

### Contributing
There are many ways to contribute to VSTest
- [Submit issues](https://github.com/Microsoft/vstest-docs/issues) and help verify fixes as they are checked in.
- Review the [documentation changes](https://github.com/Microsoft/vstest-docs/pulls).
- Contribute new topics/information, or make changes to existing documentation.

### Editing docs
We use [docfx](https://github.com/dotnet/docfx/releases) for building this documentation. A short primer on editing this repo is below.
First, [download](https://github.com/dotnet/docfx/releases) latest release of docfx and extract it locally. We will use d:\tmp\docfx as destination for these steps.
 
Open a command prompt, git clone this repo. Use the following commands to build and run a local server.
```
  > cd d:\src\vstest-docs
  > d:\tmp\docfx\docfx.exe build
  > d:\tmp\docfx\docfx.exe serve
```

Open http://localhost:8080/_site in a browser to see the rendering of the documentation.
