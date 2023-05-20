cmake_minimum_required(VERSION 3.21)
project(MyProject)
set(CMAKE_CXX_STANDARD 11)
add_subdirectory(shared_library)

add_executable(MyProject app.cpp)
target_link_libraries(MyProject geo)


# Add a custom command to copy the shared library to the executable output directory after building
add_custom_command(TARGET MyProject POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy_if_different
                   $<TARGET_RUNTIME_DLLS:MyProject>
                   $<TARGET_FILE_DIR:MyProject>)

