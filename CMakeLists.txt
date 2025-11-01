cmake_minimum_required(VERSION 3.20)
project(OCvidia LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Paths to third-party libraries
set(IMGUI_DIR ${CMAKE_SOURCE_DIR}/thirdparty/imgui)
set(NVAPI_DIR ${CMAKE_SOURCE_DIR}/thirdparty/nvapi)

# Include directories
include_directories(
    ${IMGUI_DIR}
    ${NVAPI_DIR}/inc
)

# ImGui source files
set(IMGUI_SRC
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/backends/imgui_impl_win32.cpp
    ${IMGUI_DIR}/backends/imgui_impl_dx11.cpp
)

# Main source
set(SRC
    src/main.cpp
    ${IMGUI_SRC}
)

add_executable(OCvidia ${SRC})

# Link against NVAPI (precompiled .lib inside nvapi)
target_link_libraries(OCvidia PRIVATE ${NVAPI_DIR}/amd64/nvapi64.lib)

# Ensure Windows subsystem (no console popup)
set_target_properties(OCvidia PROPERTIES LINK_FLAGS "/SUBSYSTEM:WINDOWS")
