# Troubleshooting guide
The goal of this document is to help the test platform users to collect useful information for troubleshooting issues.  

The setup to collect information depends on specific scenario:  
* [@VSTest2 Azure DevOps task](#scenario:-@vstest2-azure-devops-task)  : https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/test/vstest


# Scenario: @VSTest2 Azure DevOps task  
1) Collect diagnostic logs using `otherConsoleOptions: /Diag:vstestlog.txt`   
```yaml
  - task: VSTest@2
    inputs:
      displayName: "VsTest - testAssemblies"
      inputs:
      testAssemblyVer2: |
        ...
      otherConsoleOptions: '/Diag:$(Build.ArtifactStagingDirectory)/vstestlog/vstestlog.diag'

  - task: CopyFiles@2
    displayName: Copy vstestlog logs to staging
    inputs:
      contents: '**/*vstestlog*.diag'
      targetFolder: $(Build.ArtifactStagingDirectory)/vstestlog

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog      
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder.  

2) Collect diagnostic logs using `System.Debug` environment variable, sometime is not possible use the `otherConsoleOptions`(parallel execution)
```yaml
jobs:
- job: ...

  variables:
    - name: System.Debug
      value: true

  steps:
  ...
  - task: VSTest@2
    inputs:
      displayName: "VsTest - testAssemblies"
      inputs:
      testAssemblyVer2: |
        ...
  
  - task: CopyFiles@2
    displayName: Copy vstestlog logs to staging
    inputs:
      sourceFolder: $(Agent.TempDirectory)
      contents: '**/*.diag'
      targetFolder: $(Build.ArtifactStagingDirectory)/vstestlog

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder.  

3) Collect logs and crash dump/hang using `otherConsoleOptions: /Blame`  
```yaml
jobs:
- job: ...

  variables:
    - name: System.Debug
      value: true

  steps:
  ...
  - task: VSTest@2
    inputs:
      displayName: "VsTest - testAssemblies"
      inputs:
      testAssemblyVer2: |
        ...

      otherConsoleOptions: otherConsoleOptions: '/Blame:"CollectDump;DumpType=Full;CollectHangDump;TestTimeout=30min;HangDumpType=Full"'
    condition: always()
    continueOnError: true

  - task: CopyFiles@2
    displayName: Copy test logs to staging
    inputs:
      sourceFolder: $(Agent.TempDirectory)
      contents: '**/*.diag'
      targetFolder: $(Build.ArtifactStagingDirectory)/vstestlog
    condition: always()
    continueOnError: true

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog
    condition: always()
    continueOnError: true
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder and you can find the dump using the `Attachments` tab under `Tests` selecting the parent(first) test node.  

4) Collect logs and crash dump/hang using *.runsettings file , sometime is not possible use the `otherConsoleOptions`(parallel execution)
```yaml
jobs:
- job: ...

  variables:
    - name: System.Debug
      value: true

  steps:
  ...
  - task: VSTest@2
    inputs:
      displayName: "VsTest - testAssemblies"
      inputs:
      testAssemblyVer2: |
        ...
      runSettingsFile: ./config.runsettings
    condition: always()
    continueOnError: true

  - task: CopyFiles@2
    displayName: Copy test logs to staging
    inputs:
      sourceFolder: $(Agent.TempDirectory)
      contents: '**/*.diag'
      targetFolder: $(Build.ArtifactStagingDirectory)/vstestlog
    condition: always()
    continueOnError: true

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog
    condition: always()
    continueOnError: true
```
`config.runsettings` file
```xml
<RunSettings>
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="blame" enabled="True">
        <Configuration>
          <CollectDump DumpType="Full" />
          <CollectDumpOnTestSessionHang TestTimeout="30min" HangDumpType="Full" />
        </Configuration>
      </DataCollector>
    </DataCollectors>
  </DataCollectionRunSettings>
</RunSettings>
```