# Понимание CMakeLists.txt

По умолчанию файл CMakeLists.txt, созданный при создании пакета, должен быть отредактирован, чтобы скомпилировать предыдущий исходный код. Здесь CMakeLists.txt - файл, используемый для построения face\_tracker\_node.cpp класса.

В первых двух строках указывается минимальная версия cmake, необходимая для сборки этого пакета, а в следующей строке указывается имя пакета:

```text
cmake_minimum_required(VERSION 2.8.3)
project(face_tracker_pkg)
```

Следующая строка ищет зависимые пакеты face\_tracker\_pkg и выдает ошибку, если она не найдена:

```text
find_package(catkin REQUIRED COMPONENTS cv_bridge
image_transport roscpp
rospy sensor_msgs std_msgs
message_generation
)
```

Эта строка кода содержит зависимости системного уровня для сборки пакета:

```text
find_package(Boost REQUIRED COMPONENTS system)
```

Как мы уже видели, мы используем пользовательское определение сообщения centroid.msg, которое содержит два поля: int32 x и int32 y. Чтобы создать и сгенерировать эквивалентные заголовки C ++, мы должны использовать следующие строки:

```text
add_message_files( FILES centroid.msg )
## Генерирует добавленные сообщения и сервисы с любыми зависимостями, перечисленными здесь
generate_messages( DEPENDENCIES std_msgs )
```

Функция catkin\_package\(\) - это предоставляемый Catkin макрос CMake, необходимый для генерации PKG-config CMake файлов.

```text
catkin_package (CATKIN_DEPENDS roscpp rospy std_msgs message_runtime )
include_directories ( $ {catkin_INCLUDE_DIRS} )
```

Здесь мы создаем исполняемый файл face\_tracker\_node и связываем его с библиотеками catkin и OpenCV:

```text
add_executable(face_tracker_node src/face_tracker_node.cpp) target_link_libraries(face_tracker_node ${catkin_LIBRARIES} ${OpenCV_LIBRARIES} )
```

