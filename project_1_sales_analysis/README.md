# Анализ продаж Superstore

## Описание проекта
Анализ данных интернет-магазина Superstore: выручка по категориям, динамика по месяцам, топ-5 товаров.

## Инструменты
- SQL (MariaDB)
- DBeaver

## Результаты

### 1. Выручка по категориям
![Выручка по категориям]
<img width="1920" height="1033" alt="4_table_structure" src="https://github.com/user-attachments/assets/4b32ebfb-9749-4d7a-977b-405620eb32f1" />

### 2. Динамика по месяцам
![Динамика по месяцам]
<img width="1919" height="1040" alt="3_top_products png" src="https://github.com/user-attachments/assets/1415ffca-0751-4e61-bd19-8de722da81b2" />

### 3. Топ-5 товаров по выручке
![Топ-5 товаров]
<img width="1918" height="1014" alt="2_monthly_sales" src="https://github.com/user-attachments/assets/540769d7-d8c6-4340-af4d-9472a5bf101d" />

### 4. Структура таблицы
![Структура таблицы]
<img width="1920" height="1039" alt="1_category_sales" src="https://github.com/user-attachments/assets/d7373113-9888-4081-80d4-9f3788317b34" />

## SQL-запросы
-- Запрос 1: Выручка по категориям
SELECT 
    Category,
    ROUND(SUM(Sales), 0) AS Total_Sales,
    ROUND(SUM(Profit), 0) AS Total_Profit
FROM superstore
GROUP BY Category
ORDER BY Total_Sales DESC;

-- Запрос 2: Динамика по месяцам
SELECT 
    DATE_FORMAT(Order_Date, '%Y-%m') AS Month,
    ROUND(SUM(Sales), 0) AS Monthly_Sales
FROM superstore
GROUP BY Month
ORDER BY Month;

-- Запрос 3: Топ-5 товаров по выручке
SELECT 
    Product_Name,
    ROUND(SUM(Sales), 0) AS Total_Sales
FROM superstore
GROUP BY Product_Name
ORDER BY Total_Sales DESC
LIMIT 5;
