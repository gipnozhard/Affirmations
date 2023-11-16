# Affirmations

# Используйте RecyclerView для отображения прокручиваемого списка

1. Прежде чем вы начнете

Если вспомнить приложения, которыми вы обычно пользуетесь на своем телефоне, то почти в каждом отдельном приложении есть хотя бы один список. На экране журнала вызовов, в приложении "Контакты" и в вашем любимом приложении для социальных сетей отображается список данных. Как показано на скриншоте ниже, некоторые из этих приложений отображают простой список слов или фраз, в то время как другие отображают более сложные элементы, такие как карточки с текстом и изображениями. Независимо от содержимого, отображение списка данных является одной из наиболее распространенных задач пользовательского интерфейса в Android.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/547871b8-0f4b-4341-9ff9-931311e06018)

Чтобы помочь вам создавать приложения со списками, Android предоставляет RecyclerView. RecyclerView разработан таким образом, чтобы быть очень эффективным даже при работе с большими списками за счет повторного использования просмотров, которые были прокручены за пределы экрана. Когда элемент списка прокручивается за пределами экрана, RecyclerView повторно использует это представление для следующего элемента списка, который должен быть отображен. Это означает, что элемент заполняется новым содержимым, которое прокручивается на экране. Такое RecyclerView поведение значительно экономит время обработки и помогает спискам прокручиваться более плавно.

В последовательности, показанной ниже, вы можете видеть, что одно представление было заполнено данными, ABC. После того, как это представление исчезнет с экрана, RecyclerView повторно используйте его для получения новых данных XYZ.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/734cffa0-eb99-4a9f-940f-cfe7743eb006)


В этой кодовой лаборатории вы создадите приложение "Аффирмации". "Аффирмации" - это простое приложение, которое отображает десять положительных аффирмаций в виде текста в прокручиваемом списке. Затем, в последующей codelab, вы сделаете еще один шаг вперед, добавите вдохновляющее изображение к каждой аффирмации и усовершенствуете пользовательский интерфейс приложения.

### Предварительные требования

 * Создайте проект на основе шаблона в Android Studio.

 * Добавьте строковые ресурсы в приложение.

 * Определите макет в XML.

 * Разберитесь в классах и наследовании в Kotlin (включая абстрактные классы).

 * Наследуйте от существующего класса и переопределяйте его методы.
Используйте документацию по developer.android.com для классов, предоставляемых платформой Android.

### Что вы узнаете

 * Как использовать RecyclerView для отображения списка данных.

 * Как организовать ваш код в пакеты

 * Как использовать адаптеры с RecyclerView для настройки внешнего вида отдельного элемента списка.

### Что вы будете создавать

 * Приложение, которое отображает список строк подтверждения с помощью RecyclerView.

### Что вам нужно

 * На компьютере установлена Android Studio версии 4.1 или выше.

## 2. Создание проекта

### Создайте пустой проект Activity

Перед созданием нового проекта убедитесь, что вы используете Android Studio 4.1 или выше.

 1. Запустите новый проект Kotlin в Android Studio, используя пустой шаблон Activity.

 2. Введите утверждения в качестве названия приложения, com.example.affirmations в качестве имени пакета и выберите уровень API 19 в качестве минимального SDK.

 3. Нажмите Готово, чтобы создать проект.


## 3. Настройка списка данных

Следующим шагом в создании приложения Affirmations является добавление ресурсов. Вы добавите в свой проект следующее.

 * Строковые ресурсы для отображения в приложении в виде утверждений.

 * Источник данных для предоставления списка подтверждений вашему приложению.

-----------------------------------------------------------
Примечание: В большинстве производственных проектов для Android данные аффирмаций извлекаются из базы данных или с сервера. Сети и базы данных выходят за рамки этой кодовой лаборатории, поэтому вы будете использовать список строк утверждений, определенных внутри приложения.
-----------------------------------------------------------

### Добавьте строки подтверждения

 1. В окне Project откройте app> res> values> strings.xml . В данный момент у этого файла есть единственный ресурс, который является именем приложения.
 
 2. В strings.xml добавьте следующие утверждения в качестве отдельных строковых ресурсов. Назовите их affirmation1, affirmation2 и так далее.

Текст аффирмации

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/a5f8bd54-49cc-4f9a-853f-394e3013f0c0)

strings.xmlФайл должен выглядеть следующим образом, когда вы закончите.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/1ff7c98c-29e8-4223-8024-a5119a21240e)

Теперь, когда вы добавили строковые ресурсы, вы можете ссылаться на них в своем коде как R.string.affirmation1 или R.string.affirmation2.

## Создайте новый пакет

Логическая организация вашего кода помогает вам и другим разработчикам понимать, поддерживать и расширять его. Точно так же, как вы можете упорядочивать документы по файлам и папкам, вы можете упорядочить свой код по файлам и пакетам.

### Что такое пакет?

 1. В Android Studio в окне "Проект" (Android) просмотрите файлы вашего нового проекта в разделе "приложение> java" для приложения "Аффирмации". Они должны выглядеть так, как показано на скриншоте ниже, на котором показаны три пакета: один для вашего кода (com.example.affirmations) и два для тестовых файлов (com.example.affirmations (androidTest) и com.example.affirmations (test)).

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/570cdb49-75f7-4e50-ad28-2b3ecdee98f6)

 2. Обратите внимание, что название пакета состоит из нескольких слов, разделенных точкой.

Вы можете использовать пакеты двумя способами.

 * Создавайте разные пакеты для разных частей вашего кода. Например, разработчики часто разделяют классы, работающие с данными, и классы, создающие пользовательский интерфейс, в разные пакеты.

 * Используйте в своем коде код из других пакетов. Чтобы использовать классы из других пакетов, вам необходимо определить их в зависимостях вашей системы сборки. Также это стандартная практика использования import их в вашем коде, поэтому вы можете использовать их сокращенные имена (например, TextView) вместо их полных имен (например, android.widget.TextView). Например, вы уже использовали import инструкции для таких классов, как sqrt (import kotlin.math.sqrt) и View (import android.view.View).

В приложении Affirmations, помимо импорта классов Android и Kotlin, вы также разделите свое приложение на несколько пакетов. Даже если у вас не так много классов для вашего приложения, рекомендуется использовать пакеты для группировки классов по функциональности.

 ### Именование пакетов
Имя пакета может быть любым, если оно уникально во всем мире; ни один другой опубликованный пакет в любом месте не может иметь такого же имени. Поскольку существует очень большое количество пакетов, а придумать случайные уникальные имена сложно, программисты используют соглашения, чтобы упростить создание и понимание названий пакетов.

 * Название пакета обычно структурировано от общего к определенному, причем каждая часть названия написана строчными буквами и разделена точкой. Важно: точка - это всего лишь часть названия. Это не указывает на иерархию в коде и не определяет структуру папок!

 * Поскольку интернет-домены уникальны во всем мире, принято использовать домен, обычно ваш или домена вашей компании, в качестве первой части имени.

 * Вы можете выбрать названия пакетов, чтобы указать, что находится внутри пакета, и как пакеты связаны друг с другом.

 * Для примеров кода, подобных этому, com.example обычно используется название приложения, за которым следует.

Вот несколько примеров предопределенных названий пакетов и их содержимого:

 * kotlin.math - Математические функции и константы.

 * android.widget - Просмотры, такие какTextView.

---------------------------------------------------------------
Примечание: Хотя названия пакетов (и их расположение в окне Android Project Android Studio в виде иерархии папок) отображаются в виде иерархии, фактической иерархии в исполняемом коде нет. Точно так же, как система нумерации в библиотеке классифицирует и упорядочивает книги, все они по-прежнему находятся на одной полке, и вы можете взять любую из них.
---------------------------------------------------------------

### Создайте пакет

 1. В Android Studio на панели "Проект" щелкните правой кнопкой мыши приложение > java > com.example.affirmations и выберите Создать > Пакет.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/2444e092-40b2-468b-8487-a309ed253e70)

 2. Во всплывающем окне "Новый пакет" обратите внимание на предлагаемый префикс имени пакета. Предлагаемая первая часть имени пакета - это название пакета, который вы щелкнули правой кнопкой мыши. Хотя названия пакетов не создают иерархию пакетов, повторное использование частей названия используется для указания взаимосвязи и организации содержимого!
 
 3. Во всплывающем окне добавьте model в конец предлагаемого названия пакета. Разработчики часто используют model в качестве имени пакета для классов, которые моделируют (или представляют) данные.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/e7046f05-79d2-4adb-af31-d4799abd16b1)

 4. Нажмите Enter. При этом будет создан новый пакет под названием com.example.affirmations (root). Этот новый пакет будет содержать все классы, связанные с данными, определенные в вашем приложении.

### Создайте класс данных подтверждения

В этой задаче вы создадите класс с именем, Affirmation. экземпляр объекта Affirmation которого представляет одно подтверждение и содержит идентификатор ресурса строки с подтверждением.

 5. Щелкните правой кнопкой мыши на пакете com.example.affirmations.model и выберите Создать > Файл / класс Kotlin.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/d51ce888-40e8-4628-ae8f-36bdf7b4a0b8)

 6. Во всплывающем окне выберите класс и введите Affirmation в качестве имени класса. При этом будет создан новый файл с именем Affirmation.kt в model пакете.

 7. Создайте Affirmation класс данных, добавив data ключевое слово перед определением класса. В результате вы получите сообщение об ошибке, поскольку в классах данных должно быть определено хотя бы одно свойство.

Affirmation.kt

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/97f0d9ef-69a1-4f09-9557-cda796274668)

Когда вы создаете экземпляр Affirmation, вам необходимо передать идентификатор ресурса для строки подтверждения. Идентификатор ресурса является целым числом.

 8. Добавьте val целочисленный параметр stringResourceId в конструктор Affirmation класса. Это избавит вас от вашей ошибки.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/59f403be-d728-41a3-b47e-f90e2499c04c)

### Создайте класс в качестве источника данных

Данные, отображаемые в вашем приложении, могут поступать из разных источников (например, из вашего проекта приложения или из внешнего источника, для загрузки которого требуется подключение к Интернету). В результате данные могут быть представлены не в том формате, который вам нужен. Остальная часть приложения не должна заботиться о том, откуда берутся данные или в каком формате они изначально представлены. Вы можете и должны скрыть эту подготовку данных в отдельном Datasource классе, который подготавливает данные для приложения.

Поскольку подготовка данных - это отдельная задача, поместите Datasource класс в отдельный пакет data.

 1. В Android Studio в окне Проекта щелкните правой кнопкой мыши приложение > java > com.example.affirmations и выберите Создать > Пакет.

 2. Введите data в качестве последней части названия пакета.

 3. Щелкните правой кнопкой мыши на data пакете и выберите новый файл / класс Kotlin.

 4. Введите Datasource в качестве имени класса.

 5. Внутри Datasource класса создайте функцию с именем loadAffirmations().

loadAffirmations()Функция должна возвращать список Affirmations. Вы делаете это, создавая список и заполняя его Affirmation экземпляром для каждой строки ресурса.

 6. Объявите List<Affirmation> в качестве возвращаемого типа метода loadAffirmations().

 7. В теле loadAffirmations()добавьте return инструкцию.

 8. После return ключевого слова вызовите listOf<>(), чтобы создать List.

 9. Внутри угловых скобок <> укажите тип элементов списка как Affirmation. При необходимости импортируйте com.example.affirmations.model.Affirmation.

 10. Внутри круглых скобок создайте Affirmation, передав R.string.affirmation1 в качестве идентификатора ресурса, как показано ниже.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/67bd7558-ffb1-4901-ae32-f0d491c1d049)

 11. Добавьте оставшиеся Affirmation объекты в список всех утверждений, разделенных запятыми. Готовый код должен выглядеть следующим образом.

Datasource.kt

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/69a9c5ce-a2f7-467b-89a2-87acb43a22ec)

### [Необязательно] Отображение размера списка подтверждений в текстовом представлении

Чтобы убедиться, что вы можете создать список утверждений, вы можете вызвать loadAffirmations() и отобразить размер возвращаемого списка утверждений в TextView шаблоне приложения Empty Activity, который поставляется вместе с вашим пустым приложением Activity.

 1. В layouts/activity_main.xmlукажитеTextView, что поставляется с вашим шаблоном, id of textview.

 2. В MainActivity в onCreate() методе после существующего кода получите ссылку на textview.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/0d4e9caf-bdaf-4bfa-928e-4484a2fa174c)

 3. Затем добавьте код для создания и отображения размера списка подтверждений. Создайте Datasource, вызовите loadAffirmations(), получите размер возвращаемого списка, преобразуйте его в строку и назначьте в качестве text of textView.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/a6784ff4-bb4d-4435-bf8b-5e5472de5056)

 4. Запустите свое приложение. Экран должен выглядеть так, как показано ниже.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/97ccf8f9-1aa2-46df-b0bc-cb3d954e0f4d)

 5. Удалите код, который вы только что добавили в MainActivity.










## 4. Добавление RecyclerView в ваше приложение

В этой задаче вы настроите RecyclerView отображение списка Affirmations.

В создании и использовании мобильных приложений для Android участвует ряд компонентовRecyclerView. Вы можете рассматривать их как разделение труда. На приведенной ниже диаграмме показан общий обзор, и вы узнаете больше о каждом элементе по мере его реализации.

 * элемент - один элемент данных из списка для отображения. Представляет один Affirmation объект в вашем приложении.

 * Адаптер - принимает данные и подготавливает их к RecyclerView отображению.

 * ViewHolders - Пул просмотров, которые RecyclerView можно использовать повторно для отображения утверждений.

 * RecyclerView - просмотры на экране

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/4caecdfd-43bc-437e-a0af-fc52bcfbe62c)

### Добавьте RecyclerView в макет

Приложение Affirmations состоит из одного действия с именем MainActivity, а его файл макета называется activity_main.xml. Во-первых, вам нужно добавить RecyclerView в макет MainActivity.

 1. Открыть activity_main.xml (приложение> разрешение> макет> activity_main.xml )

 2. Если вы еще не используете их, переключитесь на разделенный вид.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/f31becb4-dbff-4c57-a92e-15754132d564)

 3. УдалитеTextView.

Используется текущий макетConstraintLayout. ConstraintLayout он идеален и гибок, когда вы хотите разместить в макете несколько дочерних представлений. Поскольку ваш макет имеет только одно дочернее представление, RecyclerView вы можете переключиться на более простое, ViewGroup вызываемое FrameLayout, которое следует использовать для хранения одного дочернего представления.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/bab3d0e1-0a1a-4e55-b57c-9d959c60ea24)

 4. В XML замените ConstraintLayout на FrameLayout. Готовый макет должен выглядеть так, как показано ниже.

activity_main.xml

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/8007dde8-1da0-402f-8281-32d259361126)

 5. Переключитесь в режим "Дизайн".

 6. В палитре выберите Контейнеры и найдите RecyclerView.

 7. Перетащите RecyclerView в макет.

 8. Если оно появится, прочитайте всплывающее окно "Добавить зависимость проекта" и нажмите "ОК". (Если всплывающее окно не появляется, никаких действий не требуется.)

 9. Подождите, пока Android Studio завершит работу и RecyclerView появится в вашем макете.

 10. При необходимости измените layout_width и layout_height атрибуты RecyclerView на match_parent, чтобы RecyclerView они могли заполнить весь экран.

 11. Установите идентификатор ресурса RecyclerView равным recycler_view.

RecyclerView поддерживает отображение элементов различными способами, такими как линейный список или сетка. Упорядочиванием элементов занимается LayoutManager. Платформа Android предоставляет менеджеры компоновки для базовых макетов элементов. Приложение Affirmations отображает элементы в виде вертикального списка, так что вы можете использоватьLinearLayoutManager.

 12.Переключитесь обратно в режим просмотра кода. В XML-коде внутри RecyclerView элемента добавьте LinearLayoutManager в качестве атрибута layout manager RecyclerView, как показано ниже.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/c4fa7a86-e2aa-4111-bd34-24f25a8d0c85)

Чтобы иметь возможность прокручивать вертикальный список элементов, длина которого превышает размер экрана, необходимо добавить вертикальную полосу прокрутки.

 13. Внутри RecyclerView добавьте android:scrollbars атрибут, установленный для vertical.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/ec7e22f0-0243-4de5-ad96-39a544d8d925)

Окончательный XML-макет должен выглядеть следующим образом:

activity_main.xml

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/3d6444cd-d245-4ae6-aaf2-1276db3c6441)

 14. Запустите свое приложение.

Проект должен скомпилироваться и запуститься без каких-либо проблем. Однако в вашем приложении отображается только белый фон, потому что вам не хватает важного фрагмента кода. Прямо сейчас у вас есть источник данных и они RecyclerView добавлены в ваш макет, но в RecyclerView нем нет информации о том, как отображать Affirmation объекты.

### Реализуйте адаптер для RecyclerView

Вашему приложению нужен способ получать данные из Datasource и форматировать их так, чтобы каждый из них Affirmation можно было отображать как элемент в RecyclerView.

Адаптер - это шаблон проектирования, который преобразует данные во что-то, что может быть использовано RecyclerView. В этом случае вам нужен адаптер, который берет Affirmation экземпляр из списка, возвращаемого loadAffirmations(), и превращает его в представление элемента списка, чтобы его можно было отображать в RecyclerView.

Когда вы запускаете приложение, оно RecyclerView использует адаптер, чтобы выяснить, как отображать ваши данные на экране. RecyclerView просит адаптер создать новый вид элемента списка для первого элемента данных в вашем списке. Получив представление, он запрашивает адаптер предоставить данные для рисования элемента. Этот процесс повторяется до тех пор, пока RecyclerView для заполнения экрана больше не понадобятся виды. Если на экране одновременно умещаются только 3 вида элементов списка, RecyclerView только просит адаптер подготовить эти 3 вида элементов списка (вместо всех 10 видов элементов списка).

На этом шаге вы создадите адаптер, который адаптирует Affirmation экземпляр объекта таким образом, чтобы его можно было отображать в RecyclerView.

### Создайте адаптер

Адаптер состоит из нескольких частей, и вам придется написать довольно много кода, более сложного, чем то, что вы делали в этом курсе до сих пор. Ничего страшного, если сначала вы не до конца разберетесь в деталях. После того, как вы завершите все это приложение с помощью RecyclerView, вы сможете лучше понять, как все части сочетаются друг с другом. Вы также сможете повторно использовать этот код в качестве основы для будущих приложений, которые вы создадите с помощью RecyclerView.

#### Создайте макет для элементов

Каждый элемент в RecyclerView имеет свой собственный макет, который вы определяете в отдельном файле макета. Поскольку вы собираетесь отображать только строку, вы можете использовать TextView для своего макета элемента.

 1. В res> layout создайте новый пустой файл с именем list_item.xml.

 2. Открыть list_item.xml в представлении кода.

 3. Добавьте TextView с id item_title помощью.

 4. Добавьте wrap_content для layout_width и layout_height, как показано в приведенном ниже коде.

Обратите внимание, что вам не нужна ViewGroup привязка к вашему макету, потому что этот макет элемента списка позже будет расширен и добавлен как дочерний к родительскому RecyclerView.

list_item.xml

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/d011721d-c609-4053-8f07-4c35ab6acc7f)

В качестве альтернативы вы могли бы использовать Файл > Создать > Файл ресурсов макета с именем файла list_item.xml и TextView в качестве корневого элемента. Затем обновите сгенерированный код, чтобы он соответствовал приведенному выше коду.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/82daa84e-9288-4bd3-8ed1-ebd378479b3d)

### Создайте класс ItemAdapter
 
 1. В Android Studio на панели "Проект" щелкните правой кнопкой мыши приложение > java > com.example.affirmations и выберите Создать > Пакет.

 2.Введите adapter в качестве последней части названия пакета.

 3. Щелкните правой кнопкой мыши на adapter пакете и выберите Создать > Файл / класс Kotlin.

 4. Введите ItemAdapter в качестве имени класса, завершите, и ItemAdapter.kt файл откроется.

Вам нужно добавить параметр в конструктор ItemAdapter, чтобы вы могли передавать список утверждений в адаптер.

 5. Добавьте в ItemAdapter конструктор параметр, который является val вызываемым dataset типом List<Affirmation>. При необходимости импортируйте Affirmation.

 6. Поскольку dataset они будут использоваться только в этом классе, сделайте это private.

ItemAdapter.kt

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/b734b5fc-f7dc-491b-81af-994455062418)

ItemAdapterТребуется информация о том, как разрешить строковые ресурсы. Эта и другая информация о приложении хранятся в Context экземпляре объекта, который вы можете передать в ItemAdapter экземпляр.

 7. Добавьте в ItemAdapter конструктор параметр, который является val вызываемым context типом Context. Поместите его в качестве первого параметра в конструкторе.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/b9da367f-4e81-4525-9f33-94b64489ca76)

### Создайте ViewHolder

RecyclerView не взаимодействует напрямую с представлениями элементов, а ViewHolders вместо этого имеет дело с ними. A ViewHolder представляет собой одно представление элемента списка в RecyclerView и может быть использовано повторно, когда это возможно. ViewHolder Экземпляр содержит ссылки на отдельные представления в макете элемента списка (отсюда название "view holder"). Это упрощает обновление представления элемента списка новыми данными. Владельцы просмотров также добавляют информацию, которая RecyclerView используется для эффективного перемещения просмотров по экрану.
 
 1. Внутри ItemAdapter класса перед закрывающей фигурной скобкой для ItemAdapter создайте ItemViewHolder класс.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/89fac1cd-d95b-4faf-899a-28e1ca0fcb73)

 * Определение класса внутри другого класса называется созданием вложенного класса.

 * Поскольку ItemViewHolder используется только ItemAdapter, создание его внутри ItemAdapter показывает эту взаимосвязь. Это не обязательно, но помогает другим разработчикам понять структуру вашей программы.

 2. Добавьте private val view тип View в качестве параметра в ItemViewHolder конструктор класса.

 3. Создайте ItemViewHolder подкласс RecyclerView.ViewHolder и передайте view параметр в конструктор суперкласса.

 4. Внутри ItemViewHolderопределите val свойство textView, имеющее тип TextView. Назначьте ему представление с идентификатором, item_title который вы определили в list_item.xml.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/a7f70cb8-5d72-479b-baca-05102fd29f5d)

Переопределение методов адаптера

 1. Добавьте код для расширения вашего ItemAdapter из абстрактного класса RecyclerView.Adapter. Укажите ItemAdapter.ItemViewHolder в качестве типа держателя представления в угловых скобках.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/66b6c66e-cc00-44c5-be2c-cd3e4e354b84)

Вы увидите сообщение об ошибке, потому что вам нужно реализовать некоторые абстрактные методы из RecyclerView.Adapter.

 2. Наведите курсор на ItemAdapter и нажмите Command +I (Control + I в Windows). Здесь показан список методов, которые необходимо реализовать: getItemCount(), onCreateViewHolder() и onBindViewHolder().

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/c4819cc3-41ac-4b1b-9c9d-84db7185d28b)

 3. Выберите все три функции с помощью Shift + click и нажмите OK.

Это создает заглушки с правильными параметрами для трех методов, как показано ниже.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/2b08c914-e688-4e40-a9c4-119267804d5b)

Вы больше не должны видеть ошибок. Далее вам нужно реализовать эти методы, чтобы они выполняли правильные действия для вашего приложения.

### Реализовать функцию getItemCount()

getItemCount()Метод должен возвращать размер вашего набора данных. Данные вашего приложения находятся в свойстве dataset , которое вы передаете в конструктор ItemAdapter , и вы можете получить его размер с помощью size.

 1. Замените getItemCount() этим:

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/60c9c9c5-6588-40e9-8f77-32c44c26227b)

Это более лаконичный способ написания этого:

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/aea73bc5-0bbf-4e8b-9e35-62eade032daa)

### Реализовать onCreateViewHolder()

onCreateViewHolder()Метод вызывается менеджером компоновки для создания новых держателей представлений для RecyclerView (когда нет существующих держателей представлений, которые можно использовать повторно). Помните, что держатель представления представляет собой представление с одним элементом списка.

onCreateViewHolder() Метод принимает два параметра и возвращает новый ViewHolder.

 * parent Параметр, представляющий собой группу представлений, к которой новое представление элемента списка будет присоединено в качестве дочернего элемента. Родительским являетсяRecyclerView.

 * viewTypeПараметр, который становится важным, когда в одном и том же представлении элементов используется несколько типовRecyclerView. Если у вас разные макеты элементов списка, отображаемые в RecyclerView, существуют разные типы представления элементов. Вы можете перерабатывать представления только с тем же типом представления элемента. В вашем случае существует только один макет элемента списка и один тип представления элемента, поэтому вам не нужно беспокоиться об этом параметре.

 1. В onCreateViewHolder() методе получите экземпляр LayoutInflater из предоставленного контекста (context из parent). Программа layout inflater знает, как преобразовать XML-макет в иерархию объектов просмотра.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/cc87d1e9-9373-487e-8293-9cbbc455efa3)

 2. Как только у вас будет LayoutInflater экземпляр объекта, добавьте точку, за которой следует другой вызов метода, чтобы увеличить фактический вид элемента списка. Передайте идентификатор ресурса XML-макета R.layout.list_item и parent группу просмотра. Третий логический аргумент - attachToRoot. Этот аргумент должен быть false, потому что RecyclerView добавляет этот элемент в иерархию представлений для вас, когда придет время.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/efa53c0b-0178-4431-9b80-50eaecd25296)

Теперь adapterLayout содержит ссылку на представление элемента списка (из которого мы позже сможем найти

дочерние представления, подобные TextView).
 
 3. В onCreateViewHolder()верните новый ItemViewHolder экземпляр, в котором находится корневое представление adapterLayout.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/03932e35-5548-458f-b0a3-953b1f559f8b)

Вот код для onCreateViewHolder() пока что.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/65138a03-232e-483e-9770-9bf55d4c00fb)

### Реализовать функцию onBindViewHolder()

Последний метод, который вам нужно переопределить, это onBindViewHolder(). Этот метод вызывается менеджером компоновки для замены содержимого представления элемента списка.

onBindViewHolder()Метод имеет два параметра: ItemViewHolder ранее созданный onCreateViewHolder() методом, и int который представляет текущий элемент position в списке. В этом методе вы найдете нужный Affirmation объект из набора данных на основе местоположения.

 1. Внутри onBindViewHolder()создайте val item элемент и получите его в заданном position поле dataset.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/56cdf782-6a69-4ecc-9365-a50ea7968046)

Наконец, вам необходимо обновить все представления, на которые ссылается владелец представления, чтобы отразить правильные данные для этого элемента. В этом случае существует только одно представление: TextView внутри ItemViewHolder. Задайте текст для TextView отображения Affirmation строки для этого элемента.

 2. С помощью Affirmation экземпляра объекта вы можете найти соответствующий идентификатор строкового ресурса, вызвав item.stringResourceId . Однако это целое число, и вам нужно найти соответствие фактическому строковому значению.

В Android Framework вы можете вызвать getString() со строковым идентификатором ресурса, и он вернет связанное с ним строковое значение. getString() это метод в Resources классе, и вы можете получить экземпляр Resources класса через context.

Это означает, что вы можете вызвать context.resources.getString() и передать строковый идентификатор ресурса. Результирующую строку можно задать как text из textView в holder ItemViewHolder. Короче говоря, эта строка кода обновляет view holder, чтобы показать строку подтверждения.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/e042d7a2-2a21-4c7e-a234-8133c034d0a3)

Завершенный onBindViewHolder() метод должен выглядеть следующим образом.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/92ea687b-c1b7-4861-ad66-e9e79a8e9d4b)

Вот готовый код адаптера.

ItemAdapter.kt

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/8378d104-3b86-4364-a216-e5fbe6e0e9ff)

Теперь, когда вы внедрили ItemAdapter, вам нужно указать RecyclerView использовать этот адаптер.

### Измените MainActivity, чтобы использовать RecyclerView

Чтобы закончить, вам нужно использовать ваши классы Datasource и ItemAdapter для создания и отображения элементов в RecyclerView. Вы делаете это в MainActivity.

 1. ОткрытьMainActivity.kt.

 2. В MainActivity, перейдите к onCreate() методу. Вставьте новый код, описанный в следующих шагах, после вызова setContentView(R.layout.activity_main).

 3. Создайте экземпляр Datasource и вызовите loadAffirmations() для него метод. Сохраните возвращенный список подтверждений в val именованном myDataset виде.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/647a0454-8db1-4060-911d-532df9fec530)

 4. Создайте переменную с именем recyclerView и используйте findViewById()для поиска ссылки на RecyclerView в макете.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/6dd60a28-148c-4352-bf85-fdd040d11e25)

 5. Чтобы указать, recyclerView использовать ItemAdapter созданный вами класс, создайте новый ItemAdapter экземпляр. ItemAdapter ожидает два параметра: контекст (this) этого действия и утверждения в myDataset.

 6. Присвойте ItemAdapter объект adapter свойству recyclerView.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/36df4ef8-12e8-4228-b46b-ba0949aea835)

 7. Поскольку размер вашего макета RecyclerView фиксирован в макете действий, вы можете установить для setHasFixedSize параметра RecyclerView значение true. Этот параметр необходим только для повышения производительности. Используйте этот параметр, если вы знаете, что изменения в содержимом не меняют размер макета RecyclerView.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/0f3f0d3c-bb33-45d7-9fd8-b3773724d015)

 8. Когда вы закончите, код для MainActivity должен быть похож на следующий.

MainActivity.kt

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/92fed37a-38f4-4c5c-85cf-af1e304ffa5b)

 9. Запустите свое приложение. На экране должен появиться список строк подтверждения.

![image](https://github.com/gipnozhard/Affirmations/assets/71705375/cc3b8a1e-2fc0-4c5e-af56-c5ad01f26ece)

Поздравляем! Вы только что создали приложение, которое отображает список данных с помощью RecyclerView и пользовательского адаптера. Потратьте некоторое время на то, чтобы просмотреть созданный вами код и понять, как разные части работают вместе.

В этом приложении есть все необходимое для отображения ваших аффирмаций, но оно не совсем готово к выпуску. Пользовательский интерфейс не помешало бы немного улучшить. В следующей codelab вы улучшите свой код, узнаете, как добавлять изображения в приложение и усовершенствовать пользовательский интерфейс.









## 5. Краткие сведения

 * RecyclerView виджет помогает отображать список данных.

 * RecyclerView использует шаблон адаптера для адаптации и отображения данных.

 * ViewHolder создает и сохраняет просмотры дляRecyclerView.

 * RecyclerView поставляется со встроеннымиLayoutManagers. RecyclerView делегирует способ размещения элементовLayoutManagers.

Для реализации адаптера:

 * Создайте новый класс для адаптера, например, ItemAdapter.

 * Создайте пользовательский ViewHolder класс, представляющий представление одного элемента списка. Расширяйте из RecyclerView.ViewHolder класса.

 * Измените ItemAdapter класс, чтобы расширить его на основеRecyclerView.Adapter класс с помощью пользовательского ViewHolder класса.

 * Реализуйте эти методы в адаптере: getItemsCount(), onCreateViewHolder() и onBindViewHolder().




