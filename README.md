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

![Preview](Preview.png)