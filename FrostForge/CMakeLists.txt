project( FrostForge )

set(CPM_DOWNLOAD_VERSION 0.27.2)
set(CPM_DOWNLOAD_LOCATION "${CMAKE_BINARY_DIR}/cmake/CPM_${CPM_DOWNLOAD_VERSION}.cmake")

if(NOT (EXISTS ${CPM_DOWNLOAD_LOCATION}))
    message(STATUS "Downloading CPM.cmake")
    file(DOWNLOAD https://github.com/TheLartians/CPM.cmake/releases/download/v${CPM_DOWNLOAD_VERSION}/CPM.cmake ${CPM_DOWNLOAD_LOCATION})
endif()

include(${CPM_DOWNLOAD_LOCATION})

# Add Global variables
set(BOX2D_BUILD_TESTBED OFF)

# Add CPMPackages for editor here with CPMAddPackage(NAME <PackageName> VERSION <Version> GITHUB_REPOSITORY <GitRepository> GIT_TAG <GitTag>)
# Example: CPMAddPackage(NAME FrostForge VERSION 0.0.1 GITHUB_REPOSITORY TheLartians/FrostForge)
CPMAddPackage(NAME GLFW GITHUB_REPOSITORY glfw/glfw GIT_TAG 3.3.8)
CPMAddPackage(NAME Box2D VERSION 2.4.1 GITHUB_REPOSITORY erincatto/box2d)
CPMAddPackage(NAME imgui VERSION 1.89.1 GITHUB_REPOSITORY ocornut/imgui)
CPMAddPackage(NAME ImGuizmo GITHUB_REPOSITORY CedricGuillemet/ImGuizmo GIT_TAG 1.83)
CPMAddPackage(NAME glm GITHUB_REPOSITORY g-truc/glm GIT_TAG 0.9.9.8)
CPMAddPackage(NAME spdlog VERSION 1.11.0 GITHUB_REPOSITORY gabime/spdlog)
CPMAddPackage(NAME yaml-cpp GITHUB_REPOSITORY jbeder/yaml-cpp GIT_TAG "yaml-cpp-0.7.0")
CPMAddPackage(NAME Boost GITHUB_REPOSITORY boostorg/boost GIT_TAG "boost-1.80.0")


# Create Library
add_library(FrostForge STATIC)

# Add Source files based on OS
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    message("Building FrostForge engine for Windows")
    target_sources(FrostForge
        PUBLIC
            src/FrostForge.hpp
            src/FrostForge/Entrypoint.hpp
            vendor/entt/include/entt.hpp
            vendor/filewatch/filewatch.hpp
            vendor/Glad/include/glad/glad.h
            vendor/Glad/include/KHR/khrplatform.h
            vendor/stb_image/stb_image.hpp
    )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    message("Building FrostForge engine for Linux")
    target_sources(FrostForge
        PUBLIC
            src/FrostForge.hpp
            src/FrostForge/Entrypoint.hpp
            vendor/entt/include/entt.hpp
            vendor/filewatch/filewatch.hpp
            vendor/Glad/include/glad/glad.h
            vendor/Glad/include/KHR/khrplatform.h
            vendor/stb_image/stb_image.hpp
    )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    message("Building FrostForge engine for Darwin")
    target_sources(FrostForge
        PUBLIC
            src/FrostForge.hpp
            src/FrostForge/Entrypoint.hpp
            vendor/entt/include/entt.hpp
            vendor/filewatch/filewatch.hpp
            vendor/Glad/include/glad/glad.h
            vendor/Glad/include/KHR/khrplatform.h
            vendor/stb_image/stb_image.hpp
    )
endif()

## Link external libraries
target_link_libraries(FrostForge
    PUBLIC
        Boost
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
        src/ffpch.hpp
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
