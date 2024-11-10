![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)

# Контроль и управление изменениями в тендерных закупках
## Описание проекта

Инструмент на базе ИИ для усовершенствования процесса контроля и управления изменениями в тендерных закупках с помощью автоматизации анализа документации от поставщиков на уровень соответствия требованиям для оперативного принятия решений, а также применения соответствующих изменений.

Проект имеет 2 режима работы:
1. Разработка
2. Инференс

Последовательное использование режимов позволяет осуществлять взаимодействие с платформенным решением для обработки и представления текстовых .docx-файлов документаций, обработкой этих представлений, обучением ML-моделей и их встраиванием в комплаенс-конвеер.

# Метрики качества решения
## Описание метрик

1. Метрика MSE (Mean Squared Error) Формула для вычисления MSE:

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$ 

2. Скорректированное MSE, предложенное компанией Atom Формула для вычисления скорректированного MSE:

$$\text{AtomMSE} = \max(0, 1.5 - \text{MSE}) / 1.5$$

## Значения достигнутых метрик на 2024.11.10
**MSE**: 0.1931
**ATOM_MSE**: 0.8713

# Инструкция по работе с проектом
## Создание виртуальной среды и работа с ноутбуками

Для подготовки окружения для работы с модулями и ноутбуками выполните следующие команды, находясь в корневой директории проекта:

```bash
# команды создания виртуального окружения
python3 -m venv .venv

# активация виртуального окружения
## Windows
.venv\Scripts\activate

## macOS & Linux
source .venv/bin/activate

# установка необходимых библиотек в виртуальное окружение
pip install -r equirements.txt
```

## Режим инференса (FULL LAUNCH)

Для проведения теста проекта и инференса используется Jupyter Notebook `FULL LAUNCH.ipynb`, расположенный в директории `./inference`.

Через данный ноутбук осуществляется следующий функционал:
1. Загрузка инференс-данных заключений типа HMI и SSTS из .docx-файлов и представление их в виде датасета
2. Загрузка ML-моделей:
   - BERT - для извлечения эмбенддингов из текста
   - Разработанной ML-модели, ранее полученной в ноутбках, относящихся к режиму разработки, для предсказания комплаенс-метки
3. Feature Extraction из текстовых данных датасета
4. Получение предсказаний модели, и корректировка предсказаний по настраивоемой бизнес-логике
5. Формирование артефактов:
   - Отчет `submission.csv`
   - График распределения комплаенс-меток
   - Лог-файл инференса

## Режим разработки

Режим разработки ведется в следующих Jupyter Notebook'ах:
- `ds_creation.ipynb`
   - Представление текстовых .docx-файлов заключений типа HMI и SSTS в виде датасета, хранящийся в `data\raw_data`
   - Формирование целевого признака на основе размеченных данных из `data\raw_data\train_data_markup.xlsx`
- `vectorizing_and_modeling.ipynb`
   - Определение платформы вычислений (CPU / CUDA)
   - Загрузка модели и токенайзера BERT
   - Извлечение эмбенддингов и конструирование фич (Feature Extraction / Feature Engineering)
   - Обучение ML-модели для задачи регрессии комплаенс-меток
   - Получение предсказаний и анализ модели
   - Сохранение артефактов:
      - ML-модель в формате `.pickle`
      - Коэффициенты линейной регрессии
      - Анализ расхождений модели

# Структура проекта

```bash
atom-compliance-ml
├─ .github                       # CI/CD
│  └─ workflows
│     ├─ check.yml
│     └─ release.yml
├─ .gitignore
├─ config                        # Ядро с конфигом
│  └─ config.yaml
├─ data                          # Данные для обучения и тестирования
│  ├─ ds
│  │  ├─ ds.unl
│  ├─ raw_data                   # Сырые данные для обучения
│  │  ├─ HMI                     # UC-визы
│  │  ├─ SSTS                    # SSTS-визы
│  │  └─ train_data_markup.xlsx  # Размеченные наблюдеия для обучения
│  └─ test_data                  # Тестовые данные
│     ├─ HMI                     # UC-визы
│     └─ SSTS                    # SSTS-визы
├─ doc
├─ logs                          # Логи инференса (FULL LAUNCH)
├─ submissions                   # Директория результатов (submissions) инференса (FULL LAUNCH)
├─ LICENSE
├─ models                        # Артефакты модели, графики, метрики и т.д.
└─ src                           # Ноутбуки для обучения и экспериментов, модули
   ├─ modules                    # Функциональная и бизнес логика, используемая во всех ноутбуках
   └─ notebooks

```

# Контакты
Если у вас есть вопросы или предложения по проекту, пожалуйста, свяжитесь с нами:
- Богдан, TL
   - @AdamCage
- Светлана, DS
   - @Wolta_1
- Егор, DevOps
   - @egor_lyadsky
- Александр, DS
   - @BeesKnights

![alt text](team_logo.png)
