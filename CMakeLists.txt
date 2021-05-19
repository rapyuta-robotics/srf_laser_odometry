project(srf_laser_odometry)

CMAKE_MINIMUM_REQUIRED(VERSION 3.3)

find_package(catkin REQUIRED
  # COMPONENTS
  #   roscpp
  #   rospy
  #   nav_msgs
  #   sensor_msgs
  #   std_msgs
  #   tf
)

## System dependencies are found with CMake's conventions
# find_package(cmake_modules REQUIRED)
find_package(Eigen3 REQUIRED)

catkin_package(
 INCLUDE_DIRS include
 LIBRARIES ${PROJECT_NAME}
#  CATKIN_DEPENDS nav_msgs roscpp sensor_msgs std_msgs tf
 DEPENDS EIGEN3
)

include_directories(include)
include_directories(SYSTEM
  # ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME}
  src/laser_odometry_refscans.cpp
)

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD_REQUIRED ON)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_EXTENSIONS OFF)

# ## Declare a cpp executable
# add_executable(${PROJECT_NAME}_node
#     src/srf_node.cpp
#     )

# ## Specify libraries to link a library or executable target against
# target_link_libraries(${PROJECT_NAME}_node
#    ${PROJECT_NAME}
# )

# add_executable(srf_to_txt_node
#     src/srf_to_txt_node
#     )

# target_link_libraries(srf_to_txt_node
#    ${catkin_LIBRARIES}
#    ${Boost_LIBRARIES}
#    ${EIGEN3_LIBRARIES}
# )

################
##  Install   ##
################

install(TARGETS ${PROJECT_NAME} #${PROJECT_NAME}_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  # RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)