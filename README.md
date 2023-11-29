# Обнаружение дорожных знаков
### Цель проекта
Создать прототип помощника для водителей, который будет оповещать их о дорожных знаках.
### Бизнес-кейсы
 1. Устройства помощи водителю
    * Где использовать: в автомобильных навигаторах, видеорегистраторах для соблюдения правил ПДД.
    * Кто заказчик: производители автомобилей, производители устройств помощи водителю и автомобильной электроники
 2. Городская инфраструктура
    * Где использовать: в городах для улучшения управления транспортным потоком, оптимизации светофоров и пешеходных зон.
    * Кто заказчик: муниципальные органы городского планирования и транспорта.
3. Транспортные компании и логистика
    * Где использовать: в грузовых транспортных средствах для мониторинга безопасности и соблюдения ПДД.
    * Кто заказчик: логистические компании
4. Автомобильная промышленность
    * Где использовать: в автомобилях, в т. ч. с технологиями автоматического/полуавтоматического вождения, для повышения безопасности и соблюдения ПДД.
    * Кто заказчик: производители автомобилей
5. Государственные службы
    * Где использовать: в автомобилях дорожно-патрульных служб и полиции для автоматического мониторинга и контроля соблюдения ПДД.
    * Кто заказчик: дорожные-патрульные службы, полиция.

### Требования к функционалу
Система детекции и классификации дорожных знаков должна удовлетворять нескольким требованиям:
- быть способным распознавать и классифицировать разнообразные дорожные знаки, включая предупреждающие, запрещающие, информационные и другие.
- эффективно обнаруживать и классифицировать дорожные знаки, которые встречаются редко в обучающих выборках.
работать эффективно при различных уровнях освещения, включая низкое освещение в темное время суток, а также в условиях неблагоприятных погодных явлений, таких как дождь или снег.
- обеспечивать высокую полноту (близкую к 100%) и точность (выше 90%) при обнаружении и классификации дорожных знаков.
### Ограничения
- Сложность в распознавании новых или измененных дорожных знаков: требует расширения обучающих данных и дообучения модели.
- Сложные условия: поврежденные, нестандартные (разных размеров) или загрязненные дорожные знаки и т. п.
- Зависимость от качества видеопотока: низкое качество видеопотока может снижать производительность системы.
- Ограниченная видимость: облачность, туман, недостаточная видимость и т. п. могут создавать сложности для корректной детекции дорожных знаков.
- Непредсказуемые дорожные сценарии: высокая плотность движения, пересекающиеся траектории и др. сложные сценарии могут усложнить задачу корректного распознавания знаков.
- Требования к вычислительным ресурсам: инференс на мобильных устройствах, бортовых и съемных навигаторах может сталкиваться с рядом сложностей из-за ограниченных вычислительных ресурсов и особенностей аппаратного обеспечения
### Датасет
Для текущго проекта используется [Russian traffic sign images dataset](https://www.kaggle.com/datasets/watchman/rtsd-dataset). <br />
Кадры получены с широкоэкранного цифрового видеорегистратора, записывающего 5 кадров в секунду. Разрешение кадров от 1280х720 до 1920х1080. Кадры сняты в разное время года (весна, осень, зима), время суток (утро, день, вечер) и в разных погодных условиях (дождь, снег, яркое солнце).
### Описание файлов репозитория
- 1_eda_and_prepare - изучание данных, преобразование их к формату yolov8, разделение их на тренировочный, валидационный и тестовый наборы
- 2_fit_model - обучение моделей
- 3_comparison_of_results - получения метрик для сравнения моделей
- 4_hyperparameter_tuning - оптимизация гиперпараметров
- 5_predict - создание примеров предсказаний моделей для оценки результата
### Выбор метрик
Детекция дорожных знаков на видео — это задача, где важны как точность, так и полнота обнаружения объектов. Поэтому в контексте данной задачи имеет смысл использовать метрики precision (точность) и recall (полнота), которые оценивают соответственно долю правильно обнаруженных объектов относительно всех обнаруженных и долю обнаруженных объектов относительно всех действительных. <br />
 Использование mAP50 (средняя точность при пороге перекрытия 50%) позволяет оценить качество детекции с учетом варьирования порога перекрытия между предсказанными и реальными объектами. Это особенно полезно для учета различных условий съемки и ракурсов на видео. <br />
 mAP50-95 (средняя точность при варьировании порога перекрытия от 50% до 95%) учитывает более широкий диапазон порогов и может быть полезной метрикой, если важно оценить производительность модели при различных требованиях к точности детекции. <br />
### Сравнение моделей
#### Метрики обучения
- По эпохам обучения
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/518f1ebc-a72f-4aee-9537-6277703aa97e)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/d1be60d0-e077-4579-a1ad-61a693bcfa3f)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/004e516e-8df4-491c-b2ea-536d374a2b8f)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/f98d5e65-b2cb-423c-845b-f88e74f952c1)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/3054a239-c755-4677-aad5-db99ef647459)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/29eb1f3e-ba17-4f96-b8c4-12c5e3a1ca8a)
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/65b453c3-08a7-44b7-9656-828402142759)
Видно, что 25 эпох недостаточно: лосссы падают, метрики растут. Можно обучать модели дальше. <br />
Также прослеживается зависимость значений от класса модели: модели с меньшим количеством параметров имеют более высокие лоссы и низкие значения метрик.
- Итоговые

![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/d677dfad-b6e1-4cfa-b422-6dfe369c8d93)

 *Данные взяты из отчета при валидации в процессе обучения <br />
 **Среднее значение на 1000 итерациях одного и того же изображения из тестовой выборки <br />
  
![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/9717c9f9-fa3b-42d7-a3dc-0052c5ab3871)

Сюда также добавлена модель "yolov8n_best", которая была получена путем оптимизацией гиперпараметров на 5 итерациях. Была взята подобная модель и такое маленькое число итераций в связи с бОльшими временными затратами при других вариантах. <br />

### Вывод
#### Выбор модели
Модель __YOLOv8m__ проявляет высокую точность __(0.876)__ и полноту __(0.768)__, что делает ее привлекательным выбором для бизнес-кейсов, где важны оба эти аспекта. Однако, стоит учитывать, что __YOLOv8s__ обеспечивает хороший баланс между точностью и скоростью предсказания, что может быть важным в реальных временных системах. Скорость предсказания на изображениях у всех моделей примерно одинакова, но __YOLOv8s__ выделяется более быстрой обработкой видео __(4.2 сек)__, в то время как __YOLOv8m__ немного медленнее __(5.084 сек)__. Таким образом, оптимальным выбором среди представленных моделей является __YOLOv8s__.
#### Итоговая оценка качества решения
В целом, модель YOLOv8s показывает неплохие результаты по распознаванию дорожных знаков при приемлемых значениях производительности. Однако обучающая выборка состоит только из российских дорожных знаков, большая часть из них в хороших погодных условиях и в хорошем качестве. Дальнейшими шагами может быть: 
1) увеличение количества эпох обучения на текущем наборе данных
2) расширения набора данных знаками из других стран
3) обучение на аугментированных данных (блюр, ухудшение качества изображения, скрытие части изображения и т.п.)<br />
#### Масштабируемость
Модель обладает высокой гибкостью - поддерживает множество форматов экспорта, может работать на CPU и GPU. <br />

![image](https://github.com/trafficsurfer/YOLOv8/assets/92330362/dcd02724-0050-40e7-84e1-5a6718e777b9) <br />
Благодаря этому решение может быть масштабируемо на мобильные устройства и видеорегистраторы.
### Пример предсказания на видео (conf=0.5)
Видео взято с [Dashcam Drive Relaxing Drive Videos](https://www.youtube.com/@dashcamdriverelaxingdrivev7021/videos) .

https://github.com/trafficsurfer/YOLOv8/assets/92330362/43d498ab-ba03-4e04-8e5b-b6e893d649eb




