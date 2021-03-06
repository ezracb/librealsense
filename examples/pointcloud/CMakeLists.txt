# ubuntu 16.04 LTS cmake version 3.5.1
cmake_minimum_required(VERSION 2.8.3)

project(RealsenseExamplesPointcloud)

# Save the command line compile commands in the build output
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
endif()

if(BUILD_GRAPHICAL_EXAMPLES)
    #pointcloud
    add_executable(rs-pointcloud rs-pointcloud.cpp ../../third-party/imgui/imgui.cpp ../../third-party/imgui/imgui_draw.cpp ../../third-party/imgui/imgui_impl_glfw.cpp ../example.hpp)
    target_link_libraries(rs-pointcloud ${DEPENDENCIES})
    include_directories(rs-pointcloud ../ ../../third-party/imgui)
    set_target_properties (rs-pointcloud PROPERTIES
        FOLDER Examples
    )

    install(
        TARGETS

        rs-pointcloud

        RUNTIME DESTINATION
        ${CMAKE_INSTALL_PREFIX}/bin
    )
endif()
