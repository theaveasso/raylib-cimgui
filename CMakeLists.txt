cmake_minimum_required(VERSION 3.28)
project(rlcimgui C CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

if (NOT TARGET raylib)
    FetchContent_Declare(
            raylib
            GIT_REPOSITORY https://github.com/raysan5/raylib.git
            GIT_TAG 5.5
    )
endif ()
if (NOT TARGET imgui)
    FetchContent_Declare(
            imgui
            GIT_REPOSITORY https://github.com/ocornut/imgui.git
            GIT_TAG v1.91.9-docking)
endif ()

if (NOT TARGET cimgui)
    FetchContent_Declare(
            cimgui
            GIT_REPOSITORY https://github.com/cimgui/cimgui.git
            GIT_TAG 5ba6e)
endif ()

FetchContent_MakeAvailable(imgui cimgui raylib)

add_library(rlcimgui STATIC ${CMAKE_CURRENT_SOURCE_DIR}/rlcimgui.c)
target_link_libraries(rlcimgui PUBLIC raylib cimgui)
target_include_directories(rlcimgui PUBLIC ${cimgui_SOURCE_DIR} ${imgui_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
