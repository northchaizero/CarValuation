# Оценка стоимости поддержанных авто

## Постановка задачи
Сервис по продаже автомобилей с пробегом разрабатывает приложение, чтобы привлечь новых клиентов. В нём можно будет узнать рыночную стоимость своего автомобиля. 
Цель - построить модель, которая умеет её определять. В нашем распоряжении данные о технических характеристиках, комплектации и ценах других автомобилей.

## Критерии, которые важны заказчику:
    качество предсказания;
    время обучения модели;
    время предсказания модели;
    rmse <= 2500.

## Этапы работы:
### Предобработка
В процессе предобработки данных были заменены Nan, изменены типы данных некоторых столбцов.
Несмотря на удаление столбцов с датами и почтовыми индексами, модель показывает хорошую RMSE, явно ниже указанного порога в 2500.

### Анализ корреляций
В ходе анализа хитмапа матрицы phik была найдена корреляция в парах:
    
    Brand - Model (1.00)
    
    VehicleType - Model (0.90)

Принято решение об удалении столбца с моделью, за исключением корреляции с входными признаками,
столбец содержит много уникальных значений, что может привести к переобучению сложных моделей.

### Моделирование

Была проведена кросс-валидация по сетке, использовались модели: обыкновенная линейная регрессия sklearn, LightGBM Regressor и CatBoost Regressor.

По итогам кросс-валидации была выбрана модель LGBM с RMSE ~= 1760.
