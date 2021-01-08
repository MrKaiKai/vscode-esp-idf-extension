# ESP-IDF Extension features for Visual Studio Code

This extension provides many features to ease development of ESP-IDF Projects.

- Quick [Configure ESP-IDF extension](./SETUP.md) for first time user to help you download, install and setup ESP-IDF and required tools within Visual Studio Code extension.
- Quick prototyping by copying ESP-IDF examples with **ESP-IDF: Show ESP-IDF Examples Projects**.
- Syntax highlighting for [KConfig](#Kconfig-files-editor) and ESP-IDF Kconfig style syntax validation if `idf.useIDFKconfigStyle` is enabled.
- GUI [SDK Configuration editor](#SDK-Configuration-editor) to configure your ESP-IDF project (esp-idf menuconfig).
- [Partition table editor](./PARTITION_TABLE_EDITOR.md)
- [NVS Partition editor](./NVS_PARTITION_EDITOR.md)
- Easily Build, Flash and Monitor your code for the ESP-32 and ESP32 S2 chip.
- OpenOCD server within Visual Studio Code.
- [DEBUGGING](./DEBUGGING.md) with [ESP-IDF Debug Adapter](https://github.com/espressif/esp-debug-adapter).
- Size analysis of binaries with **ESP-IDF: Size analysis of the binaries**.
- App tracing when using ESP-IDF Application Level Tracing Library like in [ESP-IDF Application Level Tracing Example](https://github.com/espressif/esp-idf/tree/master/examples/system/app_trace_to_host).
- [Heap tracing](./HEAP_TRACING.md)
- [System view tracing viewer](./SYS_VIEW_TRACING_VIEWER.md)
- Localization (English, Chinese, Spanish) of commands which you can also [add a language contribution](./LANG_CONTRIBUTE.md).
- [Code Coverage](./COVERAGE.md) for editor source highlighting and generate HTML reports.
- Search text editor's selected text in ESP-IDF documentation with **ESP-IDF: Search in documentation...** right click command or with its [keyboard shortcut](#Available-commands). Results will be shown in ESP-IDF Explorer Tab if found on ESP-IDF Documentation based on your current vscode language, ESP-IDF version in `idf.espIdfPath` (latest otherwise) and `idf.adapterTargetName`.
- [Rainmaker integration](./ESP_RAINMAKER.md)
- [Core dump and GdbStub](./POSTMORTEM.md) postmortem mode.
- [CMake Editor](#CMake-Editor)
- [Support for WSL 2](./WSL.md)

## Code Coverage

We provide editor code coverage highlight and HTML reports for ESP-IDF projects, if coverage files are generated on a ESP-IDF project's build directory. For more info please take a look at [Code Coverage](./COVERAGE.md).

## Debugging

Click <kbd>F5</kbd> to start debugging. To configure the debug behaviour, please review [DEBUGGING](./DEBUGGING.md). If mode is set to `auto`, OpenOCD Server is launched by the extension and the output is shown in the `OpenOCD` Output window.

> **NOTE** For correct debug experience, first `build`, `flash` your device and define the correct `idf.customExtraPaths` paths and `idf.customExtraVars` using [SETUP](./SETUP.md).

## CMake Editor

On CMakeLists.txt file right click this extension provides a custom CMake Editor to fill our ESP-IDF Project and Component registration as specified in [ESP-IDF Project CMakeLists.txt](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#project-cmakelists-file) and [ESP-IDF Component CMakeLists.txt files](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#component-cmakelists-files). You need to choose which kind of CMakeLists.txt file (project or component) to edit. There is 2 types of input, one is a simple string and another is an array of strings, such as Component Sources (SRCS). All inputs are described in the CMakeLists.txt Schema (\${this_repository}/src/cmake/cmakeListsSchema.json).

## ESP Rainmaker Support

We support connecting, viewing and editing of ESP Rainmaker enabled devices out of the box, please [refer here](./ESP_RAINMAKER.md) for more info.

## Kconfig files editor

When you open a `Kconfig`, `Kconfig.projbuild` or `Kconfig.in` file we provide syntax highlighting. If `idf.useIDFKconfigStyle` is enabled, we also provide ESP-IDF Kconfig style syntax validation such as indent validation and not closing blocks found (Example: menu-endmenu). Please review [Kconfig Formatting Rules](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/kconfig.html) and [Kconfig Language](https://github.com/espressif/esp-idf/blob/master/tools/kconfig/kconfig-language.txt) for further details about the ESP-IDF Kconfig formatting rules and Kconfig language in general.

## Log & Heap Tracing

We support [log](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/app_trace.html) and [heap tracing](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/system/heap_debug.html) out of the box, which enables users to perform log/heap tracing with just few button clicks and present the results of tracing data with UI.

You can follow [this](./HEAP_TRACING.md) quick step-by-step guide for heap tracing.

## SDK Configuration editor

This plugin includes a GUI menuconfig that reads your current project folder's sdkconfig file (if available, otherwise it would take default values) and start a configuration server process (confserver.py in **\${ESP-IDF-DIRECTORYPATH}**/tools) that enables the user to redefine ESP-IDF board parameters.

When the user modify a parameter value, the value is send to the confserver.py process, which return the new value and other values modified to GUI menuconfig and then update the values in the UI.

Values are not automatically saved to the sdkconfig file until you click save changes. You can cancel any changes and load the values from the sdkconfig file by clicking cancel changes. If you click set default the current sdkconfig file is replaced by a template sdkconfig file and then loaded into the GUI menuconfig rendered values.

The search functionality allows to find a parameter by description, i.e the name that appears in the sdkconfig file.

An IDF GUI Menuconfig log in Output is created to print all communications with `${idf.espIdfPath}\tools\confserver.py`. It can be be used to track any errors.

## System View Tracing Viewer

We have provide a [system view tracing viewer](./SYS_VIEW_TRACING_VIEWER.md) inside the vscode extension which will enable you to view the traces along with other relevant details.
