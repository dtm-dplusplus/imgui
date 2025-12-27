# ThirdParty/imgui/CMakeLists.txt
project(ImGuiLib)

# 1. List the files we need (Core + Backends)
set(IMGUI_SOURCES
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    # The Backends (SDL3 + OpenGL3)
    backends/imgui_impl_sdl3.cpp
    backends/imgui_impl_opengl3.cpp
)

# 2. Define the Static Library
add_library(ImGuiLib STATIC ${IMGUI_SOURCES})

# 3. Expose Headers (So your Engine can say #include "imgui.h")
target_include_directories(ImGuiLib PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}           # For imgui.h
    ${CMAKE_CURRENT_SOURCE_DIR}/backends  # For imgui_impl_sdl3.h
)

# 4. Link Dependencies
# ImGui needs to know what "SDL_Window" is, so we link SDL3.
#find_package(SDL3 REQUIRED)
target_link_libraries(ImGuiLib PRIVATE SDL3::SDL3)