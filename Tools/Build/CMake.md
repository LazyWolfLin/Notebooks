# CMake

CMake is an extensible, open-source system that manages the build process in an operating system and in a compiler-independent manner. Unlike many cross-platform systems, CMake is designed to be used in conjunction with the native build environment. Simple configuration files placed in each source directory (called CMakeLists.txt files) are used to generate standard build files (e.g., makefiles on Unix and projects/workspaces in Windows MSVC) which are used in the usual way. 

Version: 3.13

Resource:
* [CMake Tutorial](https://cmake.org/cmake-tutorial/)

## Introduction

## Command

```
Usage

  cmake [options] <path-to-source>
  cmake [options] <path-to-existing-build>
  cmake [options] -S <path-to-source> -B <path-to-build>

Specify a source directory to (re-)generate a build system for it in the
current working directory.  Specify an existing build directory to
re-generate its build system.

Options
  -S <path-to-source>          = Explicitly specify a source directory.
  -B <path-to-build>           = Explicitly specify a build directory.
  -C <initial-cache>           = Pre-load a script to populate the cache.
  -D <var>[:<type>]=<value>    = Create or update a cmake cache entry.
  -U <globbing_expr>           = Remove matching entries from CMake cache.
  -G <generator-name>          = Specify a build system generator.
  -T <toolset-name>            = Specify toolset name if supported by
                                 generator.
  -A <platform-name>           = Specify platform name if supported by
                                 generator.
  -Wdev                        = Enable developer warnings.
  -Wno-dev                     = Suppress developer warnings.
  -Werror=dev                  = Make developer warnings errors.
  -Wno-error=dev               = Make developer warnings not errors.
  -Wdeprecated                 = Enable deprecation warnings.
  -Wno-deprecated              = Suppress deprecation warnings.
  -Werror=deprecated           = Make deprecated macro and function warnings
                                 errors.
  -Wno-error=deprecated        = Make deprecated macro and function warnings
                                 not errors.
  -E                           = CMake command mode.
  -L[A][H]                     = List non-advanced cached variables.
  --build <dir>                = Build a CMake-generated project binary tree.
  --open <dir>                 = Open generated project in the associated
                                 application.
  -N                           = View mode only.
  -P <file>                    = Process script mode.
  --find-package               = Run in pkg-config like mode.
  --graphviz=[file]            = Generate graphviz of dependencies, see
                                 CMakeGraphVizOptions.cmake for more.
  --system-information [file]  = Dump information about this system.
  --debug-trycompile           = Do not delete the try_compile build tree.
                                 Only useful on one try_compile at a time.
  --debug-output               = Put cmake in a debug mode.
  --trace                      = Put cmake in trace mode.
  --trace-expand               = Put cmake in trace mode with variable
                                 expansion.
  --trace-source=<file>        = Trace only this CMake file/module.  Multiple
                                 options allowed.
  --warn-uninitialized         = Warn about uninitialized values.
  --warn-unused-vars           = Warn about unused variables.
  --no-warn-unused-cli         = Don't warn about command line options.
  --check-system-vars          = Find problems with variable usage in system
                                 files.
  --help,-help,-usage,-h,-H,/? = Print usage information and exit.
  --version,-version,/V [<f>]  = Print version number and exit.
  --help-full [<f>]            = Print all help manuals and exit.
  --help-manual <man> [<f>]    = Print one help manual and exit.
  --help-manual-list [<f>]     = List help manuals available and exit.
  --help-command <cmd> [<f>]   = Print help for one command and exit.
  --help-command-list [<f>]    = List commands with help available and exit.
  --help-commands [<f>]        = Print cmake-commands manual and exit.
  --help-module <mod> [<f>]    = Print help for one module and exit.
  --help-module-list [<f>]     = List modules with help available and exit.
  --help-modules [<f>]         = Print cmake-modules manual and exit.
  --help-policy <cmp> [<f>]    = Print help for one policy and exit.
  --help-policy-list [<f>]     = List policies with help available and exit.
  --help-policies [<f>]        = Print cmake-policies manual and exit.
  --help-property <prop> [<f>] = Print help for one property and exit.
  --help-property-list [<f>]   = List properties with help available and
                                 exit.
  --help-properties [<f>]      = Print cmake-properties manual and exit.
  --help-variable var [<f>]    = Print help for one variable and exit.
  --help-variable-list [<f>]   = List variables with help available and exit.
  --help-variables [<f>]       = Print cmake-variables manual and exit.
```

## CMake Language

* Directories (`CMakeLists.txt`)
* Scripts (`<script>.cmake`)
* Modules (`<module>.cmake`)

## CMake Command

### Scripting Commands

These commands are always available.

* [break](https://cmake.org/cmake/help/latest/command/break.html)
* [cmake_host_system_information](https://cmake.org/cmake/help/latest/command/cmake_host_system_information.html)
* [cmake_minimum_required](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html)
* [cmake_parse_arguments](https://cmake.org/cmake/help/latest/command/cmake_parse_arguments.html)
* [cmake_policy](https://cmake.org/cmake/help/latest/command/cmake_policy.html)
* [configure_file](https://cmake.org/cmake/help/latest/command/configure_file.html)
* [continue](https://cmake.org/cmake/help/latest/command/continue.html)
* [elseif](https://cmake.org/cmake/help/latest/command/elseif.html)
* [else](https://cmake.org/cmake/help/latest/command/else.html)
* [endforeach](https://cmake.org/cmake/help/latest/command/endforeach.html)
* [endfunction](https://cmake.org/cmake/help/latest/command/endfunction.html)
* [endif](https://cmake.org/cmake/help/latest/command/endif.html)
* [endmacro](https://cmake.org/cmake/help/latest/command/endmacro.html)
* [endwhile](https://cmake.org/cmake/help/latest/command/endwhile.html)
* [execute_process](https://cmake.org/cmake/help/latest/command/execute_process.html)
* [file](https://cmake.org/cmake/help/latest/command/file.html)
* [find_file](https://cmake.org/cmake/help/latest/command/find_file.html)
* [find_library](https://cmake.org/cmake/help/latest/command/find_library.html)
* [find_package](https://cmake.org/cmake/help/latest/command/find_package.html)
* [find_path](https://cmake.org/cmake/help/latest/command/find_path.html)
* [find_program](https://cmake.org/cmake/help/latest/command/find_program.html)
* [foreach](https://cmake.org/cmake/help/latest/command/foreach.html)
* [function](https://cmake.org/cmake/help/latest/command/function.html)
* [get_cmake_property](https://cmake.org/cmake/help/latest/command/get_cmake_property.html)
* [get_directory_property](https://cmake.org/cmake/help/latest/command/get_directory_property.html)
* [get_filename_component](https://cmake.org/cmake/help/latest/command/get_filename_component.html)
* [get_property](https://cmake.org/cmake/help/latest/command/get_property.html)
* [if](https://cmake.org/cmake/help/latest/command/if.html)
* [include](https://cmake.org/cmake/help/latest/command/include.html)
* [include_guard](https://cmake.org/cmake/help/latest/command/include_guard.html)
* [list](https://cmake.org/cmake/help/latest/command/list.html)
* [macro](https://cmake.org/cmake/help/latest/command/macro.html)
* [mark_as_advanced](https://cmake.org/cmake/help/latest/command/mark_as_advanced.html)
* [math](https://cmake.org/cmake/help/latest/command/math.html)
* [message](https://cmake.org/cmake/help/latest/command/message.html)
* [option](https://cmake.org/cmake/help/latest/command/option.html)
* [return](https://cmake.org/cmake/help/latest/command/return.html)
* [separate_arguments](https://cmake.org/cmake/help/latest/command/separate_arguments.html)
* [set_directory_properties](https://cmake.org/cmake/help/latest/command/set_directory_properties.html)
* [set_property](https://cmake.org/cmake/help/latest/command/set_property.html)
* [set](https://cmake.org/cmake/help/latest/command/set.html)
* [site_name](https://cmake.org/cmake/help/latest/command/site_name.html)
* [string](https://cmake.org/cmake/help/latest/command/string.html)
* [unset](https://cmake.org/cmake/help/latest/command/unset.html)
* [variable_watch](https://cmake.org/cmake/help/latest/command/variable_watch.html)
* [while](https://cmake.org/cmake/help/latest/command/while.html)

### Project Commands

These commands are available only in CMake projects.

* [add_compile_definitions](https://cmake.org/cmake/help/latest/command/add_compile_definitions.html)
* [add_compile_options](https://cmake.org/cmake/help/latest/command/add_compile_options.html)
* [add_custom_command](https://cmake.org/cmake/help/latest/command/add_custom_command.html)
* [add_custom_target](https://cmake.org/cmake/help/latest/command/add_custom_target.html)
* [add_definitions](https://cmake.org/cmake/help/latest/command/add_definitions.html)
* [add_dependencies](https://cmake.org/cmake/help/latest/command/add_dependencies.html)
* [add_executable](https://cmake.org/cmake/help/latest/command/add_executable.html)
* [add_library](https://cmake.org/cmake/help/latest/command/add_library.html)
* [add_link_options](https://cmake.org/cmake/help/latest/command/add_link_options.html)
* [add_subdirectory](https://cmake.org/cmake/help/latest/command/add_subdirectory.html)
* [add_test](https://cmake.org/cmake/help/latest/command/add_test.html)
* [aux_source_directory](https://cmake.org/cmake/help/latest/command/aux_source_directory.html)
* [build_command](https://cmake.org/cmake/help/latest/command/build_command.html)
* [create_test_sourcelist](https://cmake.org/cmake/help/latest/command/create_test_sourcelist.html)
* [define_property](https://cmake.org/cmake/help/latest/command/define_property.html)
* [enable_language](https://cmake.org/cmake/help/latest/command/enable_language.html)
* [enable_testing](https://cmake.org/cmake/help/latest/command/enable_testing.html)
* [export](https://cmake.org/cmake/help/latest/command/export.html)
* [fltk_wrap_ui](https://cmake.org/cmake/help/latest/command/fltk_wrap_ui.html)
* [get_source_file_property](https://cmake.org/cmake/help/latest/command/get_source_file_property.html)
* [get_target_property](https://cmake.org/cmake/help/latest/command/get_target_property.html)
* [get_test_property](https://cmake.org/cmake/help/latest/command/get_test_property.html)
* [include_directories](https://cmake.org/cmake/help/latest/command/include_directories.html)
* [include_external_msproject](https://cmake.org/cmake/help/latest/command/include_external_msproject.html)
* [include_regular_expression](https://cmake.org/cmake/help/latest/command/include_regular_expression.html)
* [install](https://cmake.org/cmake/help/latest/command/install.html)
* [link_directories](https://cmake.org/cmake/help/latest/command/link_directories.html)
* [link_libraries](https://cmake.org/cmake/help/latest/command/link_libraries.html)
* [load_cache](https://cmake.org/cmake/help/latest/command/load_cache.html)
* [project](https://cmake.org/cmake/help/latest/command/project.html)
* [qt_wrap_cpp](https://cmake.org/cmake/help/latest/command/qt_wrap_cpp.html)
* [qt_wrap_ui](https://cmake.org/cmake/help/latest/command/qt_wrap_ui.html)
* [remove_definitions](https://cmake.org/cmake/help/latest/command/remove_definitions.html)
* [set_source_files_properties](https://cmake.org/cmake/help/latest/command/set_source_files_properties.html)
* [set_target_properties](https://cmake.org/cmake/help/latest/command/set_target_properties.html)
* [set_tests_properties](https://cmake.org/cmake/help/latest/command/set_tests_properties.html)
* [source_group](https://cmake.org/cmake/help/latest/command/source_group.html)
* [target_compile_definitions](https://cmake.org/cmake/help/latest/command/target_compile_definitions.html)
* [target_compile_features](https://cmake.org/cmake/help/latest/command/target_compile_features.html)
* [target_compile_options](https://cmake.org/cmake/help/latest/command/target_compile_options.html)
* [target_include_directories](https://cmake.org/cmake/help/latest/command/target_include_directories.html)
* [target_link_directories](https://cmake.org/cmake/help/latest/command/target_link_directories.html)
* [target_link_libraries](https://cmake.org/cmake/help/latest/command/target_link_libraries.html)
* [target_link_options](https://cmake.org/cmake/help/latest/command/target_link_options.html)
* [target_sources](https://cmake.org/cmake/help/latest/command/target_sources.html)
* [try_compile](https://cmake.org/cmake/help/latest/command/try_compile.html)
* [try_run](https://cmake.org/cmake/help/latest/command/try_run.html)

### CTest Commands

These commands are available only in CTest scripts.

* [ctest_build](https://cmake.org/cmake/help/latest/command/ctest_build.html)
* [ctest_configure](https://cmake.org/cmake/help/latest/command/ctest_configure.html)
* [ctest_coverage](https://cmake.org/cmake/help/latest/command/ctest_coverage.html)
* [ctest_empty_binary_directory](https://cmake.org/cmake/help/latest/command/ctest_empty_binary_directory.html)
* [ctest_memcheck](https://cmake.org/cmake/help/latest/command/ctest_memcheck.html)
* [ctest_read_custom_files](https://cmake.org/cmake/help/latest/command/ctest_read_custom_files.html)
* [ctest_run_script](https://cmake.org/cmake/help/latest/command/ctest_run_script.html)
* [ctest_sleep](https://cmake.org/cmake/help/latest/command/ctest_sleep.html)
* [ctest_start](https://cmake.org/cmake/help/latest/command/ctest_start.html)
* [ctest_submit](https://cmake.org/cmake/help/latest/command/ctest_submit.html)
* [ctest_test](https://cmake.org/cmake/help/latest/command/ctest_test.html)
* [ctest_update](https://cmake.org/cmake/help/latest/command/ctest_update.html)
* [ctest_upload](https://cmake.org/cmake/help/latest/command/ctest_upload.html)