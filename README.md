# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Дубров Сергей Александрович
- РИ-210941
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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
### Изучить работу прецептрона на примере проекта Unity и его решения логических операций.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления: OR, AND, NAND, XOR.

### 1. Создание и подготовка проекта. Обучение логической операции OR.

> В Assets закидываем файл **Perceptron.cs**, на сцене создаём пустой GameObject.
![image](https://user-images.githubusercontent.com/71095323/204189422-21c526e5-6ec3-438e-82df-7117d6493890.png)

> Содержимое файла **Perceprton.cs**
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour
{
	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
		if (v1.Length != v2.Length)
			return -1;
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
			d += v1[x] * v2[x];
		d += bias;
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
			weights[i] = Random.Range(-1.0f,1.0f);
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)	
			weights[i] = weights[i] + error*ts[j].input[i]; 
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start ()
	{
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update ()
	{

	}
}
```

> Пустому GameObject добавляем компонент Script. В качестве скрипта будет учавствовать файл **Perceptron.cs**. Указываем параметру Elements по 4, где указываем Input по 2. В поля Input и Output приписываем логику OR.
![image](https://user-images.githubusercontent.com/71095323/204189728-2af10ad8-5e0c-4de5-9385-cef8b43c136a.png)

> В **Perceptron.cs** задаем ```Train(1)``` и запускаем сцену.
![image](https://user-images.githubusercontent.com/71095323/204190655-daedb711-9541-40e1-a152-8f9bfddfc946.png)

Сообщение в коносли ```TOTAL ERROR: 0``` означает, что игровой объект допустил 0 ошибок при обучение, а это может говорить о том, что он с успехом обучился логике OR.
____
> Второй запуск сцены, но в файле **Perceptron.cs** задаём уже ```Train(4)```.
![image](https://user-images.githubusercontent.com/71095323/204192111-504d9562-efda-465a-9390-d7be4f07fdfd.png)

За четрые итерации игровой объект обучился данной логике, что можно понять по сообщению в консоли ```TOTAL ERROR: 0```.
____
### 2. Обучение логической операции AND.

> Задаем игровому объекту значения Input и Output по принципу логики AND и запускаем сцену с ```Train(4)```.
![image](https://user-images.githubusercontent.com/71095323/204193138-3dc56ff4-a530-4b54-aee2-527901fcf21b.png)
![image](https://user-images.githubusercontent.com/71095323/204193675-70800c57-ee18-4849-af3a-176e340fd75e.png)

По истечению четырх итераций игровой объект смог успешно обучиться логике AND, что можно понять по сообщение в коносли ```TOTAL ERROR: 0```.
____
### 3. Обучение логической операции NAND.

> Задаем игровому объекту значения Input и Output по принципу логики NAND и запускаем сцену с ```Train(4)```.
![image](https://user-images.githubusercontent.com/71095323/204201347-2c7f2c1c-eb3a-4ff2-90a3-c1faf5f801cc.png)
![image](https://user-images.githubusercontent.com/71095323/204201397-9072a26d-aa00-483b-9d0f-2805f0626180.png)

Из приложенного сверху скриншота видно, что игровой объект с легкостью и успехом обучился логике NAND за четыре итерации, подтвеждая сообщением в консоли ```TOTAL ERROR: 0```.

____
### 4. Обучение логической операции XOR.

> Задаем игровому объекту значения Input и Output по принципу логики XOR и запускаем сцену с ```Train(4)```.
![image](https://user-images.githubusercontent.com/71095323/204196015-d280d1c6-0eca-4859-b700-60ca089f94e1.png)
![image](https://user-images.githubusercontent.com/71095323/204196068-27e8bd47-2083-443b-b4cf-d41f2fd6c841.png)

Спустя несколько запусков игровой объект не может успешно обучиться данной логике. Результаты тестов оказываются некорректными, а количество ошибок порой равняеться 4. Из этого следует, что программы однослойного перцептрона не достаточно для работы с логикой XOR.

Как один из вариантов решения конркетнной проблемы, здесь можно дополнить код по формуле ```X XOR Y = (X OR Y) AND (X NAND Y)```, чтобы он мог корректно работать для данной логики. Для этого внесём в файл **Perceptron.cs** данные изменения:
```C#
public TrainingSet[] modelOR;
public TrainingSet[] modelNAND;

double CalcOutput(int i, TrainingSet[] set)
{
	double dp = DotProductBias(weights,set[i].input);
	if(dp > 0) return(1);
	return (0);
}

void UpdateWeights(int j, TrainingSet[] set)
{
	double error = set[j].output - CalcOutput(j, set);
	totalError += Mathf.Abs((float)error);
	for(int i = 0; i < weights.Length; i++)		
		weights[i] = weights[i] + error * set[j].input[i];
	bias += error;
}

void Train(int epochs, TrainingSet[] set)
{
	InitialiseWeights();
	for(int e = 0; e < epochs; e++)
	{
		totalError = 0;
		for(int t = 0; t < set.Length; t++)
		{
			UpdateWeights(t, set);
			Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
		}
		Debug.Log("TOTAL ERROR: " + totalError);
	}
}

void Start ()
{
	Train(8, modelOR);
	double modelOr0 = CalcOutput(0,0);
	double modelOr1 = CalcOutput(0,1);
	double modelOr2 = CalcOutput(1,0);
	double modelOr3 = CalcOutput(1,1);

	Train(8, modelNAND);
	double modelNAND0 = CalcOutput(0,0);
	double modelNAND1 = CalcOutput(0,1);
	double modelNAND2 = CalcOutput(1,0);
	double modelNAND3 = CalcOutput(1,1);

	Train(8, ts);
	Debug.Log("Test 0 0: " + CalcOutput(modelOr0, modelNAND0));
	Debug.Log("Test 0 1: " + CalcOutput(modelOr1, modelNAND1));
	Debug.Log("Test 1 0: " + CalcOutput(modelOr2, modelNAND2));
	Debug.Log("Test 1 1: " + CalcOutput(modelOr3, modelNAND3));		
}
```
> Дополнение параметров у игрового объекта и повторный запуск сцены с новым вариантом кода файла **Perceptron.cs**.
![image](https://user-images.githubusercontent.com/71095323/204209262-66be259a-1ece-4557-8c4a-4e6f7ef49a24.png)
![image](https://user-images.githubusercontent.com/71095323/204209823-eecfaae6-561e-4619-9cec-da323e7228f7.png)

После внесений изменений в код игровой объект смог успешно обучится данной логике и мы получили корректные результаты тестирования.

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.
Необходимое количество эпох обучения зависит от заданных начальных параметров.

Для построения графиков я воспользовался Execl-таблицей. Для каждой логической операции я производил 4 запуска по 10 итераций (```Train(10);```).

> График логической операции OR выглядит вот так:
![image](https://user-images.githubusercontent.com/71095323/204212291-0a728900-bc9e-4532-867f-48c08d8e6811.png)

> График логической операции AND представлен вот так:
![image](https://user-images.githubusercontent.com/71095323/204212444-e404eab2-742f-4f8f-a6b5-bb9e47ad537a.png)

> График логической операции NAND выглядит так:
![image](https://user-images.githubusercontent.com/71095323/204213186-a9cdbf0b-fa24-42b1-af5d-bc7d87d7483f.png)

> График логической операции XOR представлен так:
![image](https://user-images.githubusercontent.com/71095323/204213279-0425065f-70aa-4d29-9388-381c39de5c1e.png)


## Выводы
### Я изучил работу прецептрона и его решения логических операций путём создания проекта в Unity и реализации работы рецептрона, который умеет воспроизводить вычисления. В ходе лабороторной работы я смог дополнить код программы рецептрона для коррекнтой работы логичесокй операции XOR, а также я построил графики зависимости количества эпох от ошибок обучения и выяснил, от чего зависит необходимое количество эпох обучения.

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
