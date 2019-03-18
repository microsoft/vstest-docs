# 0026 DataCollector Extensibility - Passing TestPlatform properties to DataCollector extensions 

## Summary
Passing TestPlatform properties as part of property bag to datacollectors. These properties can be used by the datacollectors for processing before test run start.

## Motivation
Data collector might need test platform properties while initialization. Example: Static code coverage data collector needs to instrument the test sources before test run start thus need list of test sources during initialization.

## Design
In `SessionStartEventArgs` will contain `Properties` which are passed to the data collector in `SessionStart` event.<br/>
Currently test platform passes following properties to the datacollector extensions :
    1. "TestSources" : IEnumerable <br/>
        TestSources is an enumerable of all test sources that is used by the test run.

The public APIs exposed in `SessionStartEventArgs` would be as given below.
```csharp
 /// <summary>
/// Returns all TestPlatform Properties currently specified passed to the datacollector extenstion
/// </summary>
public IEnumerator<KeyValuePair<string, object>> GetProperties()

/// <summary>
/// Returns the property value corresponding to the given property name.
/// </summary>
/// <param name="property"> Name of the property </param>
public T GetPropertyValue<T>(string property)

/// <summary>
/// Sets the property value corresponding to the given property name.
/// </summary>
/// <param name="property">Name of the property</param>
/// <param name="value">Value of the property</param>
public void SetPropertyValue(string property, object value)
```

## Usage
In the datacollector, the user can get test sources as given below.
```csharp
sources = args.GetPropertyValue<IEnumerable>("TestSources");
```
