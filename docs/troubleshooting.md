# Troubleshooting guide
The goal of this document is to help the test platform users to collect useful information for troubleshooting issues.  

# Scenario: @VSTest2 Azure DevOps task  
## Collect diagnostic logs using `otherConsoleOptions: /Diag:vstestlog.txt`   
```yaml
  - task: VSTest@2
    inputs:
      displayName: "VsTest - testAssemblies"
      inputs:
      testAssemblyVer2: |
        ...
      otherConsoleOptions: '/Diag:vstestlog.diag'

  - task: CopyFiles@2
    displayName: Copy vstestlog logs to staging
    inputs:
      contents: '**/*vstestlog*.diag'
      targetFolder: $(Build.ArtifactStagingDirectory)/vstestlog
      condition: always()

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog      
      condition: always()
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder.  

## Collect diagnostic logs using `System.Debug` environment variable, sometimes is not possible use the `otherConsoleOptions`(parallel execution)
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
      condition: always()

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog
      condition: always()
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder.  

## Collect logs and crash dump/hang using `otherConsoleOptions: /Blame`  
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
    continueOnError: true
    condition: always()

  - task: PublishPipelineArtifact@1
    displayName: Publish vstestlog log
    inputs:
      targetPath: $(Build.ArtifactStagingDirectory)/vstestlog
      artifactName: vstestlog
    condition: always()
    continueOnError: true
```
You can now zip/download all logs from the published artifacts view under the `vstestlog` folder and you can find the dump using the `Attachments` tab under `Tests` selecting the parent(first) test node.  

## Collect logs and crash dump/hang using *.runsettings file , sometimes is not possible use the `otherConsoleOptions`(parallel execution)
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
