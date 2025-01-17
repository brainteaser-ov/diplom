# Глубокое обучение в задаче поиска когнатов в малоресурсных языках


<p align="center">
  <a href="#о-проекте">О проекте</a> •
  <a href="#запуск-проекта">Запуск проекта</a> •
  <a href="#стек">Стек</a> •

<p align="center">
  <img src="/Flag-maps_of_the_subjects_of_Russia.png" alt="Siamese Text Classification
" width="738">
</p>


### О проекте 
В проекте реализована сиамская модель для задач классификации текста. Модель обучена для определения сходства между парами текстовых последовательностей и может использоваться для классификации новых пар последовательностей.

#### [Основные сущности](https://github.com/brainteaser-ov/diplom/blob/main/torch_cognates.ipynb)

`Архитектура` модели состоит из следующих основных компонентов:
1. **Embedding Layer**: Преобразует входные последовательности символов в плотные векторные представления.
2. **Position Embedding**:Добавляет позиционные эмбединги к входным эмбедингам, чтобы зафиксировать порядок следования символов в последовательности.
3. **Spatial Dropout**: Применяет dropout для регуляризации.
4. **Bidirectional LSTM**: Применяет двунаправленный LSTM для получения контекстуальных представлений последовательностей.
5. **Transformer Encoder Blocks**: Применяет несколько блоков Transformer Encoder для дальнейшего преобразования представлений последовательности.
6. **Abs Diff Layer**: Вычисляет абсолютную разницу между представлениями двух последовательностей.
7. **Fully Connected Layers**: Применяет несколько полносвязных слоев для преобразования объединенных представлений в вероятность.

#### Training

Модель `обучается` с помощью следующих шагов:

1. Загружаем и предварительно обрабатываем данные: из текстовых файлов загружаются [положительные](https://github.com/brainteaser-ov/diplom/blob/main/positive_test.txt) и [отрицательные](https://github.com/brainteaser-ov/diplom/blob/main/negative_test.txt) примеры и создается словарь символов.
   
> [!IMPORTANT]
> в качестве примера загружены только файлы для валидации, так как размер файлов для обучения не позволяет выгрузить их

3. Определяются гиперпараметры и оптимизатор: определяются такие гиперпараметры, как размер файла, максимальная длина последовательности, размер пакета и количество эпох, создается оптимизатор.
4. Обучение модели: выполняется цикл обучения, в ходе которого вычисляется функция потерь и обновляются веса модели.
5. Визуализация потерь: для визуализации функции потерь во время обучения.
6. Оценка модели на тестовых данных: модель оценивается на тестовых данных.
7. Сохранение модели: Обученная [модель](https://github.com/brainteaser-ov/diplom/blob/main/model.pth) сохраняется в файл.

## Usage

Пример использования: 
```
python
import torch
from your_model import SiameseModel

▎Load the saved model
model = SiameseModel(vocab_size, embedding_dim, max_len)
model.load_state_dict(torch.load('model.pth'))
model.to(device)

▎Prepare the input sequences
sequence1 = "This is the first sequence."
sequence2 = "This is the second sequence."

▎Convert the sequences to tensors
input_a = torch.tensor([char_tokenizer(sequence1)], dtype=torch.long, device=device)
input_b = torch.tensor([char_tokenizer(sequence2)], dtype=torch.long, device=device)

▎Forward pass through the model
output = model(input_a, input_b)
probability = torch.sigmoid(output).item()

print(f"Probability of the two sequences being similar: {probability:.4f}")

```

### Запуск проекта

#### Клонировать репозиторий и перейти в него в командной строке
```
git clone git@github.com:{name}}/{name}
```

#### Запустить docker-compose в папке [flask_cognates](https://github.com/brainteaser-ov/diplom/blob/main/positive_test.txt) docker-compose:

```
docker-compose -f docker-compose-main.yml up -d --build 

```

#### Стек
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) 
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)

#### Directed by 


[brainteaser-ov 💛](https://github.com/brainteaser-ov)  
