cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

#set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

project(testpad LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_VERBOSE_MAKEFILE ON)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5 REQUIRED COMPONENTS Core Quick Gui Qml)

if(CMAKE_VERSION VERSION_LESS "3.7.0")
    set(CMAKE_INCLUDE_CURRENT_DIR ON)
endif()

add_executable(${PROJECT_NAME} 
    main.cpp
    qml.qrc
)

# Link the Qt5 libraries to the executable
target_link_libraries(${PROJECT_NAME} 
    Qt5::Core 
    Qt5::Quick
    Qt5::Gui
    Qt5::Qml
)

# Include the Qt5 include directories
target_include_directories(${PROJECT_NAME} 
    PRIVATE ${Qt5_INCLUDE_DIRS}
)

# Add resources
qt5_add_resources(RESOURCES resources.qrc)

set_property(TARGET ${PROJECT_NAME} PROPERTY COMPILE_WARNING_AS_ERROR ON)
