cmake_minimum_required( VERSION 3.6 )

# Create Project
project( Kinect2Sample )
add_executable( PointCloud app.h app.cpp main.cpp util.h )

# Set StartUp Project
set_property( DIRECTORY PROPERTY VS_STARTUP_PROJECT "PointCloud" )

# Find Package
set( CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}" ${CMAKE_MODULE_PATH} )
find_package( KinectSDK2 REQUIRED )

find_package( OpenCV REQUIRED )

# Required Viz Module
if( OpenCV_FOUND )
  if( NOT "opencv_viz" IN_LIST OpenCV_LIBS )
    message( FATAL_ERROR "not found opencv_viz module." )
  endif()
endif()


if( KinectSDK2_FOUND AND OpenCV_FOUND )
  # Additional Include Directories
  include_directories( ${KinectSDK2_INCLUDE_DIRS} )

  # Additional Library Directories
  link_directories( ${KinectSDK2_LIBRARY_DIRS} )

  # Additional Dependencies
  target_link_libraries( PointCloud ${KinectSDK2_LIBRARIES} )
  target_link_libraries( PointCloud ${OpenCV_LIBS} )
endif()