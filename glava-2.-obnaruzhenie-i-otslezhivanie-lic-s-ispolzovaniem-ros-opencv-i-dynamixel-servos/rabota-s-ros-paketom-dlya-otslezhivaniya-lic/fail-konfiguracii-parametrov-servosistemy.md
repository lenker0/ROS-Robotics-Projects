# Файл конфигурации параметров сервосистемы

Файл servo\_param.yaml содержит конфигурацию pan\_controller, такую ​​как пределы контроллера и расстояние шага каждого движения; Кроме того, он имеет параметры экрана, такие как максимальное разрешение изображения с камеры и смещение от центра изображения. Смещение используется для определения области вокруг фактического центра изображения:

```text
servomaxx: 0.5       #максимальный градус, на который можно повернуть сервопривод (х) 
servomin: -0.5       #минимальный градус, на который можно повернуть сервопривод (х)
screenmaxx: 640      #максимальное расширение по горизонитали (х) 
center_offset: 50    #смещение пикселей от фактического центра вправо и влево
step_distancex: 0.01 #x шаг вращения сервопривода
```
