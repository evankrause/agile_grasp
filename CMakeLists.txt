cmake_minimum_required(VERSION 2.8.3)
project(agile_grasp)

## System dependencies are found with CMake's conventions
find_package(Eigen3 REQUIRED)
find_package(LAPACK REQUIRED)
find_package(OpenCV 2 REQUIRED)
find_package(PCL REQUIRED)
#~ find_package(VTK 6.0 REQUIRED NO_MODULE) # required in Fedora Core

## Set compiler optimization flags
set(CMAKE_CXX_FLAGS "-DNDEBUG -O3 -fopenmp -Wno-deprecated -Wenum-compare")

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(${PCL_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})    
INCLUDE_DIRECTORIES(include)

#~ include(${VTK_USE_FILE}) # required in Fedora Core

# Set src files
SET(SOURCES
  src/${PROJECT_NAME}/quadric.cpp
  src/${PROJECT_NAME}/finger_hand.cpp
  src/${PROJECT_NAME}/rotating_hand.cpp 
  src/${PROJECT_NAME}/antipodal.cpp
  src/${PROJECT_NAME}/localization.cpp
  src/${PROJECT_NAME}/learning.cpp
  src/${PROJECT_NAME}/handle.cpp
  src/${PROJECT_NAME}/handle_search.cpp
  src/${PROJECT_NAME}/grasp_hypothesis.cpp
  src/${PROJECT_NAME}/plot.cpp
  src/${PROJECT_NAME}/hand_search.cpp
  )

# Create shared lib
ADD_LIBRARY(${PROJECT_NAME} SHARED ${SOURCES})

## Specify libraries to link a library or executable target against
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES} lapack)


#############
## Install ##
#############

install (DIRECTORY include/${PROJECT_NAME}/ DESTINATION include/${PROJECT_NAME} FILES_MATCHING PATTERN "*.h" PATTERN ".git" EXCLUDE)
install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib)

# uninstall target
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)

add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)
