#actions

## Check commit message

- Using `if` statement

```yaml
name: "Build"
 
on:
  push:
    branches:
      - main
    paths-ignore:
      - '**/*.md'
      - '**/*.gitignore'
      - '**/*.gitattributes'
  workflow_dispatch:
    branches:
      - main
    paths-ignore:
      - '**/*.md'
      - '**/*.gitignore'
      - '**/*.gitattributes'
       
jobs:
  build:
    if: github.event_name == 'push' && contains(toJson(github.event.commits), '***NO_CI***') == false && contains(toJson(github.event.commits), '[ci skip]') == false && contains(toJson(github.event.commits), '[skip ci]') == false
    name: Build 
    runs-on: ubuntu-latest
    env:
      DOTNET_CLI_TELEMETRY_OPTOUT: 1
      DOTNET_SKIP_FIRST_TIME_EXPERIENCE: 1
      DOTNET_NOLOGO: true
      DOTNET_GENERATE_ASPNET_CERTIFICATE: false
      DOTNET_ADD_GLOBAL_TOOLS_TO_PATH: false
      DOTNET_MULTILEVEL_LOOKUP: 0
 
    steps:
    - uses: actions/checkout@v2
       
    - name: Setup .NET Core SDK
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 3.1.x
 
    - name: Restore
      run: dotnet restore
 
    - name: Build
      run: dotnet build --configuration Release --no-restore
 
    - name: Test
      run: dotnet test
```