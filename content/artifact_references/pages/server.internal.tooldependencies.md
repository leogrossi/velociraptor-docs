---
title: Server.Internal.ToolDependencies
hidden: true
tags: [Client Artifact]
---

An internal artifact that defines some tool
depenencies. Velociraptor releases for offline collector


```yaml
name: Server.Internal.ToolDependencies
description: |
  An internal artifact that defines some tool
  depenencies. Velociraptor releases for offline collector

tools:
  - name: VelociraptorWindows
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0/velociraptor-v0.7.0-rc1-windows-amd64.exe
    serve_locally: true
    version: 0.7.0-rc1

  - name: VelociraptorWindows_x86
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0/velociraptor-v0.7.0-rc1-windows-386.exe
    serve_locally: true
    version: 0.7.0-rc1

  - name: VelociraptorLinux
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0/velociraptor-v0.7.0-rc1-linux-amd64-musl
    serve_locally: true
    version: 0.7.0-rc1

  - name: VelociraptorDarwin
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0/velociraptor-v0.7.0-rc1-darwin-amd64
    serve_locally: true
    version: 0.7.0-rc1

  - name: VelociraptorWindowsMSI
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0/velociraptor-v0.7.0-rc1-windows-amd64.msi
    serve_locally: true
    version: 0.7.0-rc1

  - name: VelociraptorWindows_x86MSI
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.7.0-rc1/velociraptor-v0.7.0-rc1-windows-386.msi
    serve_locally: true
    version: 0.7.0-rc1

```
