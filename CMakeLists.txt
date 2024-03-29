cmake_minimum_required( VERSION 2.8 )
project( DrawTrajectory )

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
   add_definitions(-DCOMPILEDWITHC11)
   message(STATUS "Using flag -std=c++11.")
elseif(COMPILER_SUPPORTS_CXX0X)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
   add_definitions(-DCOMPILEDWITHC0X)
   message(STATUS "Using flag -std=c++0x.")
else()
   message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()


# 为使用 sophus，您需要使用find_package命令找到它
find_package( Sophus REQUIRED )
find_package(Pangolin REQUIRED)
include_directories( ${Sophus_INCLUDE_DIRS} 
${Pangolin_INCLUDE_DIRS}
)
include_directories( "/usr/include/eigen3" )

add_executable( DrawTrajectory draw_trajectory.cpp )
target_link_libraries( DrawTrajectory ${Sophus_LIBRARIES} ${Pangolin_LIBRARIES} )