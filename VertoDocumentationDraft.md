# Verto App

## Install and  setup react-native
- [Follow this guide for React Native CLI - macOS - iOS and android](https://reactnative.dev/docs/environment-setup)


#### Recommended versions
``` plainText

 - React Native: v0.65.1
 - Node: 14.18.1 * we recommend using nvm
 - Yarn: 1.22.10 
 - npm: 6.14.15 
 - Watchman: 2022.02.14.00 
 - CocoaPods: 1.11.3

```
> (optional to run from terminal instead of xcode) ios-deploy tool: `npm install -g ios-deploy` (this option is not working for now)

## Setup the repo 

 1. Clone the repo: `git clone git@github.com:AgentisPayments/verto-app.git`
 2. Move to repo folder: `cd ~/path/To/Repo/Folder`
 3. From project root folder install npm packages: `npm install`
 4. From project root folder install pods: `npx pod-install`
 5. Add environment folder in the root folder.
 6. Select and set a enviroment using those follow commands:


#### Environment commnads
  | Environment  |Command                         |
  |-------------|---------------------------------|
  | Development | `yarn generate-dev-credentials` |
  | Staging     | `yarn generate-qa-credentials`  |
  | Production  | `yarn generate-prod-credentials`|


 > *For development purposes you should always use dev credentials*

---

## Run the Verto App

> Before select an specific environment make sure to generate the corresponding credentials (development, staging or production).

### Steps:
1. Start react-native `npx react-native start --reset-cache`
2. Follow specific ways to run the project for android and IOS:

#### IOS
> For ios is a must before to open the workspace run `npx pod-install` in the root project

 1. Move to folder ~root/ios/verto
 2. Open Verto.xcworkspace
 3. Change app scheme according your previus environment selected (dev, qa or prod).
 4. Select a target emulator or physic device and press run.

#### Android

For android we have 2 ways to run Verto app first one is using **Android Studio**:
 1. Open android studio and select rooFolder/android
 1. Select android flavor according your previus environment selected (dev, qa or prod).
 1. Select a target emulator or physic device and press run.

the second option is using some commands previously set up (those commands should be used on the root Verto app folder and select an env)

  |Environment  |Command                 |
  |-------------|------------------------|
  | Development | `yarn run-android-dev` |
  | Staging     | `yarn run-android-qa`  |
  | Production  | `yarn run-android-prod`|



> If android install the apk but doesn't connect with metro follow these steps:
>	1. Check if your device is connected to the same net that you computer.
>	1. Check if your device is connected to the computer using `adb devices`.
>	1. Reset metro cache using `npx react-native start --reset-cache`. 
>	1. Run Verto app for android using previus command showed or using android studio.
>	1. Run this commmand `yarn adb-setup`.
>	1. Close and open Verto app again.



---


### Verto app environments 


Environment files are manage by `generate-env-credentials.sh` this script loads environment variables and replace specfic files for each platform **andorid** or **ios** using comands defined on [environment commands table](#-environment-commnads)
It is a shellscripts and basically to add specific file for any environment is necessary define file origin `dev, qa or prod` from enviroment folder as route and where that file will be replaced, and finally this script clean android gradle. example:

|Environment  |Command                                         |
|-------------|------------------------------------------------|
|Add          | `yes \| cp -rf <origin/fileName> <targetRoute>`|
|Remove       | `yes \| rm -f -- <targetRoute/fileName>`       |

Also `generate-env-credentials.sh` manage android appVerto version:

```
VERSION_CODE='XX'
VERSION_NAME='X.X.X'
VERSION_BUILD='XX'
```
### Definitions
- **VERSION_CODE**: A positive integer used as an internal version number. This number is used only to determine whether one version is more recent than another, with higher numbers indicating more recent versions. This value increases gradually per build (only for android).
- **VERSION_NAME**: A string used as the version number shown to users. The value is a string so that you can describe the app version as a `<major>.<minor>.<point>`. The versionName has no purpose other than to be displayed to users.
- **VERSION_BUILD**: A positive integer used for testing. This number can either be reset after a release or be continuously incremental throughout the app’s development.



### Environment folder basic structure:

 ``` 
/env
   |
   |- /dev
		|- .env
		|- /ios
		|- /android
   |
   |- /qa
		|- .env
		|- /ios
		|- /android
   |
   |- /prod
		|- .env
		|- /ios
		|- /android

```



----
#### TO-DO
- [ ] Add iOS "build version" and "build number" to generate-env-credentials.sh script to update automatically taking values from VERSION_NAME and VERSION_BUILD. Currently iOS values are changed on xcode.
- [ ] Update generate-env-credentials.sh script to python.
- [ ]
