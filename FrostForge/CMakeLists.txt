project( FrostForge )

set(CPM_DOWNLOAD_VERSION 0.27.2)
set(CPM_DOWNLOAD_LOCATION "${CMAKE_BINARY_DIR}/cmake/CPM_${CPM_DOWNLOAD_VERSION}.cmake")

if(NOT (EXISTS ${CPM_DOWNLOAD_LOCATION}))
    message(STATUS "Downloading CPM.cmake")
    file(DOWNLOAD https://github.com/TheLartians/CPM.cmake/releases/download/v${CPM_DOWNLOAD_VERSION}/CPM.cmake ${CPM_DOWNLOAD_LOCATION})
endif()

include(${CPM_DOWNLOAD_LOCATION})

# Add Global variables

# Add CPMPackages for editor here with CPMAddPackage(NAME <PackageName> VERSION <Version> GITHUB_REPOSITORY <GitRepository> GIT_TAG <GitTag>)
# Example: CPMAddPackage(NAME FrostForge VERSION 0.0.1 GITHUB_REPOSITORY TheLartians/FrostForge)
CPMAddPackage(NAME Asio VERSION 2.4.1 GITHUB_REPOSITORY boostorg/asio)
CPMAddPackage(NAME Box2D VERSION 2.4.1 GITHUB_REPOSITORY erincatto/box2d)
CPMAddPackage(NAME GLFW VERSION 3.3.8 GITHUB_REPOSITORY glfw/glfw)
CPMAddPackage(NAME imgui VERSION 1.89.1 GITHUB_REPOSITORY ocornut/imgui)
CPMAddPackage(NAME ImGuizmo VERSION 1.83 GITHUB_REPOSITORY CedricGuillemet/ImGuizmo)
CPMAddPackage(NAME glm VERSION 0.9.9.8 GITHUB_REPOSITORY g-truc/glm)
CPMAddPackage(NAME spdlog VERSION 1.11.0 GITHUB_REPOSITORY gabime/spdlog)
CPMAddPackage(NAME yaml-cpp VERSION 0.7.0 GITHUB_REPOSITORY jbeder/yaml-cpp)

# Add Sources
file(GLOB SOURCES CONFIGURE_DEPENDS
    src/*.hpp
    src/*.cpp
    vendor/entt/include/*.hpp
    vendor/stb_image/*.hpp
)

# Create Library
add_library(FrostForge
    STATIC
        ${SOURCES}
)

## Link external libraries
target_link_libraries(FrostForge
    PUBLIC
      Asio
      Box2D
      GLFW
      imgui
      ImGuizmo
      glm
      spdlog
      yaml-cpp
)

## Add pre-compiled headers
target_precompile_headers(FrostForge
    PUBLIC
        ffpch.hpp
)

## Add include directories
target_include_directories(FrostForge
    PUBLIC
        src
    PRIVATE
        vendor/entt/include
        vendor/Glad/include
        vendor/stb_image
        vendor/filewatch
)