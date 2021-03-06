cmake_minimum_required(VERSION 3.5)

project(control_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(action_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(trajectory_msgs REQUIRED)

set(msg_files
  msg/DynamicJointState.msg
  msg/GripperCommand.msg
  msg/InterfaceValue.msg
  msg/JointControllerState.msg
  msg/JointJog.msg
  msg/JointTolerance.msg
  msg/JointTrajectoryControllerState.msg
  msg/PidState.msg
)

set(action_files
  action/FollowJointTrajectory.action
  action/GripperCommand.action
  action/JointTrajectory.action
  action/PointHead.action
  action/SingleJointPosition.action
)

set(srv_files
  srv/QueryCalibrationState.srv
  srv/QueryTrajectoryState.srv
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  ${action_files}
  DEPENDENCIES action_msgs builtin_interfaces geometry_msgs std_msgs trajectory_msgs
  ADD_LINTER_TESTS
)
ament_export_dependencies(rosidl_default_runtime)
ament_package()
