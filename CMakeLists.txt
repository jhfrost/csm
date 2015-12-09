cmake_minimum_required(VERSION 2.8.3)
project(csm)

set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_C_FLAGS_RELEASE "-O3")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

#SET(CMAKE_BUILD_TYPE Debug)
SET(CMAKE_BUILD_TYPE RelWithDebInfo)

find_package(catkin REQUIRED COMPONENTS roslib roscpp cmake_modules)

find_package(Eigen REQUIRED)
include_directories(${EIGEN_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(src)

SET(CSM_SRC 
  src/csm/laser_data.cpp
  src/csm/math_utils.cpp
  src/csm/math_utils_gsl.cpp
  src/csm/utils.cpp
  src/csm/logging.cpp
  src/csm/sm_options.cpp
  src/csm/orientation.cpp
  src/csm/clustering.cpp)

SET(EGSL_SRC
	src/egsl/egsl.cpp
	src/egsl/egsl_conversions.cpp
	src/egsl/egsl_misc.cpp
	src/egsl/egsl_ops.cpp)

SET(GPC_SRC
	src/gpc/gpc.cpp
	src/gpc/gpc_utils.cpp)

SET(ICP_SRC
  src/icp/icp.cpp
  src/icp/icp_corr_dumb.cpp
  src/icp/icp_corr_tricks.cpp
  src/icp/icp_covariance.cpp
  src/icp/icp_debug.cpp
  src/icp/icp_loop.cpp
  src/icp/icp_outliers.cpp)

SET(OPTIONS_SRC  
   src/options/options.cpp
   src/options/options_interface.cpp)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES csm
  CATKIN_DEPENDS roslib roscpp
)

include_directories(
  include
)

add_library(csm
	${CSM_SRC}
	${EGSL_SRC} 
	${GPC_SRC}
	${ICP_SRC}
	${OPTIONS_SRC}
)
