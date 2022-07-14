# Troubleshooting guide

The goal of this document is to help the test platform users to collect useful information for troubleshooting issues.

## Azure DevOps

### @VSTest2 task

#### Collect diagnostic logs

##### Using `otherConsoleOptions: /Diag:vstestlog.txt`

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

##### Using `System.Debug` environment variable

For some scenarios, it is not possible use the `otherConsoleOptions` (e.g., parallel execution).

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

#### Collect logs and crash dump/hang

##### Using `otherConsoleOptions: /Blame`  

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

You can now zip/download all logs from the published artifacts view under the `vstestlog` folder and you can find the dump using the `Attachments` tab under `Tests` selecting the parent (first) test node.  

##### Using *.runsettings file

 For some scenarios, it is not possible use the `otherConsoleOptions` (e.g., parallel execution).

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

### DotNetCoreCLI@2 task  

#### Collect process dump using Procdump on Windows (i.e. OutOfMemory)

```yaml
  variables:
    - name: System.Debug
      value: true
    - name: PROCDUMP_PATH
      value: $(Agent.ToolsDirectory)\Procdump
    - name: VSTEST_DUMP_FORCEPROCDUMP
      value: 1
...
  - task: PowerShell@2
    displayName: 'Download ProcDump'
    inputs:
      targetType: inline
      script: |
        Invoke-WebRequest -Uri "https://download.sysinternals.com/files/Procdump.zip" -OutFile $(Agent.TempDirectory)\Procdump.zip
        Expand-Archive -LiteralPath $(Agent.TempDirectory)\Procdump.zip -DestinationPath $(Agent.ToolsDirectory)\Procdump -Force
...
  - task: DotNetCoreCLI@2
    displayName: Test project
    inputs:
      command: test
      arguments: --blame-crash --blame-crash-collect-always true --diag:log.txt
```

## Visual Studio

### Enable Diagnostic logs

* Go to Visual Studio options page (`Tools/Options`)
* Select `Test` and then `General`
* Under `Logging`, change `Logging level` to `Trace (Includes Platform logs)`
* Close the `Options` window
* Open the `Output` window and select `Tests` output
* Locate the entry similar to `C:\Users\<YOUR_USER>\AppData\Local\Temp\TestPlatformLogs\<DATE_TIME>` (e.g. `C:\Users\johndoe\AppData\Local\Temp\TestPlatformLogs\2022_07_14_15_24_06_19400`) and open the folder
* Run your tests
* Create a zip with all files available

Note: these logs could contain sensitive information (paths, project name...). Make sure to clean them or use the Visual Studio `Send Feedback` button. Don't put anything you want to keep private in the title or content of the initial report, which is public. Instead, say that you'll send details privately in a separate comment. Once the problem report is created, it's now possible to specify who can see your replies and attachments.
