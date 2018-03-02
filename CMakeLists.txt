cmake_minimum_required(VERSION 2.8.3)
project(loam_back_and_forth)

# add_compile_options(-std=c++11)
# set(CMAKE_BUILD_TYPE RelWithDebInfo)
# SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -O3 -march=native")
# SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O3 -march=native")

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  nav_msgs
  sensor_msgs
  roscpp
  rospy
  std_msgs
  pcl_conversions
  pcl_ros
)

find_package(Eigen3 REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
set(OpenCV_DIR $ENV{OPENCV2_INSTALL_DIR})
find_package(OpenCV 2 REQUIRED QUIET)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
  ${PCL_INCLUDE_DIRS}
)

LIST(APPEND LINK_LIBS
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ${OpenCV_LIBRARIES}
)

catkin_package(
  DEPENDS EIGEN3 PCL OpenCV EIGEN3
  CATKIN_DEPENDS geometry_msgs nav_msgs roscpp rospy std_msgs
)


add_executable(laserOdometry_bf src/laserOdometry.cpp)
target_link_libraries(laserOdometry_bf ${LINK_LIBS})

add_executable(laserMapping_bf src/laserMapping.cpp)
target_link_libraries(laserMapping_bf ${LINK_LIBS})

add_executable(transformMaintenance_bf src/transformMaintenance.cpp)
target_link_libraries(transformMaintenance_bf ${LINK_LIBS})

add_executable(scanRegistration_bf src/scanRegistration.cpp)
target_link_libraries(scanRegistration_bf ${LINK_LIBS})


