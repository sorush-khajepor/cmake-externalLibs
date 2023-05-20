cmake_minimum_required(VERSION 3.21)
project(MyProject)
set(CMAKE_CXX_STANDARD 11)

include(FetchContent)
FetchContent_Declare(
  geoFolder
  GIT_REPOSITORY https://github.com/sorush-khajepor/cmake-examples.git
  SOURCE_SUBDIR  shared_library
)
set(Arbitary_Geo_variable OFF CACHE INTERNAL "")
message("Downloading & preparing geoFolder...")
FetchContent_MakeAvailable(geoFolder)

add_executable(MyProject app.cpp)
target_link_libraries(MyProject geo)


# Add a custom command to copy the shared library to the executable output directory after building
add_custom_command(TARGET MyProject POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy_if_different
                   $<TARGET_RUNTIME_DLLS:MyProject>
                   $<TARGET_FILE_DIR:MyProject>)

