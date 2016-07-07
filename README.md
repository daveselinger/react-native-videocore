# react-native-videocore
> A React Native module for the [VideoCore](https://github.com/jgh-/VideoCore) iOS library.


## Getting started

1. `npm install react-native-videocore@latest --save`
2. Right click on your project on Xcode and then ➜ `Add Files to [your project's name]`
3. Go to `node_modules/react-native-videocore/ios/RNVideoCore` and add `RCTVideoCore`
4. Add [VideoCore](https://github.com/jgh-/VideoCore) to your Podfile. If you don't have a Podfile yet see the instructions below
5. Run your project


## Usage

All you need is to require the `react-native-videocore` module and then use the <VideoCore /> tag.

```javascript

import React from 'react';
import {
  AppRegistry,
  Stylesheet,
  Text,
  View,
  TouchableHighlight
} from 'react-native';

var VideoCore = require('react-native-videocore')

class VideoCoreSampleApp {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <View style={styles.container}>
        <VideoCore style={{ alignSelf: 'stretch', flex: 1 }} onConnectionStatusChanged={(e) => console.log(e)}>
          <TouchableHighlight onPress={() => VideoCore.startStreaming('rtmp://104.155.71.82:1935/live', 'myStream')}><Text style={{color: "#fff", margin: 50}}>START Streaming</Text></TouchableHighlight>
          <TouchableHighlight onPress={() => VideoCore.stopStreaming()}><Text style={{color: "#fff", margin: 50}}>STOP Streaming</Text></TouchableHighlight>
        </VideoCore>
      </View>
    );
  }
}

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  }
});

AppRegistry.registerComponent('VideoCoreSampleApp', () => VideoCoreSampleApp);

```

## Properties

#### `onConnectionStatusChanged`
Will call the specified method when VideoCore connection status has changed.

Possible values:

- VCSessionStateStarting
- VCSessionStateStarted
- VCSessionStateError
- VCSessionStateEnded
- VCSessionStateNone
- VCSessionStatePreviewStarted

Ex:

```javascript
<VideoCore onConnectionStatusChanged={ (state) => console.log('Current state: ' + state) } />
```

## I don't have a Podfile

#### 1. Create a Podfile inside the `ios` folder

```
platform :ios, '9.0'

source 'https://github.com/CocoaPods/Specs.git'

# See: http://guides.cocoapods.org/making/making-a-cocoapod.html#release
# Once the pod has been released, use a version number here instead of a path.
pod 'VideoCore', :git => 'https://github.com/phelrine/VideoCore.git', :branch => 'fixed-master'
```

As you can see, I actually use a fork which has some bugs already fixed.

#### 2. Install Cocoapods and the dependencies
Inside `ios` folder run: `sudo gem install cocoapods && pod install`
Note: you must use the most recent version (1.0.1 as of writing) because the originally documented versions of Cocoapod has bugs

#### 3. Go to the Build Settings of your Xcode project and search for Linking
In the ios folder run: `rnpm link react-native-videocore`
Open XCode and on the Other Linker Flags of your parent project, make sure you have `-ObjC` and `$(inherited)` on the list


## Known Issues
- Only works with landscape orientation
- Only works with CocoaPods < 0.37.2


-------------
Thanks to Loch Wansbrough (@lwansbrough) for the react-native-camera module which provided me with a great example of how to set up this module.
