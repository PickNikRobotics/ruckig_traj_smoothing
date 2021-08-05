cmake_minimum_required(VERSION 3.10.2)
project(ruckig_traj_smoothing LANGUAGES CXX)

find_package(ament_cmake REQUIRED)
find_package(pluginlib REQUIRED)
find_package(rclcpp REQUIRED)
find_package(ruckig REQUIRED)

set(LIB_NAME ruckig_traj_smoothing)

# Set target file path for version.h
set(VERSION_FILE_PATH ${CMAKE_BINARY_DIR}/include)

set(THIS_PACKAGE_INCLUDE_DEPENDS
  ruckig
)

add_library(${LIB_NAME} SHARED
  src/ruckig_traj_smoothing.cpp
)

set_target_properties(${LIB_NAME} PROPERTIES VERSION "${${PROJECT_NAME}_VERSION}")
ament_target_dependencies(${LIB_NAME}
  rclcpp
)
target_link_libraries(${LIB_NAME}
  ruckig::ruckig
)

install(DIRECTORY include/ DESTINATION include)

#if(BUILD_TESTING)
#  if(WIN32)
#    # TODO add windows paths
#    # set(append_library_dirs "$<TARGET_FILE_DIR:${PROJECT_NAME}>;$<TARGET_FILE_DIR:${PROJECT_NAME}_TestPlugins1>")
#  else()
#    set(append_library_dirs "${CMAKE_CURRENT_BINARY_DIR};${CMAKE_CURRENT_BINARY_DIR}/../robot_trajectory;${CMAKE_CURRENT_BINARY_DIR}/../utils")
#  endif()
#
#  ament_add_gtest(test_time_parameterization test/test_time_parameterization.cpp
#    APPEND_LIBRARY_DIRS "${append_library_dirs}")

#  target_link_libraries(test_time_parameterization moveit_test_utils ${LIB_NAME})
#
#  ament_add_gtest(test_time_optimal_trajectory_generation test/test_time_optimal_trajectory_generation.cpp)
#
#  target_link_libraries(test_time_optimal_trajectory_generation ${LIB_NAME})
#endif()
