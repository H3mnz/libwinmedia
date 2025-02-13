cmake_minimum_required(VERSION 3.15)
set(PROJECT_NAME libwinmedia_flutter)
project(${PROJECT_NAME} LANGUAGES CXX)


set(DART_VM Enabled)
add_subdirectory(
  ${CMAKE_CURRENT_SOURCE_DIR}/../.master
  ${CMAKE_CURRENT_BINARY_DIR}/libwinmedia
)


set(PLUGIN_NAME libwinmedia_plugin)
add_library(${PLUGIN_NAME} SHARED
  libwinmedia_plugin.cpp
)
apply_standard_settings(${PLUGIN_NAME})
set_target_properties(${PLUGIN_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden)
target_compile_definitions(${PLUGIN_NAME} PRIVATE FLUTTER_PLUGIN_IMPL)
target_include_directories(${PLUGIN_NAME} INTERFACE
  ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(${PLUGIN_NAME} PRIVATE flutter flutter_wrapper_plugin)

set(libwinmedia_bundled_libraries
  $<TARGET_FILE:libwinmedia>
  PARENT_SCOPE
)
