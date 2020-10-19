# WinGet CLI to manager windows packages

> More information at [WinGet Github Repo](https://github.com/microsoft/winget-cli)

## How to install

- Download latest appxbundle package from github repo. At the time of writing latest version is [Windows Package Manager v0.2.2521 Preview](https://github.com/microsoft/winget-cli/releases)
- Install the app. At the end of installation, It will ask you to test by opening an windows app from store. Just Ignore that and close the windows.
- Open powershell and type `winget` and you will see below pic.
  ![WinGet Help](/resources/winget-help.png)

## Installing a package

For demo purpose, We will try to install git on windows

- Open powershell and run below command
  `winget install git`

> By default installation requires you to approve installation at UAC dialogue. To disable that, You can pass -h flag to do silent install

That was super quick. Right!
