# Vst3PluginStarter

Vst3PluginStarter prepares build targets to create new VST3 plugins.

More precisely, Vst3PluginStarter do the steps from 1 to 5 of "How to add/create your own VST 3 Plug-ins" in the VST3 SDK documents.
(see: https://steinbergmedia.github.io/vst3_doc/ -> "VST3 API" -> "How to add/create your own VST 3 Plug-ins")

## Prerequisites

* Java JRE (or JDK) version 8 or later.
* Xcode 10 or later (for macOS).
* Visual Studio 2017 or later (for Windows).

## How to use

```sh
cd /path/to/Vst3PluginStarter/gradle

# Update submodules recursively.
./gradlew update_submodules

# Add a build target to create a new plugin.
# To create a plugin which supports a dedicated plugin editor, set `-Puse_vstgui` as true.
./gradlew add_target -Ptarget_name=<plugin name (*1)> -Puse_vstgui=<true or false>

# `prepare_project` task generates an IDE project file.
# To generate a project file for Visual Studio 2017 instead of Visual Studio 2019, set `-Pmsvc_version="Visual Studio 15 2017"`
./gradlew prepare_project [-Pconfig=<build configuration (*2)>] [-Pmsvc_version=<msvc version>]

# Now the project file is generated as `vstsdk.sln` or `vstsdk.xcodeproj` in the `../build_<build configuration>` directory.
# Open the project file and do the steps from 6 of "How to add/create your own VST 3 Plug-ins" written in the VST3 SDK documents.
# Don't forget replacing the Component ID (i.e. CID) of your plugin.
# (`generate_uuid` task is provided for this purpose.)

# You can build the plugins with both the IDE or the `build` task.
./gradlew build [-Pconfig=<build configuration>]

# The plugin will be created in `../build_<build configuration>/VST3/<build configuration>/`,
# The symbolic link files to the plugins are also created in the user VST3 directory (macOS only)
# (i.e. `~/Library/Audio/Plug-Ins/VST3`).
```

(*1): The plugin name should not contain any whitespaces or tab characters.

(*2): Build configuration is either "Debug", "Release", "MinSizeRel", or "RelWithDebInfo". "Debug" is default.

## Utility task

`generate_uuid` task generates UUIDs and display them with appropriate format for initialising FUID.

```sh
./gradlew generate_uuid [-Pnumber=<n>]
```

Example:
```sh
% ./gradlew generate_uuid -Pnumber=5

> Task :generate_uuid
(0x7c39ecc8, 0x66594d1a, 0xad84aa66, 0x81d88bce)
(0xc1660f69, 0x3c794f85, 0x8cbcdad0, 0x81ffaa94)
(0x0aa84ef0, 0xec014dc5, 0x986aa4f6, 0x085a13a0)
(0xe3d7fc32, 0x2bfd4b94, 0xb6041f5d, 0xfef1de9a)
(0x53aa2b8c, 0x01fc41a2, 0x93c62a6c, 0x458e167e)
```

## Trouble shooting

### `prepare_project` task fails after updating cmake or IDE.

The previous cmake build settings might conflict with new build settings.
Close IDE if opened, and try the following command.

(Caution! this command removes the `build_<build configuration>` directory.)

```sh
./gradlew clean_all [-Pconfig=<build configuration (*2)>]
```

## License

This project is licensed under the MIT license with some exception.

The files in `./plugins/helloworld` and `./plugins/helloworld_with_VSTGUI` are copied from the .zip package version of VST3 SDK version 3.6.13.
Thus the license of the files are same as VST3 SDK.

