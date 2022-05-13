# Running maplibre-rs demos on various platforms

During development, you will want to run the maplibre demos on your local machine to test out your changes. 
There are multiple demos of maplibre-rs for different targets. Some targets have prerequisites 
depending on your operating system.

* **Maplibre-demo** - targets Windows, MacOS and Linux, it is built directly with cargo.
* **Apple** - targets iOS and MacOS and relies on the xcode IDE.
* **Android** - targets Android devices and builds in Android Studio.
* **Web** - targets the web using a WASM binary.

All of the targets below require you to install [rustup](https://rustup.rs/) to manage your Rust toolchain.

> __Note__: Make sure you have selected the right toolchain target within rustup. You can use `rustup show` to see your
> active toolchain. If you want to change the target of the build manually, use the cargo `--target` parameter.

## Maplibre-demo

### Linux/MacOS

The build for desktop is very simple, you just have to run the following command from the root of the 
maplibre-rs project:

```bash
cargo run -p maplibre-demo
```

### Windows

Windows has two additional prerequisites to be able to run. You will need CMake, Visual Studio c++ build tools and the
sqlite3.lib within your $PATH.

Install [CMake](https://cmake.org/download/) and add it to your $PATH.

For the c++ build tools, download the [Visual Studio 2022 Build tools](https://visualstudio.microsoft.com/downloads/) 
from the Microsoft website. After the download, while installing the Build tools, make sure that you select the
*c++ build tools*.

To install sqlite3 you need to build the sqlite3.lib manually with the following 
[steps](https://gist.github.com/zeljic/d8b542788b225b1bcb5fce169ee28c55). This will generate a .lib file that
you will have to add to your $PATH.

Restart your shell to make sure you are using the new $PATH variables.

Finally, the command below should execute successfully:

```bash
cargo run -p maplibre-demo
```

## Android

You should make sure that a recent Android NDK is installed. You will need to set the `ANDROID_NDK_ROOT` variable
to something like this:

```bash
export ANDROID_NDK_ROOT=$HOME/android-sdk/ndk/23.1.7779620/
```

After that you can run the build the library:

``bash
just build-android
``

## Apple

### iOS

In order to run this app on iOS you have to open the Xcode project at `./apple/xcode`.
You can then run the app on an iOS Simulator or a real device. During the Xcode build process cargo is used to build
a static library for the required architecture.

## MacOS

You can build Unix Executables for MacOS, as explained in the first section. if you want to build a proper 
MacOS application (in OSX terminology), you will need to use the XCode project in the folder `./apple/xcode/`.

Install [XCode](https://apps.apple.com/us/app/xcode/id497799835?ls=1&mt=12).
Then open the project from the folder `./apple/xcode` with XCode. Select the scheme called *example(macOS)* and
click on *Product -> Build for -> Running*. This will build the MacOS application for the version of OSX defined
in the Build Settings. The XCode project is configured to automatically compile the Rust library with the correct target
in the *Cargo Build* build phases configuration.

If you want to run the project from XCode, you need to make sure that you have selected the version of OSX which
corresponds to your system. Otherwise, XCode will tell you that the app is incompatible with the current version of macOS.
In order to change that, go into *Build settings -> Deployment -> MacOS deployment target* and select your OSX version.
Finally, you can click on the run button to start the application.

## Web (WebGL, WebGPU)

If you have a browser which already supports a recent version of the WebGPU specification then you can start a
development server using the following commands.

```bash
cd web
npm run start
```

If you want to run maplibre-rs with WebGL which is supported on every major browser, then you have to use the following
command.

```bash
npm run webgl-start
```