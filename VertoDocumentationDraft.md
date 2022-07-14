# Verto App

### Current Verto Branches
- Main
- Development

### Setup the repo

 1. Clone the repo: `git clone git@github.com:AgentisPayments/verto-app.git`
 2. Move to repo folder: `cd ~/path/To/Repo/Folder`
 3. From project root folder install npm packages: `npm install`
 4. From project root folder install pods: `npx pod-install`
 5. Add env folder in the root (this folder should be provided by team member)
 6. Select and set a enviroment using those follow commands:

  |Environment  |Command                          |
  |-------------|---------------------------------|
  | Development | `yarn generate-dev-credentials` |
  | Staging     | `yarn generate-qa-credentials`  |
  | Production  | `yarn generate-prod-credentials`|
##

### Run the Verto App

> Before running an specific environment make sure to generate the corresponding credentials (development, staging or production).

#### Android

For android we have 2 ways to run Verto app first one is uses **Android Studio**:
 1. Open android studio and select rooFolder/android
 1. Select android flavor according your previus env selected (dev, qa, prod).
 1. Select a target emulator or physic device and press run.

the second option is use some command previusly setted up (those command should be use on root Verto app folder and select a env)

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

#### IOS
 1. Move to folder ~root/ios/verto
 2. Open Verto.xcworkspace
 3. Change app scheme according your previus env selected (dev, qa, prod).
 4. Select a target emulator or physic device and press run.

##
### How to change Verto app environments
On verto app project we use a strategy with enviromental variables for each env exist a folder with an espefic structure like this
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

Use follow commands to change evironment variables in Verto app:



Steps: 
 1. Create a feature branch using Jira/zenhub story ID.
 2. 

