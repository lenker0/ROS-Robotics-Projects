# Настройка ROS на VirtualBox

  
&lt;!--  
 /\* Font Definitions \*/  
 @font-face  
	{font-family:Wingdings;  
	panose-1:5 0 0 0 0 0 0 0 0 0;  
	mso-font-charset:2;  
	mso-generic-font-family:auto;  
	mso-font-pitch:variable;  
	mso-font-signature:0 268435456 0 0 -2147483648 0;}  
@font-face  
	{font-family:"Cambria Math";  
	panose-1:2 4 5 3 5 4 6 3 2 4;  
	mso-font-charset:0;  
	mso-generic-font-family:roman;  
	mso-font-pitch:variable;  
	mso-font-signature:3 0 0 0 1 0;}  
@font-face  
	{font-family:"Palatino Linotype";  
	panose-1:2 4 5 2 5 5 5 3 3 4;  
	mso-font-charset:204;  
	mso-generic-font-family:roman;  
	mso-font-pitch:variable;  
	mso-font-signature:-536870265 1073741843 0 0 415 0;}  
@font-face  
	{font-family:"Lucida Console";  
	panose-1:2 11 6 9 4 5 4 2 2 4;  
	mso-font-alt:"Lucida Console";  
	mso-font-charset:204;  
	mso-generic-font-family:modern;  
	mso-font-pitch:fixed;  
	mso-font-signature:-2147482993 6144 0 0 31 0;}  
 /\* Style Definitions \*/  
 p.MsoNormal, li.MsoNormal, div.MsoNormal  
	{mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-parent:"";  
	margin:0cm;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	text-autospace:none;  
	font-size:11.0pt;  
	font-family:"Palatino Linotype",serif;  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-ansi-language:EN-US;  
	mso-fareast-language:EN-US;  
	mso-bidi-language:EN-US;}  
h6  
	{mso-style-priority:9;  
	mso-style-qformat:yes;  
	mso-style-link:"Заголовок 6 Знак";  
	margin-top:1.65pt;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:5.65pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:6;  
	text-autospace:none;  
	font-size:10.5pt;  
	font-family:"Palatino Linotype",serif;  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-ansi-language:EN-US;  
	mso-fareast-language:EN-US;  
	mso-bidi-language:EN-US;}  
p.MsoBodyText, li.MsoBodyText, div.MsoBodyText  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"Основной текст Знак";  
	margin:0cm;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	text-autospace:none;  
	font-size:10.5pt;  
	font-family:"Palatino Linotype",serif;  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-ansi-language:EN-US;  
	mso-fareast-language:EN-US;  
	mso-bidi-language:EN-US;}  
p.MsoListParagraph, li.MsoListParagraph, div.MsoListParagraph  
	{mso-style-priority:34;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	margin-top:2.9pt;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:53.65pt;  
	margin-bottom:.0001pt;  
	text-indent:-13.4pt;  
	mso-pagination:none;  
	text-autospace:none;  
	font-size:11.0pt;  
	font-family:"Palatino Linotype",serif;  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-ansi-language:EN-US;  
	mso-fareast-language:EN-US;  
	mso-bidi-language:EN-US;}  
span.6  
	{mso-style-name:"Заголовок 6 Знак";  
	mso-style-priority:9;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"Заголовок 6";  
	mso-ansi-font-size:10.5pt;  
	mso-bidi-font-size:10.5pt;  
	font-family:"Palatino Linotype",serif;  
	mso-ascii-font-family:"Palatino Linotype";  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-hansi-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-bidi-language:EN-US;  
	font-weight:bold;}  
span.a  
	{mso-style-name:"Основной текст Знак";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"Основной текст";  
	mso-ansi-font-size:10.5pt;  
	mso-bidi-font-size:10.5pt;  
	font-family:"Palatino Linotype",serif;  
	mso-ascii-font-family:"Palatino Linotype";  
	mso-fareast-font-family:"Palatino Linotype";  
	mso-hansi-font-family:"Palatino Linotype";  
	mso-bidi-font-family:"Palatino Linotype";  
	mso-bidi-language:EN-US;}  
.MsoChpDefault  
	{mso-style-type:export-only;  
	mso-default-props:yes;  
	font-family:"Calibri",sans-serif;  
	mso-ascii-font-family:Calibri;  
	mso-ascii-theme-font:minor-latin;  
	mso-fareast-font-family:Calibri;  
	mso-fareast-theme-font:minor-latin;  
	mso-hansi-font-family:Calibri;  
	mso-hansi-theme-font:minor-latin;  
	mso-bidi-font-family:"Times New Roman";  
	mso-bidi-theme-font:minor-bidi;  
	mso-ansi-language:EN-US;  
	mso-fareast-language:EN-US;}  
.MsoPapDefault  
	{mso-style-type:export-only;  
	mso-pagination:none;  
	text-autospace:none;}  
@page WordSection1  
	{size:541.5pt 666.5pt;  
	margin:57.0pt 51.0pt 57.0pt 51.0pt;  
	mso-header-margin:46.25pt;  
	mso-footer-margin:47.05pt;  
	mso-paper-source:0;}  
div.WordSection1  
	{page:WordSection1;}  
@page WordSection2  
	{size:541.5pt 666.5pt;  
	margin:57.0pt 51.0pt 57.0pt 51.0pt;  
	mso-header-margin:46.25pt;  
	mso-footer-margin:47.05pt;  
	mso-paper-source:0;}  
div.WordSection2  
	{page:WordSection2;}  
@page WordSection3  
	{size:612.0pt 792.0pt;  
	margin:2.0cm 42.5pt 2.0cm 3.0cm;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:36.0pt;  
	mso-paper-source:0;}  
div.WordSection3  
	{page:WordSection3;}  
 /\* List Definitions \*/  
 @list l0  
	{mso-list-id:831993984;  
	mso-list-type:hybrid;  
	mso-list-template-ids:-1029691228 68747265 68747267 68747269 68747265 68747267 68747269 68747265 68747267 68747269;}  
@list l0:level1  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Symbol;}  
@list l0:level2  
	{mso-level-number-format:bullet;  
	mso-level-text:o;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:"Courier New";}  
@list l0:level3  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Wingdings;}  
@list l0:level4  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Symbol;}  
@list l0:level5  
	{mso-level-number-format:bullet;  
	mso-level-text:o;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:"Courier New";}  
@list l0:level6  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Wingdings;}  
@list l0:level7  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Symbol;}  
@list l0:level8  
	{mso-level-number-format:bullet;  
	mso-level-text:o;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:"Courier New";}  
@list l0:level9  
	{mso-level-number-format:bullet;  
	mso-level-text:;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	text-indent:-18.0pt;  
	font-family:Wingdings;}  
ol  
	{margin-bottom:0cm;}  
ul  
	{margin-bottom:0cm;}  
--&gt;  


Как вы знаете, полная поддержка ROS присутствует только в Ubuntu. Так что насчет пользователей Windows и Mac OS X? Они не могут использовать ROS? Да, они могут, используя инструмент под названием VirtualBox \([https://www.virtualbox.org/](https://www.virtualbox.org/)\). VirtualBox позволяет нам устанавливать гостевую ОС, не затрагивая основную ОС. Виртуальная ОС может работать вместе с хост-ОС в заданной спецификации виртуального компьютера, такой как количество процессоров и ОЗУ, а также размер жесткого диска.  


Вы можете скачать VirtualBox для популярных ОС по следующей ссылке:

https://www.virtualbox.org/wiki/Downloads

Полная процедура установки Ubuntu на VirtualBox показана в следующем учебном видео на YouTube: https://www.youtube.com/watch?v=DPIPC25xzUM.

Ниже приведен скриншот графического интерфейса VirtualBox. Вы можете увидеть список виртуальных ОС слева и конфигурацию виртуального ПК справа. Кнопки для создания новой виртуальной ОС и запуска существующего VirtualBox можно увидеть на верхней панели. Оптимальная конфигурация виртуального ПК показана на следующем снимке экрана:

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 18: &#x41A;&#x43E;&#x43D;&#x444;&#x438;&#x433;&#x443;&#x440;&#x430;&#x446;&#x438;&#x44F; VirtualBox](../.gitbook/assets/image%20%2850%29.png)

Вот основные характеристики виртуального ПК:

**·         Количество процессоров: 1**

·         **Оперативная память**: 4ГБ

·         **Видеопамять**: 128 МБ

·         **Акселерация**: 3D

·         **Место хранения**: 20 ГБ до 30 ГБ

·         Сетевой адаптер в режиме NAT

Для обеспечения аппаратного ускорения необходимо установить драйверы с диска с надстройками VirtualBox Guest. После загрузки на рабочий стол Ubuntu перейдите к Устройствам \| Вставьте образ гостевого дополнения CD. Это смонтирует образ компакт-диска в Ubuntu и попросит пользователя запустить скрипт для установки драйверов. Если мы позволим, он автоматически установит все драйверы. После перезагрузки вы получите полное ускорение гостя Ubuntu.

Нет никакой разницы в установке ROS на VirtualBox. Если виртуальный сетевой адаптер находится в режиме NAT, подключение к Интернету хост-ОС будет использоваться совместно с гостевой ОС. Так что гость может работать так же, как настоящая ОС.

