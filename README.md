# React Native Adobe Analytics

React Native bridge for Adobe Analytics.

This is a fork of https://github.com/smalltownheroes/react-native-adobe-analytics

## Installation
```
$ npm install redhotmagma/react-native-adobe-analytics --save
```
### Automatic linking
```
$ react-native link
```

### Configuration file
Get your ADBMobileConfig.json file from Adobe Mobile Services.
- On iOS, add the ADBMobileConfig.json file to your XCode project so that it's accessible in your bundle.
- On Android, the ADBMobileConfig.json file must be placed in the assets folder.

### Android Configuration
#### Update `MainApplication.java`
You need to import this package into your `MainApplication.java` file as well as load that package in the `getPackages` method:
```diff
diff --git a/MainApplication.java b/MainApplication.java
index a209301..8ada6e5 100644
--- a/MainApplication.java
+++ b/MainApplication.java
@@ -7,6 +7,7 @@ import com.facebook.react.ReactNativeHost;
 import com.facebook.react.ReactPackage;
 import com.facebook.react.shell.MainReactPackage;
 import com.facebook.soloader.SoLoader;
+import be.smalltownheroes.adobe.analytics.RNAdobeAnalyticsPackage;
 
 import java.util.Arrays;
 import java.util.List;
@@ -22,7 +23,8 @@ public class MainApplication extends Application implements ReactApplication {
     @Override
     protected List<ReactPackage> getPackages() {
       return Arrays.<ReactPackage>asList(
-          new MainReactPackage()
+          new MainReactPackage(),
+          new RNAdobeAnalyticsPackage()
       );
     }
```

### iOS Configuration
#### Manually Install Adobe Mobile SDK
- Add the extracted SDK Files to the folder `ios/AdobeMobileLibrary`.
- Add your JSON Configuration to that same folder.
- Follow the instructions provided by Adobe: https://marketing.adobe.com/resources/help/en_US/mobile/ios/dev_qs.html


#### Install Adobe Mobile SDK via Podfile
Add this to your Podfile and run `pod install`
```
pod 'AdobeMobileSDK', '~> 4.14.1'
```

When using `!use_frameworks` in your Podfile, add this to your `didFinishLaunchingWithOptions` function in AppDelegate.m

```
[ADBMobile overrideConfigPath:[[NSBundle mainBundle] pathForResource:@"ADBMobileConfig" ofType:@"json"]];
```

## Usage
### Javascript API
Import the javascript class:

```
import {AdobeAnalyticsAPI} from 'react-native-adobe-analytics'

AdobeAnalyticsAPI.init()
```

#### Static methods
`init(debug)`

Initializes Adobe Analytics 
- debug: Boolean

`setPrivacyStatus( status )`

Sets the privacy status of the current user. 
- Status: String (OPT_IN|OPT_OUT)

`trackState(state, contextData)`

Track a view or screen in your app
- state: String
- contextData: Object

`trackAction(action, contextData)`

Track an event or an action in your app
- action: String
- contextData: Object


### React components
Initializes Adobe Analytics 
```jsx harmony
<AdobeAnalytics debug={true} />
```

Track a view or screen in your app
```jsx harmony
<AdobeAnalyticsTrackState 
  state="Home screen"
  contextData={{...}}
/>
```

Track an event or an action in your app
```jsx harmony
<AdobeAnalyticsTrackAction 
  action="Logged in"
  contextData={{...}}
/>
```



