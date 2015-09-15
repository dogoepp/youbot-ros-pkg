cmake_minimum_required(VERSION 2.8.3)

project(youbot_oodl)

## check required prerequisites
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/external/cmake_modules")
set(Boost_ADDITIONAL_VERSIONS "1.39" "1.39.0" "1.40" "1.40.0" "1.41" "1.41.0" "1.42" "1.42.0" "1.43" "1.43.0" "1.44" "1.44.0" "1.45" "1.45.0" "1.46" "1.46.0")
find_package(Boost REQUIRED COMPONENTS thread date_time filesystem system)

find_package(catkin REQUIRED COMPONENTS roscpp tf)

#set(CMAKE_PREFIX_PATH /home/catkin_ws/src/youbot_oodl/external/cmake_modules ${CMAKE_PREFIX_PATH} CACHE)
SET(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/external/cmake_modules")
#message(WARNING ${CMAKE_PREFIX_PATH})
message(WARNING ${CMAKE_MODULE_PATH})
find_package(OODL_YouBot REQUIRED)
#SET(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/external/cmake_modules")
find_package(Soem REQUIRED)

## preprocessor definitions
add_definitions(-DYOUBOT_CONFIGURATIONS_DIR="${youbot_driver_PACKAGE_PATH}/config/")

catkin_package(
	INCLUDE_DIRS include
	CATKIN_DEPENDS roscpp
	DEPENDS Boost
)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

## Set Compilter flags
include_directories(
	include
	${Boost_INCLUDE_DIR}
	${catkin_INCLUDE_DIRS}
	${OODL_YOUBOT_INCLUDE_DIR}
	${SOEM_INCLUDE_DIR}
#	~/youbot_driver/
#	~/youbot_driver/soem/src
)

add_executable(youbot_oodl
    src/youbot_oodl.cpp
    src/YouBotOODLWrapper.cpp
    src/YouBotConfiguration.cpp
    src/joint_state_observer_oodl.cpp
)


target_link_libraries(youbot_oodl ${OODL_YOUBOT_LIBRARIES} ${Boost_LIBRARIES} ${catkin_LIBRARIES} )#/home/omnigrasper/youbot_driver/lib/libsoem.a /home/omnigrasper/youbot_driver/lib/libYouBotDriver.a)

OPTION(USE_SETCAP "Set permissions to access ethernet interface without sudo" OFF)

SET(SUDO_COMMAND gksudo)
IF($ENV{USE_NORMAL_SUDO})
    SET(SUDO_COMMAND sudo)
ENDIF($ENV{USE_NORMAL_SUDO})

IF(USE_SETCAP)
add_custom_command(TARGET youbot_oodl POST_BUILD
    COMMAND sudo setcap cap_net_raw+ep youbot_oodl
    #COMMAND ${SUDO_COMMAND} setcap cap_net_raw+ep youbot_oodl
    WORKING_DIRECTORY ${EXECUTABLE_OUTPUT_PATH}
)
endif(USE_SETCAP)

# add_executable(youbot_arm_test
#     examples/youbot_arm_test.cpp
# )

# add_executable(youbot_2nd_arm_test
#     examples/youbot_2nd_arm_test.cpp
# )
