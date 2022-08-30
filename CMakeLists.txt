cmake_minimum_required(VERSION 3.0)
project(volume-mixer-applet)


## cmake modules
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")
include(FindPkgConfig)
include(GNUInstallDirs)
include(PNMixer_macros)


## version and global project vars
set(PNMixer_VERSION_MAJOR 0)
set(PNMixer_VERSION_MINOR 7)
set(PNMixer_VERSION_MICRO 2)
set(PACKAGE_VERSION "${PNMixer_VERSION_MAJOR}.${PNMixer_VERSION_MINOR}.${PNMixer_VERSION_MICRO}")
set(PACKAGE "volume-mixer-applet")

# https://github.com/nicklan/pnmixer/issues/178
if (CMAKE_BUILD_TYPE STREQUAL Release)
	set(DATA_IN_CWD_default OFF)
else()
	set(DATA_IN_CWD_default ON)
endif()
option(DATA_IN_CWD "Whether to also look for data files in the current directory" ${DATA_IN_CWD_default})

## subdirectories
add_subdirectory(data)
add_subdirectory(src)


## additional global targets

# indent-code
add_custom_target(indent-code
	COMMAND "${CMAKE_SOURCE_DIR}/cmake/scripts/astyle.sh"
	WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}")

# indent-xml
add_custom_target(indent-xml
	COMMAND "${CMAKE_SOURCE_DIR}/cmake/scripts/xmllint.sh"
	WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}")


## install git hook
execute_process(
	COMMAND "${CMAKE_SOURCE_DIR}/cmake/scripts/install-git-hook.sh"
	WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}")

