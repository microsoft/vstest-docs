# 0026 DataCollector Extensibility - Getting testSources in property bag 

## Summary
Getting `testSources` as part of property bag. List of test sources can be used by datacollectors for processing before test run start.

## Motivation
Data collector might need test sources list while initialization. Example: Static code coverage data collector needs to instrument the test sources before test run start.

In `sessionStartEventArgs` the field `IDictionary<string, object> Properties` will contain all properties we need to pass to the datacollector.
The public APIs exposed in `SessionStartEventArgs` would be as given below.
```csharp
 /// <summary>
/// Returns the Session Start Properties currently specified.
/// </summary>
public IEnumerator<KeyValuePair<string, object>> GetProperties()
{
    return this.Properties.GetEnumerator();
}

/// <summary>
/// Returns the property value
/// </summary>
/// <param name="value">
/// Value of the property
/// </param>
/// <param name="property">
/// Name of the property
/// </param>
public T GetPropertyValue<T>(string property, T value)
{
    ValidateArg.NotNullOrEmpty(property, "property");

    if (this.Properties.TryGetValue(property, out object propertyValue) && propertyValue != null)
    {
        value = (T)propertyValue;
    }
    else
    {
        value = default(T);
    }

    return value;
}
/// <summary>
/// Sets the property value
/// </summary>
/// <param name="property">
/// Name of the property
/// </param>
/// <param name="value">
/// Value of the property
/// </param>
public void SetPropertyValue(string property, object value)
{
    ValidateArg.NotNull(property, "property");

    if (value != null)
    {
        this.Properties.Add(property, value);
    }
}
```

At present, we will be adding `testSources` to `sessionStartEventArgs.Properties` which can be taken use by the datacollector.

In the datacollector, the user can get test sources as given below.
```csharp
IEnumerable<string> sources = new List<string>();
sources = sessionStartEventArgs.GetPropertyValue("testSources", sources);
```