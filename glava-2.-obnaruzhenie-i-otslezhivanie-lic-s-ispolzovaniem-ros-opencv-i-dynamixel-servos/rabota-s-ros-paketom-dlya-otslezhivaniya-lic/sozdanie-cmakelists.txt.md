# Создание CMakeLists.txt

Как и в первом пакете трекера, в контрольном пакете нет особой разницы; разница в зависимостях. Здесь основной зависимостью является dynamicixel\_controllers. Мы не используем OpenCV в этом пакете, поэтому нет необходимости включать его:

```text
cmake_minimum_required(VERSION 2.8.3)
project(face_tracker_control) 
find_package(catkin REQUIRED COMPONENTS
dynamixel_controllers 
roscpp
rospy 
std_msgs
message_generation
)
find_package(Boost REQUIRED COMPONENTS system) add_message_files(FILES centroid.msg )
##Генерирует добавленные сообщения и сервисы с любыми зависимостями, перечисленными здесь
generate_messages( DEPENDENCIES std_msgs )
catkin_package(
CATKIN_DEPENDS dynamixel_controllers roscpp rospy std_msgs
)
include_directories(
${catkin_INCLUDE_DIRS}
)
add_executable(face_tracker_controller src/face_tracker_controller.cpp) target_link_libraries(face_tracker_controller ${catkin_LIBRARIES})
```

Полный исходный код этого проекта может быть клонирован из следующего репозитория Git. Следующая команда клонирует репозиторий проекта:

`$ git clone` [`https://github.com/qboticslabs/ros_robotics_projects`](https://github.com/qboticslabs/ros_robotics_projects)\`\`

