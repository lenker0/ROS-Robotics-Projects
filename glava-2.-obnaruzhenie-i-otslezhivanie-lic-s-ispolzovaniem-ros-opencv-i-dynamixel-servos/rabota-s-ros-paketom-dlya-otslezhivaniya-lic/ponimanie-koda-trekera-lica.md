# Подглава 2.5.1 Понимание кода трекера лица

Давайте начнем с заголовочного файла. Заголовочные файлы ROS, которые мы используем в коде, находятся здесь. Мы должны включить ros/ros.h в каждый узел ROS C ++; в противном случае исходный код не будет компилироваться. Остальные три заголовка являются заголовками транспорта изображения, которые имеют функции для публикации и подписки на сообщения изображения с низкой пропускной способностью. Заголовок cv\_bridge имеет функции для преобразования между типами данных OpenCV ROS. Заголовок image\_encoding.h имеет формат кодирования изображения, используемый во время преобразования ROS-OpenCV:

```text
#include <ros/ros.h>
#include <image_transport/image_transport.h>
#include <cv_bridge/cv_bridge.h>
#include <sensor_msgs/image_encodings.h>
```

Следующий набор заголовков для OpenCV. Заголовок imgproc состоит из функций обработки изображений, highgui имеет функции, связанные с GUI, а objdetect.hpp имеет API для обнаружения объектов, такие как классификатор Haar:

```text
#include <opencv2/imgproc/imgproc.hpp> 
#include <opencv2/highgui/highgui.hpp> 
#include <opencv2/objdetect.hpp>
```

Последний заголовочный файл предназначен для доступа к пользовательскому сообщению с именем centroid. Определение сообщения центроида имеет два поля, int32x ,а также Int32 года, Он может держать центр тяжести файла. Вы можете проверить это определение сообщения из папки face\_tracker\_pkg/msg/centroid.msg:

```text
#include <face_tracker_pkg/centroid.h>
```

Следующие строки кода дают имя окну необработанного изображения и окну обнаружения лица:

```text
static const std::string OPENCV_WINDOW = "raw_image_window"; 
static const std::string OPENCV_WINDOW_1 = "face_detector";
```

Следующие строки кода создают класс C ++ для нашего детектора лиц. Фрагмент кода создает дескрипторы NodeHandle, который является обязательным дескриптором для узла ROS; image\_transport, который помогает отправлять сообщения ROS Image по графу вычислений ROS; и издатель для лицевого центроида, который может публиковать значения центроидов, используя определенный нами файл centroid.msg. Остальные определения предназначены для обработки значений параметров из файла параметров track.yaml:

```text
class Face_Detector{
ros::NodeHandle nh_; 
image_transport::ImageTransport it_; 
image_transport::Subscriber image_sub_; 
image_transport::Publisher image_pub_; 
ros::Publisher face_centroid_pub; 
face_tracker_pkg::centroid face_centroid;string input_image_topic, output_image_topic, haar_file_face;
int face_tracking, display_original_image, display_tracking_image, center_offset, screenmaxx;
}
```

Ниже приведен код для извлечения параметров ROS из файла track.yaml. Преимущество использования параметров ROS состоит в том, что мы можем избежать жесткого кодирования этих значений внутри программы и изменять значения без перекомпиляции кода:

```text
try{
nh_.getParam("image_input_topic", input_image_topic); nh_.getParam("face_detected_image_topic", output_image_topic); nh_.getParam("haar_file_face", haar_file_face); nh_.getParam("face_tracking", face_tracking); nh_.getParam("display_original_image", display_original_image); nh_.getParam("display_tracking_image", display_tracking_image); nh_.getParam("center_offset", center_offset); nh_.getParam("screenmaxx", screenmaxx);
ROS_INFO("Successfully Loaded tracking parameters");
}
```

Следующий код создает подписчика для topic входного изображения и издателя для изображения с обнаруженным лицом. Всякий раз, когда изображение попадает в topic входного изображения, оно вызывает функцию imageCb. Названия тем извлекаются из параметров ROS. Мы создаем другого издателя для публикации значения центроида, который является последней строкой фрагмента кода:

```text
image_sub_ = it_.subscribe(input_image_topic, 1, &Face_Detector::imageCb, this);
image_pub_ = it_.advertise(output_image_topic, 1);
face_centroid_pub = nh_.advertise<face_tracker_pkg::centroid> ("/face_centroid",10);
```

Следующий фрагмент кода - это определение imageCb, который является обратным вызовом для input\_image\_topic, что он в основном делает, это конвертирует sensor\_msgs/Image данные в cv::Mat Тип данных OpenCV. cv\_bridge::CvImagePtr cv\_ptr буфер выделяется для хранения образа OpenCV после выполнения преобразования ROS-OpenCV с использованием функции cv\_bridge::toCvCopy:

```text
void imageCb(const sensor_msgs::ImageConstPtr& msg)
{
cv_bridge::CvImagePtr cv_ptr;
namespace enc = sensor_msgs::image_encodings;
try
{
cv_ptr = cv_bridge::toCvCopy(msg, sensor_msgs::image_encodings::BGR8);
}
//Мы уже обсуждали классификатор Хаара; Вот код для загрузки файла классификатора Хаара:
string cascadeName = haar_file_face; CascadeClassifier cascade;
if( !cascade.load( cascadeName ) )
{
cerr << "ERROR: Could not load classifier cascade" << endl;
}
```

Теперь мы переходим к основной части программы, которая заключается в обнаружении лица, выполненного для преобразованного типа данных изображения OpenCV, из сообщения ROS Image. Ниже приведен вызов функции detectAndDraw\(\), который выполняет обнаружение лица, и в последней строке вы можете увидеть опубликованную в topic выходного изображения. С помощью

`cv_ptr->image` мы можем получить cv::Mat тип данных, и в следующей строке,

`cv_ptr->toImageMsg()` может преобразовать это в ROSImage. Аргументы функции

`detectAndDraw()` - это изображение OpenCV и каскадные переменные:

`detectAndDraw( cv_ptr->image, cascade );    
image_pub_.publish(cv_ptr->toImageMsg());`

Давайте разберемся c функцией detectAndDraw\(\), которая взята из примера кода OpenCV для обнаружения лица: аргументами функции являются входное изображение и каскадный объект. Следующий фрагмент кода сначала преобразует изображение в градации серого и выровняет гистограмму с помощью API-интерфейсов OpenCV. Это своего рода предварительная обработка перед обнаружением лица по изображению. Для этого используется функция cascade.detectMultiScale\(\) \([http://docs.opencv.org/2.4/modules/objdetect/doc/cascade\_classification.html](http://docs.opencv.org/2.4/modules/objdetect/doc/cascade_classification.html)\).

```text
Mat gray, smallImg;
cvtColor( img, gray, COLOR_BGR2GRAY ); double fx = 1 / scale ;
resize( gray, smallImg, Size(), fx, fx, INTER_LINEAR ); 
equalizeHist( smallImg, smallImg );
t = (double)cvGetTickCount(); cascade.detectMultiScale( smallImg, faces, 1.1, 15, 0 |CASCADE_SCALE_IMAGE, Size(30, 30) );
```

Следующий цикл будет повторяться для каждого лица, обнаруженного с помощью функции detectMultiScale\(\). Для каждого лица он находит центроид и публикует /face\_centroid topic:

```text
for ( size_t i = 0; i < faces.size(); i++ )
{
Rect r = faces[i]; Mat smallImgROI;
vector<Rect> nestedObjects; Point center;
Scalar color = colors[i%8]; int radius;
double aspect_ratio = (double)r.width/r.height; if( 0.75 < aspect_ratio && aspect_ratio < 1.3 )
{
center.x = cvRound((r.x + r.width*0.5)*scale);
center.y = cvRound((r.y + r.height*0.5)*scale); 
radius = cvRound((r.width + r.height)*0.25*scale); 
circle( img, center, radius, color, 3, 8, 0 );
face_centroid.x = center.x; face_centroid.y = center.y;
// Публикация центроида обнаруженного лица 
face_centroid_pub.publish (face_centroid);
}
```

Чтобы сделать окно выходного изображения более интерактивным, есть текст и строки для оповещения о лице пользователя слева или справа или в центре. Этот последний раздел кода в основном для этой цели. Для этого используется API OpenCV. Вот код для отображения текста, такого как Левый, Правый и Центр, на экране:

```text
putText(img, "Left", cvPoint(50,240), FONT_HERSHEY_SIMPLEX, 1,cvScalar(255,0,0), 2, CV_AA);
putText(img, "Center", cvPoint(280,240), FONT_HERSHEY_SIMPLEX, 1, cvScalar(0,0,255), 2, CV_AA);
putText(img, "Right", cvPoint(480,240), FONT_HERSHEY_SIMPLEX, 1, cvScalar(255,0,0), 2, CV_AA);
```

Отлично! Мы закончили с кодом трекера; давайте посмотрим, как его собрать и сделать его исполняемым.

