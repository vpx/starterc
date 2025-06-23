cmake_minimum_required(VERSION 3.28)

project(starterc LANGUAGES C VERSION 0.0.1)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_subdirectory(src/)

include(CPack)

