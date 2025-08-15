cmake_minimum_required(VERSION 3.28)

project(starterc LANGUAGES C VERSION 0.0.1)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_library(starterc STATIC)
add_library(sc::starterc ALIAS starterc)
target_compile_features(starterc PRIVATE c_std_23)
target_compile_options(starterc PRIVATE
    $<$<C_COMPILER_ID:GNU,Clang>:-Werror;-Wall;-Wextra;-Wshadow;-Walloca;-Wcast-align;-Wcast-qual;-Wconversion;-Wdeprecated;-Wnull-dereference;-Wunreachable-code;-Wpedantic;>
    $<$<C_COMPILER_ID:Clang>:-Warray-bounds-pointer-arithmetic;-Wassign-enum;-Watomic-implicit-seq-cst;-Wbitwise-op-parentheses;-Wcompound-token-split-by-space;-Wconditional-uninitialized;-Wdelimited-escape-sequence-extension;-Wmost;>
    $<$<C_COMPILER_ID:GNU>:-Wmisleading-indentation;-Wduplicated-cond;-Wduplicated-branches;-Wlogical-op;>
)

option(STARTERC_CLANG_TIDY "Enable clang-tidy during the build process" OFF)
if (STARTERC_CLANG_TIDY)
    set_target_properties(starterc PROPERTIES C_CLANG_TIDY "clang-tidy")
endif()

target_include_directories(starterc
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

add_subdirectory(src/)

include(FetchContent)

option(STARTERC_BUILD_TESTS "Enable building tests" ON)
if(STARTERC_BUILD_TESTS)
    include(CTest)
    add_subdirectory(test/)
endif()

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

install(
    TARGETS starterc
    EXPORT starterc-targets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(
    DIRECTORY include/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(
    EXPORT starterc-targets
    FILE starterc-config.cmake
    NAMESPACE sc::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/starterc
)

write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/starterc-config-version.cmake
    COMPATIBILITY SameMajorVersion
)

install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/starterc-config-version.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/starterc
)

include(CPack)
