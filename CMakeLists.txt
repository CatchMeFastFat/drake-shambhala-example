cmake_minimum_required(VERSION 3.0)
project(demo)
set (CMAKE_VERBOSE_MAKEFILE true)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake/modules")

set(drake_DIR "/home/drake/drake-build/lib/cmake/drake/")
find_package(drake CONFIG REQUIRED)
find_package(PythonInterp 2.7 EXACT MODULE REQUIRED)
set(PYTHONPATH "${drake_PYTHON_DIRS}:$ENV{PYTHONPATH}")

set(PROJECT_PATH "${CMAKE_CURRENT_SOURCE_DIR}")
#Bring the headers into the project
include_directories(include)
set(EXECUTABLE_OUTPUT_PATH "${PROJECT_PATH}/bin")
set(CMAKE_BINARY_DIR "${PROJECT_PATH}/bin")
# include_directories(/home/drake/drake-build/include)

# # #Bring the libs into the project
# link_directories(/home/drake/drake-build/lib)


#The file(GLOB...) allows for wildcard additions:
file(GLOB SOURCES "${PROJECT_PATH}/src/main/*.cpp" "${PROJECT_PATH}/src/gen/*.cc")
add_executable(${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME}
    drake::drake gflags)


target_compile_options(demo PUBLIC -O0 -ggdb3 -Wall -Werror)

#ADD_SUBDIRECTORY( src )

