cmake_minimum_required(VERSION 3.0)

project(livox_sdk2)

set(CMAKE_CXX_STANDARD 14)
find_package(catkin REQUIRED)
find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

message(STATUS "main project dir: " ${PROJECT_SOURCE_DIR})

if (CMAKE_CROSSCOMPILING)
        set(THREADS_PTHREAD_ARG
                "PLEASE_FILL_OUT-FAILED_TO_RUN"
                CACHE STRING "Result from TRY_RUN" FORCE)
endif()

if (UNIX)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif(UNIX)

add_subdirectory(sdk_core)
add_subdirectory(samples)
catkin_package(
  INCLUDE_DIRS include
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)


#install(DIRECTORY include/${PROJECT_NAME}/
install(DIRECTORY include/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING
  PATTERN "*.h"
  PATTERN "*.hpp"
  PATTERN ".svn" EXCLUDE
)

