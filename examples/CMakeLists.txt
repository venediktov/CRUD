# -*- cmake -*-

cmake_minimum_required(VERSION 3.3.2)

include_directories(${Boost_INCLUDE_DIRS} ${PROJECT_SOURCE_DIR})

add_executable(
        restful_service
        main.cpp
        )

find_package (Threads)

target_link_libraries(
        restful_service
        crud_service
        ${Boost_LIBRARIES}
        ${CMAKE_THREAD_LIBS_INIT}
        )

