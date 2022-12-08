project (Editor)

set(CPM_DOWNLOAD_VERSION 0.27.2)
set(CPM_DOWNLOAD_LOCATION "${CMAKE_BINARY_DIR}/cmake/CPM_${CPM_DOWNLOAD_VERSION}.cmake")

if(NOT (EXISTS ${CPM_DOWNLOAD_LOCATION}))
    message(STATUS "Downloading CPM.cmake")
    file(DOWNLOAD https://github.com/TheLartians/CPM.cmake/releases/download/v${CPM_DOWNLOAD_VERSION}/CPM.cmake ${CPM_DOWNLOAD_LOCATION})
endif()

include(${CPM_DOWNLOAD_LOCATION})

# Add CPMPackages for editor here with CPMAddPackage(NAME <PackageName> VERSION <Version> GITHUB_REPOSITORY <GitRepository> GIT_TAG <GitTag>)
# Example: CPMAddPackage(NAME Warlock VERSION 0.0.1 GITHUB_REPOSITORY TheLartians/Warlock)

add_executable(FrostForge-Editor)

# Add Source files based on OS
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    target_sources(FrostForge-Editor
        PUBLIC
            src/EditorApp.cpp
            src/EditorLayer.cpp
            src/EditorLayer.hpp
    )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    target_sources(FrostForge-Editor
        PUBLIC
            src/EditorApp.cpp
            src/EditorLayer.cpp
            src/EditorLayer.hpp
    )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    target_sources(FrostForge-Editor
        PUBLIC
            src/EditorApp.cpp
            src/EditorLayer.cpp
            src/EditorLayer.hpp
    )
endif()

# Link libraries for editor here
target_link_libraries(FrostForge-Editor
    PRIVATE
        FrostForge
)
