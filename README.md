# Vst3PluginStarter

## How to use

```sh
cd gradle

# update submodules
./gradlew update_submodules

# add build target to create a new plugin.
# To create a plugin which supports a dedicated plugin editor, set `-Puse_vstgui=true`.
./gradlew add_target -Ptarget_name=MyPlugin [-Puse_vstgui=true]

# `prepare_project` task generates an IDE project file.
# To generate a project file for Visual Studio 2017 instead of Visual Studio 2019, set `-Pmsvc_version="Visual Studio 15 2017"`
./gradlew prepare_project [-Pmsvc_version=<msvc version>]

# Now the project file is generated.
# Open the project and modify it in the IDE or in your preferred text editor.
# Don't forget to replace class ids of your plugin.
# (`generate_uuid` task is provided for this purpose.)

# You can build the plugins with both the IDE or the `build` task.
./gradlew build
```

## utility task

```sh
# generate VST-MA ids which are formatted to pass to a constructor of FUID.
./gradlew generate_uuid
```

## License

This project is licensed under the MIT license with some exception.

The files in `./plugins/helloworld` and `./plugins/helloworld_with_VSTGUI` are copied from the .zip package version of VST3 SDK version 3.6.13.
Thus the license of the files are same as VST3 SDK.

