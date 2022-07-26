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


#### Environment commands
  | Environment |Command                          |
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


#### Android flavor commands
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

Environment files are managed by generate-env-credentials.sh this script loads environment variables and replaces specific files for each platform android or ios using commands defined on the [environment commands table](#environment-commands).
It is a shellscript and basically to add a specific file for any environment is necessary to define the file origin dev, qa or prod from the environment folder as route and where that file will be replaced, and finally, this script cleans the android gradle. example:  


|Environment  |Command                                         |
|-------------|------------------------------------------------|
|Add          | `yes \| cp -rf <origin/fileName> <targetRoute>`|
|Remove       | `yes \| rm -f -- <targetRoute/fileName>`       |

Also `generate-env-credentials.sh` manage android appVerto version:

```
VERSION_CODE=XX
VERSION_BUILD=XX
VERSION_NAME='X.X.X'

```
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


#### Differences between android and iOS versioning

- Android:
	- **Version Code**: A positive integer used as an internal version number. This number is used only to determine whether one version is more recent than another, with higher numbers indicating more recent versions. This value increases gradually per build (only for android).
	- **Version Name**: A string used as the version number shown to users. The value is a string so that you can describe the app version as a `<major>.<minor>.<point>`. The versionName has no purpose other than to be displayed to users.


	- * **VERSION_BUILD**: A positive integer used for testing. This number can either be reset after a release or be continuously incremental throughout the app’s development.
> This is a special value for android added  to customize the user agent name for keep same version displayed for android and iOS, this value should be setting up using the same ios `Build Number`.

- IOS:
	- **Build Version**: CFBundleShortVersionString (String - iOS, OS X) number you are using to denote this version of your app. Usually this follows a `<major>.<minor>.<point>` version scheme to let users know which releases are smaller maintenance updates and which are big deal new features.
	- **Build Number**: CFBundleVersion (String - iOS, OS X) specifies the build version number of the bundle, which identifies an iteration (released or unreleased) of the bundle. The build version number should be a string comprised of three non-negative, period-separated integers with the first integer being greater than zero.


#### User Agent name

- Android
`WebViewApp Verto (Environment Name)/(Version Name).(Version Build) (HelloApp/0.1) (Device Model)`

- IOS
`WebViewApp Verto (Environment Name)/(Build Version).(Build Number) (HelloApp/0.1) (Device Model)`



## Libraries Implemented

- [react-native-webview](https://github.com/react-native-webview/react-native-webview): `npm install --save react-native-webview`
- [react-native-firebase](https://rnfirebase.io/#1-install-via-npm): `npm install --save @react-native-firebase/app`
- [lottie-react-native](https://github.com/lottie-react-native/lottie-react-native): `npm i --save lottie-react-native && npm i --save lottie-ios@3.2.3`
- [react-navigation/native](https://reactnavigation.org/docs/getting-started/): `npm install @react-navigation/native react-native-screens react-native-safe-area-context`
- [react-navigation/native-stack](https://reactnavigation.org/docs/hello-react-navigation): `npm install @react-navigation/native-stack`
- [react-native-lottie-splash-screen](https://github.com/HwangTaehyun/react-native-lottie-splash-screen): `npm i react-native-lottie-splash-screen --save`
- [react-native-dotenv](https://github.com/goatandsheep/react-native-dotenv): `npm i react-native-dotenv`
- [react-native-device-info](https://github.com/react-native-device-info/react-native-device-info) `yarn add react-native-device-info`
- [babel-plugin-module-resolver](https://www.npmjs.com/package/babel-plugin-module-resolver): `yarn add --dev babel-plugin-module-resolver`
- [react-native-vector-icons](https://www.npmjs.com/package/react-native-vector-icons): `yarn add react-native-vector-icons`
- [react-native-community/async-storage](https://www.npmjs.com/package/@react-native-community/async-storage): `yarn add @react-native-community/async-storage`
- [react-native-permissions](https://github.com/zoontek/react-native-permissions): `npm install --save react-native-permissions`
- [apollo/client & graphQL](https://www.apollographql.com/docs/react/integrations/react-native/): `npm install @apollo/client graphql`
- [react-native-community/netinfo](https://github.com/react-native-netinfo/react-native-netinfo): `npm i @react-native-community/netinfo`
- [segment/analytics-react-native & segment/sovran-react-native](https://github.com/segmentio/analytics-react-native): `npm install --save @segment/analytics-react-native @segment/sovran-react-native`
- [axios](https://github.com/axios/axios): `npm install axios`
- [react-native-appboy-sdk](https://github.com/Appboy/appboy-react-sdk): `npm install react-native-appboy-sdk`
- [react-native-branch](https://github.com/BranchMetrics/react-native-branch-deep-linking-attribution): `npm install react-native-branch@5.4.1`
- [react-native-camera](https://github.com/react-native-camera/react-native-camera/tree/master): `npm install --save react-native-camera@git+https://git@github.com/react-native-community/react-native-camera.git`
- [react-native-contacts](https://github.com/morenoh149/react-native-contacts): `npm install react-native-contacts --save`
- [react-native-dialog](https://github.com/mmazzarolo/react-native-dialog): `npm install react-native-dialog`
- [react-native-image-crop-picker](https://github.com/ivpusic/react-native-image-crop-picker): `npm i react-native-image-crop-picker --save`
- [react-native-keychain](https://github.com/oblador/react-native-keychain): `npm i react-native-keychain`
- [react-native-permissions](https://www.npmjs.com/package/react-native-permissions): `npm i react-native-permissions`
- [react-native-qr-decode-image-camera](https://github.com/escolarea/react-native-qr-decode-image-camera.git): `npm install --save https://github.com/escolarea/react-native-qr-decode-image-camera.git`
- [rollbar-react-native](https://docs.rollbar.com/docs/react-native): `npm install rollbar-react-native --save`
- [react-native-touch-id](https://github.com/escolarea/react-native-touch-id.git#v4-0-1): `npm install --save https://github.com/escolarea/react-native-touch-id.git#v4-0-1`
- [react-native-svg](https://github.com/react-native-svg/react-native-svg): `npm install react-native-svg`
- [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons): `npm install --save react-native-vector-icons`
- [redux](https://react-redux.js.org/introduction/getting-started): `npm install react-redux`
- [redux-thunk](https://github.com/reduxjs/redux-thunk): `npm install redux-thunk`
- [redux-persist](https://github.com/rt2zz/redux-persist): `npm install redux-persist`
- [redux-logger](https://github.com/LogRocket/redux-logger): `npm i --save redux-logger`
- [react-native-screens](https://github.com/software-mansion/react-native-screens): `npm i react-native-screens`
- [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context): `npm install react-native-safe-area-context`



## Upload builds for iOS and android


----
#### TO-DO
- [ ] Add iOS "build version" and "build number" to generate-env-credentials.sh script to update automatically taking values from VERSION_NAME and VERSION_BUILD. Currently iOS values are changed on xcode.
- [ ] Update generate-env-credentials.sh script to python.
- [ ] ...


