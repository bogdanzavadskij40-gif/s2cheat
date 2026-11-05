cmake_minimum_required(VERSION 3.18)
project(s2cheat CXX)
set(CMAKE_CXX_STANDARD 17)

# Подключаем Dobby как подпроект
add_subdirectory(dobby)

add_library(standoff2_cheat SHARED main.cpp
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_tables.cpp
    imgui/imgui_widgets.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

target_include_directories(standoff2_cheat PRIVATE . imgui imgui/backends dobby/include)
# Линкуем основную библиотеку с Dobby
target_link_libraries(standoff2_cheat log android EGL GLESv3 dl dobby)
target_compile_options(standoff2_cheat PRIVATE -O2 -fvisibility=hidden -fno-exceptions -fno-rtti)
