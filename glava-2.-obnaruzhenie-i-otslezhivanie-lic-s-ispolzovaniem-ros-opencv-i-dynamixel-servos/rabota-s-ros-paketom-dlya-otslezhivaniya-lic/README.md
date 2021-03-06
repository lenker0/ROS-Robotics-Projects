# Работа с ROS-пакетом для отслеживания лиц

Мы уже создали или скопировали пакет face\_tracker\_pkg в рабочую область и обсудили некоторые из его важных зависимостей. Теперь мы собираемся обсудить, что именно делает этот пакет!  


Этот пакет состоит из узла ROS с именем face\_tracker\_node, который может отслеживать лица с помощью API OpenCV и публиковать центроид лица в теме. Вот блок-схема работы face\_tracker\_node:

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 15: &#x411;&#x43B;&#x43E;&#x43A;-&#x441;&#x445;&#x435;&#x43C;&#x430; face\_tracker\_node](../../.gitbook/assets/image%20%2814%29.png)

![](file:///C:/Users/MICHAE~1/AppData/Local/Temp/msohtmlclip1/01/clip_image003.jpg)Давайте обсудим вещи, связанные с face\_tracker\_node. Один из разделов, который может быть вам незнаком, - это классификатор Face Haar:

* **Face** **Haar** **классификатор**: Каскадный классификатор на основе признаков Хаара - это подход машинного обучения для обнаружения объектов. Этот метод был предложен Полом Виола и Майклом Джонсом в их работе «Быстрое обнаружение объектов» с использованием расширенного каскада простых функций в 2001 году. В этом методе каскадный файл обучается с использованием положительного и отрицательного образца изображения, и после обучения этот файл используется для обнаружения объекта.
* В нашем случае мы используем обученный файл классификатора Haar вместе с исходным кодом OpenCV. Вы получите эти файлы классификатора Хаара из папки данных OpenCV \([https://github.com/opencv/opencv/tree/master/data](https://github.com/opencv/opencv/tree/master/data)\). Вы можете заменить нужный файл Haar в соответствии с вашей задачей. Здесь мы используем классификатор лица. Классификатор это XML-файл, в котором есть теги, содержащие признаки лица. После того, как функции внутри XML совпадают, мы можем извлечь интересующую область \(ROI\) лица из изображения, используя API-интерфейсы OpenCV. Вы можете проверить классификатор Хаара этого проекта из face\_tracker\_pkg / data / face.xml.
* track.yaml: Это файл параметров ROS, имеющий такие параметры, как путь к файлу Haar, тема входного изображения, тема выходного изображения и флаги для включения и отключения отслеживания лица. Мы используем файлы конфигурации ROS, потому что мы можем изменить параметры узла без изменения исходного кода трекера лица. Вы можете получить этот файл из face\_tracker\_pkg/config/track.xml.
*  Узел usb\_cam. В пакете usb\_cam есть узел, публикующий поток изображений с камеры в сообщениях ROS Image. Узел usb\_cam публикует изображения с камеры в топике /usb\_cam/raw\_image, и эта тема подписывается узлом отслеживания лица для обнаружения лица. Мы можем изменить топик ввода в файле track.yaml, если потребуется.
* face\_tracker\_control: это второй пакет, который мы собираемся обсудить. Пакет face\_tracker\_pkg может обнаруживать лица и определять центр тяжести лица на изображении. Сообщение центроида содержит два значения, X и Y. Мы используем пользовательское определение сообщения для отправки значений центроида. Эти значения центроида подписываются узлом контроллера и перемещают Dynamixel для отслеживания лица. Dynamixel контролируется этим узлом.

Вот файловая структура face\_tracker\_pkg:

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 16: &#x424;&#x430;&#x439;&#x43B;&#x43E;&#x432;&#x430;&#x44F; &#x441;&#x442;&#x440;&#x443;&#x43A;&#x442;&#x443;&#x440;&#x430; face\_tracker\_pkg](../../.gitbook/assets/image%20%284%29.png)

Давайте посмотрим, как работает код отслеживания лица. Вы можете открыть файл CPP по адресуface\_tracker\_pkg/SRC/face\_tracker\_node.cpp, Этот код выполняет обнаружение лица и отправляет значение центроида в тему.

Мы рассмотрим и поймем некоторые фрагменты кода.

