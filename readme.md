# Тестовое задание на распознавание именованных сущностей

### Цель проекта
Написать скрипт для парсинга диалогов из предоставленных данных по заданным условиям.  

### Задачи скрипта
* Извлечь из диалогов реплики с приветствием, в которых менеджер поздоровался с клиентом.
* Извлчечь реплики, в которых менеджер представил себя.
* Извлечь имя менеджера из реплик.
* Извлечь название компании.
* Извлечь реплики, в которых менеджер попрощался.
* Проверить выполнение требования к менеджеру: «В каждом диалоге обязательно необходимо поздороваться и попрощаться с клиентом».	

### Итоги

- Выделены три базовых типа именованных сущностей, которые модель должна находить в репликах: `PERSON` - имя менеджера, `COMPANY` - название компании и `EVENT` событие в виде привествия или прощания.
- Осуществлена ручная разметка предоставленных данных, чтобы иметь возможность оценки качества выделения сущностей по выбранной метрике.
- В качестве метрики использована `F1`-мера, вычисляемая для каждого вида выделяемых сущностей.
- За *baseline* решение приняты результаты работы предобученной модели из библиотеки `spaСy`, которые обеспечили результат по `F1`-метрике, равный `0.38`.
- Так как диалоги в данных получены в результате автоматического преобразования речи в текст (`speech-to-text`), то тексты не содержали разметки, что затрудняет выделение именованных сущностей. Для добавления разметки была использована библиотека `silero` и после её работы была снова использована предобученная модель `spaСy`. в результате данных действий количество распознаваемых сущностей возросло, но качество работы модели по `F1`-метрике снизилось до `0.29`, так как одновременно возросло и количество ошибок в виде ложноположительных срабатываний.
- Было произведено дообучение дефолтной модели `ru_core_news_lg` на предварительно размеченных данных. Это позволило получить среднее значение `F1`-метрики, равное `0.74`. Недостаток этого решения в том, что так как объём выборки небольшой, для обучения и тестирования были использованы одни и те же данные.

### Использованный стек инструментов

- python
- pandas
- numpy
- torch
- spacy
- silero
