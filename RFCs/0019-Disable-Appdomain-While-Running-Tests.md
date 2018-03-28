# 0019 Disable Appdomain while Running Tests

## Summary
The RFC outlines why

1. Test adapters should honour disable app domain setting

2. Running of tests with disable appdomain is important for resiliency 

## Motivation
In past we have seen customer hitting issue with Appdomain.Unload. There are two main issues with Appdoamin.Unload call

1. Hang in Appdoamin.Unload (Tracking issue https://github.com/Microsoft/testfx/issues/225)

2. AppDomain.Unload call crashes the process even if you have an exception handler in code. This is due to a CLR and OS bug which ends up ignoring the exception handler in code and terminates the process.

## Proposed changes

Proposed guidelines are for customers and test adapters who wants to avoid these issues.

**Adapters**
1. Test Adapter should honour ```<DisableAppDomain>``` setting inside RunConfiguration node of runsettings. Check https://github.com/Microsoft/vstest-docs/blob/master/docs/configure.md for information on this setting. This will ensure that adapters dont create AppDomain at all to run tests

**Test platform**

1. Change in test platform to merge the app.config for a test assembly when ```<DisableAppDomain>``` is set. This is to ensure test's app.config is honoured while running tests

2. Make sure when ```<DisableAppDomain>``` is set, each test source have isolation. This is done by spawning testhost process for each test source.