# 0020 Adapter Discovery Cost Improvement For Assemblies

## Summary
This note outlines the proposed changes for improving adapter discovery cost for assemblies by:
1. Passing test sources to adapter based on assmebly type (in addition to existing way of passing test sources based on file extensions).

## Motivation
Every adapter specifies file extensions supported by it. Test sources are passed to adapters based on their file extensions.

In case when extension is an assembly (.dll or .exe), we require additional filter based on which we can pass test source to an adapter. The reason is, an assembly can be either `native` or `managed`. Its possible that an adapter supports only native or only manaeged or both types of assemblies.

Currently even though an adapter supports one type of assembly, there is no way for it to specify the same and thus we end up giving all type of assemblies to that adapter, which causes overhead in test discovery time.

Proposed changes are to allow adapters to specify which assmebly type is supported, and thus in result:
1. Native assemblies will not be passed to adapters which don't support native assemblies.
2. Managed assemblies will not be passed to adapters which don't support managed assemblies.

## Proposed Changes
1. FileExtensionAttribute will be reused for passing native and managed support. Adapter can specify native assemblies suppotr by adding `[FileExtension("_native_")]` in their discoverer. Similaryl for manages `[FileExtension("_managed_")]` can be specified.
2. In addition to FileExtensionAttribute, adapter can also specify native and managed support using new attribute `AssemblyType` i.e. `[AssemblyType("native")]` and `[AssemblyType("managed")]`. Using this attribute is a compat break as older ObjectModel will not have this attribute.
3. AssemblyType attribute will be prefered over FileExtensionAttribute in case both are specified by adaptet for native and managed support.
4. `System.Reflection.PortableExecutable.PEReader` API will be used to find whether an test source assembly is native or managed.
5. Test source assemblies will be passed based on both file extensions and assembly type (i.e. whether its native or managed).
6. Adapter can specify both native and managed support by adding both `[FileExtension("_native_")]` and `[FileExtension("_managed_")]`.
7. `[FileExtension("_native_")]` and `[FileExtension("_managed_")]` will be ignored if adapter doesn't support assemblies i.e. none of `[FileExtension(".dll")]` or `[FileExtension(".exe")]` is present in adapter discoverer.
