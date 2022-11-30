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
- Выводы.
- ✨Magic ✨

## Цель работы
### Научиться работать с интеграцией экономической системы в проект Unity и обучением ML-Agent.

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

### 1. Подготовка проекта.

> Открытие готового проекта в Unity
![image](https://user-images.githubusercontent.com/71095323/204819762-b682c9c6-c3fa-4220-8b0d-c740b7fc19a3.png)

> Помещение файла **Economic.yaml** в директорию проекта Unity.

![image](https://user-images.githubusercontent.com/71095323/204820093-8322931e-5333-4213-95c4-cf738de10757.png)

> Содержимое файла **Economic.yaml**:
```yaml
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 3.0e-4
      learning_rate_schedule: linear
      beta: 1.0e-2
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    checkpoint_interval: 500000
    max_steps: 750000
    time_horizon: 64
    summary_freq: 5000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```
> Виртуальное окружение было создано еще при выполнении Лабораторной работы №3. Процесс установок библиотек mlagents, torch и tensorflow.
![image](https://user-images.githubusercontent.com/71095323/204821018-b4ec5e3d-c1ff-473c-950b-7700f07d1d7b.png)
![image](https://user-images.githubusercontent.com/71095323/204821128-e3ec270a-7eed-4454-9f48-7bbf3d7a07ef.png)
![image](https://user-images.githubusercontent.com/71095323/204821968-9bdc4e57-3cbd-4dbe-9035-d1d078f7bd0e.png)


> Успешное считывание файла **Economic.yaml** в Anaconda Prompt.
![image](https://user-images.githubusercontent.com/71095323/204821546-5d2e5aab-926f-421b-9e0e-b7798e595b8e.png):

____
Для ускорение процесса обучения я оставил в проекте 24 полей. Далее я изменял некоторые параметры в **Economic.yaml**.

##### a) Вариант графиков без изменений:
![image](https://user-images.githubusercontent.com/71095323/204823954-7c802894-0fcd-47ca-ae0d-1f7e9bdf4f72.png)
![image](https://user-images.githubusercontent.com/71095323/204823995-ee305d70-11f4-4251-8cd1-c53669ce2510.png)
![image](https://user-images.githubusercontent.com/71095323/204824057-5d15e624-c1b3-4ea0-bd9b-c3e5e351510c.png)

##### b) Вариант графиков с ```batch_size: 2048```:
![image](https://user-images.githubusercontent.com/71095323/204823000-03a9efd7-69bc-4333-acb0-6a89e56de6ed.png)
![image](https://user-images.githubusercontent.com/71095323/204823115-9a8f4c60-8dee-45cc-8ccf-aa0d621528ca.png)




## Задание 2
### Опишите результаты, выведенные в TensorBoard.

По результатам, показанных графиками в TensorBoard, можно сказать, что обучение является успешным при условии, что график в Cumulative Reward стремится вверх.
Без изменений в файле **Economic.yaml** графики ведут себя плавнеее, когда параметр batch_size при увеличении его значения влияет на стремительность графиков - они возвышаются и снижаются реще, образуя тем самым более острые углы.

## Выводы
Я научился работать с интеграцией экономической системы в проект Unity и провёл обучение, используя ML-Agent. В ходе лабораторной работы я воспользовался TensorBoard, которая построила графики, основываясь на данных, полученных во время обучения MLAgent, и помогла понять разницу между параметрами **Economic.yaml** по умолчанию и в ситуациях, где их значения изменелись.

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
