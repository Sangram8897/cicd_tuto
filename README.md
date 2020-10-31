
**Basic cmd of React Native**


source ~/.bash_profile

_To Check setup of react native_
> npx @react-native-community/cli doctor

_To check React Native version_
 > "react-native -v"

_To Upgrade react native_
 > npx react-native upgrade

_To install specific react native version_
npm install react-native@0.43.8

_To Create react native Project_
 > npx react-native init <PROJECT_NAME>

_To run react native Project_
 > npx react-native run-android  or run-ios

_To start Metro bundler and reset cache_
 > npx react-native start --reset-cache 

_To run in the postinstall target of your package.json (Any time your dependencies update you have to jetify again)_
 > npx jetify

_For installation of node-modules or pods_
 > npm install / npm i   or  npx pod-install ios  

_To remove node-modules_
 > rm -rf node_modules

_To performs a moment-in-time security review of your project’s dependency tree_
 > npm audit fix

_To clear npm cache_
 > npm cache clean --force

_For installation of yarn_
 > install yarn  

_For global installation Eslint_
 > yarn add --dev eslint @react-native-community/eslint-config
  
_To generate signingReport in android_
 > cd android && ./gradlew signingReport

_To clean gradlew_
 > cd android && ./gradlew clean

_For debugging_
 > adb shell input keyevent 82

_For close react-native port For windows_ 
 > netstat -ano | findstr :8081

_For clear all instance of node for Mac_ 
 > kill -9 node

_Looks like you installed react-native globally, maybe you meant react-native-cli? To fix the issue, run_
 > npm uninstall -g react-native
 > npm install -g react-native-cli

_Error: spawn ./gradlew EACCES_
 > cd android && chmod -R 777 ./gradlew && cd ..

**Generating Signed APK**

_Generating a signing key_
 > keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

_Setting up gradle 
1. Place the my-release-key.keystore file under the android/app directory
2. Edit the file ~/.gradle/gradle.properties
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****

_Adding signing config to your app's gradle config_
 signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }

_To enable Proguard_
buildTypes {
        release {
            ...
            minifyEnabled true
        }
    }
_To enable Proguard, edit android/app/build.gradle:_
def enableProguardInReleaseBuilds = true

_for generating signed apk_
 > cd android && ./gradlew assembleRelease

_Testing the release build of signed app_
 > cd android && ./gradlew installRelease

_for generating bundle apk_
 > cd android &&  ./gradlew bundleRelease

_Testing the release build of bundled app_
 > npx react-native run-android --variant=release

_Change For metro builder connectivity issue_
var sharedBlacklist = [
  /node_modules[\/\\]react[\/\\]dist[\/\\].*/,
  /website\/node_modules\/.*/,
  /heapCapture\/bundle\.js/,
  /.*\/__tests__\/.*/
];

_ISSUE-Invalid maximum heap size_
Error: Could not create the Java Virtual Machine.
Error: A fatal exception has occurred. Program will exit.
Java HotSpot(TM) Client VM warning: ignoring option MaxPermSize=2048m; support was removed in 8.0
Invalid maximum heap size: -Xmx4g
The specified size exceeds the maximum representable size.
> update java 

## ISSUE when try to install firebase dependencies-> compileSdkVersion is not specified
_ISSUE-A problem occurred configuring project react-native-firebase-crashlytics_
> this is npm versioning error remove all npm manually and try to install again