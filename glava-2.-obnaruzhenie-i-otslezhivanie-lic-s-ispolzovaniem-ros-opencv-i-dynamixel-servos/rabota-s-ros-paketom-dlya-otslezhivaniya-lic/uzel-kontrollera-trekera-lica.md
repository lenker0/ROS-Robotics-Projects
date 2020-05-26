# Узел контроллера трекера лица

Как мы уже видели, узел контроллера трекера лица отвечает за управление сервоприводом Dynamixel в соответствии с положением центроида лица. Давайте разберемся в коде этого узла, который находится по адресу face\_tracker\_control/src/face\_tracker\_controller.cpp.

Основные заголовки ROS, включенные в этот код, следующие. Здесь заголовок Float64 используется для хранения сообщения значения позиции контроллеру:

```text
#include "ros/ros.h"
#include "std_msgs/Float64.h" 
#include <iostream>
```

Следующие переменные содержат значения параметров из servo\_param.yaml:

```text
int servomaxx, servomin,screenmaxx, center_offset, center_left, center_right;
float servo_step_distancex, current_pos_x;
```

Следующие заголовки сообщения std\_msgs::Float64 предназначены для хранения начальной и текущей позиции контроллера, соответственно. Контроллер принимает только этот тип сообщения:

```text
std_msgs::Float64 initial_pose; 
std_msgs::Float64 current_pose;
```

Это обработчик издателя для публикации команд положения в контроллере:

```text
ros::Publisher dynamixel_control;
```

Переходя к функции main\(\) кода, вы можете увидеть следующие строки кода. Первая строка - это подписчик /face\_centroid, у которого есть значение centroid, и когда значение приходит в тему, оно вызывает функцию face\_callback \(\):

```text
ros::Subscriber number_subscriber = node_obj.subscribe("/face_centroid",10,face_callback);
```

Следующая строка инициализирует дескриптор издателя, в котором значения будут опубликованы в разделе / ​​pan\_controller / command:

```text
dynamixel_control = node_obj.advertise<std_msgs::Float64> ("/pan_controller/command",10);
```

Следующий код создает новые ограничения вокруг фактического центра изображения. Это будет полезно для получения приблизительной центральной точки изображения:

```text
center_left = (screenmaxx / 2) - center_offset; 
center_right = (screenmaxx / 2) + center_offset;
```

Вот функция обратного вызова, выполняемая при получении значения центроида, поступающего через раздел /face\_centroid. Этот обратный вызов также имеет логику для перемещения Dynamixel для каждого значения центроида.

В первом разделе значение x в центроиде сравнивается с center\_left, а если оно слева, оно просто увеличивает положение сервоконтроллера. Он будет публиковать текущее значение, только если текущая позиция находится в пределах лимита. Если он находится в пределе, то он опубликует текущую позицию в контроллере. Логика одинакова для правой стороны: если грань находится на правой стороне изображения, это уменьшит положение контроллера.

Когда камера достигает центра изображения, она останавливается и ничего не делает, и это то, чего мы тоже хотим. Этот цикл повторяется, и мы получим непрерывное отслеживание:

```text
void track_face(int x,int y)
{
if (x < (center_left)){
current_pos_x += servo_step_distancex; 
current_pose.data = current_pos_x;
if (current_pos_x < servomaxx and current_pos_x > servomin ){ dynamixel_control.publish(current_pose);
  }
}
else if(x > center_right){ current_pos_x -= servo_step_distancex; current_pose.data = current_pos_x;
if (current_pos_x < servomaxx and current_pos_x > servomin ){ dynamixel_control.publish(current_pose);
  }
}
else if(x > center_left and x < center_right){; 
  }
}
```

