cmake_minimum_required(VERSION 3.13)
project(foami)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC_ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
endif()

# qt
find_package(Qt5Core REQUIRED)
message(STATUS "Found Qt${Qt5Core_VERSION}: ${Qt5Core_INCLUDE_DIRS}")
find_package(Qt5Gui REQUIRED)
message(STATUS "Found Qt${Qt5Gui_VERSION}: ${Qt5Gui_INCLUDE_DIRS}")
find_package(Qt5Widgets REQUIRED)
message(STATUS "Found Qt${Qt5Widgets_VERSION}: ${Qt5Widgets_INCLUDE_DIRS}")

add_executable(${PROJECT_NAME}
        main.cpp
        )

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        Qt5::Core
        Qt5::Gui
        Qt5::Widgets
        )

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_definitions(${PROJECT_NAME} PRIVATE -DQT_NO_DEBUG_OUTPUT)
endif()

# ============
# Unit test
# ============

if(BUILD_FOAM_TESTS)
    add_subdirectory(tests)
endif()
