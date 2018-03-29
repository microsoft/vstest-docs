# 0020 Improving Logic To Pass Sources To Adapters

## Summary
This note outlines the proposed changes for improving logic to pass test sources to adapter by adding assembly type filter (in addition to existing file extensions based filter).

## Motivation
Every adapter specifies file extensions supported by it. Test sources are passed to adapters based on their supported file extensions.

In case when extension is an assembly (.dll or .exe), we require additional filter based on which we can pass test source to an adapter. The reason is, an assembly can be either `native` or `managed`. Its possible that an adapter supports only native or only managed or both types of assemblies.

Currently even though an adapter supports one type of assembly, there is no way for it to specify the same and thus we end up giving all type of assemblies to that adapter, which causes overhead in test discovery time.

Proposed changes are to allow adapters to specify which assembly type is supported, and thus in result:
1. Native assemblies will not be passed to adapters which don't support native assemblies.
2. Managed assemblies will not be passed to adapters which don't support managed assemblies.

## Proposed Changes
1. System.ComponentModel.CategoryAttribute will be used for passing native and managed support. Adapter can specify native assemblies support by adding `[Category("native")]` in their discoverer. Similarly for managed support, `[Category("managed")]` can be specified.
2. In addition to CategoryAttribute, adapter can also specify native and managed support using new attribute `AssemblyType` i.e. `[AssemblyType("native")]` and `[AssemblyType("managed")]`. Using this attribute is a compat break as older ObjectModel will not have this attribute.
3. Adapter can specify both native and managed support by adding both `[Category("native")]` and `[Category("managed")]`.
4. `[Category("native")]` and `[Category("managed")]` will be ignored if adapter doesn't support assemblies i.e. none of `[FileExtension(".dll")]` or `[FileExtension(".exe")]` is present in adapter discoverer.
5. `[Category("managed")]` is the default value in case adapter supports assemblies but none of `[Category("native")]` and `[Category("managed")]` are present.
6. `System.Reflection.PortableExecutable.PEReader` API will be used to find whether an test source assembly is native or managed.
7. Test source assemblies will be passed based on both file extensions and assembly type (i.e. whether its native or managed).

## Adapter side changes
1. Adapter can use either of `CategoryAttribute` and `AssemblyTypeAttribute` to specify native or managed assemblies support.
2. If adapter supports only managed assemblies, specifying `[Category("managed")]` or `[AssemblyType("managed")]` is not required.
3. If adapter supports only native assemblies, then either `[Category("native")]` or `[AssemblyType("native")]` can be specified.
4. If adapter supports both native and managed assemblies, then both
`[Category("native")]` or `[AssemblyType("native")]` and
`[Category("managed")]` or `[AssemblyType("managed")]`
 needs to be specified.
5. If AssemblyTypeAttribute is used, then adapter will not work if used with older VS versions.

**Example 1**: If adapter supports native .dll, .js, .appx, then adapter discover can either do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".js")]
    [FileExtension(".appx")]
    [Category("native")]
```

or do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".js")]
    [FileExtension(".appx")]
    [AssemblyType("native")]
```

**Example 2**: If adapter supports managed .dll, managed .exe, .js, .xap, then adapter discover can either do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".exe")]
    [FileExtension(".js")]
    [FileExtension(".xap")]
    [Category("managed")]
```

or do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".exe")]
    [FileExtension(".js")]
    [FileExtension(".xap")]
    [AssemblyType("managed")]
```


**Example 3**: If adapter supports managed .dll, .js, .xap, then adapter discover can either do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".js")]
    [FileExtension(".xap")]
```
    No need to specify CategoryAttribute or AssemblyType Attribute

or do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".js")]
    [FileExtension(".xap")]
    [Category("managed")]
```

or do:
```
    [DefaultExecutorUri(<ExecutorUriValue>)]
    [FileExtension(".dll")]
    [FileExtension(".js")]
    [FileExtension(".xap")]
    [AssemblyType("managed")]
```
