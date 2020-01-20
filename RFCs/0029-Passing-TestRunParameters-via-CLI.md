# Passing test run parameters via cli

## Summary
Test run parameters given via cli are passed to runsettings.

## Motivation
Every time editing or creating one test run parameter in run settings at a time is a tedious task. So passing test run parameters via cli 
removes burden of editing run settings every time.

## Syntax

`vstest.console.exe  abc.dll -- TestRunParaeters.Parameter(name="YourParameterName",value="YourParameterValue ")`

### Argument description 
` -- TestRunParaeters.Parameter(name="YourParamterName",value="YourParameterValue ")` <br>

The above argument reflects the following change in runsettings. 

```xml
<RunSettings>
    <RunConfiguration>
        <TestRunParameters>
          <Parameter name="YourParameterName",value="YourParameterValue"/>
        </TestRunParameters>
    </RunConfiguration>
</RunSettings>
```

<ul>
<li>TestRunParameters as Node</li>
<li>Parameter as child element of TestRunParamter node</li>
<li>YourParamterName as Attribute name </li>
<li>YourParameterValue as Attribute value </li>
</ul>

## Design
Eventually the arguments are parsed and we get `attribute name` and `attribute value` of `test run parameter`.
Later an xml element is overrode if exists with `attribute name` or created with `'Parameter'` as it's name and with attributes that are obtained by the above step.
Finally we get `test run parameter` node if exists or created and append the created xml element to child nodes list of it.


## Allowed Characters
|  Attributes | Vaild Characters |
| -------------- | -------------------- |
| name         | <ul><li>Alphabets</li><li>Digits</li><li>_</li> |
| value    | <ul><li>Alphabets</li><li>Digits</li><li>Special Charcters</li></ul> |

### Note
Some special characters like &,<,> are converted to their escaped form and stored in runsettings. <br>
For more info on escaped strings refer [this](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_xml_escape.html).
