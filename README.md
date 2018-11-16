cmake-example-library
=====================

This is an example of how to install a library with CMake, and then use
`find_package()` command to find it.

In this example, Foo is the library and Bar a binary (which uses the library).

The **advantage** of this example is that it is auto-generated. You only need to change
the *project name*.

It is based on the these two examples:
  * [How to create a ProjectConfig.cmake file (cmake.org)]
    (http://www.cmake.org/Wiki/CMake/Tutorials/How_to_create_a_ProjectConfig.cmake_file)
  * [How to install a library (kde.org)]
    (https://projects.kde.org/projects/kde/kdeexamples/repository/revisions/master/show/buildsystem/HowToInstallALibrary)

### How to create a library from this example?

Follow these steps:

  * Copy files in a new folder.

  * Change project name in the top-level `CMakeLists.txt`.

  * [Optional] Set variables: `LIBRARY_NAME` and `LIBRARY_FOLDER`.
    If it is not set explicitally, project name in lowercase will be used.
    See `cmake/SetEnv.cmake` file to see the implementation details.

  * [Optional] 'examples/' folder can be removed, it is the 'bar' example.
    In this case, remove the 'add_subdirectory(examples)' too.

### How to compile?

Assume the following settings:

    project(Foo)
    ...
    set(LIBRARY_NAME foo)   # [optional] generated automatically (in lowercase)
    set(LIBRARY_FOLDER foo) # [optional] generated automatically (in lowercase)

Example of a local installation:

    > mkdir build
    > cd build
    > cmake -DCMAKE_INSTALL_PREFIX=../installed ..
    > make install

Installed files:

    > tree ../installed

    ├── bin
    │   └── bar
    ├── include
    │   └── foo
    │       ├── foo.h
    │       └── version.h
    └── lib
        ├── CMake
        │   └── Foo
        │       ├── FooConfig.cmake
        │       ├── FooConfigVersion.cmake
        │       ├── FooTargets.cmake
        │       └── FooTargets-noconfig.cmake
        └── libfoo.so

Unintall library:

    > make uninstall

### How to use the library (internally)?

See the [bar example](examples/).

### How to use the library (in an external project)?

Once the library is installed, CMake will be able to find it using
`find_package()` command. For example:
```
    cmake_minimum_required(VERSION 2.6)
    project(Bar)

    find_package(Foo REQUIRED)
    # use PROJECT_NAME_UPPERCASE_LIBRARIES
    include_directories(${FOO_INCLUDE_DIRS})

    add_executable(bar bar.cpp)
    target_link_libraries(bar ${FOO_LIBRARIES})
```
Could not find a package configuration file provided by [project]
set prefix in ~/.bashrc
```
export CMAKE_PREFIX_PATH=/path/cmake
```