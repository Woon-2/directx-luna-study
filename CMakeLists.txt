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

function(COMMON_CONFIGURATION targetName)
    # See below link for finding GCC options.
    # https://gcc.gnu.org/onlinedocs/gcc/Option-Summary.html
    if(CMAKE_CXX_COMPILER_ID MATCHES GNU)
        target_compile_options(${targetName}
        PRIVATE
            -fconcepts
            -Wall
            -pedantic
            -Wextra
        )

    # See below link for finding Clang options.
    # https://clang.llvm.org/docs/ClangCommandLineReference.html
    elseif(CMAKE_CXX_COMPILER_ID MATCHES CLANG)
        # Clang options differ by platform.
        if(WIN32)   # clang-cl
            target_compile_options(${targetName}
            PRIVATE
                "/clang:-fcoroutines-ts"
                -fms-compatiability)
        else()  # AppleClang or Clang on Linux
            target_compile_options(${targetName}
            PRIVATE
                -std=c++2a
            )
        endif()

    # See below link for finding MSVC options.
    # https://docs.microsoft.com/en-us/cpp/build/reference/compiler-options-listed-by-category?view=msvc-160
    elseif(CMAKE_CXX_COMPILER_ID MATCHS MSVC)
        target_compile_options(${targetName}
        PRIVATE
            /W3
            /JMC-
            /Zc:__cplusplus
            /Zc:preprocessor
        )
    endif()

    # Platform setting
    if(WIN32)
        target_compile_definitions(${targetName}
        PRIVATE
            WIN32_LEAN_AND_MIN NOMINMAX
        )
        set_target_properties(${targetName}
        PROPERTIES
            WINDOWS_EXPORT_ALL_SYMBOLS OFF
        )
    endif()
endfunction()