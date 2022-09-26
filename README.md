# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Дубров Сергей Александрович
- РИ-210941
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.
## Задание 1
### Написать программы Hello World на Python и Unity.
1) Показ содержимого кода и его успешный запуск:
![image](https://user-images.githubusercontent.com/71095323/192280031-00a88975-676c-4eae-a9ef-cb627ac4258a.png)	
2) Успешное сохранение ipynb-файла на Google Drive:
![image](https://user-images.githubusercontent.com/71095323/192280548-9316d71d-b01a-49c0-bba0-d57d93a6b235.png)

### Hello World в Unity
1) Успешный запуск кода в Unity, вывод в Console:
![image](https://user-images.githubusercontent.com/71095323/192281487-977440ef-85a4-4f1b-8962-e8c188ca893b.png)

2) Показ содержимого кода:
![image](https://user-images.githubusercontent.com/71095323/192281582-02389f96-84c6-4c93-bd3e-55db7dc44bea.png)

## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
Ход работы:
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

In [ ]:
#Import the required modules, numpy for calculation, and Matplotlib for drawing
import numpy as np
import matplotlib.pyplot as plt
#This code is for jupyter Notebook only
%matplotlib inline

# define data, and change list to array
x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

#Show the effect of a scatter plot
plt.scatter(x,y)

```
1) Показ кода и его запуск в PyCharm:
![image](https://user-images.githubusercontent.com/71095323/192297449-42292302-c0fc-4ac1-9bf4-d0a199951344.png)

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

2) Показ связанных функций в PyCharm:

![image](https://user-images.githubusercontent.com/71095323/192301068-6afdaf1f-03cb-4070-afac-f4955b6843ad.png)

## 3) Начало итераций:

#### Шаг 1: Инициализация и модель итеративной оптимизации.
![image](https://user-images.githubusercontent.com/71095323/192308069-6e8e43c1-7f8d-4757-8a29-8fc0599ee7e7.png)

#### Шаг 2: На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации.
![image](https://user-images.githubusercontent.com/71095323/192308191-fd3fcf96-5baa-48b4-b290-7555e813cff4.png)
#### Шаг 3: Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации.
![image](https://user-images.githubusercontent.com/71095323/192308440-79265dfb-1aa6-4b95-b536-a7a9e8f96ccc.png)
#### Шаг 4: На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации.
![image](https://user-images.githubusercontent.com/71095323/192308554-b9cc5452-5fc6-46dd-864b-486372de4671.png)
#### Шаг 5: Пятая итерация показывает значение параметра, значение потерь и эффект визуализации после итерации.
![image](https://user-images.githubusercontent.com/71095323/192308689-d363925b-4381-46da-a362-62491e068ccd.png)
#### Шаг 6: 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации.
![image](https://user-images.githubusercontent.com/71095323/192308751-e0e3fc87-bac0-40c3-bd8b-9325030c71b0.png)


## Задание 3
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.
В приведенном мной скриншоте можно заметить, что переменные a и b, которые вычисляют значение loss, имеют зависимость от параметра times. Можно сделать вывод о том, что чем больше значение параметра times в функции iterate, тем меньше будет значение loss. Следовательно, величина loss должна стремится к нулю.

![image](https://user-images.githubusercontent.com/71095323/192312208-a71afb80-86f8-41cb-b5fb-f32123287b22.png)

### Примеры
#### 1) При times = 1 значение loss будет составлять приблизительно ~2367:
![image](https://user-images.githubusercontent.com/71095323/192310290-54e3e84b-93cc-40a4-8a30-4b012c79d1e2.png)

#### 2) При times = 234 значение loss приблизительно будет уже равняться ~887:
![image](https://user-images.githubusercontent.com/71095323/192313835-31ab4dda-7505-4f05-a5ea-7b784536f349.png)

#### 3) А при times = 1232 значене loss будет эквивалентно приблизительно ~192:
![image](https://user-images.githubusercontent.com/71095323/192313996-05d4b81e-dfda-4754-b3f4-af71fae6a6c2.png)


## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
Роль параметра Lr заключается в том, что его значение влияет на угол прямой, изображенной на графике.

### Примеры (Во всех примерах times = 1)
#### 1) lr = 0.000001:
![image](https://user-images.githubusercontent.com/71095323/192315094-968b86ad-af9e-48ca-9dbc-5653a8b71a09.png)

#### 2) lr = 0.00001:
![image](https://user-images.githubusercontent.com/71095323/192315383-c78b9d87-e9d1-4158-b790-6d35b7a29d78.png)

#### 3) lr = 0.001:
![image](https://user-images.githubusercontent.com/71095323/192315570-75262c0a-64cb-44f4-87de-d0bfca86b477.png)


## Выводы

Вывод: Я ознакомился с основными операторами языка Python на примере реализации линейной регрессии. В ходе лабораторной работы я выяснил зависимость в работе кода от таких параметров, как Lr и times. Также я разобрался в работе с кодом в Google Colab и Unity в связке с Visual Studio Code.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
