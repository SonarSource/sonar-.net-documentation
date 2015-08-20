# Appendix 3: Advanced MSBuild SonarQube Runner configuration options

This appendix contains additional information on how the MSBuild SonarQube Runner can be configured to work effectively in more complex real-world scenarios.

## Conditionally excluding projects from analysis

Setting *SonarQubeExclude* at project level is a simple way to ensure that a project is always included or excluded.
However, because *SonarQubeExclude* is an MSBuild property it can be set conditionally like any other MSBuild property.
This allows considerable flexibility in deciding whether a project should be excluded or not which can be useful in a number of scenarios.

For example, the same MSBuild project may be included in multiple different solutions.
In this situation it is generally desirable that the MSBuild project should only be analysed once e.g.
```
Solution1 contains projects *A*, *B* and *X*. All of the projects should be analysed as part of SonarQube project *example.sqproject1*
Solution2 contains projects *C*, *D* and *X*. Only projects *C* and *D* should be analysed as part of SonarQube project *example.sqproject2*
```

Two possible methods of handling this scenario using a small amount of customisation and configuration are shown below.
Both methods conditionally set the *SonarQubeExclude* property based on additional data supplied during the build phase.

### Explicitly associating an MSBuild project with a SonarQube project

In this approach, a property is added to MSBuild project *X* specifying the SonarQube project key to which the MSBuild project belongs:

```xml
<PropertyGroup>
	<TargetSQProjectKey>example.sqproject2</TargetSQProjectKey>
</PropertyGroup>
```

The following targets file will conditionally set *SonarQubeExclude* based on a value supplied on the command line:

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="4.0">
	<!-- This target customises the SonarQube MSBuild runner targets to limit the project that are analysed.
	Only projects with matching SonarQube project keys will be analysed.
	-->
	<PropertyGroup Condition=" $(SQProjectKey) != '' AND $(SonarQubeExclude) == '' ">
		<!-- If the current project specifies a target SQ project then exclude unless the project keys match. -->
		<SonarQubeExclude Condition="$(TargetSQProjectKey) != '' AND $(SQProjectKey) != $(TargetSQProjectKey) " >true</SonarQubeExclude>
	</PropertyGroup>
</Project>
```

This custom targets file would be imported using one of the standard MSBuild mechanisms e.g. either explicitly <Import>ed into the relevant projects, 
or dropped in a location in which it will be automatically imported such as *%ProgramFiles(x86)%\MSBuild\*[MSBuild version]*\Microsoft.Common.Targets\ImportBefore\*.

At build time, the relevant SonarQube project key would be specified on the command line e.g.

```
msbuild Solution1.sln /p:SQProjectKey=example.sqproject1

msbuild Solution2.sln /p:SQProjectKey=example.sqproject2
```

This would have the desired effect of ensuring MSBuild project *X* is only analysed once.


### Excluding projects based on the file path
Depending on the layout of the projects on disk, it might be possible to specify the projects to analyse based on the file paths.

For example, suppose the projects above are laid out on disk as follows:

```
c:\Web\ProjectA
c:\Web\ProjectB
c:\Framework\ProjectC
c:\Framework\ProjectD
c:\Framework\ProjectX
```

The following custom targets file selects the projects to analyse based on the file path:

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="4.0">
	<!-- This target customises the SonarQube MSBuild runner targets to limit the projects that are analysed.
	Projects whose full path and file name do not match the specified filter will be marked as "excluded".
	The regular expression uses the normal .NET regular expression syntax.
	-->
	<PropertyGroup Condition=" $(SonarQubeExclude) == '' AND $(SQPathFilter) != '' ">
		<MatchesSQPathFilter Condition="$([System.Text.RegularExpressions.Regex]::IsMatch($(MSBuildProjectFullPath), $(SQPathFilter), System.Text.RegularExpressions.RegexOptions.IgnoreCase)) ">true</MatchesSQPathFilter>
		<SonarQubeExclude Condition="$(MatchesSQPathFilter) != 'true' " >true</SonarQubeExclude>
	</PropertyGroup>
</Project>
```

This targets file would allow the projects to be filtered as follows:

```
REM Only analyse the web projects, regardless of which projects are included in the solution
REM Note: the backslash in the supplied path is escaped
msbuild Solution1.sln /p:SQPathFilter=c:\\web

REM Only analyse the framework projects
msbuild Solution2.sln /p:SQPathFilter=c:\\framework
```
