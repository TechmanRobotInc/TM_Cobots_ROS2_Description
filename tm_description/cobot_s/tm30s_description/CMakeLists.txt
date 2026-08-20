cmake_minimum_required(VERSION 3.10.2)
project(tm30s_description)

find_package(ament_cmake REQUIRED)

install(
  DIRECTORY launch meshes rviz xacro
  DESTINATION share/${PROJECT_NAME}
)

ament_package()
