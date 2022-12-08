cmake_minimum_required(VERSION 3.24.0)
project(Warlock_Engine VERSION 0.0.1 LANGUAGES CXX)

## 64 Bit Check
if(NOT CMAKE_SIZEOF_VOID_P MATCHES 8)
    message(FATAL_ERROR "Warlock Engine only supports 64-bit builds.")
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

#add_compile_options(-Wall -Wextra -Werror)

add_subdirectory(FrostForge)
add_subdirectory(Editor)
