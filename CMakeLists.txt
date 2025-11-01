cmake_minimum_required(VERSION 3.10)
project(NVAPI_Zara_GUI)
set(CMAKE_CXX_STANDARD 17)

add_subdirectory(thirdparty/imgui)
add_executable(NVAPI_Zara_GUI src/main.cpp)
target_include_directories(NVAPI_Zara_GUI PRIVATE external/NVAPI)
target_link_libraries(NVAPI_Zara_GUI PRIVATE imgui)
