cmake_minimum_required(VERSION 3.25.1)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(basedmath)

add_library(basedmath INTERFACE)
add_library(based::math ALIAS basedmath)

set_target_properties(
    basedmath PROPERTIES
    LANGUAGES CXX
    DEBUG_POSTFIX d
    SOVERSION 1
    VERSION 1.0.0
)

target_include_directories(basedmath INTERFACE basedmath)
target_compile_features(basedmath INTERFACE cxx_std_23)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    basedmath-config-version.cmake
    VERSION 1.0.0
    COMPATIBILITY SameMajorVersion
)

include(GNUInstallDirs)
install(TARGETS basedmath
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        COMPONENT basedmath_runtime
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        COMPONENT basedmath_runtime
        NAMELINK_COMPONENT basedmath_development
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        COMPONENT basedmath_development
)

