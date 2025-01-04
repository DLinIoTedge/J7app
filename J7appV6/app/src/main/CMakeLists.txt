cmake_minimum_required(VERSION 3.10.2)

project("J7app")

# Add native-lib.cpp as a shared library
add_library(
    native-lib
    SHARED
    cpp/native-lib.cpp
)

find_library(
    log-lib
    log
)

target_link_libraries(
    native-lib
    ${log-lib}
)
