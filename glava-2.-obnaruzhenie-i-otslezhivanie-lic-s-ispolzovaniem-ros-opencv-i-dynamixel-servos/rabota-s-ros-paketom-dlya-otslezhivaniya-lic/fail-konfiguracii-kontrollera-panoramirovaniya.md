# Файл конфигурации контроллера панорамирования

Файл конфигурации контроллера панорамирования содержит конфигурацию контроллера, которую собирается создать узел порождения контроллера. Вот определение файла pan.yaml для нашего контроллера:

```text
pan_controller: 
  controller:
    package: dynamixel_controllers 
    module: joint_position_controller 
    type: JointPositionController
joint_name: pan_joint 
joint_speed: 1.17 
  motor: 
    id: 1
    init: 512
    min: 316
    max: 708
```

В этом файле конфигурации мы должны упомянуть детали сервомотора, такие как идентификатор, начальное положение, минимальные и максимальные пределы сервопривода, скорость перемещения сервопривода и имя соединения. Имя контроллера - pan\_controller, и это совместный контроллер положения. Мы пишем одну конфигурацию контроллера для ID 1, потому что мы используем только один сервопривод.
