# Файлы запуска

Файлы запуска в ROS могут выполнять несколько задач в одном файле. Файлы запуска имеют расширение .launch. В следующем коде показано определение start\_usb\_cam.launch, которое запускает узел usb\_cam для публикации изображения с камеры в качестве топика ROS:

```text
<launch>
<node name="usb_cam" pkg="usb_cam" type="usb_cam_node" output="screen" >
<param name="video_device" value="/dev/video0" />
<param name="image_width" value="640" />
<param name="image_height" value="480" />
<param name="pixel_format" value="yuyv" />
<param name="camera_frame_id" value="usb_cam" />
<param name="auto_focus" value="false" />
<param name="io_method" value="mmap"/>
</node>
</launch>
```

В пределах &lt;node&gt;…&lt;/node&gt; теги, есть параметры камеры, которые могут быть изменены пользователем. Например, если у вас есть несколько камер, вы можете изменить video\_device значение от /DEV/video0 в /DEV/video1, чтобы получить кадры второй камеры.

Следующий важный файл запуска - start\_tracking.launch, который запустит узел отслеживания лица. Вот определение этого файла запуска:

```text
<launch>
<!-- Запуск файлов запуска USB CAM и контроллеров Dynamixel-->
<include file="$(find face_tracker_pkg)/launch/start_usb_cam.launch"/>
<!-- Начальный узел трекера лица -->
<rosparam file="$(find face_tracker_pkg)/config/track.yaml" command="load"/>
<node name="face_tracker" pkg="face_tracker_pkg" type="face_tracker_node" output="screen" />
</launch>
```

Этот код сначала запустит start\_usb\_cam.launch файл, чтобы получить топики ROS image, а затем загрузит track.yaml, чтобы получить необходимые параметры ROS, а затем загрузит face\_tracker\_node, чтобы начать отслеживать.

Окончательный файл запуска start\_dynamixel\_tracking.launch; это стартовый файл, который мы должны выполнить для отслеживания и управления Dynamixel. Мы обсудим этот файл запуска в конце главы после обсуждения face\_tracker\_control пакет.

