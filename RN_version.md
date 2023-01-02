## Verto React native Version

#### Current Version: `v0.65.1` 
> As recommendation is to update the react native version to v0.65.3 to solve the android builds issue because seems, for now, don't exist security risks related to this version at 22/Dec/2022


#### Why is neccesary update it?
Starting from 4th November 2022 react native had an issue generating android builds, details about the issue: [React Native issue #35210](https://github.com/facebook/react-native/issues/35210).
Currently the Verto app `1.0.9 (10)` keep  react native `0.65.1` was implemented this fix (to avoid risks previous to deploy this version):
```
//project_path/android/buld.gradle 

def REACT_NATIVE_VERSION = new File(['node', '--print',"JSON.parse(require('fs').readFileSync(require.resolve('react-native/package.json'), 'utf-8')).version"].execute(null, rootDir).text.trim())

allprojects {
    configurations.all {
        resolutionStrategy {
            // Remove this override in 0.65+, as a proper fix is included in react-native itself.
            force "com.facebook.react:react-native:" + REACT_NATIVE_VERSION
        }
    }

```
#### Alternatives to update React Native version version
[React Native versions are currently supported](https://github.com/reactwg/react-native-releases#which-versions-are-currently-supported)

- The recommend version to update is [v0.65.3](https://github.com/facebook/react-native/releases/tag/v0.65.3) in this case after tested it wasn't found any issue on android and ios builds, the unique consideration is this version is doesn't support and it was an special release for application that use react native `v0.65.x`. 

	- [Comparatative between v0.65.1 and v0.65.3](https://react-native-community.github.io/upgrade-helper/?from=0.65.1&to=0.65.3)
	- (Was not found security leaks or something like that related to this version)
- The other option is to update to a supported version, for example, `v0.68.x`, as an experiment tried to update Verto react native version to `v0.68.5` in this case, omitted to react native new architecture changes only focusing on changes necessary to run a build in both platforms (ios and android) probably if we introduce those changes can increase the risk, the unique issue found after a smoke test was in android, the QR code scanner frame overlaps the translucent frames (in the update results link can see an example )
    - [Comparatative between v0.65.1 and v0.68.5](https://react-native-community.github.io/upgrade-helper/?from=0.65.1&to=0.68.5)
	 - [Update results (temporal update)](https://github.com/AgentisPayments/verto-app/issues/190#issuecomment-1358158644)

