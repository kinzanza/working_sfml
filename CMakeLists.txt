cmake_minimum_required(VERSION 3.16)
project(CMakeSFMLJSONProject LANGUAGES CXX)

option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

include(FetchContent)

set(SFML_VERSION 2.5.1)
FetchContent_Declare(
    sfml
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG ${SFML_VERSION}
)

FetchContent_Declare(
    nlohmann_json
    GIT_REPOSITORY https://github.com/nlohmann/json.git
    GIT_TAG v3.11.2
)

FetchContent_MakeAvailable(sfml nlohmann_json)

add_executable(main game2.cpp)

target_link_libraries(main PRIVATE sfml-graphics sfml-window sfml-system nlohmann_json::nlohmann_json)

target_compile_features(main PRIVATE cxx_std_17)

if (UNIX AND NOT APPLE)
    target_compile_options(main PRIVATE -fPIC)
endif()
