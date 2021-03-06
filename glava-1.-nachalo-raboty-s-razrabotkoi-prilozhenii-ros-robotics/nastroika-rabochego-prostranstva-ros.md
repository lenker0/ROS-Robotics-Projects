# Настройка рабочего пространства ROS

После установки ROS на реальном ПК или VirtualBox, следующим шагом является создание рабочего пространства в ROS. Рабочая область ROS - это место, где мы храним пакеты ROS. В последнем выпуске ROS мы используем рабочее пространство на основе catkin для сборки и установки пакетов ROS. Система сережек \([http://wiki.ros.org/catkin](http://wiki.ros.org/catkin)\) - это официальная система сборки ROS, которая помогает нам встраивать исходный код в целевой исполняемый файл или библиотеки внутри рабочей области ROS.

Создание рабочего пространства ROS - это простая задача; просто откройте терминал и следуйте этим инструкциям:

1. Первым шагом является создание пустой папки рабочего пространства и другой папки с именем src для хранения пакета в ROS. Следующая команда выполнит эту работу. Имя папки рабочей области здесь catkin\_ws.

**`$ mkdir -p ~/catkin_ws/src`**

  
2.    Переключиться на src папку и выполните catkin\_init\_workspaceкоманда. Эта команда инициализирует рабочую область catkin в текущей src папки. Теперь мы можем начать создавать пакеты внутри src папки.

**`$ cd ~/catkin_ws/src  
$ catkin_init_workspace`**

3.    После инициализации рабочего пространства catkin мы можем собрать пакеты внутри рабочего пространства, используя следующую команду: catkin\_make, Мы можем построить рабочее пространство даже без каких-либо пакетов.

**`$ cd  ~/catkin_ws/  
$ catkin_make`**

4.    Это создаст дополнительные папки с именем build и devel внутри рабочей области ROS:

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 19: &#x41F;&#x430;&#x43F;&#x43A;&#x438; &#x440;&#x430;&#x431;&#x43E;&#x447;&#x435;&#x433;&#x43E; &#x43F;&#x440;&#x43E;&#x441;&#x442;&#x440;&#x430;&#x43D;&#x441;&#x442;&#x432;&#x430; catkin](../.gitbook/assets/image%20%2820%29.png)

5.    После того, как вы создали рабочее пространство, для доступа к пакетам внутри рабочего пространства мы должны добавить среду рабочего пространства в нашу .bashrc файл с помощью следующей команды:

**`$ echo "source ~/catkin_ws/devel/setup.bash" >> ~ /.Bashrc  
$ source ~/.bashrc`**

6.    Если все сделано, вы можете проверить это, выполнив следующую команду. Эта команда напечатает весь путь к пакету ROS. Если ваш путь к рабочей области находится в выходных данных, все готово!

**`$ echo $ ROS_PACKAGE_PATH`**

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 20. &#x41F;&#x443;&#x442;&#x44C; &#x43A; &#x43F;&#x430;&#x43A;&#x435;&#x442;&#x443; ROS](../.gitbook/assets/image%20%2816%29.png)



