# UnsignedBytes UBBuildTools
## PowerShell Build Tools for managing script projects

The UnsignedBytes UBBuildTools provides a way to manage your PS Modules
using a consistant structure and allows testing, static analysis through
ScriptCop, dynamically generated manifest files, and packages your scripts
into a convenient zip file for transport. The entire configuration of the 
project is controlled by a single psproj.json file that guides the tool through
your project allowing the build to remain flexible.

**To Build:**

Building the project is not required to use it. you can just download the 
zip file for the version you would like from the dist folder on this repository if
you don't want to build the artifacts yourself.

Prerequisites: ScriptCop (http://scriptcop.start-automating.com/)

```PowerShell
cd ./PSBuild/
ipmo ./src/UBBuildTools.psm1 
Invoke-PSBuild -ProjectRoot ./ -ModuleName UBBuildTools
```

**To Install:**

Grab the latest UBBuildTools-x.x.x.zip file to get all the required
artifacts and unzip the contents to:
```PowerShell
%UserProfile%\Documents\WindowsPowerShell\Modules 
```

**Create a Project File:**

Create a new folder for your project
```PowerShell
mkdir MyProject
cd MyProject
mkdir src
mkdir dist
mkdir tests
```

Create a new psproj.json file in the new project directory and add the following to the file.
Update to use your information.
```json
{
	"projectName": "My Fancy New Project",
	"uniqueId": "9cb01216-d85b-49e7-a501-bb22d3a94046",
	"companyName": "My Company, Inc.",
	"version": "3.1.1",
	"description": "My summary description of the project",
	"authors": [
		"Timmy Developer <timmy@testdeveloper.com>"
	],
	"dotNetVersion": "4.5",
	"powerShellVersion": "4.0",
	"src": "src",
	"dist": "dist",
	"tests": "tests"
}

```
* The src, dist, and tests properties represent the three project directories created earlier
and can be overridden to point to any relative path e.g. "dist": "Bin" would indicate that the
Bin directory should be used to hold your distributable artifacts after a build.

* The uniqueId field is a unique identifier that will be used in the psd1 manifest file.

**Add Your Module and about_ files:**

Add your .psm1 files and about_ help files into the src directory.

**Add Tests:**

Add any powershell tests with the format *.Test.ps1 to the tests directory

**Build:**

Run the Invoke-PSBuild command to build the zip package for your module. See Get-Help Invoke-PSBuild for more details.
