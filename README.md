# Build or install depemdencies

Note: windows commands are run using [git-bash](https://git-scm.com/downloads) terminal.

## Install vcpkg

When on windows [set up vcpkg](https://learn.microsoft.com/en-us/vcpkg/get_started/get-started?pivots=shell-cmd) inside `/c/bin/` folder. 

```
> cd /c/bin
> git clone https://github.com/microsoft/vcpkg.git
> cd vcpkg
> ./bootstrap-vcpkg.bat
```

## Install libuv

When on windows install `uv` library using `vcpkg`

```
> /c/bin/vcpkg/vcpkg install libuv:x64-windows
```

## Build Micro websockets

Clone the [repository](https://github.com/uNetworking/uWebSockets.git) inside the project root.

```
> git clone --recursive https://github.com/uNetworking/uWebSockets.git
```

```



