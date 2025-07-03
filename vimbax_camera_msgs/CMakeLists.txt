cmake_minimum_required(VERSION 3.8)
project(vimbax_camera_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

###############################################################################
# Dependencies
###############################################################################
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(std_msgs REQUIRED)

###############################################################################
# Interface files
###############################################################################
set(vimbax_camera_MSGS
  msg/FeatureFlags.msg
  msg/FeatureInfo.msg
  msg/EventDataEntry.msg
  msg/EventData.msg
  msg/Error.msg
  msg/FeatureModule.msg
  msg/TriggerInfo.msg
  msg/StereoSyncStatus.msg
  msg/CameraMetadata.msg
)

set(vimbax_camera_SRVS
  srv/FeatureIntGet.srv
  srv/FeatureIntSet.srv
  srv/FeatureIntInfoGet.srv
  srv/FeatureFloatGet.srv
  srv/FeatureFloatSet.srv
  srv/FeatureFloatInfoGet.srv
  srv/FeatureStringGet.srv
  srv/FeatureStringSet.srv
  srv/FeatureStringInfoGet.srv
  srv/FeatureBoolGet.srv
  srv/FeatureBoolSet.srv
  srv/FeatureCommandIsDone.srv
  srv/FeatureCommandRun.srv
  srv/FeatureEnumGet.srv
  srv/FeatureEnumSet.srv
  srv/FeatureEnumInfoGet.srv
  srv/FeatureEnumAsIntGet.srv
  srv/FeatureEnumAsStringGet.srv
  srv/FeatureRawGet.srv
  srv/FeatureRawSet.srv
  srv/FeatureRawInfoGet.srv
  srv/FeatureAccessModeGet.srv
  srv/FeatureInfoQuery.srv
  srv/FeaturesListGet.srv
  srv/SettingsLoadSave.srv
  srv/Status.srv
  srv/StreamStartStop.srv
  srv/SubscribeEvent.srv
  srv/UnsubscribeEvent.srv
  srv/TriggerTime.srv
  srv/ConnectionStatus.srv
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${vimbax_camera_MSGS}
  ${vimbax_camera_SRVS}
  DEPENDENCIES builtin_interfaces std_msgs
)

###############################################################################
# Install / export the generated headers *once*
###############################################################################
# This grabs everything under the build-tree include dir and puts it in
#   install/vimbax_camera_msgs/include/vimbax_camera_msgs/…
install(
  DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/rosidl_generator_cpp/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
)

ament_export_include_directories(include)

###############################################################################
# Tests
###############################################################################
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
