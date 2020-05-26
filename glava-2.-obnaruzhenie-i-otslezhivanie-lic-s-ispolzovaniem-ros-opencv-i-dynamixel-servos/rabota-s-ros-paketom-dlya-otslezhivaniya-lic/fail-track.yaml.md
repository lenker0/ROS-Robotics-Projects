# Подглава 2.5.3 Файл track.yaml

Как мы уже говорили, файл track.yaml содержит параметры ROS, которые требуются face\_tracker\_node, Вот содержимое track.yaml:

```text
image_input_topic: "/usb_cam/image_raw" 
face_detected_image_topic: "/face_detector/raw_image" 
haar_file_face: "/home/robot/ros_robotics_projects_ws/src/face_tracker_pkg/data/face.xml"
face_tracking: 1
display_original_image: 1
display_tracking_image: 1
```

Вы можете изменить все параметры в соответствии с вашими потребностями. В частности, вам может потребоваться изменить haar\_file\_face, который является доступом к файлу лица Haar. Если мы установим face\_tracking: 1, он включит отслеживание лица, в противном случае нет. Кроме того, если вы хотите отобразить исходное изображение и изображение для отслеживания лица, вы можете установить здесь флаг.

