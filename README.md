
# react-native-static-server

A cross platform component for serving static assets with React Native.

## Getting started

`$ npm install react-native-static-server --save`

### Mostly automatic installation

`$ react-native link react-native-static-server`

### Manual installation


#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-static-server` and add `FPStaticServer.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libFPStaticServer.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.reactlibrary.FPStaticServerPackage;` to the imports at the top of the file
  - Add `new FPStaticServerPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-static-server'
  	project(':react-native-static-server').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-static-server/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-static-server')
  	```

## Usage

Declare the `StaticServer` with a port or use the default `9999`

```javascript
import StaticServer from 'react-native-static-server';

let server = new StaticServer(8080);

// Start the server
server.start().then((url) => {
  console.log("Serving at URL", url);
});

// Stop the server
server.stop();
```

`StaticServer` serves from the document directory or takes an optional absolute path to serve from.
For instance, using [react-native-fs](https://github.com/johanneslumpe/react-native-fs) you can get the document directory and specify a directory from there.

```javascript
import StaticServer from 'react-native-static-server';
import RNFS from 'react-native-fs';

// create a path you want to write to
let path = RNFS.DocumentDirectoryPath + '/www';

let server = new StaticServer(8080, path);
```

If the server should only be accessible from within the app, set `localOnly` to `true`

```javascript
import StaticServer from 'react-native-static-server';

// Just set options with defaults
let server = new StaticServer({localOnly : true });
// Or also valid are:
let server = new StaticServer(8080, {localOnly : true });
let server = new StaticServer(8080, path, {localOnly : true });

```

## Credits

* iOS server: [CocoaHTTPServer](https://github.com/robbiehanson/CocoaHTTPServer)
* Android server: [NanoHttpd Webserver](https://github.com/NanoHttpd/nanohttpd)

Thanks to [CorHttpd](https://github.com/floatinghotpot/cordova-httpd) and [react-native-httpserver](https://gitlab.com/base.io/react-native-httpserver#README) for the basis of this library.
