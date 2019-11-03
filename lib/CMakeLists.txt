# Copyright 2011,2012 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Setup library
########################################################################
include(GrPlatform) #define LIB_SUFFIX

include_directories(${Boost_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIRS})
list(APPEND burst_sources
    interp_cpdu_impl.cc
    correlator_filter_impl.cc
    length_detect_c_impl.cc
    synchronizer_v4_impl.cc
    qa_helpers.cc )
    
set(burst_sources "${burst_sources}" PARENT_SCOPE)
if(NOT burst_sources)
	MESSAGE(STATUS "No C++ sources... skipping lib/")
	return()
endif(NOT burst_sources)

add_library(gnuradio-burst SHARED ${burst_sources})
target_link_libraries(gnuradio-burst ${Boost_LIBRARIES} gnuradio::gnuradio-runtime
	gnuradio::gnuradio-filter
	gnuradio::gnuradio-fft
gnuradio::gnuradio-pmt ${MAPPER_LIBRARIES})

target_include_directories(gnuradio-burst
    PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
    PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/>
    PUBLIC $<INSTALL_INTERFACE:include>
  )
  
set_target_properties(gnuradio-burst PROPERTIES DEFINE_SYMBOL "gnuradio_burst_EXPORTS")

if(APPLE)
    set_target_properties(gnuradio-burst PROPERTIES
        INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib"
    )
endif(APPLE)

########################################################################
# Install built library files
########################################################################
include(GrMiscUtils)
GR_LIBRARY_FOO(gnuradio-burst RUNTIME_COMPONENT "burst_runtime" DEVEL_COMPONENT "burst_devel")

########################################################################
# Print summary
########################################################################
message(STATUS "Using install prefix: ${CMAKE_INSTALL_PREFIX}")
message(STATUS "Building for version: ${VERSION} / ${LIBVER}")

########################################################################
# Build and register unit test
########################################################################
include(GrTest)

# If your unit tests require special include paths, add them here
#include_directories()
# List all files that contain Boost.UTF unit tests here
list(APPEND test_burst_sources
)
# Anything we need to link to for the unit tests go here
list(APPEND GR_TEST_TARGET_DEPS gnuradio-burst)

if(NOT test_burst_sources)
    MESSAGE(STATUS "No C++ unit tests... skipping")
    return()
endif(NOT test_burst_sources)

foreach(qa_file ${test_burst_sources})
    GR_ADD_CPP_TEST("burst_${qa_file}"
        ${CMAKE_CURRENT_SOURCE_DIR}/${qa_file}
    )
endforeach(qa_file)

GR_ADD_TEST(test_burst test-burst)

########################################################################
# Print summary
########################################################################
message(STATUS "Using install prefix: ${CMAKE_INSTALL_PREFIX}")
message(STATUS "Building for version: ${VERSION} / ${LIBVER}")
