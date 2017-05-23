cmake_minimum_required( VERSION 3.6 )

# Create Project
project( Kinect2Sample )
add_executable( Fusion app.h app.cpp main.cpp util.h KinectFusionHelper.h KinectFusionHelper.cpp )

# Set StartUp Project
set_property( DIRECTORY PROPERTY VS_STARTUP_PROJECT "Fusion" )

# Find Package
set( CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}" ${CMAKE_MODULE_PATH} )
set( KinectSDK2_FUSION TRUE )
find_package( KinectSDK2 REQUIRED )

find_package( OpenCV REQUIRED )

if( KinectSDK2_FOUND AND OpenCV_FOUND )
  # Additional Include Directories
  include_directories( ${KinectSDK2_INCLUDE_DIRS} )

  # Additional Library Directories
  link_directories( ${KinectSDK2_LIBRARY_DIRS} )

  # Additional Dependencies
  target_link_libraries( Fusion ${KinectSDK2_LIBRARIES} )
  target_link_libraries( Fusion ${OpenCV_LIBS} )

  # Post Build Event
  add_custom_command( TARGET Fusion POST_BUILD ${KinectSDK2_COMMANDS} )
endif()