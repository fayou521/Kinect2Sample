cmake_minimum_required( VERSION 3.6 )

# Create Project
project( Kinect2Sample )
add_executable( FaceClip app.h app.cpp main.cpp util.h )

# Set StartUp Project
set_property( DIRECTORY PROPERTY VS_STARTUP_PROJECT "FaceClip" )

# Find Package
set( CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}" ${CMAKE_MODULE_PATH} )
set( KinectSDK2_FACE TRUE )
find_package( KinectSDK2 REQUIRED )

find_package( OpenCV REQUIRED )


if( KinectSDK2_FOUND AND OpenCV_FOUND )
  # Additional Include Directories
  include_directories( ${KinectSDK2_INCLUDE_DIRS} )

  # Additional Library Directories
  link_directories( ${KinectSDK2_LIBRARY_DIRS} )

  # Additional Dependencies
  target_link_libraries( FaceClip ${KinectSDK2_LIBRARIES} )
  target_link_libraries( FaceClip ${OpenCV_LIBS} )

  # Post Build Event
  add_custom_command( TARGET FaceClip POST_BUILD ${KinectSDK2_COMMANDS} )
endif()