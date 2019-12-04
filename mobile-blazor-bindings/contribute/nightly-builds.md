---
title: 'Use nightly builds'
---

# Use nightly builds

## NuGet.config file for nightly feed

If you're using official releases (including previews) from NuGet.org, this step is not needed.

If you're using nightly dev builds from the GitHub repo, you'll need to add a file named `NuGet.config` to your solution's directory with these contents:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <add key="Emblazon Feed" value="https://devdiv.pkgs.visualstudio.com/_packaging/Emblazon/nuget/v3/index.json" />
    </packageSources>
</configuration>
```
