# Android Simple Project

[@stankinmeetup](https://vk.com/stankin_meetup)

Доклад создан при поддержеке Профком МГТУ "СТАНКИН".

В данном докладе я расскажу о том как создать простой проект с использованием следующих исструментов:
  - AndroidStudio
  - Gradle
  - AndroidManifest и ресуры
  - Activity и ее lifecycle

# AndroidStudio
Android Studio — это интегрированная среда разработки (IDE) для работы с платформой Android, анонсированная 16 мая 2013 года на конференции Google I/O.

IDE находилась в свободном доступе начиная с версии 0.1, опубликованной в мае 2013, а затем перешла в стадию бета-тестирования, начиная с версии 0.8, которая была выпущена в июне 2014 года. Первая стабильная версия 1.0 была выпущена в декабре 2014 года, тогда же прекратилась поддержка плагина Android Development Tools (ADT) для Eclipse.

Android Studio, основанная на программном обеспечении IntelliJ IDEA от компании JetBrains, официальное средство разработки Android приложений. Данная среда разработки доступна для Windows, OS.

Что следует знать о работе в Android Studio(AS). 
 - Создание простого sample проекта 
 - Работа с git в AS
 - terminal и основные команды
 - sdk manager
 - avd manager

#  Gradle

Gradle — система автоматической сборки, построенная на принципах Apache Ant и Apache Maven, но предоставляющая DSL на языке Groovy вместо традиционной XML-образной формы представления конфигурации проекта.
Рассмотрим основные команды gradle и разберемся для чего они нужны.
>  compileSdkVersion 24
>  buildToolsVersion "24.0.3"

В данных строчках мы указываем версию sdk. Так как более поздние поддерживают более рание версии выберем последнюю версию sdk. 

>     defaultConfig {
>             applicationId "ru.fedosov.test"
>             minSdkVersion 17
>             targetSdkVersion 24
>             versionCode 1
>             versionName "1.0"
>             testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
>        }

В данных стрчоках кода указываем поддерживаемые нами версии sdk, aplicationid(Для google console), versionCode(Версия кода, которая не видна для пользователя программы), versionName(версия кода, которая видна для пользователя).


```sh  
buildTypes {
        release {
             minifyEnabled false
          proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
     }
}
```

Gradle дает возможность зашифровать код чтобы в последствии нельзя было за декомпелироват программу.
```sh 
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:24.2.1'
    testCompile 'junit:junit:4.12'
>}
```
Здесь мы указываем подлкючаемые библиотеки например support:appcompat.

# AndroidManifext.xml и ресурсы

Файл манифеста AndroidManifest.xml предоставляет основную информацию о программе системе. Каждое приложение должно иметь свой файл AndroidManifest.xml. Редактировать файл манифеста можно вручную, изменяя XML-код или через визуальный редактор Manifest Editor (Редактор файла манифеста), который позволяет осуществлять визуальное и текстовое редактирование файла манифеста приложения.

Назначение файла

- объявляет имя Java-пакета приложения, который служит уникальным идентификатором;
- описывает компоненты приложения — деятельности, службы, приемники широковещательных намерений и контент-провайдеры, что - - - позволяет вызывать классы, которые реализуют каждый из компонентов, и объявляет их намерения;
- содержит список необходимых разрешений для обращения к защищенным частям API и взаимодействия с другими приложениями;
- объявляет разрешения, которые сторонние приложения обязаны иметь для взаимодействия с компонентами данного приложения;
- объявляет минимальный уровень API Android, необходимый для работы приложения;

Рассмотрим основные элементы Android Manifest
#### manifest
Элемент <manifest> является корневым элементом манифеста. По умолчанию AndroidStudio создает элемент такого вида:
```sh
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="ru.fedosov.test">
    ........
</manifest>    
```
#### uses-permision   
Элемент uses-permission запрашивает разрешение, которые приложению должны быть предоставлены системой для его нормального функционирования. Разрешения предоставляются во время установки приложения, а не во время его работы.
android:name
uses-permission имеет единственный атрибут с именем разрешения android:name. Это может быть разрешение, определенное в элементе permission данного приложения, разрешение, определенное в другом приложении или одно из стандартных системных разрешений, например: 
```
shandroid:name="android.permission.CAMERA" или android:name=""android.permission.READ_CONTACTS"  
```
#### aplication
Элемент application один из основных элементов манифеста, содержащий описание компонентов приложения, доступных в пакете: стили, значок и др. Содержит дочерние элементы, которые объявляют каждый из компонентов, входящих в состав приложения. В манифесте может быть только один элемент application.

#### activity
Элемент activity объявляет активность. Если приложение содержит несколько активностей, не забывайте объявлять их в манифесте, создавая для каждой из них свой элемент <activity>. Если активность не объявлена в манифесте, она не будет видна системе и не будет запущена при выполнении приложения или будет выводиться сообщение об ошибке.

Для этого класса зарегистрирован фильтр вызовов, определяющий, что это действие запущено в приложении (действие android:name=«android.intent.action.MAIN»). Определение категории (категория android:name=«android.intent.category.LAUNCHER» ) определяет, что это приложение добавлено в директорию приложений на Android-устройстве. Значения @ направляют файлы ресурсов, которые содержат актуальные значения. Это упрощает работу с разными ресурсами, такими как строки, цвета, значки.

#### intent-filter
Каждый тег activity поддерживает вложенные узлы intent-filter. Элемент intent-filter определяет типы намерений, на которые могут ответить деятельность, сервис или приемник намерений. Фильтр намерений объявляет возможности его родительского компонента — что могут сделать деятельность или служба и какие типы рассылок получатель может обработать. Фильтр намерений предоставляет для компонентов-клиентов возможность получения намерений объявляемого типа, отфильтровывая те, которые не значимы для компонента, и содержит дочерние элементы action, category, data.

#### action
Элемент action добавляет действие к фильтру намерений. Элемент intent-filter должен содержать один или более элементов <action>. Если в элементе intent-fiiter не будет этих элементов, то объекты намерений не пройдут через фильтр. Пример объявления действия:

 ```
<action android:name="android.intent.action.MAIN">
<category>
```
Элемент category определяет категорию компонента, которую должно обработать намерение. Это строковые константы, определенные в классе intent, например:

 ```
<category android:name="android.intent.category.LAUNCHER">
 ```   
    
#### Ресурсы
В андроид все текстовые целочисленные булевы константы принято хранить в спеицальны файлах xml таких как.
- colors.xml
- string.xml
- styles.xml

####  colors.xml
Хранит цвета используемые Android Studio.

####  string.xml
Хранит строки используемые Android Studio.

####  colors.xml
Хранит стили используемые Android Studio.Например цвет toolbar, цвет editext, цвета шрифтов.
    
# Activity и ее lifecycle    

Activity — это компонент приложения, который выдает экран, и с которым пользователи могут взаимодействовать для выполнения каких-либо действий, например набрать номер телефона, сделать фото, отправить письмо или просмотреть карту. Каждой операции присваивается окно для прорисовки соответствующего пользовательского интерфейса. Обычно окно отображается во весь экран, однако его размер может быть меньше, и оно может размещаться поверх других окон.
Активити имеет свой жизненный цикл без которого не возможно создавать простые приложения. Рассмотрим его далее на своем приложении
![logo](http://www.javatpoint.com/images/androidimages/Android-Activity-Lifecycle.png)
    
- onCreate()	Вызывается при первом создании операции. Здесь необходимо настроить все обычные статические элементы — создать представления, привязать данные и т. д. Этот метод передает объект Bundle, содержащий предыдущее состояние операции (если такое состояние было зафиксировано ранее; см. раздел Сохранение состояния операции).

- onRestart()	Вызывается после остановки операции непосредственно перед ее повторным запуском.

- onStart()	Вызывается непосредственно перед тем, как операция становится видимой для пользователя.
За ним следует метод onResume(), если операция переходит на передний план, или метод onStop(), если она становится скрытой.


- onResume()	Вызывается непосредственно перед тем, как операция начинает взаимодействие с пользователем. На этом этапе операция находится в самом верху стека операций, и в нее поступают данные, вводимые пользователем.
За ним всегда следует метод onPause().

- onPause()	Вызывается, когда система собирается возобновить другую операцию. Этот метод обычно используется для записи несохраненных изменений в постоянное место хранения данных, остановки анимаций и других элементов, которые могут использовать ресурсы ЦП и т. д. Здесь крайне важна оперативность, поскольку следующая операция не будет возобновлена до тех пор, пока она не будет возвращена на передний план.

- onStop()	Вызывается в случае, когда операция больше не отображается для пользователя. Это может произойти по причине того, что операция уничтожена, или ввиду возобновления поверх нее другой операции (существующей или новой).
За ним следует либо метод onRestart(), если операция возобновляет взаимодействие с пользователем, либо метод onDestroy(), если операция переходит в фоновый режим.

- onDestroy()	Вызывается перед тем, как операция будет уничтожена. Это финальный вызов, который получает операция. Его можно вызвать либо по причине завершения операции (вызов метода finish()), либо ввиду временного уничтожения системой этого экземпляра операции с целью освободить место. 
    
    
    
    
    
