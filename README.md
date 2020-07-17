[![CircleCI](https://circleci.com/gh/dudebowski/liquid-ice.svg?style=shield)](https://circleci.com/gh/dudebowski/liquid-ice)

# liquid-ice
Unfreezing zOS - Devops with zowe and circleCI

## Prereqs 

You need tooling to connect to mainframe's like [ZOWE CLI](https://docs.zowe.org/v1-1-x/user-guide/cli-installcli.html)  
or the [Zowe explorer](https://marketplace.visualstudio.com/items?itemName=Zowe.vscode-extension-for-zowe) in VScode.
[Mainframe account](https://www-01.ibm.com/events/wwe/ast/mtm/cobolvscode.nsf/enrollall?openform)

Also advised
[VSCode](https://code.visualstudio.com/download) and either [IBM Z Open Editor](https://ibm.github.io/zopeneditor-about/Docs/getting_started.html#installing-ibm-z-open-editor) or [Code4z](https://marketplace.visualstudio.com/items?itemName=broadcomMFD.code4z-extension-pack)

## Setup
Set up a zowe profile with the CLI or with the Zowe explorer 

## Manual runs

### Copy files to maiframe
```console
zowe zos-files upload dir-to-pds "./JCL" "<MainframeID>.JCL"  
zowe zos-files upload dir-to-pds "./CBL" "<MainframeID>.CBL"
 ```
### Compile and run 
```console
zowe jobs submit ds "z82101.jcl(compunfr)" -d . --rfj     
zowe jobs submit ds "z82101.jcl(execunfr)" -d . --rfj     
```

## Script
You can run all in one command using npm

```console
npm run build --mainframeID=<MainframeID>
```

## circleCI
circleCI runs after each push. Job runs in a node docker.
The config checks out the code installs zowe-cli, creats a zowe profile and runs the compilation on the mainframe

