cmake_minimum_required(VERSION 3.0.2)
project(cpp_controllers)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_BUILD_TYPE Release)

find_package(catkin REQUIRED)

find_package(PkgConfig REQUIRED)
pkg_check_modules(EIGEN eigen3>=3.2.7)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES cpp_controllers
#  CATKIN_DEPENDS other_catkin_pkg
  DEPENDS EIGEN
)

###########
## Build ##
###########

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${EIGEN_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME}
  src/FootGuidedController.cpp
  )
target_link_libraries(${PROJECT_NAME} PUBLIC
  ${catkin_LIBRARIES}
  ${EIGEN_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
  )

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)
