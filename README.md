# ncnn-yolo11-example-cpp
The [repository](https://github.com/HexRx/ncnn-yolo11-example-cpp) contains C++ example of using the `ncnn` framework with YOLO11 models. If you use pre-built `ncnn` and `opencv-mobile`, the project will be built without dynamic library dependencies.

## Dependencies
- [CMake](https://cmake.org)
- [ncnn](https://github.com/Tencent/ncnn)
- OpenCV (or [opencv-mobile](https://github.com/nihui/opencv-mobile))

## Build
1. Set up the [ncnn](https://github.com/Tencent/ncnn) library:
    - Option 1: Build ncnn from source. Download the library from the official repository [ncnn](https://github.com/Tencent/ncnn) and follow the build instructions.
    - Option 2: Use pre-built library. Download pre-built from the https://github.com/Tencent/ncnn?tab=readme-ov-file#download--build-status

2. Set up the OpenCV library:
    - Option 1: Build OpenCV from source.
    - Option 2: Use pre-built mobile version of OpenCV - [opencv-mobile](https://github.com/nihui/opencv-mobile). Just download the appropriate version for your platform from https://github.com/nihui/opencv-mobile?tab=readme-ov-file#download

3. Change CMakeLists.txt
    
    If you use `opencv-mobile` library, change the path string `OpenCV_DIR ~/opencv-mobile-4.10.0-ubuntu-2204/lib/cmake/opencv4` to your `opencv-mobile` path. Change include path `target_include_directories(app PRIVATE ~/ncnn-20240820-ubuntu-2204/include)` and lib path `link_directories(~/ncnn-20240820-ubuntu-2204/lib)` to your `ncnn` path.

4. Run `cmake -S . -B build`
5. Compile the project with command `cmake --build build`

## Run application
```
./build/app horses.jpg yolo11n.ncnn.param yolo11n.ncnn.bin
```

## How to use your own YOLO Model
There are two steps involved in using your own YOLO model with this project:
1. Export YOLO model to ncnn format. Run the following command, replacing your_model.pt with the actual path to your YOLO model file:
    ```
    yolo export model=your_model.pt format=ncnn
    ```

2. Open the `main.cpp` file and locate the variable named `class_names`. This variable defines the list of class names that the model will predict. Update this list to reflect the classes present in your own YOLO model.
    ```
    static const char* class_names[] = {"person", "bicycle", "car",
                                        "motorcycle", "airplane", "bus",
                                        ...
    ```