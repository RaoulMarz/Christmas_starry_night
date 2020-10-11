project (christmas_stars)
cmake_minimum_required(VERSION 3.4.1)
set (VERSION_MAJOR "1")
set (VERSION_MINOR "0")
set (VERSION_PATCH "3")
set (VERSION_BUILD "") # ie "-beta1", or empty string if release: ""
set (VERSION "${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH}")
set (CMAKE_DISABLE_IN_SOURCE_BUILD ON)

#
# This approach to labeling beta versions is in line with Apple's
# inflexible versioning scheme for pre-release beta testing versions,
# for both iOS and macOS.  Apple allows, ie, FlightTest to release
# versions like "1.0.0b1" (b2,b2,...) as a pre-release beta for
# "1.0.0".  There is no other possible beta numbering scheme in Apple
# world, dont even bother trying! :D This labelling with "-beta2" or
# "" for releases also plays well with the other package generators.
#
if (VERSION_BUILD)
  string (REGEX MATCH "[0-9]+" VERSION_BUILD_NUM ${VERSION_BUILD})
else ()
  set (VERSION_BUILD_NUM "")
endif ()

include_directories(vsgl)
file(GLOB_RECURSE SRC_VSGL_FILES vsgl/*.cpp)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/sdl2)

find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)
find_package(SDL2_ttf REQUIRED)
find_package(SDL2_mixer REQUIRED)
#find_package(SDL2_gfx REQUIRED)

# Link SDL2::Main, SDL2::Image and SDL2::GFX to our project

add_executable (christmas_stars main.cpp)
target_link_libraries (${PROJECT_NAME} ${SRC_VSGL_FILES} SDL2::Main SDL2::Image SDL2::TTF SDL2::Mixer)

