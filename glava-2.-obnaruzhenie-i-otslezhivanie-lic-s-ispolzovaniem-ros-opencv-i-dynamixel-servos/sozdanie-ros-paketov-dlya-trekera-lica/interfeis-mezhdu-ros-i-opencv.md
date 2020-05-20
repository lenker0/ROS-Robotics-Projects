# Интерфейс между ROS и OpenCV

**Open Source Computer Vision** \(OpenCV\) - это библиотека, в которой есть API для выполнения приложений компьютерного зрения. Проект был начат в Intel Russia, а позже его поддержали Willow Garage и Itseez. В 2016 году Itseez была приобретена Intel.

OpenCV website: [h](http://opencv.org/)[t](http://opencv.org/)[t](http://opencv.org/)[p](http://opencv.org/)[://o](http://opencv.org/)[p](http://opencv.org/)[e](http://opencv.org/)[n](http://opencv.org/)[c](http://opencv.org/)[v](http://opencv.org/)[.](http://opencv.org/)[o](http://opencv.org/)[r](http://opencv.org/)[g](http://opencv.org/)[/](http://opencv.org/)

Willow Garage: [h](http://www.willowgarage.com/)[t](http://www.willowgarage.com/)[t](http://www.willowgarage.com/)[p](http://www.willowgarage.com/)[://w](http://www.willowgarage.com/)[w](http://www.willowgarage.com/)[w](http://www.willowgarage.com/)[.](http://www.willowgarage.com/)[w](http://www.willowgarage.com/)[i](http://www.willowgarage.com/)[l](http://www.willowgarage.com/)[l](http://www.willowgarage.com/)[o](http://www.willowgarage.com/)[w](http://www.willowgarage.com/)[g](http://www.willowgarage.com/)[a](http://www.willowgarage.com/)[r](http://www.willowgarage.com/)[a](http://www.willowgarage.com/)[g](http://www.willowgarage.com/)[e](http://www.willowgarage.com/)[.](http://www.willowgarage.com/)[c](http://www.willowgarage.com/)[o](http://www.willowgarage.com/)[m](http://www.willowgarage.com/)[/](http://www.willowgarage.com/)

Itseez: [http://itseez.com](http://itseez.com/)

OpenCV - это кроссплатформенная библиотека, которая поддерживает большинство операционных систем. Теперь у него также есть лицензия BSD с открытым исходным кодом, поэтому мы можем использовать ее для исследовательских и коммерческих приложений. Версия OpenCV, взаимодействующая с ROS Kinetic, - 3.1. В версиях 3.x OpenCV есть несколько изменений в API по сравнению с версиями 2.x.

Библиотека OpenCV интегрирована в ROS через пакет под названием vision\_opencv, Этот пакет уже был установлен, когда мы установили ros-kinetic-desktop-full в главе 1, Начало работы с разработкой приложений ROS Robotics.

 vision\_opencv В metapackage есть два пакета:

·         cv\_bridge: Этот пакет отвечает за преобразование типа данных изображения OpenCV \(cv::Mat\) в ROS Образ Сообщения \(sensor\_msgs/Image.msg\).

·         image\_geometry: Этот пакет помогает нам интерпретировать изображения геометрически. Этот узел поможет в обработке, такой как калибровка камеры и выпрямление изображения.

Из этих двух пакетов мы в основном имеем дело с cv\_bridge. Используя cv\_bridge, узел отслеживания лица может конвертировать сообщения ROS Image из usb\_cam в эквивалент OpenCV, cv::Mat. После преобразования в cv::Mat мы можем использовать API OpenCV для обработки изображения с камеры.  


Вот блок-схема, которая показывает роль cv\_bridge в этом проекте:

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 14: &#x440;&#x43E;&#x43B;&#x44C; cv\_bridge](../../.gitbook/assets/image%20%2843%29.png)

Здесь cv\_bridge работает между узлом usb\_cam и узлом отслеживания лица. Мы узнаем больше об узле отслеживания лица в следующем разделе. До этого будет хорошо, если вы получите представление о его работе.

Еще один пакет, который мы используем для передачи сообщений ROS Image между двумя узлами ROS, это image\_transport \([http://wiki.ros.org/image\_transport](http://wiki.ros.org/image_transport)\). Этот пакет всегда используется для подписки и публикации данных изображений в ROS. Пакет может помочь нам транспортировать изображения с низкой пропускной способностью, применяя методы сжатия. Этот пакет также устанавливается вместе с полной установкой ROS на рабочем столе.

Это все об OpenCV и интерфейсе ROS. В следующем разделе мы будем работать с первым пакетом этого проекта: face\_tracker\_pkg.

Полный исходный код этого проекта может быть клонирован из следующего репозитория Git. Следующая команда клонирует репозиторий проекта:

**`$ git clone https://github.com/qboticslabs/ros_robotics_projects`**

