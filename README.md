# Dotnet-Publish-Action
Publish your dotnet app (WinUI 3, WPF, Console) as a zip file with auto changelog in Github Release with Github Action.

## How to use?
- Download yml file into your repo and `./github/workflow` folder.
- Edit yml file and Config Options:

> **_NOTE:_**  currently we build your dotnet app with `dotnet-version: 8.0.x`

### Configuring Project
- PROJECT_PATH: `App1/App1.csproj`
- APP_NAME: `MyApp`

### Configuring Dotnet Build Commands
- PUBLISH_OUTPUT_FOLDER: `publish`
- PUBLISH_SELF_CONTAINED: `false`
- PUBLISH_SINGLE_FILE: `false`
- PUBLISH_READY_TO_RUN: `false`
- PUBLISH_TRIMMED: `false`

### Configuring GitHub Release
- IS_PRE_RELEASE: `false`
- SKIP_IF_RELEASE_EXIST: `true`
- MAKE_LATEST: `false`
- ALLOW_UPDATES: `false`
- ARTIFACT_ERRORS_FAIL_BUILD: `false`

if you set a suffix (beta, alpha, preview, experiment) for version tag in your csproj file, `IS_PRE_RELEASE` will be changed to `true` based on suffix.

```xml
<Version>1.0.0-beta</Version>
```

### Platform
if you want to build your app for x64 and x86 only, you can change platform:

platform: `[x64, x86]`

or if you want x64 only:

platform: `[x64]`

## WinUI 3
there is a knonw issue for WinUI 3, if you are using Class Library in your project, you should add following code into your class library csproj file:

```xml
<EnableMsixTooling>true</EnableMsixTooling>
```

Otherwise, the build will fail.

### Solution
for fixing this, we passed `/p:GITHUB_ACTIONS=true` property into dotnet publish command.

now you can use a `Directory.Build.props` file in your project root folder with following Content:

```xml
<PropertyGroup Condition="'$(GITHUB_ACTIONS)' == 'true'">
    <EnableMsixTooling>true</EnableMsixTooling>
</PropertyGroup>
```

This way, when you are using github action, all your projects will include `EnableMsixTooling`, And the build/publish will be done successfully.

---
![Preview](Preview.png)
