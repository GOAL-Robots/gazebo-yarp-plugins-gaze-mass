# Copyright (C) 2018 Istituto Italiano di Tecnologia 
# Authors: see AUTHORS file.
# CopyPolicy: Released under the terms of the LGPLv2.1 or later, see LGPL.TXT

cmake_minimum_required(VERSION 2.8.7)

PROJECT(Plugin_Skin)

include(AddGazeboYarpPluginTarget)

set(LIB_COMMON_NAME gazebo_yarp_lib_common)
if(CMAKE_VERSION VERSION_LESS 3.0.0)
    get_property(GAZEBO_YARP_COMMON_HEADERS GLOBAL PROPERTY GAZEBO_YARP_COMMON_HEADERS)
    unset(LIB_COMMON_NAME)
endif()

# required for iCub-main libraries
find_package(ICUB)
find_package(YARP COMPONENTS gsl)
list(APPEND CMAKE_MODULE_PATH ${ICUB_MODULE_PATH})

add_gazebo_yarp_plugin_target(LIBRARY_NAME skin
                              INCLUDE_DIRS include/gazebo
                              SYSTEM_INCLUDE_DIRS ${GAZEBO_YARP_COMMON_HEADERS} ${Boost_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS}  ${SDFORMAT_INCLUDE_DIRS} ${PROTOBUF_INCLUDE_DIRS} ${OGRE_INCLUDE_DIRS}
                              LINKED_LIBRARIES ${LIB_COMMON_NAME} gazebo_yarp_singleton ${YARP_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES} ${ICUB_LIBRARIES}
                              HEADERS include/gazebo/Skin.hh
                              SOURCES src/Skin.cc
                              )
