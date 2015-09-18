cmake_minimum_required(VERSION 2.4.6)
project(youbot_battery_monitor)

find_package(catkin REQUIRED COMPONENTS roscpp)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS roscpp
)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

include_directories(
  include
)

add_executable(youbot_battery_monitor
  src/youbot_battery_monitor.cpp
  nodes/youbot_battery_monitor_node.cpp
)

target_link_libraries(youbot_battery_monitor stdc++ ${catkin_LIBRARIES})
