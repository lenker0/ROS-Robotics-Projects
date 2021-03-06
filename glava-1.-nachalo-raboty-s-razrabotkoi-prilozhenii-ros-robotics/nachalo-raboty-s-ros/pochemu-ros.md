# Почему ROS?

Основная цель создания инфраструктуры ROS, - стать общей программной средой для роботов. Несмотря на то, что до ROS проводились исследования в области робототехники, большая часть программного обеспечения была эксклюзивной для их собственных роботов. Их программное обеспечение может быть с открытым исходным кодом, но его очень сложно использовать повторно.

По сравнению с существующими роботизированными средами, ROS превосходит их по следующим аспектам:

* **Совместная разработка**: как мы уже говорили, ROS является открытым исходным кодом и может свободно использоваться для отраслей промышленности и научных исследований. Разработчики могут расширить функциональные возможности ROS, добавив пакеты. Почти все пакеты ROS работают на уровне аппаратной абстракции, поэтому его можно легко использовать для других роботов. Значит, если один университет хорош в мобильной навигации, а другой - в роботизированных манипуляторах, они могут внести свой вклад в сообщество ROS, а другие разработчики могут повторно использовать свои пакеты и создавать новые приложения.
* **Поддержка языков**: Коммуникационная структура ROS может быть легко реализована на любом современном языке. Он уже поддерживает популярные языки, такие как C ++, Python и Lisp, и имеет экспериментальные библиотеки для Java и Lua.
* **Интеграция библиотек**: ROS имеет интерфейс для многих сторонних робототехнических библиотек, таких как Open Source Computer Vision \(Open-CV\), Point Cloud Library \(PCL\), Open-NI, Open-Rave и Orocos. Разработчики могут работать с любой из этих библиотек без особых хлопот.
* **Интеграция с симуляторами**: ROS также имеет связи с симуляторами с открытым исходным кодом, такими как Gazebo, и имеет хороший интерфейс с проприетарными симуляторами, такими как Webots и V-REP.
* **Тестирование кода**: ROS предлагает встроенную среду тестирования, которая называется rostest, для проверки качества кода и ошибок.
* **Масштабируемость**: Платформа ROS разработана для масштабирования. Мы можем выполнять сложные вычислительные задачи с роботами, используя ROS, которые могут быть размещены либо в облаке, либо в гетерогенных кластерах.
* **Настраиваемость**: как мы уже говорили, ROS является полностью открытым исходным кодом и бесплатен, поэтому можно настроить эту среду в соответствии с требованиями робота. Если мы хотим работать только с платформой обмена сообщениями ROS, мы можем удалить все остальные компоненты и использовать только это. Можно даже настроить ROS для конкретного робота для лучшей производительности.
* **Сообщество**: ROS — это проект, управляемый сообществом, и в основном его возглавляет OSRF. Поддержка большого сообщества - большой плюс для ROS, и можно легко начать разработку приложений для робототехники.

Здесь приведены URL-адреса библиотек и симуляторов, интегрированных с ROS:

* Open-CV: http://wiki.ros.org/vision\_opencv
* PCL: http://wiki.ros.org/pcl\_ros
* Open-NI: http://wiki.ros.org/openni\_launch
* Open-Rave: http://openrave.org/
* Orocos: http://www.orocos.org/
* Webots: https://www.cyberbotics.com/overview
* V-REP: http://www.coppeliarobotics.com/

  Давайте рассмотрим некоторые основные концепции ROS; они могут помочь вам начать работу с проектами ROS.

