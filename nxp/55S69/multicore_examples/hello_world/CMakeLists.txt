# CMake 3.20 reports compiler information used by the IDE
CMAKE_MINIMUM_REQUIRED (VERSION 3.20)

project ("hello_world_multicore")

# Include sub-projects.
# cm33_core1 project must compile first as output from it is referenced from cm33_core0.
add_subdirectory ("cm33_core1")
add_subdirectory ("cm33_core0")