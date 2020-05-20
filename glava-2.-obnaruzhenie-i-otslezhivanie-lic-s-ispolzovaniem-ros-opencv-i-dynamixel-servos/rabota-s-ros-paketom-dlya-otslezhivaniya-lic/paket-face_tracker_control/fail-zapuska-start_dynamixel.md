# Файл запуска start\_dynamixel

Файл запуска start\_dynamixel запускает Dynamixel Control Manager, который может устанавливать соединение с адаптером USB-Dynamixel и сервоприводами Dynamixel. Вот определение этого файла запуска:

```text
<!-- Откроется контроллер USB To Dynamixel и начнется поиск сервоприводов. -->
<launch>
<node name="dynamixel_manager" pkg="dynamixel_controllers" type="controller_manager.py" required="true" output="screen">
<rosparam>
  namespace: dxl_manager serial_ports:
    pan_port:
      port_name: "/dev/ttyUSB0" 
      baud_rate: 1000000
      min_motor_id: 1
      max_motor_id: 25
      update_rate: 20
</rosparam>
</node>
<!-- Это запустит контроллер панорамирования Dynamixel -->
<include file="$(find face_tracker_control)/launch/start_pan_controller.launch"/>
</launch>
```

Мы должны упомянуть port\_name \(Вы можете получить номер порта из журналов ядра, используя dmesg команд\). baud\_rate мы настроили 1 Мбит/с, а идентификатор двигателя был 1, controller\_manager.py файл будет сканироваться с серво ID 1 в 25 и сообщать о любых обнаруженных сервоприводах. После обнаружения сервопривода он запустит файл start\_pan\_controller.launch, который будет прикреплять контроллер положения соединения ROS для каждого сервопривода.

