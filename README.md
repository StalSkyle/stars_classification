# README.md

## Описание проекта

Этот проект посвящен задаче бинарной классификации: построению модели, способной отличать переменные звёзды от статичных объектов. Исходные данные содержат признаки различных небесных объектов, но датасет изначально несбалансирован. Основной целью является обнаружение переменных звезд, поэтому ключевыми метриками являются **recall** (полнота) и **F1-score**.

## Используемые библиотеки

- `pandas` – обработка данных
- `matplotlib`, `seaborn` – визуализация
- `scikit-learn` – алгоритмы машинного обучения
- `imblearn` – работа с несбалансированными данными

## Подготовка данных

1. Загрузка датасета `whole_data_practice3.csv`.
2. Удаление столбца `type`, так как он содержит слишком много пропущенных значений.
3. Анализ корреляции между признаками, удаление `Bmag`, `gpmag`, `rpmag`, `ipmag`, так как они сильно коррелируют с `Vmag`.
4. Визуализация данных (гистограммы, boxplot, violin plot, t-SNE для двумерного представления).
5. Данные масштабированы с помощью RobustScaler из библиотеки sklearn, так как в данных содержится много выбросов

## Обучение моделей

Рассматривались различные алгоритмы машинного обучения:

- **Логистическая регрессия** (`LogisticRegression`)
- **Метод k ближайших соседей** (`KNeighborsClassifier`) – плохо работает на несбалансированных данных.
- **Дерево решений** (`DecisionTreeClassifier`)
- **Случайный лес** (`RandomForestClassifier`)
- **Градиентный бустинг** (`GradientBoostingClassifier`)

Все модели оценивались с помощью кросс-валидации `StratifiedKFold` (5 фолдов).

## Улучшение качества модели

- Применена техника **oversampling** с `SMOTE` для балансировки классов.
- Использован `GridSearchCV` для подбора гиперпараметров (оптимальные `max_depth=10, k_neighbors=5`).
- Лучшая модель после подбора параметров дала:
  - **Accuracy**: 0.94
  - **Precision**: 0.67
  - **Recall**: 0.77
  - **F1-score**: 0.71

## Запуск кода

1. Установите зависимости:
   ```bash
   pip install pandas matplotlib seaborn scikit-learn imbalanced-learn
   ```
2. Запустите скрипт:
   ```bash
   python main.py
   ```

См. также **research.ipynb**, где представлены все графики и результаты исследования

## Выводы

Использование методов балансировки классов (SMOTE) и градиентного бустинга позволило существенно повысить метрики качества. Финальная модель имеет **хороший баланс между полнотой (77%) и точностью (68%)**, что делает её полезной для поиска переменных звёзд.
