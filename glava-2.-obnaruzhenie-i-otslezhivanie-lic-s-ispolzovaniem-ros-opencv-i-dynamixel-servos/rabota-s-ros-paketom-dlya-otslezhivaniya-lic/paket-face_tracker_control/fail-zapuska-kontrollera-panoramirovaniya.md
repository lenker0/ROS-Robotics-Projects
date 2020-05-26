# Файл запуска контроллера панорамирования

Как видно из предыдущего подраздела, файл запуска контроллера панорамирования является триггером для подключения контроллера ROS к обнаруженным сервоприводам. Вот определение для файла start\_pan\_controller.launch:

Это запустит контроллер панорамирования:

```text
<launch>
<!-- Запустить контроллер наклона -->
<rosparam file="$(find face_tracker_control)/config/pan.yaml" command="load"/>
<rosparam file="$(find face_tracker_control)/config/servo_param.yaml" command="load"/>
<node name="tilt_controller_spawner" pkg="dynamixel_controllers" type="controller_spawner.py" args="--manager=dxl_manager--port pan_port pan_controller"output="screen"/>
</launch>
```

 controller\_spawner.py узел может создать контроллер для каждого обнаруженного сервопривода. Параметры контроллеров и сервоприводов включены в pan.yaml, а также servo\_param.yaml.  


