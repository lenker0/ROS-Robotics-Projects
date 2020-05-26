# Подглава 2.5.12 Соединение всех узлов вместе

Далее мы рассмотрим окончательный файл запуска, который мы пропустили при рассмотрении face\_tracker\_pkg пакет, и это start\_dynamixel\_tracking.launch, Этот файл запускает как распознавание лиц, так и отслеживание с помощью двигателей Dynamixel:

```text
<launch>
<!-- Запуск файлов запуска USB CAM и контроллеров Dynamixel -->
<include file="$(find face_tracker_pkg)/launch/start_tracking.launch"/>
<include file="$(find face_tracker_control)/launch/start_dynamixel.launch"/>
<!-- Запуск узла, отслеживающего лица -->
<node name="face_controller" pkg="face_tracker_control" type="face_tracker_controller" output="screen" />
</launch>
```

