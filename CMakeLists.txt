# -*- cmake -*-

cmake_minimum_required(VERSION 3.3.2)

# VERSION not required, but good for library versioning
project(CRUD VERSION 0.1.0)

#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
#set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
#set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)


set(CMAKE_CXX_STANDARD 14)
SET(CMAKE_CXX_STANDARD_REQUIRED ON)
SET(CMAKE_CXX_EXTENSIONS OFF)

set ( CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_BINARY_DIR})

find_package(Boost
             COMPONENTS "log" "system" "serialization" "program_options"
             REQUIRED
            )

add_subdirectory(service)

if ( DEFINED CRUD_WITH_EXAMPLES)
    add_subdirectory(examples)
endif()

