cmake_minimum_required(VERSION 3.23)
project(app)

set(OpenCV_DIR ~/opencv-mobile-4.10.0-ubuntu-2204/lib/cmake/opencv4)
find_package(OpenCV REQUIRED)
if(OpenCV_FOUND)
    message(STATUS "OpenCV library: ${OpenCV_INSTALL_PATH}")
    message(STATUS "    version: ${OpenCV_VERSION}")
    message(STATUS "    libraries: ${OpenCV_LIBS}")
    message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

    if(${OpenCV_VERSION_MAJOR} GREATER 3)
        set(CMAKE_CXX_STANDARD 11)
    endif()
endif()

link_directories(~/ncnn-20240820-ubuntu-2204/lib)

add_executable(app main.cpp)
target_include_directories(app PRIVATE ~/ncnn-20240820-ubuntu-2204/include)

target_include_directories(app PRIVATE ${OpenCV_INCLUDE_DIRS})
target_link_libraries(app PRIVATE ncnn glslang MachineIndependent GenericCodeGen OSDependent OGLCompiler SPIRV ${OpenCV_LIBS})
