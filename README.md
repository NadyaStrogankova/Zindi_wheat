# Участие в соревновании по определению степени зрелости пшеницы по фото 
https://zindi.africa/competitions/cgiar-wheat-growth-stage-challenge
итоговое место: 65

**1_step.ipynb** 

Я руками меняла категории, чтобы увеличить кол-во примеров 1 и 6 классов. 
так же убрала из "качественных меток" те, на котрых модель давала очень разные предсказания (std > 1).
Картинки были широкие и низкие. Моделям нужны квадраты. Увеличивать или масштабировать и без того плохие картинки - еще понизить качество. Я решила, что пшеничное поле можно сдублировать. Все равно объект классификации мильно меньше картинки.
Поэтому картинки были склеены в прямоугольник с минимальной стороной в 380 px. Так как некорые картинки были обрезаны по диагонали и размер черного треугольника был достаточно большой, то преимущественно черный верх картинок был обрезан. 

В результате работы этого ноутбука получились:
1. small_test.csv - список картинок для тренировки
2. Train_fixed.csv - пофиксенные метки
3. bigImages - папка с увеличенными картинками.

**do_mean.ipynb**

Из 4 сабмитов с хорошим score  я сделала блендинг.

**remake_labels.ipynb**

Эксперименты по pseudo - labeling  для тренировочных и тестовых данных. 

**rmse.ipynb**

Считала на тренировочных данных RMSE между метками и предсказаниями меток. Хорошо коррелировало с результатами предсказаний тестовых меток на LB

**do_prediction_float.ipynb**

Превращение 15 предсказаний для каждой картинки в среднеквадратичную метку. В итоге - файл для сабмита

Wheat_ResNet34.ipynb

Ноутбук, который работал в google colab. Если там не хватало GPU, то я его подключала к AWS через туннель на ноуте
Лучший результат получился на метках small_test на модели ResNet34. 
lr уменьшался ступеньками. Иногда увеличивался в 2-4 раза. 
Аугментации: кроме очевидного из ноутбука, каждый раз бралась не целая картинка, а рандомный кроп нужного для модели размера. 
Большой цикл для предсказаний эмулирует tta, когда каждый раз предсказывается метка для рандомного кропа. 

Научить EfficientNetB1б B3 и Resnet50 у меня не получилось. 
