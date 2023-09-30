# Создание модели для предсказания заработной платы на основе описания вакансии
Данный проект позволяет на основе некоторых данных о конкретной вакансии предсказывать возможную заработную плату, которая подходит данному описанию вакансии
## Как установить и пользоваться
Создайте клон репозитория:  
```
git clone https://github.com/ASoloveva01/vacancy_salary_prediction
cd vacancy_salary_prediction
```
Для установки требуемых пакетов запустите через терминал следующую команду:  
```
pip3 install -r requirements.txt
```  
Далее следуйте объяснениям в ноутбуках. 
### Используемые библиотеки
Парсинг: ```beautifulsoup4, json, requests, re, selenium, urllib```  
Предобработка данных: ```matplotlib, numpy, pandas, scipy, sklearn```  
Визуализация данных: ```seaborn, matplotlib```  
Обучение модели: ```sklearn```  
## Датасет
Данные для обучения были взяты с сайта https://hh.ru/search/vacancy.  
Датасет содержит следующие поля:
- location
- industry
- experience
- skills
- salary
### Разведочный анализ данных
![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/top15locations.png)
![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/top7industries.png)  
Изображение содержит популярные слова в разделе "Навыки".  
![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/skills_cloud.png)  
![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/salary_dist.png)  
### Предобработка данных и построение признаков
- Столбец location заменяем на два столбца latitude и longitude  
 ![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/coords.png)  
- Удаляем столбец industry из массивов строк и заменяем его на столбцы каждой отрасли, которые имеют значения 0 и 1 в зависимости от встречаемости в вакансии
- Из столбцов experience и salary извлекаем численное значение, и при наличии верхнего и нижнего пределов считаем их среднее
- Стандартизируем все численные признаки
- Удаляем столбец skills, состоящий из строковых перечислений навыков и добавляем с помощью метода TF-IDF 9 столбцов, состоящих из самых популярных слов в skills
- Удаляем выбросы применяя межквартильный диапазон
 ![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/outliers.png)  
## Результаты и оценка моделей
**Метрика: среднеквадратическая ошибка(MSE)** 
  
**Gradient Boosting Regressor:** 815195753.75  
**Lasso:** 871219393.71  
**RandomForestRegressor:** 711046155.82  
  
![Иллюстрация к проекту](https://github.com/ASoloveva01/vacancy_salary_prediction/blob/main/images/model_graphs.png)
