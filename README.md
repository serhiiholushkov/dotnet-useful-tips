# DotNet useful tips

## Table of contents

- [Aspire](#aspire)
  - [Install](#installation)
  - [CLI commands](#cli-commands)
- [Project setup](#project-setup)
  - [Central Package Management](#using-central-package-management-cpm)
  - []

# Aspire

[Docs](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-overview)

## Installation

Install templates:

```bash
dotnet new install Aspire.ProjectTemplates
```

Install CLI:

```bash
curl -sSL https://aspire.dev/install.sh -o aspire-install.sh

sh aspire-install.sh
```

For MAC need to register PATH so command line will know what's aspire:

1. In the user's root/home directory find file .zprofile
2. Add next lines to the file:

```bash
# DotNet Aspire
export PATH="/Users/<username>/.aspire/bin:$PATH"
```

3. restart command line

## CLI commands

[commands](https://learn.microsoft.com/en-us/dotnet/aspire/cli-reference/aspire)

# Project setup

Some useful tips, libraries for project setup

## Using central package management (CPM)

Groups all the packages and their versions in on place.

[Docs](https://learn.microsoft.com/en-us/nuget/consume-packages/central-package-management)

Setup:

1. Create a new file at the root of your repository named Directory.Packages.props that declares your centrally defined package versions and set the MSBuild property ManagePackageVersionsCentrally to true.

```bash
dotnet new packagesprops
```

2. Declare <PackageVersion /> items in your Directory.Packages.props.

Example:

```xml
<Project>
  <PropertyGroup>
    <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
  </PropertyGroup>
  <ItemGroup>
    <PackageVersion Include="PackageA" Version="1.0.0" />
    <PackageVersion Include="PackageB" Version="2.0.0" />
  </ItemGroup>
</Project>
```

3. Declare <PackageReference /> items without Version attributes in your project files.

Example:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="PackageA" />
  </ItemGroup>
</Project>
```

## Central msbuild settings

To share some msbuild props between all projects you can use Directory.Build.props file. It's useful for sharing .net version and other settings.

1. In the root folder create file Directory.Build.props

Example content:

```xml
<Project>
  <PropertyGroup>
    <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
    <TargetFramework>net9.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>
  <PropertyGroup>
    <NoWarn>1591</NoWarn> <!-- Remove this to turn on warnings for missing XML Comments -->
  </PropertyGroup>
</Project>
```

2. Remove shared build props from all the projects in solution.
