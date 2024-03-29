cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
set(ROS_BUILD_TYPE Debug)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)

#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

#add dynamic reconfigure api
rosbuild_find_ros_package(dynamic_reconfigure)
include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
gencfg()

rosbuild_add_executable(motion_detection src/motion_detection.cpp)
rosbuild_add_executable(motion_detection src/motion_detection.h)
rosbuild_add_executable(motion src/motion.cpp)
rosbuild_add_executable(motion src/motion.h)
#rosbuild_add_executable(tinyxml src/tinyxml.h)
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
find_package(OpenCV REQUIRED)
target_link_libraries(motion_detection ${OpenCV_LIBS})

#TODO: Define non-absolute include path
#Teporary includes of opencv with sse3 disabled
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_highgui.so)
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_imgproc.so)
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_features2d.so)
