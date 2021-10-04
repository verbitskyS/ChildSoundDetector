# Recognition of Baby Sounds
 Репозиторий содержит код проекта, примеры использования моделей и предобученные модели для различных задач распознавания звуков на аудиосигнале:
 1) Детектирование голоса няни;
 2) Детектирование звуков ребенка;
 3) Детектирование плача ребенка;
 4) Классификация детских звуков (крик, смех, плач, пение);
 5) Классификация плача ребенка (плач по причине боли, плач по другой причине).
 Также описывается точность моделей на тестовых данных для всех пяти задач.

Архитектура моделей описана в нашей статье: **[ERANNs: Efficient Residual Audio Neural Networks for Audio Pattern Recognition](https://arxiv.org/abs/2106.01621)**. Для данной задачи была дообучена лучшая модель (**ERANN-1-6**), обученная на крупном наборе данных для распозвания звуковых образов [AudioSet](http://research.google.com/audioset/), который имеет более двух миллионов аудиосигналов и 527 различных классов звуков. Лучшая модель достигает **state-of-the-art точность** для этого набора данных: **0.450 по метрике mAP** на валидационной выборке.

Обучающие и валидационные выборки для вышесказанных задач распознавания звуков были сформированы с помощью набора данных AudioSet. Количество примеров в обучающих выборках: 16778, 16778, 4850, 5396 и 142 для пяти задач соответственно. Количество примеров в валидационных выборках: 8804, 376, 204, 204, 25 для пяти задач соответственно.

## Настройка окружения
Для использования моделей необходимо наличие Python 3.7 (и выше) и предустановленных пакетов:

```
pip install -r requirements.txt
```

## Использование предобученных моделей
Для использования систем распознавания звуков необходимо загрузить предобученные модели. Предобученные модели могут быть загружены по [ссылке](https://drive.google.com/file/d/146KR9GxppqiCRfJFBp83EiuV68UIbkwy/view?usp=sharing). Название моделей оформлены в виде "model_type_N.pth", где N - номер задачи от 1 до 5.

Далее для получения результатов распознавания (распределение вероятностей от 0 до 1 наличия классов звуков)на аудиосигнале необходимо воспользоваться следующей командой:
```
python inference.py --TYPE 4 --MODEL_PATH path_to_model --AUDIO_PATH path_to_audio --CUDA True
```
Описание аргументов:
- **TYPE** - номер задачи от 1 до 5 (смотреть выше);
- **path_to_model** - путь до предобученной модели;
- **path_to_audio** - путь до аудиосигнала;
- **CUDA True** если использовать графический процессор, иначе **CUDA False** (по умолчанию).

Например, результат распознавания модели для 1ой задачи на [аудиосигнале со звуками природы](https://drive.google.com/file/d/1yKgAPiZ4NQgfwu7LyBcV8m1CI0uKfB4Q/view?usp=sharing):
```
РЕЗУЛЬТАТ:

Отсутствие голоса: 0.86
Наличие голоса: 0.14

На аудиосигнале обнаружено: Отсутствие голоса
```

Результат распознавания модели для 2ой задачи на [аудиосигнале с плачем ребенка](https://drive.google.com/file/d/1NBUqq8JvtsNxo9zWrU4GrcoI9Xo52d2P/view?usp=sharing):
```
РЕЗУЛЬТАТ:

Отсутствие звуков детей: 0.12
Наличие звуков детей: 0.88

На аудиосигнале обнаружено: Наличие звуков детей

```

Результат распознавания модели для 4ой задачи на [аудиосигнале с плачем ребенка](https://drive.google.com/file/d/1NBUqq8JvtsNxo9zWrU4GrcoI9Xo52d2P/view?usp=sharing):
```
РЕЗУЛЬТАТ:

Детский крик: 0.07
Детский смех: 0.06
Детский плач: 0.84
Детское пение: 0.05

На аудиосигнале обнаружено: Детский плач
```

Результат распознавания модели для 4ой задачи на [аудиосигнале со звуками природы](https://drive.google.com/file/d/1yKgAPiZ4NQgfwu7LyBcV8m1CI0uKfB4Q/view?usp=sharing):
```
РЕЗУЛЬТАТ:

Детский крик: 0.11
Детский смех: 0.25
Детский плач: 0.33
Детское пение: 0.17

Ничего из 4х классов на аудиосигнале не обнаружено
```
## Точность моделей
В данной секции описываются результаты точности моделей для всех пяти задач. 
Используется макро метрика mAP (mean average precision), так как она является основной для набора данных AudioSet.

**Точность детектирования голоса няни:**

| Класс   | mAP          | Количество примеров |
| ------------- | :---: | :---: | 
| Наличие голоса | 0.908  |  4402 | 
| Отсутствие голоса | 0.938  |  4402 |
| Все классы | 0.923  |  8804 | 


**Точность детектирования звуков ребенка:**
| Класс   | mAP          | Количество примеров |
| ------------- | :---: | :---: | 
| Наличие звуков детей | 0.970  |  188 | 
| Отсутствие звуков детей | 0.978  |  188 | 
| Все классы | 0.974  |  376 | 

**Точность детектирования плача ребенка:**
| Класс   | mAP   | Количество примеров |
| ------------- | :---: | :---: | 
| Наличие плача ребенка | 0.965  |  39 | 
| Отсутствие плача ребенка | 0.998  |  165 | 
| Все классы | 0.982  |  204 | 

**Точность классификации детских звуков:**
| Класс   | mAP   | Количество примеров |
| ------------- | :---: | :---: | 
| Крик ребенка | 0.999  |  57 | 
| Смех ребенка | 0.974  |  55 |
| Плач ребенка | 0.965  |  39 | 
| Пение ребенка | 0.991  |  53 | 
| Все классы | 0.982  |  204 |

**Точность классификации плача ребенка:**
| Класс   | mAP   | Количество примеров |
| ------------- | :---: | :---: | 
| Плач по причине боли | 0.898  |  11 | 
| Плач по другой причине | 0.857  |  14 | 
| Все классы | 0.878  |  25 | 


