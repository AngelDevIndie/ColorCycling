cmake_minimum_required(VERSION 3.16)
project(ColorCycling)

set(CMAKE_CXX_STANDARD 17)

find_package(GLEW REQUIRED)
find_package(SDL2 REQUIRED)
if (NOT WIN32)
    find_package(OpenGL REQUIRED)
endif ()

include_directories(${PROJECT_SOURCE_DIR}/extlibs/imgui ${PROJECT_SOURCE_DIR}/extlibs)
add_library(imgui
        # Main Imgui files
        extlibs/imgui/imgui.cpp extlibs/imgui/imgui_draw.cpp extlibs/imgui/imgui_widgets.cpp
        extlibs/imgui/misc/cpp/imgui_stdlib.cpp
        # SDL2+OpenGL-specific files
        extlibs/imgui/examples/imgui_impl_sdl.cpp)

add_library(ImGuiFileDialog
        # Main Imgui files
        extlibs/ImGuiFileDialog/ImGuiFileDialog.cpp)

include_directories(${NGLIB_HEADERS_DIR} ${SDL2_INCLUDE_DIRS})
add_executable(${PROJECT_NAME} src/main.cpp
        src/Application.cpp src/ColorCyclingApplication.cpp src/TimeSpan.cpp src/Util.cpp src/Window.cpp
        extlibs/imgui/examples/imgui_impl_opengl3.cpp)
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} GLEW::GLEW imgui ImGuiFileDialog)
