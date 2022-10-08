# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity.
## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса.

#### 1) В облачном сервисе google console подключить API для работы с google sheets и google drive.

-Зарегистрированный проект в Google Console:
![image](https://user-images.githubusercontent.com/71095323/194705579-bd501279-cb4d-410b-a9cb-2e6da64e72fb.png)

-Успешное подключение Google Drive API и Google Sheets API: 
![image](https://user-images.githubusercontent.com/71095323/194705725-a5c4bbf4-e69b-4e27-9334-d0a1db09c5f3.png)

![image](https://user-images.githubusercontent.com/71095323/194705795-248fc03c-fbd6-40da-829b-d33358a7c775.png)


#### 2) Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

-Создание проекта в PyCharm и скопированный код:
![image](https://user-images.githubusercontent.com/71095323/194705938-beecebb9-3cf8-49ea-945c-82f89cba17e1.png)

-Запуск и вывод в Google-таблицу:
![image](https://user-images.githubusercontent.com/71095323/194705966-e6fce575-7fba-44cf-bbc0-d91411c96f20.png)

![image](https://user-images.githubusercontent.com/71095323/194705981-bbc95712-02b7-4706-ac1b-6d9c266b8e92.png)

#### 3) Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.

-Окно созданного проекта, куда импортированы файлы jsonPackage и soundPackage:
![image](https://user-images.githubusercontent.com/71095323/194706521-02cff27e-18cc-4b68-8d1b-d6325bbfb41f.png)

#### 4) Написать функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы.

-Написанный код в скрипте для игрового объекта Unity:
![image](https://user-images.githubusercontent.com/71095323/194706727-b6a41495-3717-4fc6-9283-9f702c09ad3e.png)
![image](https://user-images.githubusercontent.com/71095323/194706744-73adddae-cb5f-4078-8a3a-2021e6de46b3.png)

-Настроенные компоненты игрового объекта:

![image](https://user-images.githubusercontent.com/71095323/194706786-621c3bd2-7e93-487c-814a-4e99dc487ef2.png)

-Вывод в консоль Unity:

![image](https://user-images.githubusercontent.com/71095323/194706814-e694661b-48b7-47a0-b42a-b466f2fa1413.png)

![image](https://user-images.githubusercontent.com/71095323/194706822-99c0df43-6bcf-462f-92cf-bea41fe67027.png)

## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1.

-Показ изменённого кода в PyCharm:

![image](https://user-images.githubusercontent.com/71095323/194707432-2f5bd8f7-60cd-4f5a-b655-37d35dfb3fd3.png)
![image](https://user-images.githubusercontent.com/71095323/194707440-51bdfe8f-d87a-4f2a-990d-4956147f5c38.png)

-Вывод в коносоль и запись в таблицу:
![image](https://user-images.githubusercontent.com/71095323/194707506-b16c857f-1f84-4da7-a273-d40ef5532007.png)
![image](https://user-images.githubusercontent.com/71095323/194707525-95dcc4b5-c34c-4631-b854-089ebe75563b.png)

## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

Измененный код:
![image](https://user-images.githubusercontent.com/71095323/194708054-465da609-2c36-4457-a63e-bba6ed20d279.png)

Вывод в консоль:

![image](https://user-images.githubusercontent.com/71095323/194708175-07d8b2a0-5056-436a-ba8f-3f3a7c6ac092.png)


## Выводы

Вывод: Я разобрался с работой программных средств для организции передачи данных между инструментами Google, Python и Unity. В ходе лабораторной работы №2 я реализовал совместную работу и передачу данных в связке Python - Google-Sheets – Unity, а также осуществил запись в Google-таблицу набора данных с помощью линейной регрессии и возвёл для них собственный сценарий воиспроизведения звукового сопровождения в Unity.

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
