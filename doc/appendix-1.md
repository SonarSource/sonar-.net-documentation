<a name="upgradeFrom09Anchor">
# Appendix 1: Upgrading from v0.9 of the SonarQube MSBuild Runner
</a>

## Overview of the differences between v0.9 and v1.0
The integration pieces changed significantly from the v0.9 preview version. The main changes in the v1.0 release are as follows:

1. Added support for all of the scenarios supported by the *Visual Studio Bootstrapper* plugin so that the Visual Studio Bootstrapper plugin could be deprecated, and
2. Simplified the installation process.

The v0.9 release of the SonarQube MSBuild Runner did not support a number of analysis plugins (e.g. the VB.Net plugin, Resharper and StyleCop) because it did not provide any way to pass additional settings to those plugins.
In version 1.0, global settings can be specified in the new SonarQube.Analysis.xml file or passed on the command line. Settings specific to a particular MSBuild project can be specified in the MSBuild project file.

The v0.9 release required the user to manually set up and configure the sonar-runner. This is no longer required in v1.0 (although it is still necessary for Java to be pre-installed on the machine).
Previously the user had to manually install the *SonarQube.Integration.ImportBefore.targets* file. This file is now automatically installed to the appropriate per-user location for MSBuild v4.0, v12.0 and v14.0.

A number of bugs were fixed and a series of improvements made to simplify running an analysis from the command line as well as through Team Build.
Finally, the name of the exe changed from *SonarQube.MSBuild.Runner.exe* in the preview to *MSBuild.SonarQube.Runner.exe* in version 1.0 to comply with the plugin naming convention used by SonarSource.

## Required upgrade steps

Perform the following steps to upgrade from version 0.9 of the SonarQube MSBuild Runner:

1. Install the new version of the C# plugin on the SonarQube server as described [above](#installLatestPluginAnchor).
2. Install the new version of the MSBuild.SonarQube.Runner on the agent machine as described [above](#setup-of-the-msbuild-sonarqube-runner-on-the-build-agent-machine).
3. (Optional) Migrate any additional settings from the old **sonar-runner.properties** file to the **SonarQube.Analysis.xml** file.
	- If you had added any additional settings in the **sonar-runner.properties** file then these settings will need to be moved to the new **SonarQube.Analysis.xml** file. 
4. Delete *SonarQube.Integration.ImportBefore.targets* from *%ProgramFiles(x86)%\MSBuild\12.0\Microsoft.Common.Targets\ImportBefore*.
5. Upgrade any existing build definitions.
	- The name of the executable in the **Pre-build script path** and the **Post-test script path** fields should be changed from *SonarQube.MSBuild.Runner.exe* to *MSBuild.SonarQube.Runner.exe*.
	- Add *begin* to the **Pre-build script arguments**
	- Add *end* to the **Post-test script arguments**.

## Optional upgrade steps - remove the sonar-runner
It is not necessary to uninstall the manually-installed version of the sonar-runner that was required by the v0.9 version. However, if you do wish to do so then perform the following steps:

1. Delete the sonar-runner files from disc.
2. Remove the sonar-runner *bin* directory from the `%PATH%`.
3. Delete the SONAR_RUNNER_HOME environment variable.
4. Delete the SONAR_RUNNER_OPTS enviornment variable.
5. Restart the TFS Build Service.
	- If you have amended the environment variables then you will need to restart the Build Service so it uses the modified set of variables.