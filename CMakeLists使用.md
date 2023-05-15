CMakeLists使用

Exercise1 - Building a Basic Project

CMakeLists.txt

## cmake_version

Any project's top most CMakeLists.txt must start by specifying a minimum CMake version using the [`cmake_minimum_required()`](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html#command:cmake_minimum_required) command. This establishes policy settings and ensures that the following CMake functions are run with a compatible version of CMake.

`cmake_minimum_required`

Require a minimum version of cmake.

语法：

```
cmake_minimum_required(VERSION <min>[...<policy_max>] [FATAL_ERROR])
```

*New in version 3.12:* The optional `<policy_max>` version.

This command will set the value of the [`CMAKE_MINIMUM_REQUIRED_VERSION`](https://cmake.org/cmake/help/latest/variable/CMAKE_MINIMUM_REQUIRED_VERSION.html#variable:CMAKE_MINIMUM_REQUIRED_VERSION) variable to `<min>`.

Sets the minimum required version of cmake for a project. Also updates the policy settings as explained below.

`<min>` and the optional `<policy_max>` are each CMake versions of the form `major.minor[.patch[.tweak]]`, and the `...` is literal.

- If the running version of CMake is lower than the `<min>` required version it will stop processing the project and report an error. 
- The optional `<policy_max>` version, if specified, must be at least the `<min>` version and affects policy settings as described in [Policy Settings](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html#policy-settings). If the running version of CMake is older than 3.12, the extra `...` dots will be seen as version component separators, resulting in the `...<max>` part being ignored and preserving the pre-3.12 behavior of basing policies on `<min>`.

```cmake
# TODO 1: Set the minimum required version of CMake to be 3.10
cmake_minimum_required(VERSION 3.10)
```





## project name

To start a project, we use the [`project()`](https://cmake.org/cmake/help/latest/command/project.html#command:project) command to set the project name. This call is required with every project and should be called soon after [`cmake_minimum_required()`](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html#command:cmake_minimum_required). As we will see later, this command can also be used to specify other project level information such as the language or version number.

`project`：Set the name of the project.

Synopsis

```
project(<PROJECT-NAME> [<language-name>...])
project(<PROJECT-NAME>
        [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [DESCRIPTION <project-description-string>]
        [HOMEPAGE_URL <url-string>]
        [LANGUAGES <language-name>...])
```

Sets the name of the project, and stores it in the variable [`PROJECT_NAME`](https://cmake.org/cmake/help/latest/variable/PROJECT_NAME.html#variable:PROJECT_NAME). When called from the top-level `CMakeLists.txt` also stores the project name in the variable [`CMAKE_PROJECT_NAME`](https://cmake.org/cmake/help/latest/variable/CMAKE_PROJECT_NAME.html#variable:CMAKE_PROJECT_NAME).

Also sets the variables:

- [`PROJECT_SOURCE_DIR`](https://cmake.org/cmake/help/latest/variable/PROJECT_SOURCE_DIR.html#variable:PROJECT_SOURCE_DIR), [`_SOURCE_DIR`](https://cmake.org/cmake/help/latest/variable/PROJECT-NAME_SOURCE_DIR.html#variable:_SOURCE_DIR)

  Absolute path to the source directory for the project.

- [`PROJECT_BINARY_DIR`](https://cmake.org/cmake/help/latest/variable/PROJECT_BINARY_DIR.html#variable:PROJECT_BINARY_DIR), [`_BINARY_DIR`](https://cmake.org/cmake/help/latest/variable/PROJECT-NAME_BINARY_DIR.html#variable:_BINARY_DIR)

  Absolute path to the binary directory for the project.

- [`PROJECT_IS_TOP_LEVEL`](https://cmake.org/cmake/help/latest/variable/PROJECT_IS_TOP_LEVEL.html#variable:PROJECT_IS_TOP_LEVEL), [`_IS_TOP_LEVEL`](https://cmake.org/cmake/help/latest/variable/PROJECT-NAME_IS_TOP_LEVEL.html#variable:_IS_TOP_LEVEL)

  *New in version 3.21.*

  Boolean value indicating whether the project is top-level.

```cmake
# TODO 2: Create a project named Tutorial
project(Tutorial)
```





## add_executable

Finally, the [`add_executable()`](https://cmake.org/cmake/help/latest/command/add_executable.html#command:add_executable) command tells CMake to create an executable using the specified source code files.

`add_executable`: Add an executable to the project using the specified source files.

- [Normal Executables](https://cmake.org/cmake/help/latest/command/add_executable.html#normal-executables)

```
add_executable(<name> [WIN32] [MACOSX_BUNDLE]
               [EXCLUDE_FROM_ALL]
               [source1] [source2 ...])
```

Adds an executable target called `<name>` to be built from the source files listed in the command invocation. The `<name>` corresponds to the logical target name and must be globally unique within a project. The actual file name of the executable built is constructed based on conventions of the native platform (such as `<name>.exe` or just `<name>`).



- [Imported Executables](https://cmake.org/cmake/help/latest/command/add_executable.html#imported-executables)
- [Alias Executables](https://cmake.org/cmake/help/latest/command/add_executable.html#alias-executables)
- [See Also](https://cmake.org/cmake/help/latest/command/add_executable.html#see-also)

```cmake
# TODO 3: Add an executable called Tutorial to the project
# Hint: Be sure to specify the source file as tutorial.cxx
add_executable(Tutorial tutorial.cxx)
```



##  Specifying the C++ Standard

 [`CMAKE_CXX_STANDARD`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD.html#variable:CMAKE_CXX_STANDARD) and [`CMAKE_CXX_STANDARD_REQUIRED`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD_REQUIRED.html#variable:CMAKE_CXX_STANDARD_REQUIRED). 

These may be used together to specify the C++ standard needed to build the project.

One way to enable support for a specific C++ standard in CMake is by using the [`CMAKE_CXX_STANDARD`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD.html#variable:CMAKE_CXX_STANDARD) variable. 

例如：Add a feature that requires C++11.

- set the [`CMAKE_CXX_STANDARD`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD.html#variable:CMAKE_CXX_STANDARD) variable in the `CMakeLists.txt` file to `11` 
  - `set(CMAKE_CXX_STANDARD 11)`

- and [`CMAKE_CXX_STANDARD_REQUIRED`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD_REQUIRED.html#variable:CMAKE_CXX_STANDARD_REQUIRED) to `True`. 
  - `set(CMAKE_CXX_STANDARD_REQUIRED True)`

Make sure to add the [`CMAKE_CXX_STANDARD`](https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD.html#variable:CMAKE_CXX_STANDARD) declarations above the call to [`add_executable()`](https://cmake.org/cmake/help/latest/command/add_executable.html#command:add_executable).

```cmake
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```

