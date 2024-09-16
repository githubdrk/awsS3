Passing Environment Variables in PowerShell:

You can pass environment variables in PowerShell by using $env:VARIABLE_NAME = "Value".
These variables can be used in scripts or command-line invocations.
Terraform Upgrade/Update:

To upgrade Terraform CLI, you need to manually download the new version.
To update providers and modules in Terraform, use the command terraform init -upgrade.
Checkmarx Implementation for .NET:

Checkmarx is a static application security testing (SAST) tool.
You can analyze .NET code without needing to run the application, as Checkmarx focuses on static code analysis.
WhiteSource for .NET:

WhiteSource (Mend) is used for scanning open-source dependencies like NuGet packages for security vulnerabilities and license compliance.
WhiteSource doesn’t require the application to be built; it scans dependency files (e.g., packages.config, .csproj) without compiling the code.
Difference between WhiteSource and Checkmarx:

Checkmarx: Focuses on static code analysis to detect security vulnerabilities within the code itself.
WhiteSource: Scans open-source libraries (dependencies) for security vulnerabilities and license risks but does not perform static code analysis.
In essence, Checkmarx and WhiteSource serve different purposes, with Checkmarx focusing on security within the code itself and WhiteSource managing the security of external dependencies used by your .NET project.
