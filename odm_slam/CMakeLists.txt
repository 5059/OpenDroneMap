project(odm_slam)
cmake_minimum_required(VERSION 2.8)

# Set opencv dir to the input spedified with option -DOPENCV_DIR="path"
set(OPENCV_DIR "OPENCV_DIR-NOTFOUND" CACHE "OPENCV_DIR" "Path to the opencv installation directory")

# Add compiler options.
add_definitions(-Wall -Wextra)

# Find OpenCV at the default location
find_package(OpenCV HINTS "${OPENCV_DIR}" REQUIRED)

# Only link with required opencv modules.
set(OpenCV_LIBS opencv_core opencv_imgproc opencv_highgui)

# Add the Eigen and OpenCV include dirs.
# Necessary since the PCL_INCLUDE_DIR variable set by find_package is broken.)
message("${EIGEN_ROOT}")
include_directories(${EIGEN_ROOT})
include_directories(${OpenCV_INCLUDE_DIRS})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -std=c++0x")

# TODO(pau): search these paths using find_package
include_directories(/usr/include/eigen3)
include_directories(../../ORB_SLAM2)
include_directories(../../ORB_SLAM2/include)
link_directories(../../../ORB_SLAM2/lib)

# Add source directory
aux_source_directory("./src" SRC_LIST)

# Add exectuteable
add_executable(${PROJECT_NAME} ${SRC_LIST})
target_link_libraries(odm_slam ${OpenCV_LIBS} ORB_SLAM2 pangolin)

