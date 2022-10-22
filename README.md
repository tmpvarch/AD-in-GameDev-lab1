# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.
## Задание 1
### ! В методических указаниях по какой-то причине указана формилровка первой задачи из лабороторной работы №2 !

### 1. Создание проекта в Unity и успешное добавление .json-файлов в данный проект
> Убеждаемся в том, что во вкладке Components появилась строка ML Agent.
![image](https://user-images.githubusercontent.com/71095323/197333387-251cc02f-c3cb-4127-999c-ee394571c05c.png)
____
### 2. ML-Агент и установка необходимых библиотек через Anaconda Prompt
* Создание ML-агента. Для этого требуется ввести в комадную строку ```conda create -n MlAgent python-3.6.13```
![image](https://user-images.githubusercontent.com/71095323/197333574-903fe170-9a8a-4b73-a5bd-590574b969a4.png)
____
* Активация МГ-агента и последующая установка библиотек **mlagents 0.28.0** и **torch 1.7.1**

Активация работы ML-агента происходит через команду ```conda activate MLAgent```, после чего для загрузок данных библиотек надо ввести ```pip install mlagents==0.28.0 ```...

> ***Процесс успешной загрузки mlagents 0.28.0:***     

![image](https://user-images.githubusercontent.com/71095323/197333656-f231d0d1-ad6d-4cbc-9bfc-93d6bfc15527.png)

...и ```pip install torch~=1.7.1 -f https://download.pytorch.org/whl/torch_stable.html```.

> ***Успешная загрузка torch 1.7.1:***

![image](https://user-images.githubusercontent.com/71095323/197333849-6b913d70-c65c-4808-9ae7-89d9fb1e5591.png)

____
### 3. Подготовка сцены в Unity
* Создание плоскоти, куба, сферы

![image](https://user-images.githubusercontent.com/71095323/197334128-bc03b0e1-be79-43d3-9efc-069c524c869c.png)
____
* Добавление C#-скрипта к сфере
 
![image](https://user-images.githubusercontent.com/71095323/197334173-e85550ec-cfc5-4868-83dd-870515e3b7bd.png)

> ***Содержимое файла RollerAgent.cs:***
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;

    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }
        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }

    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }

    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);
        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);
        if (distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
            EndEpisode();
    }
}
```
____
* Добавление и настройка компонентов для сферы

![image](https://user-images.githubusercontent.com/71095323/197334472-a30e44b4-17d9-4b15-948d-9284284ad968.png)
____
* Добавление файла конфигурации нейронной сети в директорию проекта

![image](https://user-images.githubusercontent.com/71095323/197334606-f7071c75-cc59-4f16-902a-2e38e7983050.png)

> ***Содержимое файла rollerball_config.yaml:***
```yaml
behaviors:
  RollerBall:
    trainer_type: ppo
    hyperparameters:
      batch_size: 10
      buffer_size: 100
      learning_rate: 3.0e-4
      beta: 5.0e-4
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: linear
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    max_steps: 500000
    time_horizon: 64
    summary_freq: 10000
```
____
### 4. Запуск сцены в Unity

* Запуск файла rollerball_config.yaml

![image](https://user-images.githubusercontent.com/71095323/197334764-ededfa65-89eb-4e41-be02-0c9be2d1752d.png)
____
* Проверка работы ML-агента

![image](https://user-images.githubusercontent.com/71095323/197334821-12030fdb-3cd9-4943-84b0-23bda2a2e938.png)
____

* Запуск сцены с **9** копиями модели "Плоскость-Сфера-Куб" и результаты данного запуска

![image](https://user-images.githubusercontent.com/71095323/197334940-c712db99-1826-4e46-bf99-88f08b30acfe.png)
____
* Запуск сцены с **36** копиями модели "Плоскость-Сфера-Куб" и резульататы данного запуска

![image](https://user-images.githubusercontent.com/71095323/197335017-9eb3eb54-8fc6-444c-a02c-17804f9c2bd2.png)
____

* Присваивание сферы модели работы и результат данной модели

![image](https://user-images.githubusercontent.com/71095323/197335071-b375e545-3f76-41fe-8e63-e57a15116632.png)

> В качестве вывода можно сказать, что в представленном видео видно, что нейросеть хорошо справилась с обучением в управлении сферой и справляется с поставленной задачей - находить смещающийся по случайным координатам куб в плоскости.

https://user-images.githubusercontent.com/71095323/197336355-7e3ecccc-9a2f-4f5a-be80-ef4447bf66cc.mp4


## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.

```yaml
behaviors:
  RollerBall:
    trainer_type: ppo    /* Данная строка задаёт параметр обучения. Здесь задано обучение с поощерением */
    
    hyperparameters:
      batch_size: 10    /* Данная строка означает число опытов в каждой итерации градиентного спуска. */
      buffer_size: 100    /* Данный код принимает число необходимого опыта для обновления модели поведения. */
      learning_rate: 3.0e-4    /* Здесь задаётся начальная скорость обучения */
      beta: 5.0e-4    /* Параметр задаёт силу регуляриззации энтропии. */
      epsilon: 0.2    /* Этот параметр влияет на быстроту изменения поведения во время обучения. */
      lambd: 0.99    /* Здесь задаётся параметр регуляризации. */
      num_epoch: 3    /* В данной строке задаётся число проходов через буфер опыта
                         во время исполнения оптимизации градиентого спуска. */
      learning_rate_schedule: linear    /* В данной строке задаётся параметр изменения скорости с течением времени.*/
    
    network_settings:
      normalize: false    /* Параметр, определяющий автоматическое нормализование обучения. */
      hidden_units: 128    /* Здесь задаётся число единиц в скрытных слоях нейроной сети. */
      num_layers: 2    /* Здесь задаётся число скрытных слоев в нейроной сети */
    
    reward_signals:
      extrinsic:
        gamma: 0.99    /* Здесь задаётся коэффициент поощерения от окружающей среды, который должен быть меньше единицы. */
        strength: 1.0    /* Сила - это заданное число, на которое умножается поощерение от окружающей среды. */
    
    max_steps: 500000    /* Задаёт максимальное количество повторов симуляции сцены. */
    time_horizon: 64    /* Здесь задаются временные рамки. */
    summary_freq: 10000    /*Данная строка подразумевает суммированную частоту. */
```


## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости.



## Выводы
<!-- В выводах к работе дайте развернутый ответ, что такое игровой баланс и как
системы машинного обучения могут быть использованы для того, чтобы его
скорректировать. -->

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
