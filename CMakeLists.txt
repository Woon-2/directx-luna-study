# *****************************
# Copylight @Woon2
# (wkdauddns9@gmail.com)
# Simple script for building DirectX12 Project
# *****************************

cmake_minimum_required(VERSION 3.18)

if(NOT DEFINED CMAKE_CONFIGURATION_TYPES)
    message(STATUS "setting CMAKE_CONFIGURATION_TYPES to 'Debug;Release'
        (default configuration types) as none was specified.")
    set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING
        "Set the project configuration types." FORCE)
endif()

if(NOT DEFINED CMAKE_BUILD_TYPE)
    message(STATUS "setting CMAKE_BUILD_TYPE to Release(default build type)
        as none was specified.")
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the build type." FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE
        PROPERTY STRINGS "Debug" "Release")
endif()

if(NOT DEFINED CMAKE_INSTALL_PREFIX)
    message(STATUS "setting CMAKE_INSTALL_PREFIX to
        ${CMAKE_CURRENT_SOURCE_DIR}/install(default install prefix)
        as none was specified.")
    set(CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_SOURCE_DIR}/install" CACHE FILEPATH
        "Set path to install.")
endif()

project(DirectX_Study VERSION 2023.05.21)

message(STATUS "configuring DirectX_Study(v${CMAKE_PROJECT_VERSION})...")
message("Author: @Woon2 (wkdauddns9@gmail.com)")