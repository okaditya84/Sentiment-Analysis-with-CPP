cmake_minimum_required(VERSION 3.10)
project(sentiment)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(sentiment
    main.cpp
    DSString.cpp
    Twitter.cpp
    Word.cpp
)

# Set compiler flags
if (MSVC)
    target_compile_options(sentiment PRIVATE /W4) # Remove /WX to not treat warnings as errors
else()
    target_compile_options(sentiment PRIVATE -Wall -Wextra -pedantic -Werror)
endif()

# Copy data files to build dir
foreach(file IN LISTS input01 input02 input03)
    configure_file(${file} ${file} COPYONLY)
endforeach()

# Show compiler output and enable warnings
set(CMAKE_VERBOSE_MAKEFILE ON)