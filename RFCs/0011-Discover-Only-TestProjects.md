# 0011 Discover for Only Test Projects

## Summary
This note outlines the proposed changes to the TestWindow component inside VS IDE,
for making improvements in the test discovery.

## Motivation
* Scope of improvement in discovery through TestExplorer. See [here](#Discovery.Proof)
* Need to standardize the rules for identifying Test projects.

## Problem
TestWindow component inside VS IDE currently sends all the projects present in the solution for discovery.
This list of projects includes projects that do not contain any tests.
Sending redundant projects to the runner creates an overhead. Each adapter will try and fail to discover any tests inside such projects.

### Scenarios
There are two ways user can author C# based tests
1. Create a test project using Unit Test template
2. Add the appropriate adapter or framework references to a class library project. 

### Current State
There are existing ways to identify if a project is a test project. Brief explanation is as follows.

#### Test project Guid
All C# based classic Unit tests which are created using the default templates have a special ProjectType guid to be identified as Test project. 
```
<ProjectTypeGuids>{3AC096D0-A1C2-E12C-1390-A8335801FDAB}<ProjectTypeGuids>
```

#### Test Service Guid
Currently, there is another special guid that we dynamically add to projects that contain tests and were not created via default template.
How this works is, since all the projects are used for discovery, the projects which actually contain tests are identified post discovery
operation and a service guid is added to them.

```
 <ItemGroup>		
    <Service Include="{82A7F48D-3B50-4B1E-B82E-3ADA8210C358}" />		
  </ItemGroup>
```

#### Test container capability
The latest and recommended way of getting a project identified as a Test project is adding
*TestContainer* capability.
.Net core based test projects created using the template have this capabilty by default.

```
<ItemGroup>
    <ProjectCapability Include="TestContainer" />
</ItemGroup>
```

## Proposed Changes
Add an ability to identify the test projects using all the three rules mentioned above.
Also, provide user an option to run discovery operation for test projects only.

User will be provide with two options,
1. Discover All projects.
2. Discover Test projects

### Discover All projects.
All projects are sent for discovery operation and service guid will be added to projects if required.
In short, experience is same as the existing one.
This option would be selected by default.

### Discover Test projects only.
This would ensures only test projects are selected for discovery.
* Note: Since we would not be sending other projects, the tests authored in projects that do not fulfil
any of the rules will not be discovered. Here are a few options recommendations for users:
1. Add *TestContainer* as a project capability.
2. Discover using All projects option, this would make sure service guid gets added to projects which contain
tests but do not have TestContainer capabilities or Test ProjectTypeGuid.

## Proof of concept <a name="Discovery.Proof"></a>
In Visual Studio 2017 15.3, all .net core tests projects are filtered based on TestContainer capability.
Discovery operation with only filtered test projects is performant by 10-15% in large solutions.

