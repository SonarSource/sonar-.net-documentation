# Analyze .NET Projects From The Command Line

The following assumes that `MSBuild.SonarQube.Runner.exe` has been added to the `%PATH%`.
If that is not your case, simply specify the absolute path to it in both the *begin* and *end* phase commands.

1. **Run the MSBuild.SonarQube.Runner.exe begin phase**

	```
	MSBuild.SonarQube.Runner.exe begin /key:{SonarQube project key} /name:{SQ project name} /version:{SQ project version}
	```

	The begin phase takes four arguments:

	- begin
	- /key:{the **project key** of the SonarQube project to which the build relates}
	- /name:{the **project name** of the SonarQube project}
	- /version:{the **project version** of the SonarQube project}

	*The aliases /k:, /n: and /v: can also be used.*

	**>>NOTE >>** If any of the arguments contain spaces then that argument needs to be surrounded by double-quotes e.g. **/name:”My Project Name”**.

	See [Configuring the MSBuild SonarQube Runner](appendix-2.md) below for more information on passing additional settings.

2. **Launch your normal project build**

	Basic example:

	```
	msbuild
	```

	Example, with nuget:

	```
	nuget restore
	msbuild
	```

	**>>NOTE >>** make sure to run MSBuild.SonarQube.Runner in a "MSBuild console", or a "VS Developer Command Prompt" otherwise you will not be able to access MSBuild command and you may get an error similar to "'msbuild' is not recognized as an internal or external command,operable program or batch file."
3. **Run the MSBuild.SonarQube.Runner.exe end phase**

	```
	MSBuild.SonarQube.Runner.exe end
	```